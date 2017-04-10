---
title: "Установка параметров индекса | Microsoft Docs"
ms.custom: ""
ms.date: "02/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-indexes"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "ALLOW_ROW_LOCKS, параметр"
  - "SORT_IN_TEMPDB, параметр"
  - "DROP_EXISTING, предложение"
  - "данные большого объема, индексы"
  - "PAD_INDEX"
  - "STATISTICS_NORECOMPUTE"
  - "параметр индекса MAXDOP, параметр"
  - "параметры индекса [SQL Server]"
  - "MAXDOP, параметр индекса"
  - "IGNORE_DUP_KEY, параметр"
  - "ALLOW_PAGE_LOCKS, параметр"
  - "ONLINE"
ms.assetid: 7969af33-e94c-41f7-ab89-9d9a2747cd5c
caps.latest.revision: 44
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 44
---
# Установка параметров индекса
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  В этом разделе описывается процесс изменения свойств индекса в [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] с помощью среды [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] или [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **В этом разделе**  
  
-   **Перед началом работы выполните следующие действия.**  
  
     [Ограничения](#Restrictions)  
  
     [Безопасность](#Security)  
  
-   **Изменение свойств индекса различными средствами.**  
  
     [Среда SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Перед началом  
  
###  <a name="Restrictions"></a> Ограничения  
  
-   К индексу с помощью предложения SET в инструкции ALTER INDEX немедленно применяются следующие параметры: ALLOW_PAGE_LOCKS, ALLOW_ROW_LOCKS, IGNORE_DUP_KEY и STATISTICS_NORECOMPUTE.  
  
-   Следующие параметры можно установить при перестройке индекса с помощью инструкции ALTER INDEX REBUILD или CREATE INDEX WITH DROP_EXISTING: PAD_INDEX, FILLFACTOR, SORT_IN_TEMPDB, IGNORE_DUP_KEY, STATISTICS_NORECOMPUTE, ONLINE, ALLOW_ROW_LOCKS, ALLOW_PAGE_LOCKS, MAXDOP и DROP_EXISTING (только CREATE INDEX).  
  
###  <a name="Security"></a> Безопасность  
  
####  <a name="Permissions"></a> Разрешения  
 Необходимо разрешение ALTER для таблицы или представления.  
  
##  <a name="SSMSProcedure"></a> Использование среды SQL Server Management Studio  
  
#### Изменение свойств индекса при помощи конструктора таблиц.  
  
1.  В обозревателе объектов щелкните знак «плюс», чтобы развернуть базу данных, содержащую таблицу, в которой необходимо изменить свойства индекса.  
  
2.  Чтобы развернуть папку **Таблицы** , щелкните значок «плюс».  
  
3.  Щелкните правой кнопкой мыши таблицу, в которой необходимо изменить свойства индекса, а затем выберите пункт **Проект**.  
  
4.  В меню **Конструктор таблиц** выберите пункт **Индексы и ключи**.  
  
5.  Выберите индекс, свойства которого необходимо изменить. Его свойства отобразятся в основной сетке.  
  
6.  Измените значения любого или всех свойств, чтобы внести изменения в индекс.  
  
7.  Щелкните **Закрыть**.  
  
8.  В меню **Файл** выберите пункт **Сохранить***имя_таблицы*.  
  
#### Изменение свойств индекса при помощи обозревателя объектов.  
  
1.  В обозревателе объектов щелкните знак «плюс», чтобы развернуть базу данных, содержащую таблицу, в которой необходимо изменить свойства индекса.  
  
2.  Чтобы развернуть папку **Таблицы** , щелкните значок «плюс».  
  
3.  Щелкните знак «плюс» (+), чтобы развернуть таблицу, в которой необходимо изменить свойства индекса.  
  
4.  Чтобы развернуть папку **Индексы** , щелкните знак «плюс» (+).  
  
5.  Щелкните правой кнопкой мыши индекс, свойства которого требуется изменить, и выберите пункт **Свойства**.  
  
6.  В разделе **Выбор страницы**щелкните **Параметры**.  
  
7.  Измените значения любого или всех свойств, чтобы внести изменения в индекс.  
  
8.  Чтобы добавить столбец индекса, удалить или изменить его позицию, выберите в диалоговом окне **Свойства индекса ― ** *имя_индекса* страницу **Общие**. Дополнительные сведения см. в разделе [Index Properties F1 Help](../../relational-databases/indexes/index-properties-f1-help.md).  
  
##  <a name="TsqlProcedure"></a> Использование Transact-SQL  
  
#### Просмотр свойств всех индексов в таблице  
  
1.  В **обозревателе объектов**подключитесь к экземпляру компонента [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  На стандартной панели выберите пункт **Создать запрос**.  
  
3.  Скопируйте следующий пример в окно запроса и нажмите кнопку **Выполнить**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT i.name AS index_name,   
        i.type_desc,   
        i.is_unique,   
        ds.type_desc AS filegroup_or_partition_scheme,   
        ds.name AS filegroup_or_partition_scheme_name,   
        i.ignore_dup_key,   
        i.is_primary_key,   
        i.is_unique_constraint,   
        i.fill_factor,   
        i.is_padded,   
        i.is_disabled,   
        i.allow_row_locks,   
        i.allow_page_locks,   
        i.has_filter,   
        i.filter_definition  
    FROM sys.indexes AS i  
       INNER JOIN sys.data_spaces AS ds ON i.data_space_id = ds.data_space_id  
    WHERE is_hypothetical = 0 AND i.index_id <> 0   
       AND i.object_id = OBJECT_ID('HumanResources.Employee');   
    GO  
  
    ```  
  
#### Задание свойств индекса  
  
1.  В **обозревателе объектов**подключитесь к экземпляру компонента [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  На стандартной панели выберите пункт **Создать запрос**.  
  
3.  Скопируйте следующие примеры в окно запроса и нажмите кнопку **Выполнить**.  
  
     [!code-sql[IndexDDL#AlterIndex4](../../relational-databases/indexes/codesnippet/tsql/set-index-options_1.sql)]  
  
     [!code-sql[IndexDDL#AlterIndex2](../../relational-databases/indexes/codesnippet/tsql/set-index-options_2.sql)]  
  
 Дополнительные сведения см. в разделе [ALTER INDEX (Transact-SQL)](../../t-sql/statements/alter-index-transact-sql.md).  
  
  