---
title: "Диалоговое окно свойств каталога | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.ssis.ssms.iscreatecatalog.f1"
  - "sql13.ssis.ssms.iscatalogprop.general.f1"
ms.assetid: 3e2fcf11-e010-41c6-bc26-e4b281c0bfbc
caps.latest.revision: 8
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 8
---
# Диалоговое окно свойств каталога
  Диалоговое окно свойств каталога служит для настройки каталога SSISDB. Свойства каталога определяют методы шифрования конфиденциальных данных, параметры хранения данных о версиях операций и проектов, а также время ожидания операций проверки. Каталог служб SSISDB представляет собой центральную точку хранения и администрирования проектов, пакетов, параметров и сред служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 Свойства каталога можно также просмотреть в представлении catalog.catalog_property и задать эти свойства с помощью хранимой процедуры catalog.configure_catalog. Дополнительные сведения см. в разделах [catalog.catalog_properties (база данных SSISDB)](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md) и [catalog.configure_catalog (база данных SSISDB)](../../integration-services/system-stored-procedures/catalog-configure-catalog-ssisdb-database.md).  
  
 Дополнительные сведения о создании каталога SSISDB см. в разделе [Создание каталога служб SSIS](../../integration-services/service/create-the-ssis-catalog.md).  
  
 **Выбор действия**  
  
-   [Открытие диалогового окна свойств каталога](#open_dialog)  
  
-   [Настройка параметров](#options)  
  
##  <a name="open_dialog"></a> Открытие диалогового окна свойств каталога  
  
1.  Откройте среду [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
2.  Создайте соединение с компонентом Microsoft SQL Server Database Engine.  
  
3.  В обозревателе объектов разверните узел **Службы Integration Services**, щелкните правой кнопкой мыши элемент **SSISDB** и выберите пункт **Свойства**.  
  
##  <a name="options"></a> Настройка параметров  
  
### Параметры  
 В следующей таблице описаны некоторые свойства, определенные в диалоговом окне, а также соответствующие свойства в представлении catalog.catalog_property.  
  
|Имя свойства (диалоговое окно свойств каталога)|Имя свойства (представление catalog.catalog_property)|Description|  
|-----------------------------------------------------|------------------------------------------------------|-----------------|  
|Имя алгоритма шифрования|ENCRYPTION_CLEANUP_ENABLED|Указывает тип шифрования, который используется при шифровании значений конфиденциальных параметров каталога. Допустимы следующие значения:<br /><br /> DES<br /><br /> TRIPLE_DES<br /><br /> TRIPLE_DES_3KEY<br /><br /> DESPX<br /><br /> AES_128<br /><br /> AES_192<br /><br /> AES_256 (по умолчанию)|  
|Время ожидания проверки (в секундах)|VALIDATION_TIMEOUT|Задайте максимальное время в секундах, в течение которого может выполняться операция проверки проекта или пакета до того, как будет остановлена. Значение по умолчанию — 300 секунд.<br /><br /> Выполнение проверки является асинхронной операцией. Чем больше проект или пакет, тем больше времени необходимо для проверки.<br /><br /> Дополнительные сведения о проверке проектов и пакетов см. в разделе [Integration Services Data Types in Expressions](../../integration-services/expressions/integration-services-data-types-in-expressions.md).|  
|Периодическая очистка журналов|OPERATION_CLEANUP_ENABLED|Установите это свойство в значение True, чтобы указать, что задание агента SQL Server по очистке операций выполняется. В противном случае установите свойство в значение False.|  
|Срок хранения (в днях)|RETENTION_WINDOW|Задайте максимальный срок хранения данных о допустимых операциях (в днях). Данные, которые хранятся дольше указанного числа дней, удаляются заданием агента SQL Server по очистке операций.|  
|Максимальное количество версий в проекте|MAX_PROJECT_VERSIONS|Укажите, сколько версий проекта будет храниться в каталоге. Когда общее количество версий превышает максимальное значение, более ранние версии проектов удаляются при выполнении задания по очистке версий проекта.|  
  
  