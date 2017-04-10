---
title: "Скомпилированные в собственном коде хранимые процедуры | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine-imoltp"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "скомпилированные в собственном коде хранимые процедуры"
ms.assetid: d5ed432c-10c5-4e4f-883c-ef4d1fa32366
caps.latest.revision: 54
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 54
---
# Скомпилированные в собственном коде хранимые процедуры
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  Скомпилированные в собственном коде хранимые процедуры — это хранимые процедуры [!INCLUDE[tsql](../../includes/tsql-md.md)], скомпилированные в машинный код, который обращается к таблицам с оптимизацией для памяти. Скомпилированные в собственном коде хранимые процедуры позволяют эффективно выполнять запросы и бизнес-логику в хранимой процедуре. Дополнительные сведения о процессе компиляции в собственный код см. в разделе [Native Compilation of Tables and Stored Procedures](../../relational-databases/in-memory-oltp/native-compilation-of-tables-and-stored-procedures.md). Дополнительные сведения о миграции дисковых хранимых процедур в скомпилированные в собственном коде хранимые процедуры см. в разделе [Проблемы миграции, связанные с хранимыми процедурами, которые скомпилированы в собственном коде](../../relational-databases/in-memory-oltp/migration-issues-for-natively-compiled-stored-procedures.md).  
  
> [!NOTE]  
>  Одним из различий между интерпретируемыми (дисковыми) хранимыми процедурами и хранимыми процедурами, скомпилированными в собственном коде, является то, что интерпретируемые хранимые процедуры компилируются при первом выполнении, а хранимые процедуры, скомпилированные в собственном коде, компилируются при их создании. При работе со скомпилированными хранимыми процедурами многие условия ошибки (арифметическое переполнение, преобразование типов и в некоторых случаях деления на нуль) могут быть обнаружены во время создания, что приведет к сбою операции создания компилируемой хранимой процедуры. При работе с интерпретируемыми хранимыми процедурами эти условия ошибки обычно не приводят к появлению ошибок при создании хранимой процедуры, но все выполнения такой процедуры завершатся ошибкой.  
  
 Подразделы в этом разделе:  
  
-   [Создание хранимых процедур, скомпилированных в собственном коде](../../relational-databases/in-memory-oltp/creating-natively-compiled-stored-procedures.md)  
  
-   [Блоки ATOMIC](../../relational-databases/in-memory-oltp/атомарные-блоки-в-собственных-процедурах.md)  
  
-   [Поддерживаемые функции для модулей, скомпилированных в собственном коде T-SQL](../../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md)  
  
-   [Поддерживаемые конструкции DDL для модулей, скомпилированных в собственном коде T-SQL](../../relational-databases/in-memory-oltp/supported-ddl-for-natively-compiled-t-sql-modules.md)  
  
-   [Скомпилированные в собственном коде хранимые процедуры и параметры SET выполнения](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures-and-execution-set-options.md)  
  
-   [Рекомендации по вызову хранимых процедур, скомпилированных в собственном коде](../../relational-databases/in-memory-oltp/best-practices-for-calling-natively-compiled-stored-procedures.md)  
  
-   [Отслеживание производительности скомпилированных в собственном коде хранимых процедур](../../relational-databases/in-memory-oltp/monitoring-performance-of-natively-compiled-stored-procedures.md)  
  
-   [Вызов хранимых процедур, скомпилированных в собственном коде, из приложений для доступа к данным](../../relational-databases/in-memory-oltp/calling-natively-compiled-stored-procedures-from-data-access-applications.md)  
  
## См. также:  
 [Таблицы, оптимизированные для памяти](../../relational-databases/in-memory-oltp/memory-optimized-tables.md)  
  
  