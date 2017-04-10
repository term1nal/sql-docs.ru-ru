---
title: "Свойства публикации, статьи | Microsoft Docs"
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
  - "sql13.rep.newpubwizard.pubproperties.articles.f1"
ms.assetid: bdeea318-a153-44b8-9e51-9155f3bad18b
caps.latest.revision: 29
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 29
---
# Свойства публикации, статьи
  Страница **Статьи** диалогового окна **Свойства публикации** : содержит данные о статьях, имеющихся в публикации, позволяет добавлять статьи в существующие публикации и удалять из публикаций статьи, позволяет изменять свойства статьи и фильтрацию столбцов.  
  
> [!NOTE]  
>  После создания публикации для некоторых изменений свойств требуется новый моментальный снимок. Если на публикацию имеются подписки, для некоторых изменений также требуется повторная инициализация всех подписок. Дополнительные сведения см. в разделе [Изменение публикации и свойства статей](../../relational-databases/replication/publish/change-publication-and-article-properties.md) и [Добавление и удаление статей в существующих публикациях](../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md).  
  
 При публикации объекта базы данных, зависящего от одного или нескольких других объектов базы данных, необходимо опубликовать и все связанные с ним объекты. Например, при публикации представления, зависящего от таблицы, необходимо также опубликовать и таблицу.  
  
 Красный значок рядом с объектом указывает на то, что объект не может быть опубликован; объяснение приводится в справочной панели внизу страницы мастера. Не могут быть опубликованы следующие объекты:  
  
-   Зашифрованные объекты.  
  
-   Индексированные представления, содержащие столбцы, которые допускают значение NULL.  
  
-   Таблицы без первичных ключей не могут быть опубликованы в публикациях транзакций.  
  
-   Таблицы не могут быть опубликованы одновременно в публикациях слиянием и в публикациях транзакций, включенных для подписок, обновляемых посредством очередей. Дополнительные сведения о публикации статьи в нескольких публикациях см. в разделе «Публикация таблиц в нескольких публикациях» [публикации данных и объектов базы данных](../../relational-databases/replication/publish/publish-data-and-database-objects.md).  
  
## Издатели Oracle  
 Дополнительные вопросы, касающиеся издателей Oracle:  
  
-   Список объектов, которые могут публиковаться из Oracle, см. в разделе [Design Considerations and Limitations for Oracle Publishers](../../relational-databases/replication/non-sql/design-considerations-and-limitations-for-oracle-publishers.md). Объекты, которые не могут быть опубликованы, не отображаются.  
  
-   Список типов данных, которые могут быть опубликованы, см. в разделе [Data Type Mapping for Oracle Publishers](../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md). Столбцы с типами данных, которые не могут быть опубликованы, не отображаются.  
  
## Фильтры столбцов  
 Фильтрации столбцов на этой странице раскройте таблицу в **объекты для публикации** и выберите только необходимые столбцы (фильтрация строк доступна в **Фильтрация строк таблицы** этого мастера). Фильтрация столбцов полезна по ряду причин, в том числе из соображений безопасности (предотвращение репликации конфиденциальных данных) и производительности (предотвращение репликации столбцов с большими двоичными объектами (BLOB)). Дополнительные сведения о фильтрации столбцов, включая список типов столбцов, которые не могут быть отфильтрованы, см. [Фильтрация опубликованных данных](../../relational-databases/replication/publish/filter-published-data.md).  
  
## Параметры  
 Панель **Объекты для публикации** позволяет:  
  
-   Просмотреть все объекты, доступные для репликации.  
  
-   Добавить в публикацию статью, установив флажок рядом с этим объектом.  
  
-   Удалить из публикации статью, сняв флажок рядом с этим объектом. Чтобы узнать, когда статьи могут быть удалены, см. [Добавление и удаление статей в существующих публикациях](../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md).  
  
-   Включить все объекты определенного типа (например, таблицы) в публикацию, установив флажок рядом с полем, тип объекта (например, **таблицы**).  
  
-   Раскрывать узлы таблицы для просмотра ее столбцов.  
  
-   Отфильтруйте столбцы таблицы, которые не должны входить в публикацию, сняв флажки рядом с соответствующими столбцами, или включите непубликуемые столбцы, установив флажки.  
  
-   Щелкните правой кнопкой мыши объект на панели, чтобы вызвать меню команд для этого объекта.  
  
 **Свойства статьи**  
 Щелкните **Свойства статьи** , а затем выберите один из следующих:  
  
-   Щелкните **указать свойства выделенной \< ObjectType> статьи** для запуска **Свойства статьи — \< имя_объекта>** диалоговое окно; свойство изменения, внесенные в этом диалоговом окне, применяются только объект, который будет выделен на панели объектов на **статьи** страницы.  
  
-   Щелкните **Установка свойств всех \< ObjectType> статьи**, чтобы открыть **Свойства всех \< ObjectType> статьи** диалоговое окно; свойство изменения, внесенные в этом диалоговом окне применяются ко всем объектам этого типа на панели объектов на **статьи** страницы, включая объекты, не выбранные для публикации.  
  
    > [!NOTE]  
    >  Изменения, произведенные в **Свойства для всех \< ObjectType> статьи** диалоговое окно отменяют изменения, сделанные ранее в **Свойства статьи — \< имя_объекта>** диалоговое окно. Например, если нужно установить некоторое количество значений по умолчанию для всех статей типа объекта, но при этом задать некоторые свойства для отдельных объектов, сначала установите значения по умолчанию для всех статей. Затем установите свойства для отдельных объектов.  
  
 **Выделенная таблица предназначена только для загрузки**  
 Только репликация слиянием. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] и более поздних версий. Выберите, чтобы указать, что при использовании клиентской подписки вносить изменения на подписчике не допускается. Учитывая то, что статьи только для загрузки не могут обновляться у подписчика, отслеживаемые метаданные подписчикам не отправляются. Это может привести к уменьшению объема хранилища на подписчиках и увеличению производительности, особенно в условиях медленного сетевого соединения. Этот параметр соответствует параметру значение **только для загрузки на подписчик, запретить изменения на подписчике** для параметра **направление синхронизации** в **Свойства статьи** диалоговое окно. Дополнительные сведения см. в разделе [оптимизировать слияния производительности репликации со статьями, доступными только для загрузки](../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md).  
  
 **Показывать в списке только отмеченные объекты**  
 Установите этот флажок, чтобы показать только те статьи, которые выбраны на панели объектов.  
  
## См. также:  
 [Создание публикации](../../relational-databases/replication/publish/create-a-publication.md)   
 [Просмотр и изменение свойств публикации](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Создание и применение исходного моментального снимка](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)   
 [Повторная инициализация подписки](../../relational-databases/replication/reinitialize-a-subscription.md)   
 [Публикация данных и объектов базы данных](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  