---
title: "выполнять скрипты во время синхронизации (программирование репликации на языке Transact-SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "TSQL"
helpviewer_keywords: 
  - "синхронизация [репликация SQL Server], скрипты"
  - "скрипты [репликация SQL Server], синхронизация и"
  - "sp_addscriptexec, хранимая процедура"
ms.assetid: b58a0877-4e43-4fab-a281-24e6022d3fb1
caps.latest.revision: 34
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 34
---
# выполнять скрипты во время синхронизации (программирование репликации на языке Transact-SQL)
  Выполнение скрипта по требованию на подписчике поддерживается для репликации транзакций и публикации слиянием. Эта функция осуществляет копирование скрипта в рабочий каталог репликации, а затем командой **sqlcmd** применяет скрипт на подписчике. По умолчанию при возникновении ошибки применения скрипта к подписке на публикацию транзакций работа агента распространителя будет остановлена. Программным путем можно задать скрипт [!INCLUDE[tsql](../../includes/tsql-md.md)] , который будет выполняться с помощью хранимых процедур репликации.  
  
### Настройка скрипта для выполнения всеми подписчиками на публикацию моментальных снимков, транзакций или слиянием  
  
1.  Создайте и протестируйте скрипт на языке [!INCLUDE[tsql](../../includes/tsql-md.md)] , который будет выполняться по запросу.  
  
2.  Сохраните файл скрипта в папке, доступной для агента моментальных снимков публикации.  
  
3.  На издателе в базе данных публикации выполните хранимую процедуру [sp_addscriptexec & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addscriptexec-transact-sql.md). Задайте параметр **@publication**и имя созданного на шаге 2 файла скрипта в полном UNC-формате в параметре **@scriptfile**, а в параметре **@skiperror**укажите одно из следующих значений.  
  
    -   **0** -агент остановится при выполнении сценария, если возникает ошибка.  
  
    -   **1** -агент будет ведения журнала ошибок и продолжить выполнение сценария при возникновении ошибок.  
  
4.  Указанный скрипт будет выполнен на всех подписчиках при следующем сеансе синхронизации подписки.  
  
## См. также:  
 [Синхронизация данных](../../relational-databases/replication/synchronize-data.md)  
  
  