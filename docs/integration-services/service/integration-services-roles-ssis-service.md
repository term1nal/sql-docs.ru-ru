---
title: "Роли служб Integration Services (службы SSIS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "безопасность [службы Integration Services], роли"
  - "db_ssisoperator, роль"
  - "db_ssisadmin, роль"
  - "предопределенные роли базы данных [службы Integration Services]"
  - "пакеты [службы Integration Services], безопасность"
  - "роли [службы Integration Services]"
  - "db_ssisltduser, роль"
ms.assetid: 9702e90c-fada-4978-a473-1b1423017d80
caps.latest.revision: 50
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 50
---
# Роли служб Integration Services (службы SSIS)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] предоставляет конкретные предопределенные роли уровня базы данных для обеспечения безопасного доступа к пакетам, которые хранятся в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Доступные роли зависят от того, где хранятся пакеты: в базе данных каталога служб SSIS (SSISDB) или в базе данных msdb.  
  
## Роли в базе данных каталога служб SSIS (SSISDB)  
 База данных каталога служб SSIS (SSISDB) предоставляет следующие предопределенные роли уровня базы данных, позволяющие обеспечить безопасный доступ к пакетам и сведениям о пакетах:  
  
-   **ssis_admin** — предоставляет полный административный доступ к базе данных каталога служб SSIS.  
  
-   **ssis_logreader** — предоставляет разрешение на доступ ко всем представлениям, связанным с операционными журналами SSISDB.  
  
     Список представлений включает в себя: [catalog].[projects], [catalog].[packages], [catalog].[operations], [catalog].[extended_operation_info], [catalog].[operation_messages], [catalog].[event_messages], [catalog].[execution_data_statistics], [catalog].[execution_component_phases], [catalog].[execution_data_taps], [catalog].[event_message_context], [catalog].[executions], [catalog].[executables], [catalog].[executable_statistics], [catalog].[validations], [catalog].[execution_parameter_values] и [catalog].[execution_property_override_values].  
  
## Роли в базе данных msdb  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] содержат три предопределенные роли уровня базы данных, предназначенные для управления доступом к пакетам, которые сохранены в базе данных **msdb**: **db_ssisadmin**, **db_ssisltduser** и **db_ssisoperator**. С помощью среды [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] можно назначить роль пакету. Назначения ролей сохраняются в базу данных **msdb**.  
  
