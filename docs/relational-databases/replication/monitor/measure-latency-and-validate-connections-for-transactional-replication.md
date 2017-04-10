---
title: "Измерение задержки и проверка правильности соединений для репликации транзакций | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "монитор репликации, производительность"
  - "трассировочные токены [репликация SQL Server]"
  - "задержка [репликация SQL Server]"
  - "репликация транзакций, трассировочные маркеры"
  - "мониторинг производительности [репликация SQL Server], трассировочные маркеры"
ms.assetid: 4addd426-7523-4067-8d7d-ca6bae4c9e34
caps.latest.revision: 36
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 36
---
# Измерение задержки и проверка правильности соединений для репликации транзакций
  В данном разделе описывается измерение задержки и проверка соединений для репликации транзакций в [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] с помощью монитора репликации, [!INCLUDE[tsql](../../../includes/tsql-md.md)] или объектов RMO. Репликация транзакций предоставляет функцию трассировочных токенов, которая обеспечивает удобный способ измерения длительности задержки в топологиях репликации транзакций и помогает проверять соединения между издателем, распространителем и подписчиками. Токен (небольшой объем данных) записывается в журнал транзакций базы данных публикации и помечается так, как если бы он был обычной реплицируемой транзакцией, а затем проходит по системе, позволяя вычислить следующие характеристики:  
  
-   Время, прошедшее между фиксацией транзакции на издателе и вставкой соответствующей команды в базу данных распространителя на распространителе.  
  
-   Время, прошедшее между вставкой команды в базу данных распространителя и соответствующей транзакцией, зафиксированной у подписчика.  
  
 Из этих вычислений можно получить ответы на следующие вопросы:  
  
-   Какой подписчик позднее всех получает изменения от издателя?  
  
-   Какие подписчики, ожидающие получение трассировочного токена, его не получили (если таковые имеются)?  
  
 **В этом разделе**  
  
