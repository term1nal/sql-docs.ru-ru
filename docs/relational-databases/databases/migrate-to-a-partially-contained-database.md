---
title: "Миграция на частично автономную базу данных | Microsoft Docs"
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
  - "автономная база данных, миграция на"
ms.assetid: 90faac38-f79e-496d-b589-e8b2fe01c562
caps.latest.revision: 17
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 17
---
# Миграция на частично автономную базу данных
  В этом разделе описано, как подготовить к переходу на частично автономную модель базы данных, и приведены шаги по миграции.  
  
 **В этом разделе:**  
  
-   [Подготовка к миграции базы данных](#prepare)  
  
-   [Включение автономных баз данных](#enable)  
  
-   [Преобразование базы данных в частично автономную](#convert)  
  
-   [Миграция пользователей в пользователей автономной базы данных](#users)  
  
##  <a name="prepare"></a> Подготовка к миграции базы данных  
 Перед началом перевода базы данных в частичную автономную модель просмотрите следующие указания.  
  
-   Для этого потребуется понимание модели частично автономной базы данных. Дополнительные сведения см. в разделе [Contained Databases](../../relational-databases/databases/contained-databases.md).  
  
-   Необходимо понимать риски, связанные с частично автономными базами данных. Дополнительные сведения см. в статье [Security Best Practices with Contained Databases](../../relational-databases/databases/security-best-practices-with-contained-databases.md).  
  
-   Автономные базы данных не поддерживают репликацию, отслеживание измененных данных или отслеживание изменений. Убедитесь, что в базе данных не используются эти функции.  
  
-   Просмотрите список функций базы данных, которые изменились для частично автономных баз данных. Дополнительные сведения см. в разделе [Измененные функции (автономная база данных)](../../relational-databases/databases/modified-features-contained-database.md).  
  
-   Выполнив запрос к представлению [sys.dm_db_uncontained_entities (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-uncontained-entities-transact-sql.md), найдите в базе данных неавтономные объекты или функции. Дополнительные сведения см. в разделе  
  
-   Мониторьте XEvent **database_uncontained_usage**, чтобы определить, когда используются неавтономные функции.  
  
##  <a name="enable"></a> Включение автономных баз данных  
 Перед созданием автономных баз данных поддержка автономных баз данных должна быть включена на экземпляре [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
### Включение автономных баз данных с помощью Transact-SQL  
 В следующем примере в экземпляре компонента [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] создаются автономные базы данных.  
  
```tsql  
sp_configure 'contained database authentication', 1;  
GO  
RECONFIGURE ;  
GO  
```  
  
#### Включение автономных баз данных с помощью среды Management Studio  
 В следующем примере в экземпляре компонента [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] создаются автономные базы данных.  
  
1.  В обозревателе объектов щелкните правой кнопкой мыши имя сервера и выберите пункт **Свойства**.  
  
2.  На странице **Расширенные** в разделе **Включение** установите параметр **Включить автономные базы данных** в значение **True**.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="convert"></a> Преобразование базы данных в частично автономную  
 База данных преобразуется в автономную путем изменения ее параметра **CONTAINMENT** .  
  
### Преобразование базы данных в частично автономную с помощью Transact-SQL  
 В следующем примере база данных показано преобразование `Accounting` в частично автономную базу данных.  
  
```tsql  
USE [master]  
GO  
ALTER DATABASE [Accounting] SET CONTAINMENT = PARTIAL  
GO  
```  
  
### Преобразование базы данных в частично автономную с помощью среды Management Studio  
 В следующем примере база данных преобразуется в частично автономную базу данных.  
  
1.  В обозревателе объектов разверните узел **Базы данных**, щелкните правой кнопкой мыши базу данных, которую нужно преобразовать, а затем выберите пункт **Свойства**.  
  
2.  На странице **Параметры** измените параметр **Тип вложения** на **Частичный**.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="users"></a> Миграция пользователей в пользователей автономной базы данных  
 В следующем примере выполняется миграция всех пользователей, основанных на имени входа [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , в пользователей автономной базы данных с паролями. Этот пример исключает имена входа, которые не были включены. Этот пример должен выполняться в автономной базе данных.  
  
```tsql  
DECLARE @username sysname ;  
DECLARE user_cursor CURSOR  
    FOR   
        SELECT dp.name   
        FROM sys.database_principals AS dp  
        JOIN sys.server_principals AS sp   
        ON dp.sid = sp.sid  
        WHERE dp.authentication_type = 1 AND sp.is_disabled = 0;  
OPEN user_cursor  
FETCH NEXT FROM user_cursor INTO @username  
    WHILE @@FETCH_STATUS = 0  
    BEGIN  
        EXECUTE sp_migrate_user_to_contained   
        @username = @username,  
        @rename = N'keep_name',  
        @disablelogin = N'disable_login';  
    FETCH NEXT FROM user_cursor INTO @username  
    END  
CLOSE user_cursor ;  
DEALLOCATE user_cursor ;  
```  
  
## См. также:  
 [Автономные базы данных](../../relational-databases/databases/contained-databases.md)   
 [sp_migrate_user_to_contained (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-migrate-user-to-contained-transact-sql.md)   
 [sys.dm_db_uncontained_entities (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-uncontained-entities-transact-sql.md)  
  
  