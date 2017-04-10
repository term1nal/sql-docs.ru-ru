---
title: "Создание пользовательского набора элементов сбора, использующего тип сборщика &#171;Универсальный запрос T-SQL&#187; (Transact-SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/23/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "тип «сборщик запросов T-SQL»"
  - "наборы элементов сбора [SQL Server], создание настраиваемых"
ms.assetid: 6b06db5b-cfdc-4ce0-addd-ec643460605b
caps.latest.revision: 26
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
---
# Создание пользовательского набора элементов сбора, использующего тип сборщика &#171;Универсальный запрос T-SQL&#187; (Transact-SQL)
  Можно создать пользовательский набор сбора с элементами, которые будут использовать тип сборщика «Универсальный запрос T-SQL» с помощью хранимых процедур, поставляемых вместе со сборщиком данных. Эта задача решается с помощью редактора запросов в среде [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] для выполнения следующих процедур.  
  
-   Настройка расписаний передачи.  
  
-   Определение и создание набора элементов сбора  
  
-   Определение и создание элемента сбора.  
  
-   Проверка существования набора сбора и элементов сбора.  
  
> [!NOTE]  
>  Перед созданием пользовательского набора сбора необходимо настроить параметры сбора данных. Дополнительные сведения см. в разделе [Настройка параметров сбора данных (Transact-SQL)](../../relational-databases/data-collection/configure-data-collection-parameters-transact-sql.md).  
  
### Определение и создание набора элементов сбора  
  
1.  Определите новый набор сбора с помощью хранимой процедуры sp_syscollector_create_collection_set.  
  
    ```  
    USE msdb;  
    DECLARE @collection_set_id int;  
    DECLARE @collection_set_uid uniqueidentifier;  
    EXEC sp_syscollector_create_collection_set   
        @name=N'DMV Test 1',   
        @collection_mode=0,   
        @description=N'This is a test collection set',   
        @logging_level=1,   
        @days_until_expiration=14,   
        @schedule_name=N'CollectorSchedule_Every_15min',   
        @collection_set_id=@collection_set_id OUTPUT,   
        @collection_set_uid=@collection_set_uid OUTPUT;  
    SELECT @collection_set_id, @collection_set_uid;  
    ```  
  
     В качестве режима сбора можно задать либо 0 (с кэшированием), либо 1 (без кэширования).  
  
     Уровень ведения журнала можно установить в значение 0, 1 или 2.  
  
     Следующие предварительно настроенные расписания поставляются со сборщиком данных.  
  
    -   CollectorSchedule_Every_5min  
  
    -   CollectorSchedule_Every_10min  
  
    -   CollectorSchedule_Every_15min  
  
    -   CollectorSchedule_Every_30min  
  
    -   CollectorSchedule_Every_60min  
  
    -   CollectorSchedule_Every_6h  
  
     При необходимости можно создать новое расписание и использовать его в наборе сбора. Дополнительные сведения см. в разделе [Создание и присоединение расписаний к заданиям](../../ssms/agent/create-and-attach-schedules-to-jobs.md).  
  
### Определение и создание элемента сбора  
  
1.  Поскольку новый элемент сбора создан на базе универсального типа сборщика, который уже установлен, можно выполнить следующий код, чтобы изменить его идентификатор GUID для соответствия типу «Универсальный сборщик запросов T-SQL».  
  
    ```tsql  
    DECLARE @collector_type_uid uniqueidentifier;  
    SELECT @collector_type_uid = collector_type_uid FROM [msdb].[dbo].[syscollector_collector_types]   
    WHERE name = N'Generic T-SQL Query Collector Type';  
    DECLARE @collection_item_id int;  
    ```  
  
2.  С помощью хранимой процедуры sp_syscollector_create_collection_item создайте элемент сбора. Объявите схему для элемента сбора, чтобы он был сопоставлен со схемой, необходимой для типа сборщика «Универсальный запрос T-SQL».  
  
    ```tsql  
    EXEC sp_syscollector_create_collection_item   
        @name=N'Query Stats - Test 1',   
        @parameters=N'  
            <ns:TSQLQueryCollector xmlns:ns="DataCollectorType">  
            <Query>  
            <Value>SELECT * FROM sys.dm_exec_query_stats</Value>  
            <OutputTable>dm_exec_query_stats</OutputTable>  
            </Query>  
            </ns:TSQLQueryCollector>',   
        @collection_item_id=@collection_item_id OUTPUT,   
        @frequency=5,   
        @collection_set_id=@collection_set_id,   
        @collector_type_uid=@collector_type_uid;  
    SELECT @collection_item_id;  
    ```  
  
### Проверка существования набора сбора и элемента сбора  
  
1.  Перед запуском нового набора сбора запустите следующий запрос, чтобы убедиться, что новый набор сбора и его элемент сбора были созданы:  
  
    ```tsql  
    USE msdb;  
    SELECT * FROM syscollector_collection_sets;  
    SELECT * FROM syscollector_collection_items;  
    GO  
    ```  
  
     Можно также провести визуальную проверку в среде [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. В обозревателе объектов разверните узел **Управление** , затем узел **Сбор данных**. Будет отображен новый набор сбора. Красный круглый кружок на значке набора сбора означает, что набор сбора остановлен.  
  
## Пример  
 В следующем образце кода объединены примеры, приведенные в предыдущих шагах. Обратите внимание, что частота сбора, установленная для данного элемента сбора (5 секунд), не учитывается, поскольку для набора сбора установлен режим сбора 0, то есть режим с кэшированием. Дополнительные сведения см. в разделе [Data Collection](../../relational-databases/data-collection/data-collection.md).  
  
```tsql  
USE msdb;  
  
DECLARE @collection_set_id int;  
DECLARE @collection_set_uid uniqueidentifier  
  
EXEC dbo.sp_syscollector_create_collection_set  
    @name = N'DMV Stats Test 1',  
    @collection_mode = 0,  
    @description = N'This is a test collection set',  
    @logging_level=1,  
    @days_until_expiration = 14,  
    @schedule_name=N'CollectorSchedule_Every_15min',  
    @collection_set_id = @collection_set_id OUTPUT,  
    @collection_set_uid = @collection_set_uid OUTPUT;  
SELECT @collection_set_id,@collection_set_uid;  
  
DECLARE @collector_type_uid uniqueidentifier;  
SELECT @collector_type_uid = collector_type_uid FROM syscollector_collector_types   
WHERE name = N'Generic T-SQL Query Collector Type';  
  
DECLARE @collection_item_id int;  
EXEC sp_syscollector_create_collection_item  
@name= N'Query Stats - Test 1',  
@parameters=N'  
<ns:TSQLQueryCollector xmlns:ns="DataCollectorType">  
<Query>  
  <Value>select * from sys.dm_exec_query_stats</Value>  
  <OutputTable>dm_exec_query_stats</OutputTable>  
</Query>  
 </ns:TSQLQueryCollector>',  
    @collection_item_id = @collection_item_id OUTPUT,  
    @frequency = 5, -- This parameter is ignored in cached mode  
    @collection_set_id = @collection_set_id,  
    @collector_type_uid = @collector_type_uid;  
SELECT @collection_item_id;  
  
GO  
```  
  
## См. также:  
 [Хранимые процедуры сборщика данных (Transact-SQL)](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [Управление расписаниями](../../ssms/agent/manage-schedules.md)   
 [Запуск или остановка набора элементов сбора](../../relational-databases/data-collection/start-or-stop-a-collection-set.md)  
  
  