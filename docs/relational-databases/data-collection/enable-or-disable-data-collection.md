---
title: "Включение или отключение сбор данных | Microsoft Docs"
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
  - "сборщик данных [SQL Server], отключение"
  - "сборщик данных [SQL Server], включение"
ms.assetid: 0137971b-fb48-4a3e-822a-3df2b9bb09d7
caps.latest.revision: 18
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 18
---
# Включение или отключение сбор данных
  В этом разделе описывается включение и отключение сбора данных в [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] с помощью среды [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] или [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **В этом разделе**  
  
-   **Перед началом работы выполните следующие действия.**  
  
     [Безопасность](#Security)  
  
-   **Включение или отключение сбора данных с помощью следующих средств**  
  
     [Среда SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Перед началом  
  
###  <a name="Security"></a> Безопасность  
  
####  <a name="Permissions"></a> Разрешения  
 Для выполнения этой процедуры требуется членство в предопределенной роли базы данных **dc_admin** или **dc_operator** (с разрешением EXECUTE).  
  
##  <a name="SSMSProcedure"></a> Использование среды SQL Server Management Studio  
  
#### Включение сборщика данных  
  
1.  В обозревателе объектов раскройте узел **Управление** .  
  
2.  Щелкните правой кнопкой мыши **Сбор данных**, затем выберите **Включить сбор данных**.  
  
#### Отключение сборщика данных  
  
1.  В обозревателе объектов раскройте узел **Управление** .  
  
2.  Щелкните правой кнопкой мыши пункт **Сбор данных** и выберите команду **Отключить сбор данных**.  
  
##  <a name="TsqlProcedure"></a> Использование Transact-SQL  
  
#### Включение сборщика данных  
  
1.  Установите соединение с компонентом [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  На панели «Стандартная» нажмите **Создать запрос**.  
  
3.  Скопируйте следующий пример в окно запроса и нажмите кнопку **Выполнить**. В этом примере используется хранимая процедура [sp_syscollector_enable_collector](../../relational-databases/system-stored-procedures/sp-syscollector-enable-collector-transact-sql.md) для включения сборщика данных.  
  
```tsql  
USE msdb;  
GO  
EXEC dbo.sp_syscollector_enable_collector ;  
```  
  
#### Отключение сборщика данных  
  
1.  Установите соединение с компонентом [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  На панели «Стандартная» нажмите **Создать запрос**.  
  
3.  Скопируйте следующий пример в окно запроса и нажмите кнопку **Выполнить**. В этом примере используется хранимая процедура [sp_syscollector_disable_collector](../../relational-databases/system-stored-procedures/sp-syscollector-disable-collector-transact-sql.md) для отключения сборщика данных.  
  
```tsql  
USE msdb;  
GO  
EXEC dbo.sp_syscollector_disable_collector;  
```  
  
## См. также:  
 [Сбор данных](../../relational-databases/data-collection/data-collection.md)   
 [Системные хранимые процедуры (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  