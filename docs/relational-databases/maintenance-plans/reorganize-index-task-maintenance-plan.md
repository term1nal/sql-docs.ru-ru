---
title: "Задача &#171;Реорганизация индекса&#187; (план обслуживания) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.swb.maint.defrag.f1"
helpviewer_keywords: 
  - "диалоговое окно «Задача реорганизации индекса»"
ms.assetid: e9cbebbd-f36f-4176-9832-382a46ac946c
caps.latest.revision: 33
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 33
---
# Задача &#171;Реорганизация индекса&#187; (план обслуживания)
  Используйте диалоговое окно **Задача ReorganizeIndex** для изменения порядка страниц индекса в целях повышения эффективности поиска. Эта задача использует инструкцию `ALTER INDEX REORGANIZE` с базами данных [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
## Параметры  
 **Соединение**  
 Выберите соединение с сервером, которое будет использоваться для выполнения этой задачи.  
  
 **Создать**  
 Создать новое соединение с сервером для его использования при выполнении этой задачи. Диалоговое окно **Создание соединения** описано ниже.  
  
 **Базы данных**  
 Укажите базы данных, для которых должна выполняться эта задача.  
  
-   **Все базы данных**  
  
     Создается план обслуживания, по которому задачи обслуживания должны выполняться для всех баз данных [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , кроме базы данных tempdb.  
  
-   **Все системные базы данных**  
  
     Будет сформирован план обслуживания, запускающий задачи обслуживания для каждой системной базы данных [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , за исключением базы данных **tempdb**. Для баз данных, созданных пользователями, задачи обслуживания выполняться не будут.  
  
-   **Все пользовательские базы данных**  
  
     Создается план обслуживания, по которому задачи обслуживания выполняются для всех баз данных, созданных пользователем. Для системных баз данных [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] задачи обслуживания выполняться не будут.  
  
-   **Определенные базы данных**  
  
     Создается план обслуживания, по которому задачи обслуживания должны выполняться только для указанных баз данных. Если выбран этот параметр, необходимо выбрать в списке хотя бы одну базу данных.  
  
 **Объект**  
 Ограничьте сетку **Выбор** для отображения таблиц, представлений или обоих элементов.  
  
 **Выбор**  
 Укажите таблицы или индексы, которые должны обрабатываться этой задачей. Этот параметр недоступен, если в окне **Объекты** выбран пункт **Таблицы и представления** .  
  
 **Сжатие больших объектов**  
 По возможности освобождается пространство для таблиц и представлений. Этот параметр использует инструкцию `ALTER INDEX LOB_COMPACTION = ON`.  
  
 **Просмотр T-SQL**  
 Просмотрите инструкции [!INCLUDE[tsql](../../includes/tsql-md.md)], выполняемые для данной задачи по отношению к серверу, на основе выбранных параметров.  
  
> [!NOTE]  
>  Если количество затронутых объектов велико, построение этого отображения может занять значительное время.  
  
## Диалоговое окно «Создание соединения»  
 **Имя соединения**  
 Введите имя нового соединения.  
  
 **Выберите или введите имя сервера**  
 Выберите сервер для подключения при выполнении этой задачи.  
  
 **Обновить**  
 Обновите список доступных серверов.  
  
 **Введите данные для входа на сервер**  
 Укажите способ проверки подлинности на сервере.  
  
 **Использовать встроенную безопасность Windows**  
 Подключиться к экземпляру компонента [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] c проверкой подлинности Windows [!INCLUDE[msCoName](../../includes/msconame-md.md)].  
  
 **Использовать указанные имя пользователя и пароль**  
 Подключиться к экземпляру компонента [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] с использованием проверки подлинности [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Этот параметр недоступен.  
  
 **Имя пользователя**  
 Укажите имя входа, используемое при проверке подлинности [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Этот параметр недоступен.  
  
 **Пароль**  
 Укажите используемый при проверке подлинности пароль. Этот параметр недоступен.  
  
## См. также:  
 [ALTER INDEX (Transact-SQL)](../../t-sql/statements/alter-index-transact-sql.md)   
 [DBCC INDEXDEFRAG (Transact-SQL)](../../t-sql/database-console-commands/dbcc-indexdefrag-transact-sql.md)  
  
  