---
title: "Удаление следящего сервера из сеанса зеркального отображения базы данных (SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "следящий сервер [SQL Server], отключение"
  - "следящий сервер [SQL Server], удаление"
  - "зеркальное отображение базы данных [SQL Server], следящий сервер"
ms.assetid: f3ce7afc-8936-4d35-80ce-d0f8fbc318d3
caps.latest.revision: 39
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 39
---
# Удаление следящего сервера из сеанса зеркального отображения базы данных (SQL Server)
  В этом разделе описано, как удалить следящий сервер из сеанса зеркального отображения базы данных [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] с помощью среды [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] или [!INCLUDE[tsql](../../includes/tsql-md.md)]. Во время сеанса зеркального отображения владелец базы данных в любой момент может отключить следящий сервер для сеанса зеркального отображения базы данных.  
  
 **В этом разделе**  
  
-   **Перед началом работы выполните следующие действия.**  
  
     [Безопасность](#Security)  
  
-   **Удаление следящего сервера с помощью:**  
  
     [Среда SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Дальнейшие действия**. [После удаления следящего сервера](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Перед началом  
  
###  <a name="Security"></a> Безопасность  
  
####  <a name="Permissions"></a> Разрешения  
 Необходимо разрешение ALTER на базу данных.  
  
##  <a name="SSMSProcedure"></a> Использование среды SQL Server Management Studio  
  
#### Удаление следящего сервера  
  
1.  Установите соединение с экземпляром основного сервера и на панели **Обозреватель объектов** щелкните имя сервера, чтобы развернуть этот узел.  
  
2.  Раскройте **Базы данных**и выберите базу данных, для которой нужно удалить следящий сервер.  
  
3.  Щелкните базу данных правой кнопкой мыши, выберите пункт **Задачи**, а затем пункт **Зеркальное отображение**. Откроется страница **Зеркальное отображение** диалогового окна **Свойства базы данных** .  
  
4.  Чтобы удалить следящий сервер, удалите его сетевой адрес из поля **Следящий** .  
  
    > [!NOTE]  
    >  При переключении из режима высокого уровня безопасности с автоматической отработкой отказа в высокопроизводительный режим поле **Следящий** автоматически очищается.  
  
##  <a name="TsqlProcedure"></a> Использование Transact-SQL  
  
#### Удаление следящего сервера  
  
1.  Установите соединение с компонентом [!INCLUDE[ssDE](../../includes/ssde-md.md)] на экземпляре любого из серверов-участников.  
  
2.  На панели «Стандартная» нажмите **Создать запрос**.  
  
3.  Выполните следующую инструкцию:  
  
     [ALTER DATABASE](../Topic/ALTER%20DATABASE%20Database%20Mirroring%20\(Transact-SQL\).md) *имя_базы_данных* SET WITNESS OFF  
  
     где *имя_базы_данных* — имя зеркально отображаемой базы данных.  
  
     В следующем примере показано удаление следящего сервера для базы данных [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
    ```  
    ALTER DATABASE AdventureWorks2012 SET WITNESS OFF ;  
    ```  
  
##  <a name="FollowUp"></a> Дальнейшие действия. После удаления следящего сервера  
 При отключении следящего сервера [режим работы](../../database-engine/database-mirroring/database-mirroring-operating-modes.md) изменяется в соответствии с параметром безопасности транзакций.  
  
-   Если уровень безопасности транзакций установлен в FULL (значение по умолчанию), то сеанс использует синхронный режим с высоким уровнем защиты без автоматической отработки отказа.  
  
-   Когда безопасность транзакций отключена, сеанс работает асинхронно (в режиме высокой производительности), не требуя кворума. При отключенной безопасности транзакций настоятельно рекомендуется также отключить следящий сервер.  
  
> [!TIP]  
>  Параметры безопасности транзакций для каждого участника в экземпляре сервера доступны через представление каталога [sys.database_mirroring](../../relational-databases/system-catalog-views/sys-database-mirroring-transact-sql.md) в столбцах **mirroring_safety_level** и **mirroring_safety_level_desc**.  
  
##  <a name="RelatedTasks"></a> Связанные задачи  
  
-   [Добавление следящего сервера для зеркального отображения базы данных с использованием проверки подлинности Windows (Transact-SQL)](../../database-engine/database-mirroring/add-a-database-mirroring-witness-using-windows-authentication-transact-sql.md)  
  
-   [Добавление или замена следящего сервера зеркального отображения базы данных (среда SQL Server Management Studio)](../../database-engine/database-mirroring/add-or-replace-a-database-mirroring-witness-sql-server-management-studio.md)  
  
## См. также:  
 [Зеркальное отображение базы данных ALTER DATABASE (Transact-SQL)](../Topic/ALTER%20DATABASE%20Database%20Mirroring%20\(Transact-SQL\).md)   
 [Изменение безопасности транзакций в сеансах зеркального отображения базы данных (Transact-SQL)](../../database-engine/database-mirroring/change-transaction-safety-in-a-database-mirroring-session-transact-sql.md)   
 [Добавление следящего сервера для зеркального отображения базы данных с использованием проверки подлинности Windows (Transact-SQL)](../../database-engine/database-mirroring/add-a-database-mirroring-witness-using-windows-authentication-transact-sql.md)   
 [Следящий сервер зеркального отображения базы данных](../../database-engine/database-mirroring/database-mirroring-witness.md)  
  
  