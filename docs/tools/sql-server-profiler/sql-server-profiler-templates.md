---
title: "Шаблоны приложения SQL Server Profiler | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "шаблоны приложения SQL Server Profiler по умолчанию"
  - "шаблоны [SQL Server], приложение SQL Server Profiler"
  - "Profiler [SQL Server Profiler], шаблоны"
  - "шаблоны трассировки [SQL Server]"
  - "предопределенные шаблоны [приложение SQL Server Profiler ]"
  - "SQL Server Profiler, шаблоны"
ms.assetid: b674e491-dc58-47a1-acdd-7028e9a201fc
caps.latest.revision: 35
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 35
---
# Шаблоны приложения SQL Server Profiler
  Можно использовать приложение [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] для создания шаблонов, определяющих классы событий и столбцы данных с целью включения в трассировку. После определения и сохранения шаблона можно запустить трассировку, которая будет записывать данные для каждого выбранного класса событий. Шаблоны можно использовать для многих трассировок; сам шаблон не выполняется.  
  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] предлагает предопределенные шаблоны трассировки, которые позволяют легко настроить классы событий, которые наверняка потребуются для определенных трассировок. Например, шаблон «Стандартный» помогает создать общую трассировку для записи входов в систему, выходов из системы, завершенных пакетов и сведений о соединениях. Можно использовать этот шаблон без изменений для выполнения трассировок, либо как начальный вариант с целью создания дополнительных шаблонов с разными конфигурациями событий.  
  
