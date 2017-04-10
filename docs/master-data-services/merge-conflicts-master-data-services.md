---
title: "Слияние конфликтов (Master Data Services) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 797219ad-5109-4666-94d3-dd1d59440a33
caps.latest.revision: 5
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 5
---
# Слияние конфликтов (Master Data Services)
  В [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] попытка публикации данных, измененных другим пользователем, завершится ошибкой из-за конфликта. Чтобы устранить эту ошибку, можно выполнить слияние конфликтов и повторно опубликовать изменения.  
  
## Предварительные требования  
 Чтобы выполнить эту процедуру:  
  
-   Необходимо иметь разрешение на доступ к функциональной области **Обозреватель** .  
  
-   Как минимум, необходимо разрешение на обновление для конечного объекта модели для сущности, которую нужно обновить.  
  
### Слияние конфликтов  
  
1.  На странице **Обозреватель** обновите атрибут элемента.  
  
2.  Если другой пользователь изменил тот же атрибут элемента, появится диалоговое окно **Объединить конфликты**.  
  
3.  В диалоговом окне **Объединить конфликты** можно выполнить одно из указанных ниже действий.  
  
    -   Выберите **Последний** и нажмите кнопку **Применить**, чтобы отменить ожидающие изменения и повторно загрузить последнюю версию с сервера.  
  
    -   Выберите **Исходный** и нажмите кнопку **Применить**, чтобы применить исходную версию на листе.  
  
    -   Выберите **Ваш** и нажмите кнопку **Применить**, чтобы сохранить существующие локальные изменения.  
  
4.  Нажав кнопку **Применить**, можно внести дополнительные изменения и опубликовать данные снова. Можно также нажать кнопку **Отменить**, чтобы отменить обновление и повторно загрузить последнюю версию с сервера.  
  
## См. также:  
 [Элементы (службы Master Data Services)](../master-data-services/members-master-data-services.md)  
  
  