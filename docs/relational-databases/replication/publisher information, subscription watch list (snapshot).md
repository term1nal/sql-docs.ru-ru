---
title: "Сведения об издателе, список наблюдения за подписками (публикация моментальных снимков, SQL Server 2005 и более поздние версии) | Microsoft Docs"
ms.custom: ""
ms.date: "03/23/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.monitor.publisherinfo.subscriptionssummary.snapshot.f1"
ms.assetid: 2ebeee62-7f54-4c77-9d37-15708bc5cc23
caps.latest.revision: 32
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Сведения об издателе, список наблюдения за подписками (публикация моментальных снимков, SQL Server 2005 и более поздние версии)
  Вкладка **Список наблюдения за подписками** доступна для распространителей под управлением [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] и более поздних версий. Она предназначается для отображения сведений о подписках на все публикации, доступные на выбранном издателе. Список подписок можно фильтровать для просмотра ошибок, предупреждений и подписок с низкой производительностью. На этой вкладке содержатся в одном месте для наблюдения за активностью всех репликаций на издателе: монитор репликации отображает все подписки, требующие вмешательства, в зависимости от выбранного типа репликации и параметр, выбранный в **Показать** поле раскрывающегося списка. Элементы отображаются на этой вкладке в соответствии с текущим состоянием и производительностью, поэтому подписки отображаются на этой странице только в случае, если они в настоящее время соответствуют параметру в списке **Показать** .  
  
## Параметры  
 Для получения дополнительных сведений о подписке и о связанных с ней задачах щелкните правой кнопкой мыши на строке с этой подпиской, а затем выберите соответствующий параметр в контекстном меню. Чтобы изменить способ отображения данных в сетке, щелкните правой кнопкой мыши сетку, а затем один из следующих параметров.  
  
-   **Сортировать**: сортировка по одному или нескольким столбцам в диалоговом окне **Сортировка столбцов** .  
  
-   **Выберите столбцы для отображения**: выбор столбцов для отображения и порядка их отображения в диалоговом окне **Выбор столбцов** .  
  
-   **Фильтр**: фильтрация строк в сетке на основании значений столбцов в диалоговом окне **Параметры фильтра** .  
  
-   **Очистить фильтр**: удаление всех параметров фильтра для сетки.  
  
 Настройки фильтра уникальны для каждой сетки. Выбор и сортировка столбцов применяются ко всем сеткам одного типа, как, например, сетка публикаций для каждого издателя.  
  
 **Показать подписки на моментальные снимки**  
 Выберите типы подписок (на публикацию транзакций, на моментальные снимки или слиянием), которые будут выводиться для выбранного издателя.  
  
 **Показать**  
 Выберите состояния подписки, которые должны отображаться для выбранного типа подписки. Например, можно выбрать отображение только тех подписок, которые содержат ошибку.  
  
 **Состояние**  
 Состояние каждой подписки, определяемое состоянием агента моментальных снимков или агента распространителя (отображается состояние с более высоким приоритетом).  
  
 По умолчанию, в сетке, содержащей сведения о подписках, они сортируются по столбцу **Состояние** . В следующем списке показаны возможные значения состояния и порядок сортировки значений (например, ошибки всегда показываются в верхней части сетки).  
  
-   Ошибка  
  
-   Срок действия скоро истекает или истек  
  
-   Неинициализированная подписка  
  
-   Повтор последней невыполненной команды  
  
-   Синхронизация  
  
-   Нет синхронизации  
  
 Порядок сортировки также определяет отображаемое значение, если данная подписка имеет более одного состояния. Например, если подписка содержит ошибку и срок ее действия скоро истекает, в столбце **Состояние** отображается **Ошибка**.  
  
 Значения состояния **Срок действия скоро истекает или истек** и **Неинициализированная подписка** являются предупреждениями. Когда выводится предупреждение, столбец **Состояние** также отображается при запущенном агенте. Например, состояние может быть **выполняется, срок действия скоро истекает или истек**.  
  
 Значение состояния **Срок действия скоро истекает или истек** отображается только при установленном пороге. Сведения об установке пороговых значений см. в разделе [задать пороговые значения и предупреждения в мониторе репликации](../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md).  
  
 **Подписка**  
 Имя каждой подписки в виде: *подписки: подписки*.  
  
 **Публикация**  
 Имя публикации, с которой синхронизируется подписка, в форме: *ИмяБазыДанныхПубликации: ИмяПубликации*.  
  
 **Последняя синхронизация**  
 Время последнего запуска агента распространителя. Если в данный момент синхронизация выполняется, то выводится сообщение **Выполняется** .  
  
## См. также:  
 [Запуск монитора репликации](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [Просмотр сведений и выполнение задач для издателя и #40; Монитор репликации & #41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-publisher-replication-monitor.md)   
 [Наблюдение за репликацией](../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  