> [!NOTE]  
>  Помимо трассировок из предопределенных шаблонов, приложение [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] позволяет создать трассировки из пустых шаблонов, которые по умолчанию не содержат никаких классов событий. Использование пустого шаблона трассировки полезно, если планируемая трассировка не похожа ни на одну существующую конфигурацию предопределенных шаблонов.  
  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] может выполнять трассировку множества типов серверов. Например, можно трассировать [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] и [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  Однако классы событий, которые могут быть включены, будут различаться для каждого сервера. Поэтому приложение [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] поддерживает различные шаблоны для различных серверов и делает доступным определенный шаблон, который соответствует выбранному типу сервера.  
  
## Предопределенные шаблоны  
 В дополнение к стандартному шаблону (по умолчанию), приложение [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] содержит несколько предопределенных шаблонов для контроля определенных типов событий. В следующей таблице перечисляются предопределенные шаблоны, их назначение, классы событий, для которых они получают сведения.  
  
|Имя шаблона|Назначение шаблона|Классы событий|  
|-------------------|----------------------|-------------------|  
|SP_Counts|Отслеживает поведение при выполнении хранимой процедуры с течением времени.|**SP:Starting**|  
|Standard Edition|Общая начальная точка для создания трассировки. Перехватывает все хранимые процедуры и выполняемые пакеты инструкций [!INCLUDE[tsql](../../includes/tsql-md.md)] . Используется для мониторинга общей активности сервера баз данных.|**Аудит входа в систему**<br /><br /> **Аудит выхода из системы**<br /><br /> **ExistingConnection**<br /><br /> **RPC:Completed**<br /><br /> **SQL:BatchCompleted**<br /><br /> **SQL:BatchStarting**|  
|TSQL|Захватывает все инструкции языка [!INCLUDE[tsql](../../includes/tsql-md.md)] , отправленные клиентами на [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , и время их отправки. Используется для отладки клиентских приложений.|**Аудит входа в систему**<br /><br /> **Аудит выхода из системы**<br /><br /> **ExistingConnection**<br /><br /> **RPC:Starting**<br /><br /> **SQL:BatchStarting**|  
|TSQL_Duration|Захватывает все инструкции языка [!INCLUDE[tsql](../../includes/tsql-md.md)], отправленные клиентами на [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], и время их выполнения (в миллисекундах), и группирует их по длительности. Используется для идентификации медленных запросов.|**RPC:Completed**<br /><br /> **SQL:BatchCompleted**|  
|TSQL_Grouped|Захватывает все инструкции языка [!INCLUDE[tsql](../../includes/tsql-md.md)], отправленные на [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], и время их отправки. Группирует сведения по имени пользователя или клиента, который отправил инструкцию. Используется для изучения запросов от определенного клиента или пользователя.|**Аудит входа в систему**<br /><br /> **Аудит выхода из системы**<br /><br /> **ExistingConnection**<br /><br /> **RPC:Starting**<br /><br /> **SQL:BatchStarting**|  
|TSQL_Locks|Захватывает все инструкции языка [!INCLUDE[tsql](../../includes/tsql-md.md)], переданные клиентами на [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], и исключительные события блокировки. Позволяет устранять неполадки с взаимоблокировками, временем истечения ожидания блокировок и событиями укрупнения блокировки.|**Blocked Process Report**<br /><br /> **SP:StmtCompleted**<br /><br /> **SP:StmtStarting**<br /><br /> **SQL:StmtCompleted**<br /><br /> **SQL:StmtStarting**<br /><br /> **Deadlock Graph**<br /><br /> **Lock:Cancel**<br /><br /> **Lock:Deadlock**<br /><br /> **Lock:Deadlock Chain**<br /><br /> **Lock:Escalation**<br /><br /> **Lock:Timeout (timeout>0)**|  
|TSQL_Replay|Захватывает подробные сведения об инструкциях [!INCLUDE[tsql](../../includes/tsql-md.md)], которые требуются для воспроизведения трассировки. Используется для выполнения последовательной настройки, такой как проверка пропускной способности.|**CursorClose**<br /><br /> **CursorExecute**<br /><br /> **CursorOpen**<br /><br /> **CursorPrepare**<br /><br /> **CursorUnprepare**<br /><br /> **Аудит входа в систему**<br /><br /> **Аудит выхода из системы**<br /><br /> **Existing Connection**<br /><br /> **RPC Output Parameter**<br /><br /> **RPC:Completed**<br /><br /> **RPC:Starting**<br /><br /> **Exec Prepared SQL**<br /><br /> **Prepare SQL**<br /><br /> **SQL:BatchCompleted**<br /><br /> **SQL:BatchStarting**|  
|TSQL_SPs|Захватывает подробные сведения обо всех выполняющихся хранимых процедурах. Используется для анализа составных шагов хранимых процедур. Добавьте событие **SP:Recompile** , если подозреваете, что хранимые процедуры находятся в процессе повторной компиляции.|**Аудит входа в систему**<br /><br /> **Аудит выхода из системы**<br /><br /> **ExistingConnection**<br /><br /> **RPC:Starting**<br /><br /> **SP:Completed**<br /><br /> **SP:Starting**<br /><br /> **SP:StmtStarting**<br /><br /> **SQL:BatchStarting**|  
|Настройка|Захватывает сведения о хранимых процедурах и выполнении пакетов инструкций языка [!INCLUDE[tsql](../../includes/tsql-md.md)] . Используется для создания трассировки, которую помощник по настройке компонента [!INCLUDE[ssDE](../../includes/ssde-md.md)] может использовать в качестве рабочей нагрузки для настройки баз данных.|**RPC:Completed**<br /><br /> **SP:StmtCompleted**<br /><br /> **SQL:BatchCompleted**|  
  
 Дополнительные сведения о классах событий см. в разделе [SQL Server Event Class Reference](../../relational-databases/event-classes/sql-server-event-class-reference.md).  
  
## Шаблон по умолчанию  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] автоматически назначает шаблон **Standard Edition** в качестве шаблона по умолчанию для любой новой трассировки. Однако шаблон по умолчанию можно заменить на любой предопределенный шаблон или определенный пользователем шаблон. Чтобы изменить шаблон по умолчанию, установите флажок **Применять как шаблон по умолчанию для выбранного типа сервера** при создании или редактировании шаблона на вкладке **Общие** в диалоговом окне **Свойства шаблона трассировки** .  
  
 Чтобы перейти в диалоговое окно **Свойства шаблона трассировки** , в приложении [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] **Файл** выберите пункт **Шаблоны**и затем выберите пункт **Создать шаблон** или **Изменить шаблон**.  
  
> [!NOTE]  
>  Для каждого типа сервера существует свой шаблон по умолчанию. Изменения шаблона по умолчанию для одного типа сервера не влияет на шаблон по умолчанию для сервера другого типа. Дополнительные сведения о настройке шаблона по умолчанию для определенного типа сервера см. в разделе [Установка значений по умолчанию для определения трассировки (приложение SQL Server Profiler)](../../tools/sql-server-profiler/set-trace-definition-defaults-sql-server-profiler.md).  
  
## См. также:  
 [Создание шаблона трассировки (приложение SQL Server Profiler)](../../tools/sql-server-profiler/create-a-trace-template-sql-server-profiler.md)   
 [Изменение шаблона трассировки (приложение SQL Server Profiler)](../../tools/sql-server-profiler/modify-a-trace-template-sql-server-profiler.md)   
 [Экспорт шаблона трассировки (приложение SQL Server Profiler)](../../tools/sql-server-profiler/export-a-trace-template-sql-server-profiler.md)   
 [Импорт шаблона трассировки (приложение SQL Server Profiler)](../../tools/sql-server-profiler/import-a-trace-template-sql-server-profiler.md)  
  
  