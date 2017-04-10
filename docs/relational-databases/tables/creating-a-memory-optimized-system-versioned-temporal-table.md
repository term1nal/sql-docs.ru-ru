---
title: "Создание оптимизированной для памяти темпоральной таблицы с системным управлением версиями | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "05/05/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-tables"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1c1fc682-bf5b-4096-a0ff-3235d71c205a
caps.latest.revision: 14
author: "CarlRabeler"
ms.author: "carlrab"
manager: "jhubbard"
caps.handback.revision: 14
---
# Создание оптимизированной для памяти темпоральной таблицы с системным управлением версиями
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Подобно созданию таблицы журнала на диске, можно создать темпоральную таблицу, оптимизированную для памяти, несколькими способами.  
  
> [!NOTE]  
>  Для создания оптимизированных для памяти таблиц необходимо сначала создать [файловую группу с оптимизированной памятью](../../relational-databases/in-memory-oltp/the-memory-optimized-filegroup.md).  
  
 Темпоральная таблица с таблицей журнала по умолчанию удобна в тех случаях, когда вы хотите контролировать именование, но при этом автоматически создать таблицу журнала с конфигурацией по умолчанию. В приведенном ниже примере новая оптимизированная для памяти таблица с системным управлением версиями связывается с новой таблицей журнала на диске.  
  
```  
CREATE SCHEMA History  
GO  
CREATE TABLE dbo.Department   
(  
    DepartmentNumber char(10) NOT NULL PRIMARY KEY NONCLUSTERED,   
    DepartmentName varchar(50) NOT NULL,   
    ManagerID int  NULL,   
    ParentDepartmentNumber char(10) NULL,   
    SysStartTime datetime2 GENERATED ALWAYS AS ROW START HIDDEN NOT NULL,   
    SysEndTime datetime2 GENERATED ALWAYS AS ROW END HIDDEN NOT NULL,     
    PERIOD FOR SYSTEM_TIME (SysStartTime,SysEndTime)     
)  
WITH   
    (  
        MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA,  
            SYSTEM_VERSIONING = ON ( HISTORY_TABLE = History.DepartmentHistory )   
    );  
```  
  
 Создание темпоральной таблицы, связанной с существующей таблицей журнала, полезно, если вам нужно добавить системное управление версиями с использованием существующей таблицы, например, если требуется перенести пользовательское темпоральное решение в решение со встроенной поддержкой. В приведенном ниже примере создается новая темпоральная таблица, связанная с существующей таблицей журнала.  
  
```  
  
--Existing table   
CREATE TABLE Department_History   
(  
    DepartmentNumber char(10) NOT NULL,   
    DepartmentName varchar(50) NOT NULL,   
    ManagerID int  NULL,   
    ParentDepartmentNumber char(10) NULL,   
    SysStartTime datetime2 NOT NULL,   
    SysEndTime datetime2 NOT NULL   
);  
--Temporal table  
CREATE TABLE Department   
(  
    DepartmentNumber char(10) NOT NULL PRIMARY KEY NONCLUSTERED,   
    DepartmentName varchar(50) NOT NULL,   
    ManagerID INT  NULL,   
    ParentDepartmentNumber char(10) NULL,   
    SysStartTime datetime2 GENERATED ALWAYS AS ROW START HIDDEN NOT NULL,   
    SysEndTime datetime2 GENERATED ALWAYS AS ROW END HIDDEN NOT NULL,     
    PERIOD FOR SYSTEM_TIME (SysStartTime,SysEndTime)    
)  
WITH   
    (  
        SYSTEM_VERSIONING = ON  
            (  
                HISTORY_TABLE = dbo.Department_History  
                , DATA_CONSISTENCY_CHECK = ON   
            )  
        , MEMORY_OPTIMIZED = ON  
        , DURABILITY = SCHEMA_AND_DATA  
    );  
```  
  
## Эта статья помогла вам? Мы слушаем  
 Какие сведения вы искали и удалось ли вам их найти? Мы прислушиваемся к вашим отзывам для совершенствования материалов. Отправляйте свои комментарии по адресу [sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com?subject=Your%20feedback%20about%20the%20Creating%20a%20Memory-Optimized%20System-Versioned%20Temporal%20Table%20page)  
  
## См. также:  
 [Темпоральные таблицы с системным управлением версиями и таблицы, оптимизированные для памяти](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)   
 [Работа с оптимизированными для памяти темпоральными таблицами с системным управлением версиями](../../relational-databases/tables/working-with-memory-optimized-system-versioned-temporal-tables.md)   
 [Мониторинг оптимизированных для памяти темпоральных таблиц с системным управлением версиями](../../relational-databases/tables/monitoring-memory-optimized-system-versioned-temporal-tables.md)   
 [Вопросы производительности темпоральных таблиц с системным управлением версиями, оптимизированных для памяти](../../relational-databases/tables/memory-optimized-system-versioned-temporal-tables-performance.md)   
 [Темпоральные таблицы](../../relational-databases/tables/temporal-tables.md)   
 [Проверка согласованности системной темпоральной таблицы](../../relational-databases/tables/temporal-table-system-consistency-checks.md)   
 [Управление хранением данных журнала в темпоральных таблицах с системным управлением версиями](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)   
 [Представления и функции метаданных для временной таблицы](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)  
  
  