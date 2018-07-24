---
title: Просмотр и изменение параметров командной строки агента репликации (среда SQL Server Management Studio) | Документация Майкрософт
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
- agents [SQL Server replication], command prompt parameters
ms.assetid: 45f2e781-c21d-4b44-8992-89f60fb3d022
caps.latest.revision: 19
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a3282ba855984dcf8a9880616ef9c582de7475a2
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2018
ms.locfileid: "37283520"
---
# <a name="view-and-modify-replication-agent-command-prompt-parameters-sql-server-management-studio"></a>Просмотр и изменение параметров командной строки агента репликации (среда SQL Server Management Studio)
  Агенты репликации — это исполняемые файлы, принимающие параметры командной строки. По умолчанию агенты выполняются в рамках шагов заданий агента [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], поэтому эти параметры можно просматривать и изменять с помощью диалогового окна **Свойства задания — \<задание>**. Доступ к этому диалоговому окну можно получить из папки **Задания** в среде [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] и на вкладке **Агенты** монитора репликации. Сведения о запуске монитора репликации см. в [этой статье](../monitor/start-the-replication-monitor.md).  
  
> [!NOTE]  
>  Изменения параметров агента вступают в действие при следующем запуске агента. Если агент выполняется в непрерывном режиме, следует остановить и перезапустить агент.  
  
 Хотя параметры можно изменять непосредственно, чаще всего их изменяют через профиль агента. Дополнительные сведения см. в разделе [Replication Agent Profiles](replication-agent-profiles.md).  
  
 При доступе к заданиям агента из папки **Задания** для определения имени задания и параметров, доступных для каждого агента, воспользуйтесь следующей таблицей.  
  
|Агент|Имя задания|Для просмотра списка параметров см...|  
|-----------|--------------|------------------------------------|  
|агент моментальных снимков|**\<Издатель>-\<база данных публикации>-\<публикация>-\<целое число>**|[Replication Snapshot Agent](replication-snapshot-agent.md)|  
|Агент моментальных снимков для секции публикации слиянием|**Dyn_\<Издатель>-\<база данных публикации>-\<публикация>-\<идентификатор GUID>**|[Replication Snapshot Agent](replication-snapshot-agent.md)|  
|Агент чтения журнала.|**\<Издатель>-\<база данных публикации>-\<целое число>**|[Агент чтения журнала репликации](replication-log-reader-agent.md)|  
|Агент слияния для подписок по запросу|**\<Издатель>-\<база данных публикации>-\<публикация>-\<подписчик>-\<база данных подписки>-\<целое число>**|[Replication Merge Agent](replication-merge-agent.md)|  
|Агент слияния для принудительных подписок|**\<Издатель>-\<база данных публикации>-\<публикация>-\<подписчик>-\<целое число>**|[Replication Merge Agent](replication-merge-agent.md)|  
|Агент распространителя для принудительных подписок|**\<Издатель>-\<база_данных_публикации>-\<публикация>-\<подписчик>-\<целое_число>** <sup>1</sup>|[Replication Distribution Agent](replication-distribution-agent.md)|  
|Агент распространителя для подписок по запросу|**\<Издатель>-\<база_данных_публикации>-\<публикация>-\<подписчик>-\<база_данных_подписки>-\<идентификатор_GUID>** <sup>2</sup>|[Replication Distribution Agent](replication-distribution-agent.md)|  
|Агент распространителя для принудительных подписок подписчиков серверов, отличных от подписчиков SQL Server|**\<Издатель>-\<база_данных_публикации>-\<публикация>-\<подписчик>-\<целое_число>**|[Replication Distribution Agent](replication-distribution-agent.md)|  
|Агент чтения очереди.|**[\<Распространитель>].\<целое_число>**|[Replication Queue Reader Agent](replication-queue-reader-agent.md)|  
  
 <sup>1</sup> Для принудительных подписок на публикации Oracle значение должно иметь вид **\<Издатель>-\<Издатель**>, а не **\<Издатель>-\<БД_публикации>**  
  
 <sup>2</sup> Для подписок по запросу на публикации Oracle значение должно иметь вид **\<Издатель>-\<БД_распространения**>, а не **\<Издатель>-\<БД_публикации>**  
  
### <a name="to-view-and-modify-replication-agent-command-line-parameters-from-management-studio"></a>Просмотр и изменение параметров командной строки агента репликации из среды Management Studio  
  
1.  Подключитесь к соответствующему компьютеру в [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)], а затем раскройте узел сервера:  
  
    -   В случае использования агента распространителя и агента слияния для подписок по запросу подключитесь к подписчику.  
  
    -   Для всех иных агентов подключитесь к распространителю.  
  
2.  Раскройте папку **Агент SQL Server** , а затем — папку **Задания** .  
  
3.  Правой кнопкой мыши щелкните задание и выберите **Свойства**.  
  
4.  На странице **Шаги** диалогового окна **Свойства задания — \<задание>** выберите действие **Запустить агент**, а затем нажмите кнопку **Изменить**.  
  
5.  В диалоговом окне **Свойства шага задания — запустить агент** отредактировать поле **Команда** .  
  
6.  Нажмите кнопку **OK** в обоих диалоговых окнах.  
  
### <a name="to-view-and-modify-distribution-agent-and-merge-agent-command-line-parameters-from-replication-monitor"></a>Просмотр и изменение параметров командной строки агента распространителя и агента слияния из монитора репликации  
  
1.  На левой панели монитора репликации раскройте группу издателей, раскройте нужный издатель, а затем выберите публикацию.  
  
2.  Перейдите на вкладку **Все подписки** .  
  
3.  Щелкните правой кнопкой мыши подписку, а затем выберите **Просмотреть сведения**.  
  
4.  В **подписки \< SubscriptionName >** окно, нажмите кнопку **действие**, а затем нажмите кнопку  **\<Имя_агента > Свойства задания**.  
  
5.  На странице **Шаги** диалогового окна **Свойства задания — \<задание>** выберите действие **Запустить агент**, а затем нажмите кнопку **Изменить**.  
  
6.  В диалоговом окне **Свойства шага задания — запустить агент** отредактировать поле **Команда** .  
  
7.  Нажмите кнопку **OK** в обоих диалоговых окнах.  
  
### <a name="to-view-and-modify-snapshot-agent-log-reader-agent-and-queue-reader-agent-command-line-parameters-from-replication-monitor"></a>Просмотр и изменение параметров командной строки агента моментальных снимков, агента чтения журнала и агента чтения очереди из монитора репликации  
  
1.  На левой панели монитора репликации раскройте группу издателей, раскройте нужный издатель, а затем выберите публикацию.  
  
2.  Перейдите на вкладку **Агенты** .  
  
3.  Щелкните правой кнопкой мыши агент в сетке, а затем щелкните **Свойства**.  
  
4.  На странице **Шаги** диалогового окна **Свойства задания — \<задание>** выберите действие **Запустить агент**, а затем нажмите кнопку **Изменить**.  
  
5.  В диалоговом окне **Свойства шага задания — запустить агент** отредактировать поле **Команда** .  
  
6.  Нажмите кнопку **OK** в обоих диалоговых окнах.  
  
## <a name="see-also"></a>См. также  
 [Администрирование агента репликации](replication-agent-administration.md)   
 [Основные понятия исполняемых файлов агента репликации](../concepts/replication-agent-executables-concepts.md)   
 [Replication Agents Overview](replication-agents-overview.md)  
  
  