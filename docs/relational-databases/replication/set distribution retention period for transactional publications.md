---
title: "настроить срок хранения на распространителе для публикаций транзакций (среда SQL Server Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "03/23/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "срок хранения транзакции [репликация SQL Server]"
  - "срок хранения [репликация SQL Server]"
ms.assetid: 9a98c53a-fea5-4235-b23d-6c69587c5676
caps.latest.revision: 37
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# настроить срок хранения на распространителе для публикаций транзакций (среда SQL Server Management Studio)
  Укажите минимальный срок хранения распространения и максимальный срок хранения распространения на **Свойства базы данных распространителя — \< База_данных_распространителя>** диалоговое окно. Этот параметр доступен из **Общие** Страница **Свойства распространителя — \< распространитель>** диалоговое окно. Дополнительные сведения о доступе к этому диалоговому окну см. в разделе [представления и свойств издателя и распространителя изменить](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md).  
  
### Указание срока хранения на распространителе  
  
1.  На **Общие** Страница **Свойства распространителя — \< распространитель>** диалогового окна нажмите кнопку с многоточием (**...**) для базы данных распространителя.  
  
2.  Для указания минимального срока хранения на распространителе введите значение в поле **Минимум** ; для указания максимального срока хранения на распространителе введите значение в поле **Но не более** .  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## См. также:  
 [Настройка распространителя](../../relational-databases/replication/configure-distribution.md)   
 [Окончание срока действия и отключение подписки](../../relational-databases/replication/subscription-expiration-and-deactivation.md)  
  
  