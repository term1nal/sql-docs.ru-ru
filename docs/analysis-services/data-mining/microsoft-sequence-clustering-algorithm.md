---
title: "Алгоритм кластеризации последовательностей (Майкрософт) | Microsoft Docs"
ms.custom: ""
ms.date: "03/02/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "кластеры [службы Analysis Services]"
  - "алгоритмы [интеллектуальный анализ данных]"
  - "алгоритмы кластеризации последовательностей [службы Analysis Services]"
  - "последовательность [службы Analysis Services]"
ms.assetid: ae779a1f-0adb-4857-afbd-a15543dff299
caps.latest.revision: 49
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 49
---
# Алгоритм кластеризации последовательностей (Майкрософт)
  Алгоритм кластеризации последовательностей [!INCLUDE[msCoName](../../includes/msconame-md.md)] — это уникальный алгоритм сочетающий в себе анализ последовательностей и кластеризацию. Данный алгоритм можно использовать для просмотра данных, содержащих события, которые могут быть связаны в *последовательность*. Алгоритм находит самые распространенные последовательности и выполняет кластеризацию для поиска идентичных последовательностей. Ниже описаны типы последовательностей, которые можно использовать в качестве данных для машинного обучения, чтобы получить сведения о стандартных проблемах или бизнес-сценариях:  
  
-   Сведения о посещениях и схемах щелчков, которые создаются, когда пользователи переходят по веб-сайту или просматривают его.  
  
-   Журналы, в которых перечислены события, предшествовавшие инциденту, такие как сбой жесткого диска или взаимоблокировка сервера.  
  
-   Записи транзакций, описывающие порядок, в котором клиент добавляет в корзину товары, выбранные в интернет-магазине.  
  
