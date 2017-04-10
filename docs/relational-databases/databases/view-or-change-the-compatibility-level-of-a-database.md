---
title: "Просмотр или изменение уровня совместимости базы данных | Microsoft Docs"
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
  - "уровни совместимости [SQL Server], просмотр"
  - "совместимость [SQL Server], базы данных"
  - "уровни совместимости [SQL Server], изменение"
ms.assetid: 579867ec-57cb-4cb8-af35-9688c1e9e15d
caps.latest.revision: 20
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 20
---
# Просмотр или изменение уровня совместимости базы данных
  В этом разделе описывается просмотр и изменение уровня совместимости базы данных в [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] с помощью [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] или [!INCLUDE[tsql](../../includes/tsql-md.md)]. Перед изменением уровня совместимости базы данных проанализируйте, как это повлияет на имеющиеся приложения. Дополнительные сведения см. в разделе [Уровень совместимости инструкции ALTER DATABASE (Transact-SQL)](../Topic/ALTER%20DATABASE%20Compatibility%20Level%20\(Transact-SQL\).md).  
  
 **В этом разделе**  
  
-   **Перед началом работы выполните следующие действия.**  
  
     [Безопасность](#Security)  
  
-   **Просмотр или изменение уровня совместимости базы данных с использованием следующих средств:**  
  
     [Среда SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Перед началом  
  
###  <a name="Security"></a> Безопасность  
  
####  <a name="Permissions"></a> Разрешения  
 Необходимо разрешение ALTER на базу данных.  
  
##  <a name="SSMSProcedure"></a> Использование среды SQL Server Management Studio  
  
#### Просмотр или изменение уровня совместимости базы данных  
  
1.  После соединения с соответствующим экземпляром [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]в обозревателе объектов нажмите имя сервера.  
  
2.  Раскройте узел **Базы данных**и в зависимости от типа восстанавливаемой базы данных выберите пользовательскую базу данных или раскройте узел **Системные базы данных** и выберите системную базу данных.  
  
3.  Щелкните правой кнопкой мыши базу данных, а затем выберите пункт **Свойства**.  
  
     Откроется диалоговое окно **Свойства базы данных** .  
  
4.  На панели **Выбор страницы** щелкните **Параметры**.  
  
     Текущий уровень совместимости будет указан в списке **Уровень совместимости** .  
  
5.  Чтобы изменить уровень совместимости, выберите в списке другой параметр. Доступны следующие значения: **SQL Server 2008 (100)**, **SQL Server 2012 (110)** и **SQL Server 2014 (120)**.  
  
##  <a name="TsqlProcedure"></a> Использование Transact-SQL  
  
#### Просмотр уровня совместимости базы данных  
  
1.  Установите соединение с компонентом [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  На панели «Стандартная» нажмите **Создать запрос**.  
  
3.  Скопируйте следующий пример в окно запроса и нажмите кнопку **Выполнить**. В этом примере возвращается уровень совместимости базы данных [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
```tsql  
USE AdventureWorks2012;  
GO  
SELECT compatibility_level  
FROM sys.databases WHERE name = 'AdventureWorks2012';  
GO  
  
```  
  
#### Изменение уровня совместимости базы данных  
  
1.  Установите соединение с компонентом [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  На панели «Стандартная» нажмите **Создать запрос**.  
  
3.  Скопируйте следующий пример в окно запроса и нажмите кнопку **Выполнить**. В этом примере изменяется уровень совместимости базы данных [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] на `120,` т. е. на значение уровня совместимости для [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)].  
  
```tsql  
ALTER DATABASE AdventureWorks2012  
SET COMPATIBILITY_LEVEL = 120;  
GO  
```  
  
  