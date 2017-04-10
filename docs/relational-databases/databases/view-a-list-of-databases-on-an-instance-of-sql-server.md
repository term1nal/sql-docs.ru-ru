---
title: "Просмотр списка баз данных в экземпляре SQL Server | Microsoft Docs"
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
  - "текущие базы данных"
  - "базы данных, находящиеся в настоящее время на сервере [SQL Server]"
  - "список баз данных [SQL Server]"
  - "просмотр списка баз данных"
  - "отображение списка баз данных"
  - "базы данных [SQL Server], просмотр"
  - "серверы [SQL Server], перечисленные базы данных"
  - "перечисление баз данных"
ms.assetid: 7ee7a789-db36-4be9-8a0e-0362a1e152dd
caps.latest.revision: 31
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 31
---
# Просмотр списка баз данных в экземпляре SQL Server
  В этой теме описывается, как просмотреть список баз данных в экземпляре [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] с помощью среды [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] или [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **В этом разделе**  
  
-   **Перед началом работы выполните следующие действия.**  
  
     [Безопасность](#Security)  
  
-   **Просмотр списка баз данных в экземпляре SQL Server выполняется при помощи следующих средств.**  
  
     [Среда SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Перед началом  
  
###  <a name="Security"></a> Безопасность  
  
####  <a name="Permissions"></a> Разрешения  
 Если участник, вызывающий представление каталога **sys.databases**, не является владельцем базы данных, а база данных не является базой данных **master** или **tempdb**, минимально необходимыми разрешениями для просмотра соответствующей строки являются разрешения уровня сервера ALTER ANY DATABASE или VIEW ANY DATABASE, или разрешение CREATE DATABASE в базе данных **master**. Узнать базу данных, к которой подключен участник, можно в представлении каталога **sys.databases**.  
  
##  <a name="SSMSProcedure"></a> Использование среды SQL Server Management Studio  
  
#### Просмотр списка баз данных в экземпляре SQL Server  
  
1.  В **обозревателе объектов**подключитесь к экземпляру компонента [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]и разверните его.  
  
2.  Для просмотра списка всех баз данных в экземпляре разверните список **Базы данных**.  
  
##  <a name="TsqlProcedure"></a> Использование Transact-SQL  
  
#### Просмотр списка баз данных в экземпляре SQL Server  
  
1.  Установите соединение с компонентом [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  На панели «Стандартная» нажмите **Создать запрос**.  
  
3.  Скопируйте следующий пример в окно запроса и нажмите кнопку **Выполнить**. Этот пример возвращает список баз данных, размещенных в экземпляре [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Список содержит имена баз данных, их идентификаторы и даты создания.  
  
```tsql  
USE AdventureWorks2012;  
GO  
SELECT name, database_id, create_date  
FROM sys.databases ;  
GO  
  
```  
  
## См. также:  
 [Представления каталогов баз данных и файлов (Transact-SQL)](../../relational-databases/system-catalog-views/databases-and-files-catalog-views-transact-sql.md)   
 [sys.databases (Transact-SQL)](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)  
  
  