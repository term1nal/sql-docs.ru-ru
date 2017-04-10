---
title: "Создание и применение моментального снимка | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "моментальные снимки [репликация SQL Server], применение"
  - "моментальные снимки [репликация SQL Server], создание"
ms.assetid: 631f48bf-50c9-4015-b9d8-8f1ad92d1ee2
caps.latest.revision: 38
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 38
---
# Создание и применение моментального снимка
  Моментальные снимки создаются агентом моментальных снимков после создания публикации. Моментальные снимки могут создаваться:  
  
-   Немедленно. По умолчанию моментальный снимок для публикации слиянием формируется немедленно после создания публикации в мастере создания публикаций.  
  
-   По расписанию. Расписание задается на **агента моментальных снимков** страницы мастера создания публикаций или при использовании хранимых процедур или объекты управления репликацией (RMO).  
  
-   Вручную. Агент моментальных снимков запускается из командной строки или из среды [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Дополнительные сведения о запуске агентов см. в разделе [Основные понятия исполняемых файлов агента репликации](../../relational-databases/replication/concepts/replication-agent-executables-concepts.md) и [Запуск и остановка агента репликации & #40; SQL Server Management Studio & #41;](../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md).  
  
 Для репликации слиянием моментальный снимок формируется при каждом запуске агента моментальных снимков. Для репликации транзакций формирование моментального снимка зависит от значения свойства публикации **immediate_sync**. Если значение свойства установлено в TRUE (значение по умолчанию при использовании мастера создания публикаций), моментальный снимок создается при каждом запуске агента моментальных снимков и может быть применен к подписчику в любое время. Если свойство имеет значение FALSE (значение по умолчанию при использовании **sp_addpublication**), моментальный снимок создается только в том случае, если был добавлен новую подписку с момента запуска последнего агента моментальных снимков; Подписчики должны ждать завершения синхронизации агента моментальных снимков.  
  
 Когда создаются моментальные снимки, они сохраняются по умолчанию в стандартной папке моментальных снимков, расположенной на распространителе. Файлы моментальных снимков можно также сохранить на сменных носителях, например на сменных дисках, компакт-дисках или в местоположениях, отличных от папки моментальных снимков по умолчанию. Кроме этого, эти файлы можно сжимать для облегчения их хранения и передачи, а также выполнять скрипты до или после применения моментального снимка на подписчике. Дополнительные сведения об этих параметрах см. в разделе [Snapshot Options](../../relational-databases/replication/snapshot-options.md).  
  
 Если требуется моментальный снимок для публикации слиянием, в которой используются параметризованные фильтры, процесс создания моментального снимка происходит в два этапа. Сначала создается моментальный снимок схемы, который содержит скрипты репликации и схему публикуемых объектов, но не содержит данные. Потом каждая подписка инициализируется при помощи моментального снимка, который содержит скрипты и схему, скопированную из моментального снимка схемы, и данные, которые принадлежат секции подписки. Дополнительные сведения см. в статье [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md).  
  
 После того как моментальный снимок создан на издателе и сохранен в папке по умолчанию или в каком-либо другом местоположении, этот моментальный снимок можно передать подписчику и применить. Агент распространителя (для репликации моментальных снимков или репликации транзакций) или агент слияния (для репликации слиянием) передает моментальный снимок и применяет файлы схемы и данных в базе данных подписки на подписчике во время выполнения первоначальной синхронизации. Если используется мастер создания подписки, первоначальная синхронизация происходит по умолчанию немедленно после создания подписки. Этот режим управляется параметром **Инициализировать, когда** на странице **Инициализация подписок** мастера. Когда моментальные снимки создаются после инициализации подписки, они не применяются на подписчике, если подписка не помечена для повторной инициализации. Дополнительные сведения см. в разделе [повторно инициализировать подписки](../../relational-databases/replication/reinitialize-subscriptions.md).  
  
 После того, как агент распространителя или агент слияния применяет исходный моментальный снимок, агент распространяет последующие обновления и другие изменения данных. Когда моментальные снимки распространяются и применяются на подписчиках, воздействие оказывается только на подписчики, ожидающие исходные или новые моментальные снимки. Другие подписчики на данную публикацию (уже получающие вставки, обновления, удаления или другие изменения опубликованных данных) не подвергаются воздействию.  
  
 Чтобы создать и применить исходный моментальный снимок, см. раздел [Create and Apply the Initial Snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
 Чтобы просмотреть или изменить папку по умолчанию для моментального снимка, см.  
  
-   [! ВКЛЮЧИТЬ [ssManStudioFull] (.. / Token/ssManStudioFull_md.md)]: [Specify the Default Snapshot Location &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/specify-the-default-snapshot-location-sql-server-management-studio.md)  
  
-   Программирование репликации и RMO: [Configure Publishing and Distribution](../../relational-databases/replication/configure-publishing-and-distribution.md)  
  
## См. также:  
 [Инициализация подписки с помощью моментального снимка](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)   
 [Организация безопасности папки моментальных снимков](../../relational-databases/replication/security/secure-the-snapshot-folder.md)   
 [sp_addpublication & #40; Transact-SQL и #41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)  
  
  