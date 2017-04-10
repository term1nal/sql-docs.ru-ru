---
title: "Вкладки &#171;Поток данных&#187; | Microsoft Docs"
ms.custom: ""
ms.date: "03/03/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2d847adf-4b3d-4949-a195-ef43de275077
caps.latest.revision: 9
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 9
---
# Вкладки &#171;Поток данных&#187;
 Вы можете добавить отвод данных в путь потока данных пакета во время выполнения и перенаправить отвод данных во внешний файл. Для использования этой функции следует развернуть проект служб SSIS на сервере служб SSIS с помощью модели развертывания проекта. После развертывания пакета на сервере до выполнения пакета следует выполнить T-SQL скрипты на базе данных SSISDB, чтобы добавить отводы данных. Пример сценария.  
  
1.  Создайте экземпляр выполнения пакета с помощью хранимой процедуры [catalog.create_execution (база данных SSISDB)](../../integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database.md).  
  
2.  Добавьте отвод данных с помощью хранимой процедуры [catalog.add_data_tap](../../integration-services/system-stored-procedures/catalog-add-data-tap.md) или [catalog.add_data_tap_by_guid](../../integration-services/system-stored-procedures/catalog-add-data-tap-by-guid.md).  
  
3.  Запустите экземпляр выполнения пакета с помощью хранимой процедуры [catalog.start_execution (база данных SSISDB)](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md).  
  
 Пример SQL-скрипта, реализующий шаги, описанные выше.  
  
```  
  
Declare @execid bigint  
EXEC [SSISDB].[catalog].[create_execution] @folder_name=N'ETL Folder', @project_name=N'ETL Project', @package_name=N'Package.dtsx', @execution_id=@execid OUTPUT  
EXEC [SSISDB].[catalog].add_data_tap @execution_id = @execid, @task_package_path = '\Package\Data Flow Task', @dataflow_path_id_string = 'Paths[Flat File Source.Flat File Source Output]', @data_filename = 'output.txt'  
EXEC [SSISDB].[catalog].[start_execution] @execid  
  
```  
  
 Параметры имен папки, проекта и пакета хранимой процедуры create_execution соответствуют именам папки, проекта и пакета в каталоге служб Integration Services. Эти имена для вызова процедуры create_execution можно получить в среде SQL Server Management Studio, как показано на следующем рисунке. Если вашего проекта служб SSIS здесь нет, возможно, вы еще не развернули проект на сервер служб SSIS. Щелкните правой кнопкой мыши по проекту служб SSIS в Visual Studio и выберите команду «Развернуть», чтобы развернуть проект на нужный сервер служб SSIS.  
  
 Вместо ввода инструкций SQL можно сформировать скрипт выполнения пакета, выполнив следующие действия.  
  
1.  Щелкните правой кнопкой мыши **Package.dtsx** и выберите команду **Выполнить**.  
  
2.  Нажмите кнопку **Скрипт** на панели инструментов, чтобы сформировать скрипт.  
  
3.  Теперь добавьте инструкцию add_data_tap до вызова start_execution.  
  
 Параметр task_package_path хранимой процедуры add_data_tap соответствует свойству PackagePath задачи потока данных в Visual Studio. В Visual Studio щелкните правой кнопкой мыши **Задача потока данных**, а затем выберите **Свойства**. Откроется окно свойств.  Значение свойства **PackagePath** используйте в качестве значения для параметра task_package_path при вызове хранимой процедуры add_data_tap.  
  
 Параметр dataflow_path_id_string хранимой процедуры add_data_tap соответствует свойству IdentificationString задания пути потока данных, к которому следует добавить отвод данных. Чтобы получить dataflow_path_id_string, щелкните по пути потока данных (стрелка между задачами в потоке данных) и отметьте значение свойства **IdentificationString** в окне свойств.  
  
 При выполнении скрипта выходной файл сохранятся в папке \<Program Files>\Microsoft SQL Server\110\DTS\DataDumps. Если уже существует файл с таким именем, будет создан новый файл с суффиксом (например, output[1].txt).  
  
 Как упоминалось ранее, также вместо использования хранимой процедуры add_data_tap можно применить хранимую процедуру [catalog.add_data_tap_by_guid](../../integration-services/system-stored-procedures/catalog-add-data-tap-by-guid.md). Эта хранимая процедура принимает в качестве параметра идентификатор задачи потока данных вместо task_package_path. Идентификатор этой задачи потока данных можно узнать в окне «Свойства» среды Visual Studio.  
  
## Удаление отвода данных  
 Отвод данных можно удалить до начала выполнения, воспользовавшись хранимой процедурой [catalog.remove_data_tap](../../integration-services/system-stored-procedures/catalog-remove-data-tap.md). Эта хранимая процедура принимает в качестве параметра идентификатор отвода данных, который можно получить после вызова хранимой процедуры add_data_tap.  
  
```  
  
DECLARE @tap_id bigint  
EXEC [SSISDB].[catalog].add_data_tap @execution_id = @execid, @task_package_path = '\Package\Data Flow Task', @dataflow_path_id_string = 'Paths[Flat File Source.Flat File Source Output]', @data_filename = 'output.txt' @data_tap_id=@tap_id OUTPUT  
EXEC [SSISDB].[catalog].remove_data_tap @tap_id  
  
```  
  
## Перечисление всех отводов данных  
 С помощью представления add_data_tap можно перечислить все отводы данных. В следующем примере показано, как извлечь отводы данных для экземпляра выполнения спецификации (ID: 54).  
  
```  
select * from [SSISDB].[catalog].execution_data_taps where execution_id=@execid  
```  
  
## Вопросы производительности  
 Включение подробного уровня ведения журнала и добавление отводов данных увеличивает количество операций ввода-вывода, выполняемых решением по интеграции данных. Поэтому рекомендуется добавлять отводы данных только для устранения неполадок  
  
## Видеоролик  
 Этот [видеоролик в библиотеке TechNet](http://technet.microsoft.com/sqlserver/dn600163) демонстрирует добавление и использование отводов данных в каталоге SQL Server 2012 SSISDB для программной отладки пакетов и получения частичных результатов во время выполнения. Также там обсуждается вопрос перечисления или удаления отводов данных и рекомендации по их применению в пакетах SSIS.  
  
## Связанные задачи  
 [Отладка потока данных](../../integration-services/troubleshooting/debugging-data-flow.md)  
  
 [Устранение неполадок инструментов с помощью отчетов](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md)  
  
  