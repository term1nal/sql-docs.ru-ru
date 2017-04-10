---
title: "Средства расширенных событий | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
  - "xevents"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "расширенные события [SQL Server], использование"
  - "расширенные события [SQL Server], параметры для использования"
ms.assetid: d312a9ff-50ba-4721-baef-50bfd3169d38
caps.latest.revision: 19
author: "MightyPen"
ms.author: "genemi"
manager: "jhubbard"
caps.handback.revision: 19
---
# Средства расширенных событий
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  Для создания сеансов расширенных событий [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] и управления ими можно использовать следующие средства:  
  
-   Инструкции языка описания данных DDL. Позволяют создавать и изменять сеанс расширенных событий.  
  
-   Динамическое административное представление, представления каталогов и системные таблицы. Позволяют получать данные и метаданные сеансов с помощью инструкций [!INCLUDE[tsql](../../includes/tsql-md.md)] . Системные таблицы помогают определить существующие эквиваленты расширенных событий для классов и столбцов событий трассировки SQL.  
  
-   Узел **Расширенные события** в обозревателе объектов. Позволяет запускать, останавливать и удалять сеансы, а также импортировать и экспортировать шаблоны сеансов.  
  
-   Поставщик [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell. Предоставляет широкий набор функций для создания, изменения сеансов расширенных событий и управления ими. Дополнительные сведения см. в статье [Использование поставщика PowerShell для расширенных событий](../../relational-databases/extended-events/use-the-powershell-provider-for-extended-events.md).  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Позволяет создавать и выполнять образцы кода, приведенные в разделах справочника по расширенным событиям. Дополнительные сведения см. в статье [Семантический поиск](../../ssms/object/object-explorer.md).  
  
 Помимо сеансов, которые создает пользователь, на сервере существует системный сеанс по умолчанию для сбора данных о работоспособности системы. В этом сеансе собираются системные данные, которые можно использовать для решения проблем производительности. Дополнительные сведения см. в статье [Использование сеанса system_health](../../relational-databases/extended-events/use-the-system-health-session.md).  
  
## Инструкции DDL  
 Следующие инструкции DDL можно использовать для создания, изменения и удаления сеансов расширенных событий.  
  
|Название|Описание|  
|----------|-----------------|  
|[CREATE EVENT SESSION (Transact-SQL)](../../t-sql/statements/create-event-session-transact-sql.md)|Создает объект сеанса расширенных событий, определяющий источник событий, цели и параметры сеанса событий.|  
|[ALTER EVENT SESSION (Transact-SQL)](../../t-sql/statements/alter-event-session-transact-sql.md)|Запускает или останавливает сеанс событий или изменяет конфигурацию сеанса.|  
|[DROP EVENT SESSION (Transact-SQL)](../../t-sql/statements/drop-event-session-transact-sql.md)|Удаляет сеанс событий.|  
  
## Представления каталога  
 Следующие представления каталога используются для получения метаданных, сформированных при создании сеанса событий.  
  
|Название|Описание|  
|----------|-----------------|  
|[sys.server_event_sessions (Transact-SQL)](../../relational-databases/system-catalog-views/sys-server-event-sessions-transact-sql.md)|Содержит список определений всех сеансов событий.|  
|[sys.server_event_session_actions (Transact-SQL)](../../relational-databases/system-catalog-views/sys-server-event-session-actions-transact-sql.md)|Возвращает строку для каждого действия над каждым событием из сеанса событий.|  
|[sys.server_event_session_events (Transact-SQL)](../../relational-databases/system-catalog-views/sys-server-event-session-events-transact-sql.md)|Возвращает строку для каждого события в сеансе событий.|  
|[sys.server_event_session_fields (Transact-SQL)](../../relational-databases/system-catalog-views/sys-server-event-session-fields-transact-sql.md)|Возвращает строку для каждого настраиваемого столбца, явно установленного на события и цели.|  
|[sys.server_event_session_targets (Transact-SQL)](../../relational-databases/system-catalog-views/sys-server-event-session-targets-transact-sql.md)|Возвращает строку для каждой цели события для сеанса событий.|  
  
## Динамические административные представления  
 Следующие динамические административные представления используются для получения метаданных и данных сеанса. Метаданные получают из представлений каталога, а данные сеанса создаются при запуске и работе сеанса событий.  
  
> [!NOTE]  
>  Эти представления не содержат данных сеанса до запуска сеанса.  
  
|Название|Описание|  
|----------|-----------------|  
|[sys.dm_os_dispatcher_pools (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-os-dispatcher-pools-transact-sql.md)|Возвращает сведения о пулах диспетчера сеансов.|  
|[sys.dm_xe_objects (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-xe-objects-transact-sql.md)|Возвращает строку для каждого объекта, представленного пакетом событий.|  
|[sys.dm_xe_object_columns (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-xe-object-columns-transact-sql.md)|Возвращает сведения о схеме для всех объектов.|  
|[sys.dm_xe_packages (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-xe-packages-transact-sql.md)|Содержит список всех пакетов, зарегистрированных подсистемой расширенных событий.|  
|[sys.dm_xe_sessions (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-xe-sessions-transact-sql.md)|Возвращает сведения об активном сеансе расширенных событий.|  
|[sys.dm_xe_session_targets (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-xe-session-targets-transact-sql.md)|Возвращает сведения о целях сеанса.|  
|[sys.dm_xe_session_events (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-xe-session-events-transact-sql.md)|Возвращает сведения о событиях сеанса.|  
|[sys.dm_xe_session_event_actions (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-xe-session-event-actions-transact-sql.md)|Возвращает сведения о действиях сеанса событий.|  
|[sys.dm_xe_map_values (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-xe-map-values-transact-sql.md)|Содержит сопоставления внутренних цифровых ключей с понятным текстом.|  
|[sys.dm_xe_session_object_columns (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-xe-session-object-columns-transact-sql.md)|Отображает значения конфигурации объектов, привязанных к сеансу.|  
  
## Системные таблицы  
 Следующие системные таблицы используются для получения сведений об эквивалентах расширенных событий для классов и столбцов событий трассировки SQL.  
  
|Название|Описание|  
|----------|-----------------|  
|[trace_xe_event_map (Transact-SQL)](../Topic/trace_xe_event_map%20\(Transact-SQL\).md)|Содержит одну строку для каждого события из числа расширенных событий, сопоставленного с классом событий трассировки SQL.|  
|[trace_xe_action_map (Transact-SQL)](../Topic/trace_xe_action_map%20\(Transact-SQL\).md)|Содержит одну строку для каждого действия из числа расширенных событий, сопоставленного с идентификатором столбца трассировки SQL.|  
  
## См. также:  
 [Динамические административные представления и функции (Transact-SQL)](../Topic/Dynamic%20Management%20Views%20and%20Functions%20\(Transact-SQL\).md)   
 [Представления каталога (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Таблицы расширенных событий SQL Server (Transact-SQL)](../Topic/SQL%20Server%20Extended%20Events%20Tables%20\(Transact-SQL\).md)   
 [Использование сеанса system_health](../../relational-databases/extended-events/use-the-system-health-session.md)   
 [Использование поставщика PowerShell для расширенных событий](../../relational-databases/extended-events/use-the-powershell-provider-for-extended-events.md)  
  
  