---
title: "Инициализировать подписки | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.newsubwizard.initializesubscriptions.f1"
ms.assetid: 7b170e4e-470d-4828-a9ed-7435b0b03514
caps.latest.revision: 24
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 24
---
# Инициализировать подписки
  Необходимо инициализировать подписчиков, прежде чем они смогут начать прием реплицируемых данных. Начальный набор данных не требуется, но подписчик должен, по крайней мере, обладать схемой для каждого реплицируемого объекта и всеми таблицами метаданных и процедурами, необходимыми для репликации.  
  
## Параметры  
 **Свойства подписки**  
 Установите флажок в **инициализации** столбец для каждого подписчика, требующего наличия начального набора данных. Если флажок не установлен, будут инициализированы только метаданные и процедуры репликации. Дополнительные сведения об инициализации подписки без моментального снимка см. в разделе [инициализировать транзакционной подписки без моментального снимка](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md).  
  
 Выберите **немедленно** из раскрывающегося списка в **инициализировать, когда** столбец, чтобы агент слияния или агент распространителя передал моментальный снимок к подписчику после завершения этого мастера. Выберите пункт **При первой синхронизации** , чтобы агент переслал файлы при следующем запланированном запуске. Параметр **Немедленно** недоступен для подписок по запросу на [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]. Агент слияния и агент распространителя не работают на экземплярах выпуска [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], поэтому подписка должна быть инициализирована при помощи другого метода.  
  
> [!NOTE]  
>  Мастер может запросить соединение с распространителем, чтобы запустить соответствующее задание для агента распространителя или агента слияния.  
  
## См. также:  
 [Создание подписки по запросу](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Создание принудительной подписки](../../relational-databases/replication/create-a-push-subscription.md)   
 [Инициализация подписки](../../relational-databases/replication/initialize-a-subscription.md)   
 [Подписка на публикации](../../relational-databases/replication/subscribe-to-publications.md)  
  
  