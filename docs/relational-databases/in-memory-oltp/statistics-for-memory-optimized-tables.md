---
title: "Статистика для таблиц, оптимизированных для памяти | Microsoft Docs"
ms.custom: ""
ms.date: "10/23/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine-imoltp"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e644766d-1d1c-43d7-83ff-8ccfe4f3af9f
caps.latest.revision: 18
author: "MightyPen"
ms.author: "genemi"
manager: "jhubbard"
caps.handback.revision: 18
---
# Статистика для таблиц, оптимизированных для памяти
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Оптимизатор запросов использует статистику о столбцах для создания планов запросов, которые повышают производительность запросов. Статистические данные собираются из таблиц в базе данных и сохраняются в метаданных этой базы.  
  
 Статистические данные создаются автоматически, но также могут быть созданы вручную. Например, статистика создается автоматически для ключевых столбцов индекса при создании индекса. Дополнительные сведения о создании статистики см. в разделе [Statistics](../../relational-databases/statistics/statistics.md).  
  
 Табличные данные обычно с течением времени изменяются по мере вставки, обновления и удаления строк. Это означает, что статистику необходимо периодически обновлять. По умолчанию статистика по таблицам обновляется автоматически, когда оптимизатор решит, что она могла устареть.  
  
 Замечания по статистике для оптимизированных для памяти таблиц.  
  
-   Начиная с версии SQL Server 2016 и в [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] автоматическое обновление статистики поддерживается для оптимизированных для памяти таблиц, если используется уровень совместимости базы данных не ниже 130. См. раздел [Уровень совместимости инструкции ALTER DATABASE (Transact-SQL)](../Topic/ALTER%20DATABASE%20Compatibility%20Level%20(Transact-SQL).md). Если в базе данных есть таблицы, которые были созданы ранее с использованием более низкого уровня совместимости, статистику необходимо обновить один раз вручную, чтобы затем ее обновление могло происходить автоматически.
  
-   Для скомпилированных в собственном коде хранимых процедур планы выполнения запросов в процедуре оптимизируются при компиляции процедуры, которое производится во время ее создания. Они не перекомпилируются автоматически при обновлении статистики. Таким образом, таблицы должны содержать показательный набор данных на момент создания процедур.  
  
-   Скомпилированные в собственном коде хранимые процедуры можно перекомпилировать вручную с помощью процедуры [sp_recompile (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-recompile-transact-sql.md). Кроме того, они перекомпилируются автоматически, если база данных переводится в режим "не в сети", а затем возвращается в режим "в сети", либо если произошла отработка отказа базы данных или перезапуск сервера.  
  
## Включение автоматического обновления статистики в существующих таблицах

При создании таблиц в базе данных с уровнем совместимости не ниже 130 автоматическое обновление включается для всех статистических данных по этим таблицам — никаких дополнительных действий не требуется.

Если в базе данных есть оптимизированные для памяти таблицы, которые были созданы в более ранней версии [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] или с использованием более низкого уровня совместимости, чем 130, статистику необходимо обновить один раз вручную, чтобы затем ее обновление могло происходить автоматически.

Чтобы включить автоматическое обновление статистики для оптимизированных для памяти таблиц, созданных с использованием более низкого уровня совместимости, выполните указанные ниже действия.

1. Измените уровень совместимости базы данных. `ALTER DATABASE CURRENT SET COMPATIBILITY_LEVEL=130`

2. Вручную обновите статистику для таблиц, оптимизированных для памяти. Ниже приведен пример скрипта, выполняющего эти действия.

3. Вручную перекомпилируйте хранимые процедуры, скомпилированные в собственном коде, чтобы можно было использовать обновленную статистику.

*Одноразовый скрипт для обновления статистики.* Для оптимизированных для памяти таблиц, созданных с использованием более низкого уровня совместимости, можно однократно выполнить следующий скрипт Transact-SQL, чтобы обновить статистику для всех оптимизированных для памяти таблиц и обеспечить ее дальнейшее автоматическое обновление (предполагается, что для базы данных включен параметр AUTO_UPDATE_STATISTICS):

```
-- Assuming AUTO_UPDATE_STATISTICS is already ON for your database:
-- ALTER DATABASE CURRENT SET AUTO_UPDATE_STATISTICS ON;

ALTER DATABASE CURRENT SET COMPATIBILITY_LEVEL = 130;
GO
DECLARE @sql NVARCHAR(MAX) = N'';
SELECT
      @sql += N'UPDATE STATISTICS '
         + quotename(schema_name(t.schema_id))
         + N'.'
         + quotename(t.name)
         + ';' + CHAR(13) + CHAR(10)
   FROM sys.tables AS t
   WHERE t.is_memory_optimized = 1 AND 
        t.object_id IN (SELECT object_id FROM sys.stats WHERE no_recompute=1)
;
EXECUTE sp_executesql @sql;
GO
-- Each row appended to @sql looks roughly like:
-- UPDATE STATISTICS [dbo].[MyMemoryOptimizedTable];
```

*Проверка включения автоматического обновления.* Приведенный ниже скрипт проверяет, включено ли автоматическое обновление статистики для оптимизированных для памяти таблиц. По завершении выполнения приведенный выше скрипт возвращает `1` в столбце `auto-update enabled` для всех объектов статистики.

```
SELECT 
    quotename(schema_name(o.schema_id)) + N'.' + quotename(o.name) AS [table],
    s.name AS [statistics object],
    1-s.no_recompute AS [auto-update enabled]
FROM sys.stats s JOIN sys.tables o ON s.object_id=o.object_id
WHERE o.is_memory_optimized=1
```

## Рекомендации по развертыванию таблиц и процедур  
 Чтобы убедиться в том, что оптимизатор запросов имеет актуальную статистику при создании планов запросов, развертывайте оптимизированные для памяти таблицы и скомпилированные в собственном коде хранимые процедуры, получающие доступ к этим таблицам, в четыре этапа.  
  
1.  Убедитесь в том, что база данных имеет уровень совместимости не ниже 130. См. раздел [Уровень совместимости инструкции ALTER DATABASE (Transact-SQL)](../Topic/ALTER%20DATABASE%20Compatibility%20Level%20(Transact-SQL).md).

2.  Создайте таблицы и индексы. Индексы необходимо указывать как встроенные в инструкциях **CREATE TABLE**.  
  
3.  Загрузите данные в таблицы.  
  
4.  Создайте хранимые процедуры, обращающиеся к таблицам.  
  
 Создание скомпилированных в собственном коде хранимых процедур после загрузки данных гарантирует то, что оптимизатор имеет доступ к статистическим данным для оптимизированных для памяти таблиц. Это обеспечит формирование эффективных планов запросов при компиляции процедуры.  

## См. также:  
 [Таблицы, оптимизированные для памяти](../../relational-databases/in-memory-oltp/memory-optimized-tables.md)  
  
  