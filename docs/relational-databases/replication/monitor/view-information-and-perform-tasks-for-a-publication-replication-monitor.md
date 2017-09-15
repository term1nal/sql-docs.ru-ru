---
title: "Просмотр сведений и выполнение задач для публикации (монитор репликации) | Документация Майкрософт"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- viewing publication information
- publications [SQL Server replication], viewing information
- publications [SQL Server replication], Replication Monitor tasks
ms.assetid: 92e28a07-d6a7-461b-a0b3-bd9bc6afcbe5
caps.latest.revision: 39
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d01adb7abcb4c110f826e0cd54814a66c83c0051
ms.contentlocale: ru-ru
ms.lasthandoff: 06/22/2017

---
# <a name="view-information-and-perform-tasks-for-a-publication-replication-monitor"></a>Просмотр сведений и выполнение задач для публикации (монитор репликации)
  Монитор репликации содержит следующие вкладки, предоставляющие информацию о выбранной публикации:  
  
-   **Все подписки**  
  
     На этой вкладке отображаются сведения о всех подписках на выбранную публикацию.  
  
-   **Агенты**  
  
     На этой вкладке отображаются сведения о всех агентах, используемых в публикации.  
  
    -   Агент моментальных снимков, используемый всеми публикациями.  
  
    -   Агент чтения журналов, используемый всеми публикациями транзакций.  
  
    -   Агент чтения очереди, используемый публикациями транзакций, имеющих обновляемые посредством очередей подписки.  
  
-   **Предупреждения** (для распространителей, на которых выполняется [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] или более поздние версии)  
  
    -   Эта вкладка позволяет задать предупреждения для агентов.  
  
-   **Трассировочные токены** (только для репликации транзакций, для распространителей, использующих [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] или более позднюю версию).  
  
     Эта вкладка позволяет измерять величину задержки между моментом фиксации транзакции на издателе и моментом фиксации соответствующей транзакции на подписчике.  
  
 Чтобы перейти к дополнительным сведениям о параметрах на каждой вкладке, щелкните вкладку на правой панели, а затем нажмите **Справка** в строке меню. Сведения о запуске монитора репликации см. в [этой статье](../../../relational-databases/replication/monitor/start-the-replication-monitor.md).  
  
### <a name="to-view-information-and-perform-tasks-for-a-publication"></a>Просмотр информации и выполнение задач публикации  
  
1.  Раскройте на левой панели группу издателей, раскройте издатель и выберите нужную публикацию.  
  
2.  Для просмотра и изменения свойств публикации щелкните публикацию правой кнопкой мыши, затем щелкните **Свойства**.  
  
3.  Для просмотра сведений о подписках щелкните вкладку **Все подписки** .  
  
     Для просмотра и изменения свойств подписки щелкните подписку правой кнопкой мыши, затем щелкните **Свойства**. На этой вкладке можно также просмотреть другие подробные сведения и выполнить дополнительные задачи. Дополнительные сведения см. в статье [Просмотр сведений и выполнение задач для агентов, связанных с подпиской (монитор репликации)](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-subscription-agents.md).  
  
4.  Чтобы просмотреть сведения об агентах, перейдите на вкладку **Агенты** . На этой вкладке можно также просмотреть другие подробные сведения и выполнить дополнительные задачи. Дополнительные сведения см. в статье [Просмотр сведений и выполнение задач для агентов, связанных с публикацией (монитор репликации)](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-publication-agents.md).  
  
5.  Чтобы просмотреть сведения о предупреждениях агентов и пороговых значениях, перейдите на вкладку **Предупреждения** . Дополнительные сведения см. в разделе [Set Thresholds and Warnings in Replication Monitor](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md).  
  
6.  Чтобы просмотреть сведения о трассировочных токенах, перейдите на вкладку **Трассировочные токены** . Дополнительные сведения об использовании трассировочных токенов см. в разделе [Measure Latency and Validate Connections for Transactional Replication](../../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md).  
  
## <a name="see-also"></a>См. также:  
 [Просмотр и изменение свойств публикации](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Наблюдение за репликацией](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  