-   Записи, следящие за взаимодействием с клиентом или пациентом во времени для прогнозирования отмены услуг или других нежелательных итогов.  
  
 Этот алгоритм во многом напоминает алгоритм кластеризации [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Однако вместо поиска кластеров вариантов, содержащих похожие атрибуты, алгоритм кластеризации последовательностей [!INCLUDE[msCoName](../../includes/msconame-md.md)] находит кластеры вариантов, содержащие похожие пути в последовательности.  
  
## Пример  
 Веб-сайт [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] web site collects information about what pages site users visit, and about the order in which the pages are visited. Поскольку компания предоставляет возможность заказа по сети, клиентам необходимо зарегистрироваться на сайте. Благодаря этому с каждым щелчком мыши клиента компания получает сведения о действиях в рамках узла, выполняемых под клиентским профилем. Применив в отношении таких данных алгоритм кластеризации последовательностей [!INCLUDE[msCoName](../../includes/msconame-md.md)] , организация может найти группы или кластеры клиентов, для которых характерны похожие закономерности или последовательности щелчков. Компания затем может использовать данные кластеры для анализа перемещения пользователей в рамках веб-сайта, определения страниц, которые ближе всех связаны с продажей конкретного продукта, а также прогнозирования страниц, которые клиент с наибольшей долей вероятности посетит в следующий раз.  
  
## Принцип работы алгоритма  
 Алгоритм кластеризации последовательностей [!INCLUDE[msCoName](../../includes/msconame-md.md)] — это гибридный алгоритм, сочетающий методы с анализом марковских цепей для определения кластеров и их последовательностей.  Одной из особенностей алгоритма кластеризации последовательностей [!INCLUDE[msCoName](../../includes/msconame-md.md)] является то, что он использует данные последовательностей. Такие данные обычно представляют ряд событий или переходов между состояниями в наборе данных, например ряд приобретений продуктов или щелчков мышью на веб-узле для конкретного пользователя. Алгоритм изучает вероятность переходов и измеряет различия, или расстояния, между всеми возможными последовательностями в наборе данных, чтобы определить, какие последовательности лучше всего использовать в качестве входных данных для кластеризации. После создания алгоритмом списка вероятных последовательностей он использует эти сведения в качестве входных данных для кластеризации методом максимизации ожиданий (EM).  
  
 Подробное описание этой реализации см. в разделе [Microsoft Sequence Clustering Algorithm Technical Reference](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm-technical-reference.md).  
  
## Данные, необходимые для моделей кластеризации последовательностей  
 При подготовке данных, предназначенных для использования в обучении модели кластеризации последовательностей, следует учитывать требования к конкретному алгоритму, в том числе к объему необходимых данных, и то, как эти данные используются.  
  
 К модели кластеризации последовательностей предъявляются следующие требования.  
  
-   **Одиночный ключевой столбец**. Модели кластеризации последовательностей требуется ключ, по которому идентифицируются записи.  
  
-   **Столбец последовательности** Для данных последовательности модель должна иметь вложенную таблицу, содержащую столбец идентификатора последовательности. Идентификатор последовательности может иметь любой подлежащий сортировке тип данных. Например, можно использовать идентификатор веб-страницы, целое число или текстовую строку с условием, что столбец идентифицирует события в последовательности. Для каждой последовательности допускается только один идентификатор последовательности, а в каждой модели допускается только один тип последовательности.  
  
-   **Необязательные атрибуты, не относящиеся к последовательности** алгоритм поддерживает добавление других атрибутов, не связанных с последовательностью. Эти атрибуты могут включать вложенные столбцы.  
  
 Например, в случае с указанным выше веб-сайтом [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] модель кластеризации последовательности может включать в качестве не связанных с последовательностью атрибутов такие сведения о заказе, как таблица вариантов и демографические данные клиента. Кроме того, она будет включать вложенную таблицу, содержащую последовательность просмотра веб-сайта клиентом или покупки в корзине в качестве данных последовательности.  
  
 Дополнительные сведения о типах содержимого и типах данных, поддерживаемых моделями кластеризации последовательностей, см. в подразделе "Требования" раздела [Технический справочник по алгоритму кластеризации последовательностей (Майкрософт)](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm-technical-reference.md).  
  
## Просмотр модели кластеризации последовательности  
 Модель интеллектуального анализа данных, создаваемая данным алгоритмом, содержит описания самых распространенных последовательностей в данных. Чтобы исследовать модель, можно использовать **Средство просмотра кластеризации последовательностей (Майкрософт)**. При просмотре модели кластеризации последовательности службы [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] отображают кластеры, содержащие несколько переходов. Можно также просмотреть соответствующие статистические данные. Дополнительные сведения см. в разделе [Просмотр модели с помощью средства просмотра кластеризации последовательностей (Майкрософт)](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-sequence-cluster-viewer.md).  
  
 Чтобы получить более подробные сведения, можно просмотреть модель с помощью [средства просмотра деревьев содержимого общего вида (Майкрософт)](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md). Содержимое, сохраняемое для модели, включает распределение всех значений в каждом узле, вероятность каждого кластера и подробные сведения о переходах. Дополнительные сведения см. в разделе [Содержимое моделей интеллектуального анализа данных для моделей кластеризации последовательностей (службы Analysis Services — интеллектуальный анализ данных)](../../analysis-services/data-mining/mining model content for sequence clustering models.md).  
  
## Создание прогнозов  
 После обучения модели результаты хранятся в виде набора шаблонов. Можно использовать описания наиболее распространенных последовательностей в данных для прогноза следующего наиболее вероятного шага в новой последовательности. Но поскольку алгоритм включает другие столбцы, результирующую модель можно использовать для определения связи между данными, включенными в последовательность, и данными, не включенными в нее. Например, если к модели добавляются демографические данные, можно сделать прогноз для конкретной группы клиентов. Прогнозирующие запросы можно настраивать для того, чтобы они возвращали переменное число прогнозов или описательные статистические данные.  
  
 Дополнительные сведения о создании запросов к модели интеллектуального анализа данных см. в разделе [Запросы интеллектуального анализа данных](../../analysis-services/data-mining/data-mining-queries.md). Примеры использования запросов с моделью кластеризации последовательностей см. в разделе [Примеры запросов к модели кластеризации последовательностей](../../analysis-services/data-mining/sequence-clustering-model-query-examples.md).  
  
## Замечания  
  
-   Не поддерживается использование языка разметки прогнозирующих моделей (PMML) для создания моделей интеллектуального анализа данных.  
  
-   Поддерживается детализация.  
  
-   Поддерживается использование моделей интеллектуального анализа OLAP и создание измерений интеллектуального анализа данных.  
  
## См. также  
 [Алгоритмы интеллектуального анализа данных (службы Analysis Services — интеллектуальный анализ данных)](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Технический справочник по алгоритму кластеризации последовательностей (Майкрософт)](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm-technical-reference.md)   
 [Примеры запросов к модели кластеризации последовательностей](../../analysis-services/data-mining/sequence-clustering-model-query-examples.md)   
 [Просмотр модели с помощью средства просмотра кластеризации последовательностей (Майкрософт)](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-sequence-cluster-viewer.md)  
  
  