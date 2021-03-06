---
title: Использование предупреждений для событий агента репликации | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
helpviewer_keywords:
- viewing alerts
- Queue Reader Agent, alerts
- alerts [SQL Server replication]
- predefined replication alerts [SQL Server replication]
- Log Reader Agent, alerts
- Distribution Agent, alerts
- Merge Agent, alerts
- agents [SQL Server replication], alerts
- displaying alerts
- Snapshot Agent, alerts
ms.assetid: 8c42e523-7020-471d-8977-a0bd044b9471
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 60976006bb9c26a6b3bae613ddfa96f52113dced
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/02/2018
ms.locfileid: "48129443"
---
# <a name="use-alerts-for-replication-agent-events"></a>Используйте предупреждения для событий агента репликации
  Среда[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] и агент [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] предоставляют способ наблюдения за событиями (например, событиями агента репликации) с использованием предупреждений. Агент[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] отслеживает в журнале приложений Windows события, связанные с предупреждениями. При наступлении события агент [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] автоматически реагирует на него, выполняя определенную пользователем задачу или отправляя сообщения на электронную почту или на пейджер указанного оператора. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] содержит набор стандартных предупреждений для агентов репликации, которые можно настроить для выполнения задачи или уведомления оператора. Дополнительные сведения об определении выполняемых задач см. в подразделе «Автоматизация отклика на предупреждение» этого раздела.  
  
 При настройке компьютера в качестве распространителя производится установка следующих предупреждений.  
  
|Идентификатор сообщения|Стандартное предупреждение|Условие, вызывающее предупреждение|Наличие дополнительных сведений в msdb..sysreplicationalerts|  
|----------------|----------------------|-----------------------------------------|-----------------------------------------------------------------|  
|14150|**Репликация: успех агента**|Успешное завершение работы агента.|Да|  
|14151|**Репликация: неудача агента**|Работа агента завершена с ошибкой.|Да|  
|14152|**Репликация: повторная попытка агента**|Агент завершает работу после неудачной повторной попытки выполнения операции (агент обнаружил ошибку: например, сервер недоступен, взаимоблокировка, сбой подключения, ошибка времени ожидания).|Да|  
|14157|**Репликация: истекшая подписка удалена**|Подписка с истекшим сроком удалена.|Нет|  
|20572|**Репликация: подписка повторно инициализирована после ошибки проверки достоверности**|Повторная инициализация подписки с помощью ответного задания «Повторная инициализация подписки при ошибке проверки данных» выполнена успешно.|Нет|  
|20574|**Репликация: ошибка проверки данных подписчиком**|Ошибка проверки данных агентом распространителя или агентом слияния.|Да|  
|20575|**Репликация: прошла проверку данных подписчиком**|Проверка данных агентом распространителя или агентом слияния проведена успешно.|Да|  
|20578|**Репликация: нестандартное завершение работы агента**|||  
|22815|**Предупреждение об обнаружении конфликта в одноранговой топологии**|Агент распространителя обнаружил конфликт при попытке применения изменений на одноранговом узле.|Да|  
  
 Наряду с этими предупреждениями монитор репликации предоставляет набор предупреждений и оповещений, относящихся к состоянию и производительности. Дополнительные сведения см. в разделе [настройка пороговых значений и предупреждений в мониторе репликации](../monitor/set-thresholds-and-warnings-in-replication-monitor.md) инфраструктуры предупреждений. Дополнительные сведения см. в статье [Создание пользовательского события](../../../ssms/agent/create-a-user-defined-event.md).  
  
 **Настройка стандартных предупреждений репликации**  
  
-   [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]: [Настройка стандартных предупреждений репликации (среда SQL Server Management Studio)](../administration/configure-predefined-replication-alerts-sql-server-management-studio.md)  
  
