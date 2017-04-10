---
title: "Зеркальное отображение и репликация баз данных (SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "зеркальное отображение базы данных [SQL Server], взаимодействие"
  - "репликация [SQL Server], зеркальное отображение базы данных и"
ms.assetid: 82796217-02e2-4bc5-9ab5-218bae11a2d6
caps.latest.revision: 39
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 39
---
# Зеркальное отображение и репликация баз данных (SQL Server)
  Зеркальное отображение базы данных может использоваться совместно с репликацией для повышения доступности базы данных публикации. В зеркальном отображении базы данных участвуют две копии одной базы данных, которые обычно расположены на разных компьютерах. В любой момент только одна копия базы данных доступна клиентам. Эта копия называется основной базой данных. Обновления, вносимые клиентами в основную базу данных, применяются к другой копии базы данных, называемой зеркальной базой данных. Зеркальное отображение включает применение к зеркальной базе данных журнала транзакций всех вставок, обновлений или удалений, выполненных в основной базе данных.  
  
 Переход репликации на зеркальную базу данных полностью поддерживается для баз данных публикации, с ограниченной поддержкой для баз данных подписки. Зеркальное отображение баз данных не поддерживается для базы данных распространителя. Сведения о восстановлении базы данных распространителя или базы данных подписки без перенастройки репликации см. в статье [Создание резервной копии и восстановление из копий реплицируемых баз данных](../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md). Дополнительные сведения о зеркальном отображении базы данных подписчика см. в разделе  
  
> [!NOTE]  
>  После перехода на зеркальную базу данных в результате отработки отказа основной базы данных зеркальная база данных становится основной. В этом разделе термины «основная» и «зеркальная» всегда относятся к исходной основной и зеркальной базе данных соответственно.  
  
## Требования и дополнительные соображения по использованию репликации с зеркальным отображением базы данных  
 При использовании репликации совместно с зеркальным отображением базы данных помните о следующих требованиях и правилах.  
  
-   Основная и зеркальная базы данных должны совместно использовать распространитель. Рекомендуется, чтобы это был удаленный распространитель, который обеспечивает большую устойчивость к отказам в ситуации, когда на издателе при сбое происходит незапланированная отработка отказа.  
  
-   Репликация поддерживает зеркальное отображение базы данных публикации для репликации слиянием и репликации транзакций с подписчиками, доступными только для чтения, или с подписчиками, обновляемыми посредством очередей. Подписчики с немедленным обновлением, издатели Oracle, издатели в одноранговой топологии, а также переиздание не поддерживаются.  
  
-   Метаданные и объекты, которые существуют за пределами базы данных, не копируются на зеркало. Это касается имен входа, заданий, связанных серверов и так далее. Если в зеркальной базе данных нужны метаданные и объекты, их необходимо скопировать вручную. Дополнительные сведения см. в статье [Управление именами входа и заданиями после переключения ролей (SQL Server)](../../sql-server/failover-clusters/management-of-logins-and-jobs-after-role-switching-sql-server.md).  
  
## Настройка репликации с зеркальным отображением базы данных  
 Настройка репликации и зеркального отображения базы данных состоит из пяти шагов. Каждый шаг описывается в следующем разделе.  
  
1.  Настройка издателя.  
  
2.  Настройка зеркального отображения базы данных.  
  
3.  Настройка зеркала для использования вместе с основной базой данных одного и того же распространителя.  
  
4.  Настройка агентов репликации для перехода на зеркальную базу в случае отработки отказа.  
  
5.  Добавление основной и зеркальной базы данных в монитор репликации.  
  
 Шаги 1 и 2 могут быть выполнены в обратном порядке.  
  
#### Настройка зеркального отображения базы данных для базы данных публикации  
  
1.  Настройте издатель.  
  
    1.  Рекомендуется использовать удаленный распространитель. Дополнительные сведения о настройке распространения см. в статье [Настройка распространения](../../relational-databases/replication/configure-distribution.md).  
  
    2.  Базу данных можно активировать для использования публикаций моментальных снимков, публикаций транзакций или публикаций слиянием. Для зеркальных баз данных, которые будут содержать более одного типа публикаций, базу данных при помощи процедуры [sp_replicationdboption](../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md) следует активировать для обоих типов публикаций на том же узле. Например, можно было бы выполнить следующие вызовы хранимых процедур в основной базе данных:  
  
        ```  
        exec sp_replicationdboption @dbname='<PublicationDatabase>', @optname='publish', @value=true;  
        exec sp_replicationdboption @dbname='<PublicationDatabase>', @optname='mergepublish', @value=true;  
        ```  
  
         Дополнительные сведения о создании публикаций см. в статье [Публикация данных и объектов базы данных](../../relational-databases/replication/publish/publish-data-and-database-objects.md).  
  
2.  Настройка зеркального отображения базы данных. Дополнительные сведения см. в статьях [Создание сеанса зеркального отображения базы данных с использованием проверки подлинности Windows (среда SQL Server Management Studio)](../../database-engine/database-mirroring/establish database mirroring session - windows authentication.md) и [Настройка зеркального отображения базы данных (SQL Server)](../../database-engine/database-mirroring/setting-up-database-mirroring-sql-server.md).  
  
