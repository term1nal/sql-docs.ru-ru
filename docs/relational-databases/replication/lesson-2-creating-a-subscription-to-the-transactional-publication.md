---
title: "Занятие 2. Создание подписки на публикацию транзакций | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
helpviewer_keywords: 
  - "репликация [SQL Server], учебники"
ms.assetid: 5995b7d2-7c06-46f5-b96c-2bee879bcda2
caps.latest.revision: 13
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 13
---
# Занятие 2. Создание подписки на публикацию транзакций
На этом занятии с помощью среды [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]будет создана подписка. Приступать к этому занятию нужно только по завершении предыдущего: [Занятие 1. Публикация данных с помощью репликации транзакций](../../relational-databases/replication/lesson-1-publishing-data-using-transactional-replication.md).  
  
### Создание подписки  
  
1.  Подключитесь к издателю в среде [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], а затем раскройте узел сервера и папку **Репликация** .  
  
2.  В папке **Локальные публикации** щелкните правой кнопкой мыши публикацию **AdvWorksProductTrans** и выберите команду **Создать подписку**.  
  
    Откроется мастер создания подписки.  
  
3.  На странице «Публикация» выберите публикацию **AdvWorksProductTrans**и нажмите кнопку **Далее**.  
  
4.  На странице «Расположение агента распространителя» установите флажок **Выполнять все агенты на распространителе**и нажмите кнопку **Далее**.  
  
5.  Если имя экземпляра подписчика не отображается, на странице «Подписчики» нажмите кнопку **Добавить подписчик**, выберите **Добавить подписчик SQL Server**, в диалоговом окне **Соединение с сервером** введите имя экземпляра подписчика, затем нажмите кнопку **Соединить**.  
  
6.  На странице "Подписчики" выберите имя экземпляра сервера подписчика, а затем выберите **<New Database>** в поле **База данных подписки**.  
  
7.  В диалоговом окне **Создание базы данных** в поле **Имя базы данных** введите **ProductReplica** , нажмите кнопку **ОК**, затем **Далее**.  
  
8.  В диалоговом окне **Безопасность агента распространителя** нажмите кнопку с многоточием (**…**), введите \<*имя_компьютера>***\repl_distribution** в поле **Учетная запись процесса**, а затем введите пароль для этой учетной записи, нажмите кнопки **ОК** и **Далее**.  
  
9. Нажмите кнопку **Готово** , чтобы принять значения по умолчанию на оставшихся страницах и завершить работу мастера.  
  
### Установка разрешений базы данных на подписчике  
  
1.  Подключитесь к подписчику в среде [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], последовательно разверните узлы **Базы данных**, **ProductReplica** и **Безопасность**, щелкните правой кнопкой мыши элемент **Пользователи** и выберите пункт **Создать пользователя**.  
  
2.  На странице **Общие** в списке **Тип пользователя** выберите **Пользователь Windows**.  
  
3.  Выберите поле **Имя пользователя**, нажмите кнопку с многоточием (…), в поле **Введите имя объекта** введите \<имя_компьютера>**\repl_distribution**, щелкните **Проверить имена**, а затем нажмите кнопку **ОК**.  
  
4.  Чтобы создать пользователя, на странице **Членство** в поле **Членство в роли базы данных** выберите **db_owner** и нажмите кнопку **ОК**.  
  
### Просмотр состояния синхронизации подписки  
  
1.  Подключитесь к издателю в среде [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], а затем раскройте узел сервера и папку **Репликация** .  
  
2.  В папке **Локальные публикации** разверните публикацию **AdvWorksProductTrans**, щелкните правой кнопкой мыши подписку в базе данных **ProductReplica** и выберите пункт **Просмотр состояния синхронизации**.  
  
    Отобразится текущее состояние синхронизации подписки.  
  
3.  Если подписка не отображается под публикацией **AdvWorksProductTrans**, нажмите клавишу F5 для обновления списка.  
  
## Следующие шаги  
Создание подписки на публикацию транзакций успешно завершено. Ввиду того, что агент распространителя для этой подписки постоянно запущен, подписка инициализируется при создании. Далее необходимо использовать трассировочные токены, чтобы проверить выполнение репликации изменений и определить задержку. См. раздел [Lesson 3: Validating the Subscription and Measuring Latency](../../relational-databases/replication/lesson-3-validating-the-subscription-and-measuring-latency.md).  
  
## См. также:  
[Инициализация подписки с помощью моментального снимка](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
[Создание принудительной подписки](../../relational-databases/replication/create-a-push-subscription.md)  
[Подписка на публикации](../../relational-databases/replication/subscribe-to-publications.md)  
  