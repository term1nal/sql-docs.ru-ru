---
title: "восстановить базу данных master (Transact-SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-backup-restore"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "база данных master [SQL Server], восстановление"
ms.assetid: c83d802c-e84e-4458-b3ca-173d9ba32f73
caps.latest.revision: 42
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 42
---
# восстановить базу данных master (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Этот раздел посвящен восстановлению базы данных **master** из полной резервной копии.  
  
### Восстановление базы данных master  
  
1.  Запустите экземпляр сервера в однопользовательском режиме.  
  
     Дополнительные сведения об указании параметра запуска в однопользовательском режиме (**-m**) см. в разделе [Настройка параметров запуска сервера (диспетчер конфигурации SQL Server)](../../database-engine/configure-windows/configure-server-startup-options-sql-server-configuration-manager.md).  
  
2.  Чтобы восстановить полную резервную копию базы данных **master**, используйте следующую инструкцию [RESTORE DATABASE](../Topic/RESTORE%20\(Transact-SQL\).md)[!INCLUDE[tsql](../../includes/tsql-md.md)] :  
  
     `RESTORE DATABASE master FROM`  *\<устройство_резервного_копирования>*  `WITH REPLACE`  
  
     Если задан параметр REPLACE, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] восстанавливает указанную базу данных, даже если база данных с таким же именем уже существует. Существующая база данных в таком случае будет удалена. В однопользовательском режиме рекомендуется вводить инструкцию RESTORE DATABASE в [программе sqlcmd](../../tools/sqlcmd-utility.md). Дополнительные сведения см. в статье [Программа sqlcmd](../../relational-databases/scripting/use-the-sqlcmd-utility.md).  
  
    > [!IMPORTANT]  
    >  После восстановления базы данных **master** экземпляр [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] завершает работу и останавливает процесс **sqlcmd** . Перед перезапуском экземпляра сервера удалите параметр запуска однопользовательского режима. Дополнительные сведения см. в разделе [Настройка параметров запуска сервера (диспетчер конфигурации SQL Server)](../../database-engine/configure-windows/configure-server-startup-options-sql-server-configuration-manager.md).  
  
3.  Перезапустите экземпляр сервера и выполните остальные шаги восстановления из копии, такие как восстановление других баз данных, присоединение баз данных и исправление несовпадающих данных пользователей.  
  
## Пример  
 Следующий пример восстанавливает базу данных `master` в определенном по умолчанию экземпляре сервера. В этом примере предполагается, что экземпляр сервера уже работает в однопользовательском режиме. В примере запускается `sqlcmd` и выполняется инструкция `RESTORE DATABASE` , которая восстанавливает полную резервную копию базы данных `master` с дискового устройства: `Z:\SQLServerBackups\master.bak`.  
  
> [!NOTE]  
>  Для именованного экземпляра команда **sqlcmd** должна задавать параметр **-S***\<имя_компьютера>*\\*\<имя_экземпляра>*.  
  
```  
  
      C:\> sqlcmd  
1> RESTORE DATABASE master FROM DISK = 'Z:\SQLServerBackups\master.bak' WITH REPLACE;  
2> GO  
```  
  
## См. также:  
 [Выполнение полного восстановления базы данных (простая модель восстановления)](../../relational-databases/backup-restore/complete-database-restores-simple-recovery-model.md)   
 [Выполнение полного восстановления базы данных (модель полного восстановления)](../../relational-databases/backup-restore/complete-database-restores-full-recovery-model.md)   
 [Диагностика пользователей, утративших связь с учетной записью (SQL Server)](../../sql-server/failover-clusters/troubleshoot-orphaned-users-sql-server.md)   
 [Присоединение и отсоединение базы данных (SQL Server)](../../relational-databases/databases/database-detach-and-attach-sql-server.md)   
 [Перестроение системных баз данных](../../relational-databases/databases/rebuild-system-databases.md)   
 [Параметры запуска службы Database Engine](../../database-engine/configure-windows/database-engine-service-startup-options.md)   
 [Диспетчер конфигурации SQL Server](../../relational-databases/sql-server-configuration-manager.md)   
 [Резервное копирование и восстановление системных баз данных (SQL Server)](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md)   
 [RESTORE (Transact-SQL)](../Topic/RESTORE%20\(Transact-SQL\).md)   
 [Запуск SQL Server в однопользовательском режиме](../../database-engine/configure-windows/start-sql-server-in-single-user-mode.md)  
  
  