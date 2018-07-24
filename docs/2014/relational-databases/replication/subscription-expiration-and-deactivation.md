---
title: Окончание срока действия и отключение подписки | Документация Майкрософт
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Distributors [SQL Server replication], distribution retention period
- subscriptions [SQL Server replication], expiration
- publications [SQL Server replication], publication retention periods
- expiration [SQL Server replication]
- retention periods [SQL Server replication]
- publication retention periods
- distribution retention period
- subscriptions [SQL Server replication], deactivation
- deactivating subscriptions
ms.assetid: 4d03f5ab-e721-4f56-aebc-60f6a56c1e07
caps.latest.revision: 44
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f8ffb9785ae609d72e49fed4c91e7c983bbff35d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2018
ms.locfileid: "37227204"
---
# <a name="subscription-expiration-and-deactivation"></a>Окончание срока действия и отключение подписки
  Подписки могут быть деактивированы или могут закончиться сроки их действия, если они не будут синхронизированы в течение определенного *срока хранения*. Выполняемое действие зависит от типа репликации и от превышенного срока хранения.  
  
 Чтобы задать сроки хранения, выполните действия из статей [Установка срока действия подписок](publish/set-the-expiration-period-for-subscriptions.md), [Настройка срока хранения распространения для публикаций транзакций (SQL Server Management Studio)](set-distribution-retention-period-for-transactional-publications.md) и [Настройки публикации и распространения](configure-publishing-and-distribution.md).  
  
## <a name="transactional-replication"></a>репликация транзакций  
 Репликация транзакций использует значения максимального срока хранения распространения (параметр **@max_distretention** процедуры [sp_adddistributiondb &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql)) и срока хранения публикаций (параметр **@retention** процедуры [sp_addpublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql)):  
  
-   Если подписка не синхронизирована в пределах максимального срока хранения распространения (по умолчанию 72 часа) и в базе данных распространителя есть изменения, которые не были доставлены подписчику, то подписка будет помечена как деактивированная заданием **Очистка распространения** , выполняемым на распространителе. Эта подписка должна быть инициализирована повторно.  
  
-   Если подписка не будет синхронизирована в пределах срока хранения публикации (по умолчанию 336 часов), то срок действия подписки истечет и она будет удалена заданием **Очистка истекшей подписки** , выполняемым на издателе. Эта подписка должна быть вновь создана и синхронизирована.  
  
     Если истекает срок действия принудительной подписки, она полностью удаляется, а подписки по запросу не удаляются. Подписки по запросу должны удаляться на подписчике. Дополнительные сведения см. в статье [Delete a Pull Subscription](delete-a-pull-subscription.md).  
  
## <a name="merge-replication"></a>Репликация слиянием  
 Репликация слиянием использует срок хранения публикации (параметры **@retention** и **@retention_period_unit** процедуры [sp_addmergepublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql)). Когда срок действия подписки истекает, ее необходимо повторно инициализировать, потому что метаданные для этой подписки удаляются. Не инициализированные повторно подписки удаляются заданием **Очистка истекшей подписки** , выполняемым на издателе. По умолчанию это задание запускается ежедневно; оно удаляет все принудительные подписки, которые не синхронизированы для удвоения срока хранения публикации. Например:  
  
-   Допустим, срок хранения публикации равен 14 дням, тогда действие подписки может истечь, если она не будет синхронизирована в течение 14 дней.  
  
     Если на издателе выполняется [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] или более поздняя версия, и агент подписки входит в состав [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] или более поздней версии, тогда действие подписки истечет, только если будут внесены изменения в данные секции этой подписки. Например, предположим, что подписчик получает пользовательские данные только для клиентов в Германии. Если срок хранения задан равным 14 дням, срок действия подписки истечет на 14-й день, только если за последние 14 дней не вносились изменения в данные немецких клиентов.  
  
-   В интервале от 14 до 27 дней после последней синхронизации подписка может быть инициализирована повторно.  
  
-   Через 28 дней после последней синхронизации подписка удаляется заданием **Очистка истекшей подписки** . Если истекает срок действия принудительной подписки, она полностью удаляется, а подписки по запросу не удаляются. Подписки по запросу должны удаляться на подписчике. Дополнительные сведения см. в статье [Delete a Pull Subscription](delete-a-pull-subscription.md).  
  
### <a name="considerations-for-setting-the-publication-retention-period-for-merge-publications"></a>Вопросы установки срока хранения публикации слиянием  
 При установке срока хранения для публикаций слиянием учитывайте следующие факторы:  
  
-   Срок хранения для публикаций слиянием содержит 24-часовой льготный период для размещения подписчиков в разных часовых поясах. Например, если установить срок хранения продолжительностью в один день, то действительный срок хранения будет равен 48 часам.  
  
-   Очистка метаданных репликации слиянием зависит от срока хранения публикации:  
  
    -   Репликации не удастся очистить метаданные в базах данных публикации и подписки, пока не закончится срок хранения. Будьте осмотрительны при указании больших значений срока хранения, так как они могут негативно сказываться на производительности репликации. Рекомендуется использовать небольшие значения, если можно надежно предсказать, что все подписчики будут синхронизироваться регулярно в течение указанного периода времени.  
  
    -   Можно указать бесконечный срок действия подписок (значение «0» параметра **@retention**), однако настоятельно рекомендуется не использовать это значение, потому что в этом случае метаданные невозможно будет очистить.  
  
-   Срок хранения, устанавливаемый для любого переиздающего подписчика, не должен превышать срок хранения, заданный для исходного издателя. Для всех издателей и их альтернативных участников синхронизации также следует использовать одинаковые значения срока хранения публикаций. Использование разных значений может привести к несогласованности данных. Если необходимо изменить значение срока хранения публикации, выполните повторную инициализацию подписчика, чтобы избежать несогласованности данных.  
  
-   Если после очистки срок хранения публикации увеличен и выполняется попытка объединения подписки с издателем (на котором уже удалены метаданные), срок действия подписки не истечет, поскольку было увеличено значение срока хранения. Однако издатель не имеет достаточно метаданных для загрузки изменений на подписчик, что ведет к несогласованности данных.  
  
## <a name="see-also"></a>См. также  
 [Повторная инициализация подписок](reinitialize-subscriptions.md)   
 [Администрирование агента репликации](agents/replication-agent-administration.md)   
 [Подписка на публикации](subscribe-to-publications.md)  
  
  