### Действия чтения и записи  
 В следующей таблице приводятся операции чтения и записи Windows и предопределенных ролей уровня базы данных в службах [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
|Роль|Операция чтения|Операция записи|  
|----------|-----------------|------------------|  
|**db_ssisadmin**<br /><br /> либо<br /><br /> **sysadmin**|Перечислить свои пакеты.<br /><br /> Перечислить все пакеты.<br /><br /> Посмотреть свои пакеты.<br /><br /> Посмотреть все пакеты.<br /><br /> Выполнить свои пакеты.<br /><br /> Выполнить все пакеты.<br /><br /> Экспортировать свои пакеты.<br /><br /> Экспортировать все пакеты.<br /><br /> Выполнить все пакеты агента [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|Импортировать пакеты.<br /><br /> Удалить свои пакеты.<br /><br /> Удалить все пакеты.<br /><br /> Изменить роли своих пакетов.<br /><br /> Изменить роли всех пакетов.<br /><br /> <br /><br /> **\*\* Предупреждение. \*\*** Члены роли db_ssisadmin и роли dc_admin могут повышать свои права доступа до sysadmin. Такое повышение права доступа может произойти, так как эти роли могут изменять пакеты служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], а пакеты [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] могут выполняться [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] при помощи контекста безопасности sysadmin агента [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Чтобы предотвратить такое повышение прав при выполнении планов обслуживания, наборов сбора данных и других пакетов служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], настройте задания агента [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], запускающие пакеты, на использование учетной записи-посредника с ограниченными правами или добавьте членов sysadmin в роли db_ssisadmin и dc_admin.|  
|**db_ssisltduser**|Перечислить свои пакеты.<br /><br /> Перечислить все пакеты.<br /><br /> Посмотреть свои пакеты.<br /><br /> Выполнить свои пакеты.<br /><br /> Экспортировать свои пакеты.|Импортировать пакеты.<br /><br /> Удалить свои пакеты.<br /><br /> Изменить роли своих пакетов.|  
|**db_ssisoperator**|Перечислить все пакеты.<br /><br /> Посмотреть все пакеты.<br /><br /> Выполнить все пакеты.<br /><br /> Экспортировать все пакеты.<br /><br /> Выполнить все пакеты агента [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|Нет|  
|**Администраторы Windows**|Просмотреть подробности выполнения всех запущенных пакетов.|Остановить все выполняемые пакеты.|  
  
### Таблица Sysssispackages  
 Таблица **sysssispackages** базы данных **msdb** содержит пакеты, сохраненные в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Дополнительные сведения см. в статье [sysssispackages (Transact-SQL)](../../relational-databases/system-tables/sysssispackages-transact-sql.md).  
  
 Таблица **sysssispackages** включает в себя столбцы, которые содержат сведения о ролях, назначенных пакетам.  
  
-   В столбце **readerrole** указывается роль, у которой есть право чтения из пакета.  
  
-   В столбце **writerrole** указывается роль, у которой есть право записи в пакет.  
  
-   Столбец **ownersid** содержит уникальный идентификатор безопасности пользователя, создавшего пакет. Этот столбец определяет владельца пакета.  
  
### Permissions  
 По умолчанию разрешения предопределенных ролей уровня базы данных **db_ssisadmin** и **db_ssisoperator** и уникальный идентификатор безопасности пользователя, создавшего пакет, применяются к роли модуля чтения пакета, а разрешение роли **db_ssisadmin** и уникальный идентификатор безопасности пользователя, создавшего пакет, применяются к роли модуля записи пакета. Пользователь должен быть членом роли **db_ssisadmin**, **db_ssisltduser** или **db_ssisoperator**, чтобы получить доступ на чтение пакета. Пользователь должен быть членом роли **db_ssisadmin**, чтобы получить доступ для записи.  
  
### Доступ к пакетам  
 Фиксированные роли уровня базы данных работают в сочетании с пользовательскими ролями. Пользовательские роли — это роли, которые создаются в среде [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] и после используются для назначения разрешений пакетам. Чтобы получить доступ к пакету, пользователь должен быть членом пользовательской роли и соответствующей предопределенной роли служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] уровня базы данных. Например, если пользователи являются членами определяемой пользователем роли **AuditUsers**, которая назначена пакету, они также должны быть членами роли **db_ssisadmin**, **db_ssisltduser** или **db_ssisoperator**, чтобы иметь доступ для чтения пакета.  
  
 Если пакетам не назначить пользовательских ролей, то доступом к пакетам будут управлять только предопределенные роли базы данных.  
  
 Если используются пользовательские роли, то перед тем как назначать их пакетам, нужно добавить их в базу данных **msdb**. Новую роль базы данных можно создать в среде [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 Роли уровня базы данных служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] предоставляют право доступа к системным таблицам служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] базы данных msdb.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (служба MSSQLSERVER) должна быть запущена перед тем, как подключиться к ядру СУБД и базе данных **msdb**.  
  
 Чтобы назначить роли пакетов, необходимо выполнить следующие задачи.  
  
-   **Откройте обозреватель объектов и подключитесь к службам Integration Services**  
  
     Перед тем как с помощью среды [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] назначить роли для пакетов, необходимо открыть обозреватель объектов в среде [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] и подключиться к службам [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
     Служба [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] должна быть запущена перед подключением к [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
-   **Назначение пакетам ролей модулей чтения и записи**  
  
     Можно назначить роль чтения и модуля записи для каждого пакета.  
  
## Связанные задачи  
  
-   [Назначение пакетам роли чтения и модуля записи](../../integration-services/service/assign-a-reader-and-writer-role-to-a-package.md)  
  
-   [Создание пользовательской роли](../../integration-services/service/create-a-user-defined-role.md)  
  
-   [Подключение к службам Integration Services](../../integration-services/service/connect-to-integration-services.md)  
  
  