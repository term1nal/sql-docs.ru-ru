---
title: "Подписчики | Документация Майкрософт"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rep.newsubwizard.subscribers.f1
helpviewer_keywords:
- Subscribers [SQL Server replication]
ms.assetid: 43fb2454-c220-4d25-a826-83c332eb00d2
caps.latest.revision: 26
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1a7a3174c0eab10b0a05dd4844e214f3ab70ee75
ms.contentlocale: ru-ru
ms.lasthandoff: 06/22/2017

---
# <a name="subscribers"></a>Подписчики
  Укажите [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] или отличных от[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] подписчиков, которые будут получать подписку выбранной публикации.  
  
## <a name="options"></a>Параметры  
 **Подписчики**  
 Установите флажок на сетке, чтобы выбрать соответствующие [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] или отличные от[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] источники данных в качестве подписчика публикации, выбранной на странице **Публикация** . Если подписчика нет в списке, выберите пункт **Добавить подписчик** или **Добавить подписчик SQL Server**.  
  
 **База данных подписки**  
 Данные и операции в данном столбце зависят от типов подписчиков, перечисленных в столбце **Подписчики** .  
  
-   Для подписчиков [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] выберите из списка **База данных подписки** базу данных или создайте новую базу данных с помощью команды **Создать базу данных** в этом же списке.  
  
    > [!NOTE]  
    >  Если издатель выбран также в качестве подписчика, база данных подписки должна отличаться от базы данных публикации.  
  
-   Для подписчиков, отличных от[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , база данных подписки не отображается. В поле **Имя источника данных** диалогового окна **Добавление сервера, отличного от подписчика SQL Server** укажите базу данных вместе с другими сведениями о соединении. Чтобы открыть это диалоговое окно, нажмите кнопку **Добавить подписчик** , а затем выберите пункт **Добавить подписчик, отличный от подписчика SQL Server**.  
  
 **Добавить подписчик**  
 Добавьте сервер в список серверов, которые могут быть включены в качестве подписчиков. Данная кнопка отображается, когда выполняются все перечисленные далее условия.  
  
-   Выбранная публикация является публикацией транзакций или моментальных снимков без поддержки обновляемых подписок.  
  
    > [!NOTE]  
    >  Если публикация, на которую выполняется подписка, имеет подписки [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , но еще не подготовлена для подписчиков, не являющихся[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , добавить подписку, не являющуюся[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , невозможно.  
  
-   Подписка является принудительной.  
  
-   Издателем выбранной публикации является [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] или более поздней версии.  
  
 При нажатии кнопки **Добавить подписчик** отображается меню с двумя пунктами: **Добавить подписчик SQL Server** и **Добавить подписчик, отличный от подписчика SQL Server**. Чтобы добавить подписчик Oracle или IBM DB2, выберите пункт **Добавить подписчик, отличный от подписчика SQL Server** .  
  
 **Добавить подписчик SQL Server**  
 Добавьте сервер в список серверов, которые могут быть включены в качестве подписчиков. Данная кнопка отображается при выполнении одного или нескольких из перечисленных ниже условий.  
  
-   Выбранная публикация является публикацией слиянием, публикацией моментальными снимками или публикацией транзакций с поддержкой обновляемых подписок.  
  
-   Подписка является подпиской по запросу.  
  
-   Версия издателя выбранной публикации ниже [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Для более ранних версий данная кнопка отображается при выполнении одного или нескольких из перечисленных ниже условий.  
  
    -   Вы являетесь членом предопределенной роли сервера **sysadmin** на издателе.  
  
    -   Подписка добавлена на странице **Подписчики** в диалоговом окне **Свойства издателя** .  
  
    -   Публикация допускает анонимные подписки.  
  
## <a name="see-also"></a>См. также:  
 [Создание подписки по запросу](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)   
 [Подписчики, отличные от подписчиков SQL Server](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)   
 [Подписка на публикации](../../relational-databases/replication/subscribe-to-publications.md)  
  
  