3.  Настройте распространение для зеркальной базы данных. Укажите имя зеркальной базы данных в качестве имени издателя и укажите те же самые распространитель и папку моментальных снимков, которые используются основной базой данных. Например, если проводится настройка репликации с помощью хранимых процедур, выполните [sp_adddistpublisher](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md) на распространителе, а затем [sp_adddistributor](../../relational-databases/system-stored-procedures/sp-adddistributor-transact-sql.md) на зеркальном сервере. Для **sp_adddistpublisher** выполните следующее:  
  
    -   установите значение параметра **@publisher** равным сетевому имени зеркала;  
  
    -   установите значение параметра **@working_directory** равным имени папки моментальных снимков, используемой основной базой данных.  
  
4.  Укажите имя зеркала в параметре агента **–PublisherFailoverPartner** . Этот параметр требуется следующим агентам для определения зеркала после отработки отказа:  
  
    -   агенту моментальных снимков (для всех публикаций);  
  
    -   агенту чтения журнала (для всех публикаций транзакций);  
  
    -   агенту чтения очереди (для публикаций транзакций, которые поддерживают подписки, обновляемые посредством очередей);  
  
    -   агенту слияния (для подписок на публикацию слиянием);  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] прослушивателю репликации (replisapi.dll: для подписок на публикацию слиянием, синхронизируемых с помощью веб-синхронизации);  
  
    -   элементу управления ActiveX слияния SQL (для подписок на публикацию слиянием, синхронизируемых с помощью этого элемента управления).  
  
     Агент распространителя и элемент управления ActiveX распространения не имеют этого параметра, потому что они не подключаются к издателю.  
  
     Изменения параметров агента вступают в действие при следующем запуске агента. Если агент выполняется в непрерывном режиме, следует остановить и перезапустить агент. Параметры могут быть заданы в профилях агента или из командной строки. Дополнительные сведения см. в разделе:  
  
    -   [Просмотр и изменение параметров командной строки агента репликации (среда SQL Server Management Studio)](../../relational-databases/replication/agents/view and modify replication agent command prompt parameters.md)  
  
    -   [Основные понятия исполняемых файлов агента репликации](../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)  
  
     Рекомендуется добавить параметр **–PublisherFailoverPartner** в профиль агента, а затем указать в профиле имя зеркала. Например, если настраивается репликация с помощью хранимых процедур:  
  
    ```  
    -- Execute sp_help_agent_profile in the context of the distribution database to get the list of profiles.  
    -- Select the profile id of the profile that needs to be updated from the result set.  
    -- In the agent_type column returned by sp_help_agent_profile:   
    -- 1 = Snapshot Agent; 2 = Log Reader Agent; 3 = Distribution Agent; 4 = Merge Agent; 9 = Queue Reader Agent.  
  
    exec sp_help_agent_profile;  
  
    -- Setting the -PublisherFailoverPartner parameter in the default Snapshot Agent profile (profile 1).  
    -- Execute sp_add_agent_parameter in the context of the distribution database.  
    exec sp_add_agent_parameter @profile_id = 1, @parameter_name = N'-PublisherFailoverPartner', @parameter_value = N'<Failover Partner Name>';  
  
    -- Setting the -PublisherFailoverPartner parameter in the default Merge Agent profile (profile 6).  
    -- Execute sp_add_agent_parameter in the context of the distribution database.  
    exec sp_add_agent_parameter @profile_id = 6, @parameter_name = N'-PublisherFailoverPartner', @parameter_value = N'<Failover Partner Name>';  
    ```  
  
5.  Добавление основной и зеркальной базы данных в монитор репликации. Дополнительные сведения см. в статье [Добавление и удаление издателей в мониторе репликации](../../relational-databases/replication/monitor/add-and-remove-publishers-from-replication-monitor.md).  
  
## Обслуживание зеркальной базы данных публикации  
 Обслуживание зеркальной базы данных публикации существенно не отличается от обслуживания незеркальной базы данных, со следующими оговорками.  
  
-   Администрирование и наблюдение должны выполняться на активном сервере. В среде [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]в папке **Локальные публикации** находятся публикации только для активного сервера. Например, если в результате отработки отказа выполнен переход на зеркало, публикации будут отображаться на зеркале и больше не будут отображаться в основной базе данных. Если база данных переходит на зеркальный сервер, возможно, понадобится вручную обновить среду [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] и монитор репликации, чтобы в них отображалось произошедшее изменение.  
  
-   Монитор репликации отображает узлы издателя в дереве объектов как для основного, так и для зеркального сервера. Если активным является основной сервер, сведения о публикации отображаются в мониторе репликации только на главном узле.  
  
     Если активным является зеркальный сервер:  
  
    -   если возникла ошибка агента, эта ошибка показывается только в основном узле и не отображается в зеркальном узле;  
  
    -   если основной сервер недоступен, то в основном и зеркальном узлах отображаются идентичные списки публикаций. Наблюдение должно выполняться только для публикаций на зеркальном узле.  
  
