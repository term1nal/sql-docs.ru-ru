---
title: "Параметр конфигурации сервера &#171;проверка подлинности автономной базы данных&#187; | Microsoft Docs"
ms.custom: ""
ms.date: "03/02/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "автономная база данных, включение"
  - "проверка подлинности автономной базы данных"
ms.assetid: b80768d2-ac20-4035-a335-d9adb74b3f6e
caps.latest.revision: 11
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 10
---
# Параметр конфигурации сервера &#171;проверка подлинности автономной базы данных&#187;
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Параметр **проверка подлинности автономной базы данных** позволяет включить автономные базы данных на экземпляре [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
 Данный параметр сервера позволяет управлять **проверкой подлинности автономной базы данных**.  
  
-   Если **проверка подлинности автономной базы данных** в экземпляре выключена (0), автономные базы нельзя создавать или присоединять к экземпляру компонента [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
-   Если **проверка подлинности автономной базы данных** в экземпляре включена (1), автономные базы можно создавать или присоединять к экземпляру компонента [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
 Автономная база данных содержит все параметры базы данных и метаданные, необходимые для определения базы данных, и не зависит от экземпляра компонента [!INCLUDE[ssDE](../../includes/ssde-md.md)], где установлена базы данных. Пользователи могут соединяться с базой данных без проверки подлинности имени входа на уровне компонента [!INCLUDE[ssDE](../../includes/ssde-md.md)] . Если изолировать базу данных от компонента Database Engine, будет легко переместить эту базу данных на другой экземпляр [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Помещение всех параметров базы данных внутрь базы данных позволяет ее владельцу управлять всеми параметрами для этой базы данных. Дополнительные сведения об автономных базах данных см. в разделе [Contained Databases](../../relational-databases/databases/contained-databases.md).  

> [!NOTE] Автономные базы данных всегда включены для [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] и [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)] и не могут быть отключены.
  
 Если экземпляр [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] содержит автономные базы данных, можно установить параметр **contained database authentication** в значение 0 с помощью инструкции **RECONFIGURE WITH OVERRIDE** . Значение параметра **contained database authentication** , равное 0, отключает проверку подлинности автономной базы данных для автономных баз данных.  
  
> [!IMPORTANT]  
>  При включении автономных баз данных базы данных пользователи с разрешением ALTER ANY USER, такие как члены роли базы данных db_owner или db_accessadmin, могут предоставлять доступ к базам данных и таким образом предоставлять доступ к экземпляру [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Это означает, что управление доступом к серверу больше не принадлежит только членам предопределенной роли сервера sysadmin и securityadmin и входам с разрешениями CONTROL SERVER и ALTER ANY LOGIN на уровне сервера. С использованием автономных баз данных связаны определенные риски. Дополнительные сведения см. в статье [Security Best Practices with Contained Databases](../../relational-databases/databases/security-best-practices-with-contained-databases.md).  
  
## Примеры  
 В следующем примере в экземпляре компонента [!INCLUDE[ssDE](../../includes/ssde-md.md)] создаются автономные базы данных.  
  
```tsql  
sp_configure 'contained database authentication', 1;  
GO  
RECONFIGURE;  
GO  
```  
  
## См. также:  
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [RECONFIGURE (Transact-SQL)](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Параметры конфигурации сервера (SQL Server)](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
  