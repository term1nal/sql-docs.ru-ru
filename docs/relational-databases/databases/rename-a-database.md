---
title: "Переименование базы данных | Microsoft Docs"
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
  - "базы данных [SQL Server], переименование"
  - "переименование баз данных"
ms.assetid: 44c69d35-abcb-4da3-9370-5e0bc9a28496
caps.latest.revision: 19
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 19
---
# Переименование базы данных
  В этом подразделе описывается, как переименовать пользовательскую базу данных в [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] с помощью [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] или [!INCLUDE[tsql](../../includes/tsql-md.md)]. Имя базы данных может содержать все символы, соответствующие правилам для идентификаторов.  
  
 **В этом разделе**  
  
-   **Перед началом работы выполните следующие действия.**  
  
     [Ограничения](#Restrictions)  
  
     [Безопасность](#Security)  
  
-   **Переименование базы данных с использованием следующих средств:**  
  
     [Среда SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Дальнейшие действия**. [После переименования базы данных](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Перед началом  
  
###  <a name="Restrictions"></a> Ограничения  
  
-   Системные базы данных не могут быть переименованы.  
  
###  <a name="Security"></a> Безопасность  
  
####  <a name="Permissions"></a> Разрешения  
 Необходимо разрешение ALTER на базу данных.  
  
##  <a name="SSMSProcedure"></a> Использование среды SQL Server Management Studio  
  
#### Переименование базы данных  
  
1.  В **обозревателе объектов**подключитесь к экземпляру компонента [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]и разверните его.  
  
2.  Убедитесь в том, что никто не использует эту базу данных, а затем [переведите ее в однопользовательский режим работы](../../relational-databases/databases/set-a-database-to-single-user-mode.md).  
  
3.  Раскройте узел **Базы данных**, щелкните правой кнопкой мыши базу данных, которую необходимо переименовать, а затем выберите пункт **Переименовать**.  
  
4.  Введите новое имя базы данных и нажмите кнопку **ОК**.  
  
##  <a name="TsqlProcedure"></a> Использование Transact-SQL  
  
#### Переименование базы данных  
  
1.  Установите соединение с компонентом [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  На панели «Стандартная» нажмите **Создать запрос**.  
  
3.  Скопируйте следующий пример в окно запроса и нажмите кнопку **Выполнить**. В этом примере имя базы данных `AdventureWorks2012` изменяется на `Northwind`.  
  
```tsql  
USE master;  
GO  
ALTER DATABASE AdventureWorks2012  
Modify Name = Northwind ;  
GO  
```  
  
###  <a name="TsqlExample"></a>   
##  <a name="FollowUp"></a> Дальнейшие действия. После переименования базы данных  
 Создавайте резервную копию базы данных **master** после переименования любой базы данных.  
  
## См. также:  
 [ALTER DATABASE (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql.md)   
 [Идентификаторы баз данных](../../relational-databases/databases/database-identifiers.md)  
  
  