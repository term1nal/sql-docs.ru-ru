---
title: "Агент моментальных снимков (мастер создания публикаций) | Документация Майкрософт"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rep.newpubwizard.configuresnapshotagent.f1
ms.assetid: 0257d4ee-1f7b-49fd-b4ef-65bfc1ef6951
caps.latest.revision: 29
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 7682f989a77d79eb011088fe927c199b6c2b36fe
ms.contentlocale: ru-ru
ms.lasthandoff: 06/22/2017

---
# <a name="snapshot-agent-new-publication-wizard"></a>Агент моментальных снимков (мастер создания публикаций)
  Агент моментальных снимков создает файлы, содержащие схему публикации и данные для инициализации новых подписок. По умолчанию агент моментальных снимков запускается сразу же после создания публикации в мастере создания публикаций. Впоследствии этот агент запускается по указанному расписанию. Будет ли этот агент создавать новые файлы моментальных снимков при каждом запуске, зависит от типа репликации и выбранных параметров. Дополнительные сведения см. в статье [Создание и применение моментального снимка](../../relational-databases/replication/create-and-apply-the-snapshot.md).  
  
 Для публикаций слиянием, использующих параметризованные фильтры, необходимо создать моментальный снимок для каждой секции данных после завершения снимка публикации. Дополнительные сведения см. в статье [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md).  
  
## <a name="options"></a>Параметры  
 **Создать моментальный снимок немедленно** (репликация слиянием) или **Создать моментальный снимок немедленно и обеспечить доступ к нему для инициализации подписок** (репликация транзакций)  
 Установите этот флажок для немедленного создания моментального снимка по завершении работы мастера создания публикаций. Снимите этот флажок, если планируете изменить свойства моментального снимка в диалоговом окне **Свойства публикации** перед созданием снимка или если будете инициализировать подписчик без моментального снимка. Дополнительные сведения см. в статье [Initialize a Transactional Subscription Without a Snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md).  
  
> [!NOTE]  
>  Мастер может запросить соединение с распространителем, чтобы запустить соответствующее задание для агента распространителя или агента слияния.  
  
 **Запланировать запуск агента моментальных снимков в следующее время**  
 Примите расписание по умолчанию для запусков агента моментальных снимков или нажмите кнопку **Изменить** , чтобы задать собственное расписание.  
  
## <a name="see-also"></a>См. также:  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [Создание и применение исходного моментального снимка](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)   
 [Просмотр и изменение свойств публикации](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Инициализация подписки с помощью моментального снимка](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)   
 [Публикация данных и объектов базы данных](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Replication Agents Overview](../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  