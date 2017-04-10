---
title: "Добавление и удаление статей в существующих публикациях | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "статьи [репликация SQL Server], удаление"
  - "удаление статей"
  - "удаление статей"
  - "удаление статей"
  - "добавление статей"
  - "управление репликацией, статьи"
  - "публикации [репликация SQL Server], добавление и удаление статей"
  - "статьи [репликация SQL Server], добавление"
ms.assetid: b148e907-e1f2-483b-bdb2-59ea596efceb
caps.latest.revision: 48
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 46
---
# Добавление и удаление статей в существующих публикациях
  Возможно добавлять и удалять статьи после создания публикации. Можно добавить статьи в любое время, но действия, необходимые для удаления статей, зависят от типа репликации и времени удаления статьи.  
  
## Добавление статей  
 Добавление статьи включает следующие операции: добавление статьи в публикацию, создание нового моментального снимка публикации, синхронизация подписки для применения схемы и данных для новой статьи.  
  
> [!NOTE]  
>  Если существующая статья зависит от новой статьи при добавлении статьи в публикацию слиянием, необходимо указать порядок обработки для обеих статей с помощью **@processing_order** параметр [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) и [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md). Рассмотрим следующий сценарий: необходимо опубликовать таблицу без публикации функции, на которую ссылается эта таблица. Если функция не будет опубликована, то таблица не сможет быть создана на подписчике. При добавлении функции к публикации: задайте значение **1** для **@processing_order** параметр **sp_addmergearticle**; и укажите значение **2** для **@processing_order** параметр **sp_changemergearticle**, указав имя таблицы для параметра **@article**. Этот порядок обработки гарантирует создание функции на подписчике до создания таблицы, которая зависит от нее. Можно использовать различные числа для каждой статьи при условии, что число для функции меньше числа для таблицы.  
  
1.  Добавьте одну или несколько статей с помощью следующих методов:  
  
    -   [Добавление и удаление статей в публикации и #40; SQL Server Management Studio & #41;](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-a-publication.md)  
  
    -   [Определение статьи](../../../relational-databases/replication/publish/define-an-article.md)  
  
2.  После добавления статьи в публикацию необходимо создать новый моментальный снимок для публикации (и все секции, если это публикация слиянием с параметризованными фильтрами). Затем агент распространителя или агент слияния копирует схему и данные для новой статьи на подписчик (он не инициализирует заново всю публикацию).  
  
    -   Сведения о создании моментального снимка см. в разделе [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
    -   Чтобы создать новый моментальный снимок для публикации слиянием с параметризованными фильтрами, см. раздел [Создать моментальный снимок для публикации слиянием с параметризованными фильтрами](../../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md).  
  
3.  После создания моментального снимка синхронизируйте подписку, чтобы скопировать схему и данные для новой статьи.  
  
    -   Сведения о синхронизации принудительной подписки см. в разделе [Synchronize a Push Subscription](../../../relational-databases/replication/synchronize-a-push-subscription.md).  
  
    -   Сведения о синхронизации подписки по запросу см. в разделе [Synchronize a Pull Subscription](../../../relational-databases/replication/synchronize-a-pull-subscription.md).  
  
## Удаление статей  
 Статьи могут быть удалены из публикации в любое время, но следует принять во внимание следующие аспекты:  
  
-   Удаление статьи из публикации не удаляет объект из базы данных публикации или соответствующий объект из базы данных подписки. Используйте DROP \< объект> для удаления этих объектов при необходимости. При удалении статьи, которая связана с другими опубликованными статьями с помощью ограничений внешних ключей, рекомендуется удалить таблицу на подписчике вручную или выполнив скрипт по требованию: укажите скрипт, который содержит соответствующие DROP \< объект> инструкции. Дополнительные сведения см. в разделе [#40; & выполнение скриптов во время синхронизации Программирование репликации Transact-SQL & #41;](../../../relational-databases/replication/execute-scripts-during-synchronization-replication-transact-sql-programming.md).  
  
-   Для публикации слиянием с уровнем совместимости 90RTM и выше возможно удаление статей в любое время, но требуется новый моментальный снимок. Дополнительно:  
  
    -   Если статья является родительской статьей в фильтре соединения или в отношении логической записи, сначала нужно удалить отношения, и это требует повторной инициализации.  
  
    -   Если статья содержит последний параметризованный фильтр в публикации, подписки должны быть повторно инициализированы.  
  
-   Для публикаций слиянием с уровнем совместимости ниже 90RTM статьи можно удалить без особых размышлений до первоначальной синхронизации подписок. Если статья удалена после синхронизации одной подписки или более, подписки должны быть удалены, заново созданы и синхронизированы.  
  
-   Для публикации моментальных снимков или публикации транзакций статьи можно удалить без особых размышлений до создания подписок. Если статья удалена после создания одной или более подписок, подписки должны быть удалены, заново созданы и синхронизированы. Дополнительные сведения об удалении подписок см. в разделе [подписаться на публикации](../../../relational-databases/replication/subscribe-to-publications.md) и [sp_dropsubscription & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md). **sp_dropsubscription** позволяет удалить одну статью из подписки, а не всей подписки.  
  
1.  Удаление статьи из публикации включает удаление статьи и создание нового моментального снимка для публикации. Удаление статьи сделает текущий моментальный снимок недействительным; поэтому должен быть создан новый моментальный снимок.  
  
    -   Удаление статьи из публикации, в разделе [добавления и удаления статей в публикации и #40; SQL Server Management Studio & #41;](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-a-publication.md) или [удалить статью](../../../relational-databases/replication/publish/delete-an-article.md).  
  
2.  После удаления статьи из публикации необходимо создать новый моментальный снимок для публикации (и все секции, если это публикация слиянием с параметризованными фильтрами).  
  
    -   Сведения о создании моментального снимка см. в разделе [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
    -   Чтобы создать новый моментальный снимок для публикации слиянием с параметризованными фильтрами, см. раздел [Создать моментальный снимок для публикации слиянием с параметризованными фильтрами](../../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md).  
  
 Как указано выше, в некоторых случаях удаление статьи требует, чтобы подписки были удалены, заново созданы и синхронизированы. Дополнительные сведения см. в разделе [подписаться на публикации](../../../relational-databases/replication/subscribe-to-publications.md) и [синхронизации данных](../../../relational-databases/replication/synchronize-data.md).  
  
## См. также:  
 [Публикация данных и объектов базы данных](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Повторная инициализация подписок](../../../relational-databases/replication/reinitialize-subscriptions.md)   
 [Внесение изменений схем в базы данных публикации](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)  
  
  