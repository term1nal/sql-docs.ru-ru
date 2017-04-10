---
title: "SQL Server, объект Workload Group Stats | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "12/04/2015"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Объект Workload Group Stats"
  - "SQLServer: статистика группы рабочей нагрузки"
ms.assetid: ca20e4f6-50ec-4456-900d-87d280fde2b3
caps.latest.revision: 14
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 14
---
# SQL Server, объект Workload Group Stats
  Объект статистики группы рабочей нагрузки SQLServer:Workload Group Stats содержит счетчики производительности, сообщающие основные данные статистики группы рабочей нагрузки регулятора ресурсов.  
  
 Каждая активная группа рабочей нагрузки создает экземпляр объекта статистики группы рабочей нагрузки SQLServer:Workload Group Stats, при этом имя экземпляра совпадает с именем группы рабочей нагрузки в регуляторе ресурсов. В следующей таблице описываются счетчики, поддерживаемые этим экземпляром.  
  
|Имя счетчика|Описание|  
|------------------|-----------------|  
|**Активные параллельные потоки**|Текущее число используемых параллельных потоков.|  
|**Активные запросы**|Число запросов, выполняющихся в настоящее время в этой группе рабочей нагрузки. Это значение должно быть равно количеству строк в представлении sys.dm_exec_requests, отфильтрованных по идентификатору группы.|  
|**Заблокированные запросы**|Фактическое количество заблокированных запросов в группе рабочей нагрузки. Это может использоваться для определения характеристик рабочей нагрузки.|  
|**Процент задержки ЦП**|Системные ЦП задерживаются для всех запросов в указанном экземпляре объекта производительности в процентах от общего времени активности.| 
|**Базовый % задержки ЦП**|Только для внутреннего применения.| 
|**Процент эффективной загрузки ЦП**|Загрузка системных ЦП всеми запросами в указанном экземпляре производительности в процентах от общего времени активности.| 
|**База % эффективной загрузки ЦП**|Только для внутреннего применения.| 
|**Загрузка ЦП, %**|Использование пропускной способности ЦП всеми запросами данной группы рабочей нагрузки, измеряемое по отношению к рабочему компьютеру и нормализованное по всем центральным процессорам системы. Это значение будет изменено при изменении количества ЦП, доступных для процесса [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Оно не нормализовано по отношению к значению, получаемому процессом [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .| 
|**Загрузка ЦП, база %**|Только для внутреннего применения.| 
|**Процент нарушений ЦП**|Разница между резервированием ЦП и эффективным планированием в процентах.|  
|**Максимальное время ЦП для запроса (мс)**|Максимальное время ЦП в миллисекундах, затраченное на запрос, выполняющийся в группе рабочей нагрузки в данный момент.|  
|**Максимальный объем памяти, предоставленный запросу (КБ)**|Максимальное значение предоставления памяти для запроса, в килобайтах (КБ).|  
|**Оптимизаций запросов/с**|Число операций по оптимизации запросов, выполняемых в данной группе рабочей нагрузки за одну секунду. Это может использоваться для определения характеристик рабочей нагрузки.|  
|**Запросы в очереди**|Текущее количество запросов в очереди, ожидающих обработки. Этот счетчик может иметь ненулевое значение, если после достижения ограничения GROUP_MAX_REQUESTS происходит регулирование.|  
|**Сокращенное выделение памяти/с**|Количество запросов в секунду, получающих меньше оптимального объема памяти.|  
|**Выполнено запросов/с**|Число запросов, полностью обработанных в группе рабочей нагрузки. Это значение является накапливаемым.|  
|**Неоптимальных планов/с**|Число неоптимальных планов, создаваемых в данной группе рабочей нагрузки за секунду.|  
  
## См. также:  
 [Наблюдение за использованием ресурсов (системный монитор)](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [SQL Server, объект Resource Pool Stats](../../relational-databases/performance-monitor/sql-server-resource-pool-stats-object.md)   
 [регулятор ресурсов](../../relational-databases/resource-governor/resource-governor.md)  
  
  