---
title: "Развертывание и выполнение пакетов служб SSIS с помощью хранимых процедур | Microsoft Docs"
ms.custom: ""
ms.date: "08/26/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 60914b0c-1f65-45f8-8132-0ca331749fcc
caps.latest.revision: 11
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 11
---
# Развертывание и выполнение пакетов служб SSIS с помощью хранимых процедур
  После настройки проекта [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] для использования модели развертывания проекта можно вызывать хранимые процедуры в каталоге служб [!INCLUDE[ssIS](../../includes/ssis-md.md)] , чтобы развернуть проект и выполнить пакеты. Дополнительные сведения о модели развертывания проектов см. в разделе [Deployment of Projects and Packages](https://msdn.microsoft.com/library/hh213290.aspx).  
  
 Для развертывания и выполнения пакетов также можно использовать среду [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] или [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] . Дополнительные сведения см. в разделе **См. также** .  
  
> [!TIP]  
>  Не составит труда создать инструкции Transact-SQL для хранимых процедур, перечисленных в следующей процедуре, за исключением catalog.deploy_project, выполнив следующие действия.  
>   
>  1.  В [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]разверните узел **Каталоги служб Integration Services** в обозревателе объектов и перейдите к пакету, который нужно выполнить.  
> 2.  Щелкните правой кнопкой мыши пакет и выберите команду **Выполнить**.  
> 3.  При необходимости задайте значения параметров, свойства диспетчера соединений и параметры на вкладке **Дополнительно** , например уровень ведения журнала.  
>   
>      Дополнительные сведения об уровнях ведения журнала см. в разделе [Enable Logging for Package Execution on the SSIS Server](../../integration-services/performance/enable-logging-for-package-execution-on-the-ssis-server.md).  
> 4.  Перед нажатием кнопки **ОК** для выполнения пакета выберите пункт **Скрипт**. Код Transact-SQL откроется в окне редактора запросов среды [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
## Развертывание и выполнение пакета с помощью хранимых процедур  
  
1.  Вызовите [catalog.deploy_project (база данных SSISDB)](../../integration-services/system-stored-procedures/catalog-deploy-project-ssisdb-database.md), чтобы развернуть проект [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], который содержит пакет, на сервере [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
     Можно использовать инструкцию SELECT с функцией OPENROWSET и поставщиком больших наборов строк (BULK) для получения двоичного содержимого файла развертывания проекта [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] для параметра *@project_stream*. Поставщик больших наборов строк позволяет считывать данные из файла. Аргумент SINGLE_BLOB для поставщика больших наборов строк возвращает содержимое файла данных в виде набора строк с одной строкой и одним столбцом типа varbinary(max). Дополнительные сведения см. в разделе [OPENROWSET (Transact-SQL)](../../t-sql/functions/openrowset-transact-sql.md).  
  
     В следующем примере проект SSISPackages_ProjectDeployment будет развернут в папке SSIS Packages на сервере [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Двоичные данные считываются из файла проекта (SSISPackage_ProjectDeployment.ispac) и сохраняются в параметре *@ProjectBinary* с типом varbinary(max). Значение параметра *@ProjectBinary* присваивается параметру *@project_stream*.  
  
    ```  
    DECLARE @ProjectBinary as varbinary(max)  
    DECLARE @operation_id as bigint  
    Set @ProjectBinary = (SELECT * FROM OPENROWSET(BULK 'C:\MyProjects\ SSISPackage_ProjectDeployment.ispac', SINGLE_BLOB) as BinaryData)  
  
    Exec catalog.deploy_project @folder_name = 'SSIS Packages', @project_name = 'DeployViaStoredProc_SSIS', @Project_Stream = @ProjectBinary, @operation_id = @operation_id out  
  
    ```  
  
2.  Вызовите функцию[catalog.create_execution (база данных SSISDB)](../../integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database.md), чтобы создать экземпляр выполнения пакета, и при необходимости вызовите функцию [catalog.set_execution_parameter_value (база данных SSISDB)](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md), чтобы задать значения параметров среды выполнения.  
  
     В следующем примере catalog.create_execution создает экземпляр для выполнения package.dtsx, содержащегося в проекте SSISPackage_ProjectDeployment. Проект располагается в папке SSIS Packages. Значение execution_id, возвращаемое хранимой процедурой, используется для вызова функции catalog.set_execution_parameter_value. Эта вторая хранимая процедура устанавливает параметр LOGGING_LEVEL равным 3 (подробный уровень ведения журнала) и задает параметру пакета Parameter1 значение 1.  
  
     Для таких параметров, как LOGGING_LEVEL, значение object_type равно 50. Для параметров пакета значение object_type равно 30.  
  
    ```  
    Declare @execution_id bigint  
    EXEC [SSISDB].[catalog].[create_execution] @package_name=N'Package.dtsx', @execution_id=@execution_id OUTPUT, @folder_name=N'SSIS Packages', @project_name=N'SSISPackage_ProjectDeployment', @use32bitruntime=False, @reference_id=1  
  
    Select @execution_id  
    DECLARE @var0 smallint = 3  
    EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,  @object_type=50, @parameter_name=N'LOGGING_LEVEL', @parameter_value=@var0  
  
    DECLARE @var1 int = 1  
    EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,  @object_type=30, @parameter_name=N'Parameter1', @parameter_value=@var1  
  
    GO  
  
    ```  
  
3.  Вызовите функцию [catalog.start_execution (база данных SSISDB)](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md) для выполнения пакета.  
  
     В следующем примере вызов catalog.start_execution добавляется в Transact-SQL, чтобы можно было начать выполнение пакета. Используется значение execution_id, возвращаемое хранимой процедурой catalog.create_execution.  
  
    ```  
    Declare @execution_id bigint  
    EXEC [SSISDB].[catalog].[create_execution] @package_name=N'Package.dtsx', @execution_id=@execution_id OUTPUT, @folder_name=N'SSIS Packages', @project_name=N'SSISPackage_ProjectDeployment', @use32bitruntime=False, @reference_id=1  
  
    Select @execution_id  
    DECLARE @var0 smallint = 3  
    EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,  @object_type=50, @parameter_name=N'LOGGING_LEVEL', @parameter_value=@var0  
  
    DECLARE @var1 int = 1  
    EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,  @object_type=30, @parameter_name=N'Parameter1', @parameter_value=@var1  
  
    EXEC [SSISDB].[catalog].[start_execution] @execution_id  
    GO  
  
    ```  
  
## Развертывание проекта из сервера на сервер с использованием хранимых процедур  
 Проект можно развернуть из сервера на сервер с помощью хранимых процедур [catalog.get_project (база данных SSISDB)](../../integration-services/system-stored-procedures/catalog-get-project-ssisdb-database.md) и [catalog.deploy_project (база данных SSISDB)](../../integration-services/system-stored-procedures/catalog-deploy-project-ssisdb-database.md).  
  
 Необходимо выполнить следующие действия перед выполнением хранимых процедур.  
  
-   Создание связанного объекта сервера. Дополнительные сведения см. в разделе [(Создание связанных серверов (компонент SQL Server Database Engine))](../../relational-databases/linked-servers/create-linked-servers-sql-server-database-engine.md).  
  
     На странице **Параметры сервера** диалогового окна **Свойства связанного сервера** назначьте для **RPC** и **RPC Out** значения **True**. Кроме того, назначьте свойству **Разрешить продвижение распределенных транзакций для RPC** значение **False**.  
  
-   Включите динамические параметры для поставщика, выбранного для связанного сервера, разверните узел **Поставщики** и выберите **Связанные серверы** в обозревателе объектов, щелкните правой кнопкой мыши поставщик, затем выберите пункт **Свойства**. Нажмите кнопку **Включить** рядом с полем **Динамический параметр.**  
  
-   Убедитесь, что на обоих серверах запущен координатор распределенных транзакций (DTC).  
  
 Вызовите catalog.get_project для получения двоичных файлов проекта, а затем вызовите catalog.deploy_project. Значение, возвращаемое catalog.get_project, вставляется в табличную переменную типа varbinary(max). Связанный сервер не может возвращать результаты типа varbinary(max).  
  
 В следующем примере catalog.get_project возвращает двоичный результат для проекта SSISPackages на связанном сервере. Catalog.deploy_project развертывает проект на локальном сервере в папке с именем DestFolder.  
  
```  
declare @resultsTableVar table (  
project_binary varbinary(max)  
)  
  
INSERT @resultsTableVar (project_binary)  
EXECUTE [MyLinkedServer].[SSISDB].[catalog].[get_project] 'Packages', 'SSISPackages'  
  
declare @project_binary varbinary(max)  
select @project_binary = project_binary from @resultsTableVar  
  
exec [SSISDB].[CATALOG].[deploy_project] 'DestFolder', 'SSISPackages', @project_binary  
  
```  
  
## См. также  
 [Развертывание проектов на сервере служб Integration Services](../../integration-services/packages/deploy-projects-to-integration-services-server.md)   
 [Запуск пакета с помощью SQL Server Data Tools](../../integration-services/packages/run-a-package-in-sql-server-data-tools.md)   
 [Выполнение пакета на сервере служб SSIS с использованием среды SQL Server Management Studio](../../integration-services/packages/run-a-package-on-the-ssis-server-using-sql-server-management-studio.md)  
  
  