-   **Перед началом работы выполните следующие действия.**  
  
     [Ограничения](#Restrictions)  
  
-   **Для измерения задержки и проверки соединений используется:**  
  
     [Монитор репликации SQL Server](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Объекты RMO](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> Перед началом  
  
###  <a name="Restrictions"></a> Ограничения  
 Трассировочные токены также могут быть полезны при «замораживании» системы, когда останавливаются все действия и проверяется получение всеми узлами всех необработанных изменений. Дополнительные сведения см. в разделе [замораживание топологии репликации & #40; Программирование репликации Transact-SQL & #41;](../../../relational-databases/replication/administration/quiesce-a-replication-topology-replication-transact-sql-programming.md).  
  
 Для применения трассировочных токенов необходимо пользоваться определенными версиями [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]:  
  
-   Распространитель должен быть версии [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] или более поздней.  
  
-   Издатель должен быть [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] или более поздней версии, либо издателем Oracle.  
  
-   Для принудительных подписок статистика по трассировочным токенам собирается с издателя, распространителя и подписчиков, если это подписчик [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 7.0 или более поздней версии.  
  
-   Для подписок по запросу статистика по трассировочным токенам собирается с подписчиков, только если это подписчик [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] или более поздней версии. Если это подписчик [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 7.0 или [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)], то статистика собирается только с издателя и распространителя.  
  
 Следует также учитывать ряд других вопросов и ограничений:  
  
-   Подписки должны быть активными, чтобы получать трассировочный токен. Подписка является активной, если она инициализирована.  
  
-   При повторной инициализации удаляются все отложенные трассировочные токены для соответствующих подписок.  
  
-   Подписчики получают только трассировочные токены, созданные после их исходной синхронизации.  
  
-   Трассировочные токены не пересылаются переиздающими подписчиками.  
  
-   После отработки отказа на вторичной реплике монитор репликации не сможет изменить имя экземпляра публикации [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] и будет продолжать отображать сведения о репликации по имени исходного первичного экземпляра [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. После отработки отказа нельзя ввести трассировочный токен с помощью монитора репликации, но трассировочный токен, введенный в новый издатель с помощью [!INCLUDE[tsql](../../../includes/tsql-md.md)], отображается в мониторе репликации.  
  
##  <a name="SSMSProcedure"></a> При помощи монитора репликации SQL Server  
 Сведения о запуске монитора репликации см. в разделе [запустить монитор репликации](../../../relational-databases/replication/monitor/start-the-replication-monitor.md).  
  
#### Вставка трассировочного токена и просмотр сведений о токене  
  
1.  Раскройте на левой панели группу издателей, раскройте издатель и выберите нужную публикацию.  
  
2.  Щелкните вкладку **Трассировочные токены** .  
  
3.  Выберите команду **Вставить трассировочный маркер**.  
  
4.  Просмотрите затраченное время для трассировочного маркера в следующих столбцах: **От издателя к распространителю**, **От распространителя к подписчику**, **Общая задержка**. Значение **Ожидание** указывает на то, что токен еще не достиг указанной точки.  
  
#### Просмотр сведений о трассировочном токене, вставленном ранее  
  
1.  Раскройте на левой панели группу издателей, раскройте издатель и выберите нужную публикацию.  
  
2.  Щелкните вкладку **Трассировочные токены** .  
  
3.  Выберите время **время вставки** раскрывающегося списка.  
  
4.  Просмотрите затраченное время для трассировочного маркера в следующих столбцах: **От издателя к распространителю**, **От распространителя к подписчику**, **Общая задержка**. Значение **Ожидание** указывает на то, что токен еще не достиг указанной точки.  
  
    > [!NOTE]  
    >  Данные трассировочных токенов хранятся в течение того же периода времени, что и другие данные предыстории; этот период определяется сроком хранения журнала в базе данных распространителя. Сведения об изменении свойства базы данных распространителя см. в разделе [представления и свойств издателя и распространителя изменить](../../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md).  
  
##  <a name="TsqlProcedure"></a> Использование Transact-SQL  
  
#### Отправка трассировочного токена в публикацию транзакций  
  
1.  (Необязательно) На издателе в базе данных публикации выполните хранимую процедуру [sp_helppublication & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md). Удостоверьтесь в том, что публикация существует и находится в активном состоянии.  
  
2.  (Необязательно) На издателе в базе данных публикации выполните хранимую процедуру [sp_helpsubscription & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md). Удостоверьтесь в том, что подписка существует и находится в активном состоянии.  
  
3.  На издателе в базе данных публикации выполните хранимую процедуру [sp_posttracertoken & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-posttracertoken-transact-sql.md), указав **@publication**. Обратите внимание на значение **@tracer_token_id** выходной параметр.  
  
#### Измерение задержки и проверка соединений для публикации транзакций  
  
1.  Передайте трассировочный токен в публикацию при помощи описанной выше процедуры.  
  
2.  На издателе в базе данных публикации выполните хранимую процедуру [sp_helptracertokens & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-helptracertokens-transact-sql.md), указав **@publication**. Будет возвращен список всех трассировочных токенов, опубликованных для публикации. Запомните нужное **tracer_id** в результирующем наборе.  
  
3.  На издателе в базе данных публикации выполните хранимую процедуру [sp_helptracertokenhistory & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-helptracertokenhistory-transact-sql.md), указав **@publication** и идентификатор трассировочного токена из шага 2 для **@tracer_id**. В результате этого будут возвращены сведения о задержке для выделенного трассировочного токена.  
  
#### Удаление трассировочных токенов  
  
1.  На издателе в базе данных публикации выполните хранимую процедуру [sp_helptracertokens & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-helptracertokens-transact-sql.md), указав **@publication**. Будет возвращен список всех трассировочных токенов, опубликованных для публикации. Примечание **tracer_id** трассировочный маркер для удаления в результате значение.  
  
2.  На издателе в базе данных публикации выполните хранимую процедуру [sp_deletetracertokenhistory & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-deletetracertokenhistory-transact-sql.md), указав **@publication** и идентификатор трассировочного маркера, полученного на шаге 2 для **@tracer_id**.  
  
###  <a name="TsqlExample"></a> Пример (Transact-SQL)  
 В этом примере продемонстрирована отправка трассировочного токена, и просмотр сведений о задержке по возвращенному идентификатору отправленного трассировочного токена.  
  
 [!code-sql[HowTo#sp_tracertokens](../../../relational-databases/replication/codesnippet/tsql/measure-latency-and-vali_1.sql)]  
  
##  <a name="RMOProcedure"></a> При помощи объектов RMO  
  
#### Отправка трассировочного токена в публикацию транзакций  
  
1.  Создайте соединение с издателем с помощью <xref:Microsoft.SqlServer.Management.Common.ServerConnection> класса.  
  
2.  Создайте экземпляр <xref:Microsoft.SqlServer.Replication.TransPublication> класса.  
  
3.  Задайте <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> и <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> Свойства для публикации, а также набор <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> Свойства подключения, созданной на шаге 1.  
  
4.  Вызов <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> метод, чтобы получить свойства объекта. Если этот метод возвращает **false**, то либо на шаге 3 были неверно определены свойства публикации, либо публикация не существует.  
  
5.  Вызов <xref:Microsoft.SqlServer.Replication.TransPublication.PostTracerToken%2A> метод. Этот метод обеспечивает вставку трассировочного токена в журнал транзакций публикации.  
  
#### Измерение задержки и проверка соединений для публикации транзакций  
  
1.  Создайте соединение с распространителем с помощью <xref:Microsoft.SqlServer.Management.Common.ServerConnection> класса.  
  
2.  Создайте экземпляр <xref:Microsoft.SqlServer.Replication.PublicationMonitor> класса.  
  
3.  Задайте <xref:Microsoft.SqlServer.Replication.PublicationMonitor.Name%2A>, <xref:Microsoft.SqlServer.Replication.PublicationMonitor.DistributionDBName%2A>, <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublisherName%2A>, и <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublicationDBName%2A> а в качестве <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> Свойства подключения, созданной на шаге 1.  
  
4.  Вызов <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> метод, чтобы получить свойства объекта. Если этот метод возвращает **false**, то либо на шаге 3 были неверно определены свойства монитора публикации, либо публикация не существует.  
  
5.  Вызов <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumTracerTokens%2A> метод. Приведите возвращенный <xref:System.Collections.ArrayList> объект в массив <xref:Microsoft.SqlServer.Replication.TracerToken> объектов.  
  
6.  Вызов <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumTracerTokenHistory%2A> метод. Передайте значение <xref:Microsoft.SqlServer.Replication.TracerToken.TracerTokenId%2A> для трассировочного токена на шаге 5. Возвращает сведения о задержке для выделенного трассировочного токена в виде <xref:System.Data.DataSet> объекта. Если возвращены все сведения о трассировочном токене, то существует соединение между издателем и распространителем, а также соединение между распространителем и подписчиком, и топология репликации работоспособна.  
  
#### Удаление трассировочных токенов  
  
1.  Создайте соединение с распространителем с помощью <xref:Microsoft.SqlServer.Management.Common.ServerConnection> класса.  
  
2.  Создайте экземпляр <xref:Microsoft.SqlServer.Replication.PublicationMonitor> класса.  
  
3.  Задайте <xref:Microsoft.SqlServer.Replication.PublicationMonitor.Name%2A>, <xref:Microsoft.SqlServer.Replication.PublicationMonitor.DistributionDBName%2A>, <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublisherName%2A>, и <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublicationDBName%2A> а в качестве <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> Свойства подключения, созданной на шаге 1.  
  
4.  Вызов <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> метод, чтобы получить свойства объекта. Если этот метод возвращает **false**, то либо на шаге 3 были неверно определены свойства монитора публикации, либо публикация не существует.  
  
5.  Вызов <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumTracerTokens%2A> метод. Приведите возвращенный <xref:System.Collections.ArrayList> объект в массив <xref:Microsoft.SqlServer.Replication.TracerToken> объектов.  
  
6.  Вызов <xref:Microsoft.SqlServer.Replication.PublicationMonitor.CleanUpTracerTokenHistory%2A> метод. Передайте одно из следующих значений.  
  
    -    <xref:Microsoft.SqlServer.Replication.TracerToken.TracerTokenId%2A> для трассировочного токена на шаге 5. В результате этого сведения для выделенного токена будут удалены.  
  
    -   A <xref:System.DateTime> объекта. В результате этого будут удалены сведения обо всех токенах, созданных до наступления указанного момента времени.  
  
  