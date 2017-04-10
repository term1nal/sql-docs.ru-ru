---
title: "Настройка базы данных Stretch для таблицы | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "08/05/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.service: "sql-server-stretch-database"
ms.suite: ""
ms.technology: 
  - "dbe-stretch"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "База данных Stretch, настройка таблицы"
  - "настройка таблицы для базы данных Stretch"
ms.assetid: de4ac0c5-46ef-4593-a11e-9dd9bcd3ccdc
caps.latest.revision: 44
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 43
---
# Настройка базы данных Stretch для таблицы
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Чтобы настроить таблицу для базы данных Stretch, в SQL Server Management Studio выберите для нужной таблицы команду **Растяжение | Включить**, чтобы открыть мастер **Включение растяжения для таблицы**. Функцию растягивания для таблицы можно включить также с помощью Transact-SQL. Либо можно создать новую таблицу, уже настроенную для базы данных Stretch.  
  
-   Если холодные данные хранятся в отдельной таблице, эту таблицу можно перенести полностью.  
  
-   Если таблица содержит как горячие, так и холодные данные, строки для переноса можно выбрать с помощью функции фильтров.    
 
 **Предварительные требования**. Если для таблицы выбрать команду **Растяжение | Включить**, предварительно не настроив базу данных Stretch для всей базы данных, мастер сначала настроит базу данных для базы данных Stretch. Следуйте указаниям в разделе [Запуск мастера включения растяжения для базы данных](../../sql-server/stretch-database/get-started-by-running-the-enable-database-for-stretch-wizard.md) вместо пошаговых инструкций в этом разделе.  
  
 **Разрешения**. Чтобы настроить базу данных Stretch для таблицы или базы данных, требуются разрешения db_owner. Также нужно обладать правами на изменение таблицы.  

 >   [!NOTE] Если позднее вы решите отключить Базу данных Stretch, помните, что ее отключение для таблицы или базы данных не ведет к удалению удаленного объекта. Если вы хотите удалить удаленную таблицу или базу данных, это нужно сделать с помощью портала управления Azure. Пока удаленные объекты не будут удалены вручную, их хранение будет сопровождаться затратами в Azure.
 
##  <a name="EnableWizardTable"></a> Настройка базы данных Stretch для таблицы в с помощью мастера  
 **Запуск мастера**  
 1.  В среде SQL Server Management Studio в обозревателе объектов выберите таблицу, для которой нужно включить перенос.  
  
2.  Щелкните таблицу правой кнопкой мыши и выберите **Растяжение** и **Включить**, чтобы запустить мастер.  
  
 **Введение**  
 Изучите информацию о назначении мастера и предварительные требования.  
  
 **Выбор таблиц из базы данных**  
 Убедитесь, что выбрана нужная таблица.  
  
 Можно перенести таблицу полностью или указать простую функцию фильтров в мастере. Если требуется использовать другой тип функции фильтров, чтобы выбрать строки для переноса, выполните одно из следующих действий.  
  
-   Закройте мастер и выполните инструкцию ALTER TABLE, чтобы включить растяжение для таблицы и указать функцию фильтров.  
  
-   Выполните инструкцию ALTER TABLE, чтобы указать функцию фильтров после выхода из мастера. Необходимые пошаговые инструкции см. в разделе [Добавление функции фильтров после запуска мастера](../../sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md#addafterwiz).  
  
 Синтаксис ALTER TABLE описан далее в этом разделе.  
  
 **Сводка**  
 Просмотрите введенные значения и выбранные в мастере параметры. Нажмите кнопку **Готово** , чтобы включить растягивание.  
  
 **Результаты**  
 Просмотрите результаты операции.  
  
##  <a name="EnableTSQLTable"></a> Настройка базы данных Stretch для таблицы с помощью Transact-SQL  
 Вы можете настроить базу данных Stretch для существующей таблицы либо создать новую таблицу, для которой уже настроена база данных Stretch. Обе операции можно выполнить с помощью Transact-SQL.  
  
### Параметры  
 Чтобы настроить базу данных Stretch для таблицы, используйте в инструкциях CREATE TABLE и ALTER TABLE следующие параметры.  
  
-   Если в таблице содержатся горячие и холодные данные, можно использовать предложение `FILTER_PREDICATE = <function>`, чтобы задать функцию для выбора переносимых строк. Этот предикат должен вызывать встроенную функцию с табличным значением. Дополнительные сведения см. в разделе [Выбор строк для миграции с использованием функции фильтров](../../sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md). Если функция фильтров не указана, переносится вся таблица.  
  
    > [!IMPORTANT]  
    >  Если указать плохо оптимизированную функцию фильтров, перенос данных будет выполняться медленно. База данных Stretch применяет функцию фильтров к таблице с помощью оператора CROSS APPLY.  
  
-   Укажите `MIGRATION_STATE = OUTBOUND` , чтобы немедленно запустить перенос данных, либо  `MIGRATION_STATE = PAUSED` , чтобы отложить его.  
  
### Настройка базы данных Stretch для существующей таблицы  
 Чтобы настроить базу данных Stretch для существующей таблицы, выполните команду ALTER TABLE.  
  
 Ниже приведен пример, в котором переносится вся таблица и перенос данных начинается немедленно.  
  
```tsql  
USE <Stretch-enabled database name>;
GO
ALTER TABLE <table name>  
    SET ( REMOTE_DATA_ARCHIVE = ON ( MIGRATION_STATE = OUTBOUND ) ) ;  
GO
```  
  
 Ниже приведен пример, в котором переносятся только строки, возвращаемые встроенной функцией с табличным значением `dbo.fn_stretchpredicate`. Начало переноса откладывается. Дополнительные сведения о функции фильтров см. в разделе [Выбор строк для миграции с использованием функции фильтров](../../sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md).  
  
```tsql  
USE <Stretch-enabled database name>;
GO
ALTER TABLE <table name>  
    SET ( REMOTE_DATA_ARCHIVE = ON (  
        FILTER_PREDICATE = dbo.fn_stretchpredicate(),  
        MIGRATION_STATE = PAUSED ) ) ;  
 GO
```  
  
 Дополнительные сведения см. в разделе [ALTER TABLE (Transact-SQL)](../../t-sql/statements/alter-table-transact-sql.md).  
  
### Создание новой таблицы, для которой уже настроена база данных Stretch  
 Чтобы создать новую таблицу с уже настроенной базой данных Stretch, выполните команду CREATE TABLE.  
  
 Ниже приведен пример, в котором переносится вся таблица и перенос данных начинается немедленно.  
  
```tsql  
USE <Stretch-enabled database name>;
GO
CREATE TABLE <table name>
    ( ... )  
    WITH ( REMOTE_DATA_ARCHIVE = ON ( MIGRATION_STATE = OUTBOUND ) ) ;  
GO
```  
  
 Ниже приведен пример, в котором переносятся только строки, возвращаемые встроенной функцией с табличным значением `dbo.fn_stretchpredicate`. Начало переноса откладывается. Дополнительные сведения о функции фильтров см. в разделе [Выбор строк для миграции с использованием функции фильтров](../../sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md).  
  
```tsql  
USE <Stretch-enabled database name>;
GO
CREATE TABLE <table name> 
    ( ... )  
    WITH ( REMOTE_DATA_ARCHIVE = ON (  
        FILTER_PREDICATE = dbo.fn_stretchpredicate(),  
        MIGRATION_STATE = PAUSED ) ) ;  
GO  
```  
  
 Дополнительные сведения см. в разделе [CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md).  
  
## См. также:  
 [ALTER TABLE (Transact-SQL)](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)  
  
  