## <a name="viewing-the-application-log-directly"></a>Непосредственный просмотр журнала приложений  
 Для просмотра журнала приложений Windows используйте средство просмотра событий [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows. Журнал приложений содержит сообщения об ошибках [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , а также сообщения о многих других действиях на компьютере. В отличие от журнала ошибок [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , новый журнал приложений не создается при каждом запуске [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (в каждом сеансе [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] новые события записываются в существующий журнал приложений), однако можно указать время хранения записанных в журнал событий. При просмотре журнала приложений Windows можно отфильтровать журнал для поиска определенных событий. Дополнительные сведения см. в документации по Windows.  
  
## <a name="automating-a-response-to-an-alert"></a>Автоматизация отклика на предупреждения  
 Репликация обеспечивает выполнение ответного задания для подписок, которые не прошли проверку данных, а также предоставляет платформу для создания дополнительных автоматизированных ответов на предупреждения. Ответное задание называется **Повторная инициализация подписок при ошибке проверки** и хранится в папке [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Задания **агента** в среде [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]. Дополнительные сведения о включении этого ответного задания см. в статье [Настройка стандартных предупреждений репликации (среда SQL Server Management Studio)](../administration/configure-predefined-replication-alerts-sql-server-management-studio.md). Если статьи в публикации транзакций не проходят проверку, ответное задание проводит повторную инициализацию только тех статей, которые не прошли проверку. Если статьи в публикации слиянием не проходят проверку, ответное задание повторно инициализирует все статьи публикации.  
  
### <a name="framework-for-automating-responses"></a>Платформа для автоматизации ответов  
 Обычно при возникновении предупреждения информация, позволяющая понять причину появления предупреждения и предпринять необходимые действия, содержится исключительно в самом предупреждающем сообщении. Анализ этой информации подвержен ошибкам и занимает немало времени. Репликация облегчает автоматическое реагирование, предоставляя дополнительную информацию о предупреждении в системной таблице **sysreplicationalerts** ; эта информация уже представлена в форме, которая может быть легко использована пользовательскими программами.  
  
 Например, если данные в таблице **Sales.SalesOrderHeader** у подписчика «A» не прошли проверку, то [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] может выдать сообщение 20574, извещающее об этой ошибке. Выводится следующее сообщение: «Ошибка проверки данных подписки подписчика A на статью SalesOrderHeader в публикации MyPublication».  
  
 Если ответ создается на основе этого сообщения, необходимо вручную выделить из сообщения имя подписчика, имя статьи, имя публикации и ошибку. Однако поскольку агент распространителя и агент слияния записывают ту же информацию в таблицу **sysreplicationalerts** (вместе с подробными сведениями, такими как тип агента, время вывода предупреждения, база данных публикации, база данных подписчика и тип публикации), ответное задание может запросить соответствующую информацию непосредственно из таблицы. Хотя конкретную строку нельзя связать с определенным экземпляром предупреждения, в таблице имеется столбец **status** , который можно использовать для отслеживания тех записей, которые были обработаны. Записи этой таблицы сохраняются в течение срока хранения журнала.  
  
 Например, если бы нужно было создать в [!INCLUDE[tsql](../../../includes/tsql-md.md)] ответное задание на предупреждение 20574, можно было бы использовать следующую логику:  
  
```  
declare @publisher sysname, @publisher_db sysname, @publication sysname, @publication_type int, @article sysname, @subscriber sysname, @subscriber_db sysname, @alert_id int  
declare hc cursor local for select publisher, publisher_db, publication, publication_type, article, subscriber,   
  subscriber_db, alert_id from   
  msdb..sysreplicationalerts where  
  alert_error_code = 20574 and status = 0  
  for read only  
open hc  
fetch hc into  @publisher, @publisher_db, @publication, @publication_type, @article, @subscriber, @subscriber_db, @alert_id  
while (@@fetch_status <> -1)  
begin  
/* Do custom work  */  
/* Update status to 1, which means the alert has been serviced. This prevents subsequent runs of this job from doing this again */  
update msdb..sysreplicationalerts set status = 1 where alert_id = @alert_id  
 fetch hc into  @publisher, @publisher_db, @publication, @publication_type, @article, @subscriber, @subscriber_db, @alert_id  
end  
close hc  
deallocate hc  
```  
  
## <a name="see-also"></a>См. также  
 [Администрирование агента репликации](replication-agent-administration.md)   
 [Best Practices for Replication Administration](../administration/best-practices-for-replication-administration.md)   
 [Наблюдение за репликацией](../monitoring-replication.md)  
  
  
