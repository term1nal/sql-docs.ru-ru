---
title: "Сведения о публикации, все подписки (публикация слиянием) | Microsoft Docs"
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
  - "sql13.rep.monitor.publicationinfo.allsubscriptions.merge.f1"
ms.assetid: 0f4fa946-a0d9-4d3b-b90b-53503c40fba2
caps.latest.revision: 28
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 28
---
# Сведения о публикации, все подписки (публикация слиянием)
  Вкладка **Все подписки** выводит сведения обо всех подписках на выбранную публикацию слиянием.  
  
## Параметры  
 Для получения дополнительных сведений о подписке и о связанных с ней задачах щелкните правой кнопкой мыши на строке с этой подпиской, а затем выберите соответствующий параметр в контекстном меню. Чтобы изменить способ отображения данных в сетке, щелкните правой кнопкой мыши сетку, а затем один из следующих параметров.  
  
-   **Сортировать**: сортировка по одному или нескольким столбцам в диалоговом окне **Сортировка столбцов** .  
  
-   **Выберите столбцы для отображения**: выбор столбцов для отображения и порядка их отображения в диалоговом окне **Выбор столбцов** .  
  
-   **Фильтр**: фильтрация строк в сетке на основании значений столбцов в диалоговом окне **Параметры фильтра** .  
  
-   **Очистить фильтр**: удаление всех параметров фильтра для сетки.  
  
 Настройки фильтра уникальны для каждой сетки. Выбор и сортировка столбцов применяются ко всем сеткам одного типа, как, например, сетка публикаций для каждого издателя.  
  
 **Показать**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] и более поздних версий. Выберите состояния подписки, которые должны отображаться для выбранного типа подписки. Например, можно выбрать отображение только тех подписок, которые содержат ошибку.  
  
 **Состояние**  
 Состояние каждой подписки, определенной состоянием агента слияния.  
  
 По умолчанию сетка, содержащая сведения о подписке, сортируется по **состояние** столбцов (а затем сортируются по **производительности** столбца для подписок в одном состоянии). В следующем списке показаны возможные значения состояния и порядок сортировки значений (например, ошибки всегда показываются в верхней части сетки).  
  
-   Ошибка  
  
-   Критическая производительность (только для версии [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] и более поздних версий)  
  
-   Длительное слияние (только [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] и более поздние версии)  
  
-   Срок действия скоро истекает или истек (только для версии [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] и более поздних версий)  
  
-   Неинициализированная подписка ([!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] и более поздние версии)  
  
-   Повтор последней невыполненной команды  
  
-   Синхронизация  
  
-   Нет синхронизации  
  
 Порядок сортировки также определяет отображаемое значение, если данная подписка имеет более одного состояния. Например, если подписка содержит ошибку и срок ее действия скоро истекает, в столбце **Состояние** отображается **Ошибка**.  
  
 Значения состояния **Критическое для производительности**, **Продолжительное слияние**, **Срок действия скоро истекает или истек**, и **Неинициализированная подписка** являются предупреждениями. При отображении предупреждения столбец **Состояние** также отображает, производит ли агент синхронизацию. Например, состояние может быть **Синхронизация, Критическое для производительности**.  
  
 Значения состояния **Срок действия скоро истекает или истек** и **Продолжительное слияние** могут отображаться только в том случае, если заданы пороговые значения. Значение состояния **Критическое для производительности** может быть отображено только после произведения пяти синхронизаций подписок с один и тот же тип соединения (коммутируемое или по локальной сети). Сведения об измерении производительности и установке пороговых значений см. в разделе [мониторинг производительности с помощью монитора репликации](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md) и [задать пороговые значения и предупреждения в мониторе репликации](../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md).  
  
 **Подписка**  
 Имя каждой подписки в виде:*подписки: подписки*.  
  
 **Понятное имя**  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] и более поздних версий. Описание каждой подписки. Описание вводится в **Свойства подписки** диалоговое окно или указывается с помощью **@description** параметр [sp_addmergesubscription](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md) или [sp_addmergepullsubscription](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md). Пользователи часто используют описание как «понятное имя» или псевдоним для подписки.  
  
 **Производительность**  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] и более поздних версий. Определение оценки производительности каждой подписки на основе последних по времени измерений скорости доставки данных, снятых монитором репликации. Оценка определяется с помощью сравнения индивидуальной производительности подписки со средним значением производительности из истории подписок на публикации, имеющие тот же тип соединения (коммутируемое или по локальной сети). Монитор репликации отображает значение после пяти синхронизаций, использующих один тип соединения, каждая из которых содержит 50 или более изменений. Если произошло менее 5 синхронизаций с 50 и более изменениями или последняя выполненная синхронизация имела менее 50 изменений, то этот столбец остается пустым.  
  
> [!NOTE]  
>  Оценка производительности основана на типе отображаемого соединения в **подключения** столбца; поэтому подписка с более низкой скоростью доставки, чтобы отобразить лучше рейтинг производительности чем другая подписка, если первая была синхронизирована с более медленным соединением.  
  
 Рейтинг производительности может иметь одно из следующих значений.  
  
-   Высокая  
  
-   Хорошая.  
  
-   удовлетворительная  
  
-   Низкая  
  
 Дополнительные сведения о определении оценки производительности и установке пороговых значений производительности см. в разделе [мониторинг производительности с помощью монитора репликации](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md).  
  
 **Скорость доставки**  
 Число строк в секунду, обрабатываемых агентом слияния.  
  
 **Последняя синхронизация**  
 Время последнего запуска агента слияния. В течение данной синхронизации изменения могут обрабатываться. Если синхронизация выполняется, то на экране отображается процент выполнения.  
  
 **Длительность**  
 Время работы агента слияния в течение последней синхронизации. При работе агента слияния на экране отображается истекшее время работы, а также общее время работы в течение предыдущих синхронизаций.  
  
 **Соединение**  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] и более поздних версий. Тип соединения между подписчиком и издателем. Возможные значения: **Локальная сеть**, **Удаленный доступ**и **Интернет**. Значение **Интернет** отображается, если подписка использует веб-синхронизацию.  
  
## См. также:  
 [Запуск монитора репликации](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [Просмотр сведений и выполнение задач для подписки и #40; Монитор репликации & #41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-subscription-replication-monitor.md)   
 [Просмотр сведений и выполнение задач для агентов, связанных с подпиской и #40; Монитор репликации & #41;](../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md)   
 [Наблюдение за репликацией](../../relational-databases/replication/monitor/monitoring-replication-overview.md)   
 [Веб-синхронизация для репликации слиянием](../../relational-databases/replication/web-synchronization-for-merge-replication.md)  
  
  