-   Если для администрирования репликации на зеркале используются хранимые процедуры или объекты RMO, то для случаев, когда указывается имя издателя, необходимо указать имя экземпляра, на котором база данных активирована для репликации. Чтобы определить соответствующее имя, воспользуйтесь функцией [publishingservername](../Topic/PUBLISHINGSERVERNAME%20\(Transact-SQL\).md).  
  
     Когда база данных публикации зеркально отображается, метаданные репликации, хранимые в зеркальной базе данных, идентичны метаданным, хранимым в основной базе данных. Поэтому для баз данных публикации, активированных для репликации на основном сервере, имя экземпляра издателя, хранимое в системных таблицах на зеркале, является именем основного сервера, а не именем зеркала. Если в результате сбоя база данных публикации переходит на зеркальный сервер, это повлияет на настройку и обслуживание репликации. Например, если после отработки отказа репликация настраивается с помощью хранимых процедур на зеркале и требуется добавить подписку по запросу в базу данных публикации, которая была активирована в основной базе данных, необходимо указать имя основной, а не зеркальной базы данных в параметре **@publisher** хранимой процедуры **sp_addpullsubscription** или **sp_addmergepullsubscription**.  
  
     Если база данных публикации активирована на зеркале после перехода на зеркало в результате отработки отказа, имя экземпляра издателя, хранимое в системных таблицах, должно быть именем зеркала. В этом случае будет использоваться имя зеркала для параметра **@publisher** .  
  
    > [!NOTE]  
    >  В некоторых случаях, например в процедуре **sp_addpublication**, параметр **@publisher** поддерживается только для издателей, не относящихся к [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], и не влияет на зеркальное отображение базы данных [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Для синхронизации подписки в среде [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] после отработки отказа необходимо синхронизировать подписки по запросу от подписчика и синхронизировать принудительные подписки от активного издателя.  
  
### Поведение репликации, когда зеркальное отображение удалено  
 Если зеркальное отображение базы данных удаляется из опубликованной базы данных, необходимо учитывать следующие моменты.  
  
-   Если зеркальное отображение опубликованной базы данных на основном сервере больше не выполняется, репликация продолжает работать без изменений для исходной основной базы данных.  
  
-   Если опубликованная база данных в результате сбоя переключается с основной на зеркальную базу данных и если связи зеркального отображения затем отключаются или удаляются, агенты репликации не будут функционировать в зеркальной базе данных. Если основная база данных бесповоротно утеряна, отключите, а затем перенастройте репликацию с зеркалом, указанным в качестве издателя.  
  
-   Если зеркальное отображение базы данных полностью удаляется, зеркальная база данных находится в состоянии восстановления и должна быть восстановлена, чтобы стать функционирующей. Поведение восстановленной базы данных в отношении репликации зависит от того, задан ли параметр KEEP_REPLICATION. Этот параметр принудительно запускает операцию восстановления, чтобы сохранить настройки репликации при восстановлении опубликованной базы данных на сервер, отличный от того, на котором была создана резервная копия. Используйте параметр KEEP_REPLICATION, только когда недоступна другая база данных публикации. Этот параметр не поддерживается, если другая база данных публикации не повреждена и реплицируется. Дополнительные сведения о параметре KEEP_REPLICATION см. в разделе [RESTORE (Transact-SQL)](../Topic/RESTORE%20\(Transact-SQL\).md).  
  
## Поведение агента чтения журнала  
 В следующей таблице описывается поведение агента чтения журнала для различных режимов зеркального отображения базы данных.  
  
|Режим работы|Поведение агента чтения журнала, когда зеркальная база данных недоступна|  
|--------------------|------------------------------------------------------------|  
|Режим высокого уровня защиты с автоматической отработкой отказа|Если зеркало недоступно, агент чтения журнала передает команды в базу данных распространителя. При отработке отказа основная база данных не сможет переключиться на зеркало, пока зеркальная база данных не вернется в режим «в сети» и не получит все транзакции из основной базы данных.|  
|Высокопроизводительный режим|Если зеркало недоступно, основная база данных выполняется без поддержки (т. е. без зеркальной базы данных). Однако агент чтения журнала реплицирует только те транзакции, которые записаны в зеркальную базу данных. Если служба включена принудительно и зеркальный сервер принимает роль основного, агент чтения журнала начнет работать на зеркале и будет собирать на нем новые транзакции.<br /><br /> Имейте в виду, что задержка репликации увеличится, если зеркальная база данных отстает от основной базы данных в изменениях.|  
|Режим высокой безопасности без автоматической отработки отказа|Гарантируется, что все зафиксированные транзакции будут записаны на диск зеркального сервера. Однако агент чтения журнала реплицирует только те транзакции, которые записаны на зеркале. Если зеркало недоступно, основной сервер запрещает дальнейшую активность в базе данных. Поэтому агент чтения журнала не имеет транзакций для репликации.|  
  
## См. также:  
 [Функции и задачи репликации](../../relational-databases/replication/replication-features-and-tasks.md)   
 [Репликация и доставка журналов (SQL Server)](../../database-engine/log-shipping/log-shipping-and-replication-sql-server.md)  
  
  