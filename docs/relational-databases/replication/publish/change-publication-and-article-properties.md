---
title: "Изменение свойств публикации и статьи | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "изменений свойств статьи"
  - "изменение свойств публикации"
  - "управление репликацией, свойства"
  - "публикации [репликация SQL Server], изменение свойств"
  - "статьи [репликация SQL Server], свойства"
ms.assetid: f7df51ef-c088-4efc-b247-f91fb2c6ff32
caps.latest.revision: 20
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 20
---
# Изменение свойств публикации и статьи
  После того как публикация создана, большинство свойств публикаций и статей можно изменить, но для некоторых изменений требуется, повторное создание моментального снимка и/или повторная инициализация подписок. В этом разделе содержатся сведения обо всех свойствах, требуемых для одного или обоих этих действий (если они изменяются).  
  
## Свойства публикации для репликации моментальных снимков и репликации транзакций.  
  
|Описание|Хранимая процедура|Свойства|Требования|  
|-----------------|----------------------|----------------|------------------|  
|Изменение формата моментального снимка.|**sp_changepublication**|**sync_method**|Создание моментального снимка.|  
|Изменение расположения моментального снимка.|**sp_changepublication**|**alt_snapshot_folder**<br /><br /> **snapshot_in_defaultfolder**|Создание моментального снимка.|  
|Изменение расположения моментального снимка.|**sp_changedistpublisher, хранимая процедура**|**working_directory**|Создание моментального снимка.|  
|Изменение сжатия моментального снимка.|**sp_changepublication**|**compress_snapshot**|Создание моментального снимка.|  
|Изменение параметров FTP-протокола для моментального снимка.|**sp_changepublication**|**enabled_for_internet**<br /><br /> **ftp_address**<br /><br /> **ftp_login**<br /><br /> **ftp_password**<br /><br /> **ftp_port**<br /><br /> **ftp_subdirectory**|Создание моментального снимка.|  
|Изменение расположения скрипта, запускаемого перед моментальным снимком или после него.|**sp_changepublication**|**pre_snapshot_script**<br /><br /> **post_snapshot_script**|Создание моментального снимка (требуется также при изменении содержимого скрипта).<br /><br /> Для применения нового скрипта к подписчику требуется повторная инициализация.|  
|Включить или отключить поддержку отличных[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] подписчиков.|**sp_changepublication**|**is_enabled_for_het_sub**|Создание моментального снимка.|  
|Изменение отчета о конфликтах подписок, обновляемых посредством очередей|**sp_changepublication**|**centralized_conflicts**|Может быть изменена только при отсутствии активных подписок.|  
|Изменение политики разрешения конфликтов для подписок, обновляемых посредством очередей|**sp_changepublication**|**conflict_policy**|Может быть изменена только при отсутствии активных подписок.|  
  
## Свойства статьи для репликации моментальных снимков и репликации транзакций.  
  
|Описание|Хранимая процедура|Свойства|Требования|  
|-----------------|----------------------|----------------|------------------|  
|Удаление статьи|**sp_droparticle**|Все параметры.|Статьи могут быть удалены до создания подписок. С помощью хранимых процедур можно удалить подписку на статью. При использовании [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]вся подписка должна быть удалена, создана повторно и синхронизирована. Дополнительные сведения см. в разделе [Добавление и удаление статей в существующих публикациях](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md).|  
|Изменение фильтра столбцов.|**sp_articlecolumn**|**@column**<br /><br /> **@operation**|Создание моментального снимка.<br /><br /> Повторная инициализация подписок.|  
|Добавление фильтра строк.|**sp_articlefilter**|Все параметры.|Создание моментального снимка.<br /><br /> Повторная инициализация подписок.|  
|Удаление фильтра строк.|**sp_articlefilter**|**@article**|Создание моментального снимка.<br /><br /> Повторная инициализация подписок.|  
|Изменение фильтра строк.|**sp_articlefilter**|**@filter_clause**|Создание моментального снимка.<br /><br /> Повторная инициализация подписок.|  
|Изменение фильтра строк.|**sp_changearticle**|**фильтр**|Создание моментального снимка.<br /><br /> Повторная инициализация подписок.|  
|Изменение параметров схемы.|**sp_changearticle**|**schema_option**|Создание моментального снимка.|  
|Изменение порядка обработки таблиц на подписчике до применения моментального снимка.|**sp_changearticle**|**pre_creation_cmd**|Создание моментального снимка.|  
|Изменение состояния статьи|**sp_changearticle**|**status**|Создание моментального снимка.|  
|Изменение команды INSERT, UPDATE или DELETE.|**sp_changearticle**|**ins_cmd**<br /><br /> **upd_cmd**<br /><br /> **del_cmd**|Создание моментального снимка.<br /><br /> Повторная инициализация подписок.|  
|Изменение имени целевой таблицы|**sp_changearticle**|**dest_table**|Создание моментального снимка.<br /><br /> Повторная инициализация подписок.|  
|Изменение владельца (схемы) целевой таблицы.|**sp_changearticle**|**destination_owner**|Создание моментального снимка.<br /><br /> Повторная инициализация подписок.|  
|Изменение сопоставление типов данных (применимо только к публикации Oracle).|**sp_changearticlecolumndatatype**|**@type**<br /><br /> **@length**<br /><br /> **@точность**<br /><br /> **@scale**|Создание моментального снимка.<br /><br /> Повторная инициализация подписок.|  
  
## Свойства публикации для репликации слиянием  
  
|Описание|Хранимая процедура|Свойства|Требования|  
|-----------------|----------------------|----------------|------------------|  
|Изменение формата моментального снимка|**sp_changemergepublication**|**sync_mode**|Создание моментального снимка.|  
|Изменение расположения моментального снимка.|**sp_changemergepublication**|**alt_snapshot_folder**<br /><br /> **snapshot_in_defaultfolder**|Создание моментального снимка.|  
|Изменение расположения моментального снимка.|**sp_changedistpublisher, хранимая процедура**|**working_directory**|Создание моментального снимка.|  
|Изменение сжатия моментального снимка|**sp_changemergepublication**|**compress_snapshot**|Создание моментального снимка.|  
|Изменение любых параметров протокола FTP для моментального снимка|**sp_changemergepublication**|**enabled_for_internet**<br /><br /> **ftp_address**<br /><br /> **ftp_login**<br /><br /> **ftp_password**<br /><br /> **ftp_port**<br /><br /> **ftp_subdirectory**|Создание моментального снимка.|  
|Изменение скриптов, запускаемых перед моментальным снимком или после него.|**sp_changemergepublication**|**pre_snapshot_script**<br /><br /> **post_snapshot_script**|Создание моментального снимка (требуется также при изменении содержимого скрипта).<br /><br /> Для применения нового скрипта к подписчику требуется повторная инициализация.|  
|Добавление фильтра соединения или логической записи.|**sp_addmergefilter**|Все параметры.|Создание моментального снимка.<br /><br /> Повторная инициализация подписок.|  
|Удаление фильтра соединения или логической записи.|**sp_dropmergefilter**|Все параметры.|Создание моментального снимка.<br /><br /> Повторная инициализация подписок.|  
|Изменение фильтра соединения или логической записи.|**sp_changemergefilter**|**@property**<br /><br /> **@value**|Создание моментального снимка.<br /><br /> Повторная инициализация подписок.|  
|Отключение использования параметризованных фильтров (включение параметризованных фильтров не требует никаких специальных действий).|**sp_changemergepublication**|Значение **false** для **dynamic_filters**|Создание моментального снимка.<br /><br /> Повторная инициализация подписок.|  
|Включение или выключение использования предварительно вычисляемых секций.|**sp_changemergepublication**|**use_partition_groups**|Создание моментального снимка.|  
|Включение или отключение [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] оптимизации секций.|**sp_changemergepublication**|**keep_partition_changes**|Повторная инициализация подписок.|  
|Включение или выключение проверки секций подписчика.|**sp_changemergepublication**|**validate_subscriber_info**|Повторная инициализация подписок.|  
|Изменение уровня совместимости публикации до 80sp3 или ниже.|**sp_changemergepublication**|**publication_compatibility_level**|Создание моментального снимка.|  
  
## Свойства статьи для репликации слиянием  
  
|Описание|Хранимая процедура|Свойства|Требования|  
|-----------------|----------------------|----------------|------------------|  
|Удаление статьи с последним параметризованным фильтром в публикации.|**sp_dropmergearticle**|Все параметры|Создание моментального снимка.<br /><br /> Повторная инициализация подписок.|  
|Удаление статьи, являющейся родителем в фильтре соединения или в логической записи (это побочный эффект удаления соединения).|**sp_dropmergearticle**|Все параметры|Создание моментального снимка.<br /><br /> Повторная инициализация подписок.|  
|Удаление статьи при прочих обстоятельствах.|**sp_dropmergearticle**|Все параметры|Создание моментального снимка.|  
|Включение в состав ранее не опубликованного фильтра столбцов.|**sp_mergearticlecolumn**|**@column**<br /><br /> **@operation**|Создание моментального снимка.<br /><br /> Повторная инициализация подписок.|  
|Добавление, удаление или изменение фильтра строк.|**sp_changemergearticle**|**subset_filterclause**|Создание моментального снимка.<br /><br /> Повторная инициализация подписок.<br /><br /> Если добавить, удалить или изменить параметризованный фильтр, ожидающие обработки изменения подписчика нельзя будет передать издателю во время повторной инициализации. Если нужно передать изменения, ожидающие обработки, то перед изменением фильтра необходимо синхронизировать все подписки.<br /><br /> Если статья не используется ни в каких фильтрах соединения, статью можно удалить и создать ее заново с другим фильтром строк, который не требует повторной инициализации всей подписки. Дополнительные сведения о добавлении и удалении статей см. в разделе [Добавление и удаление статей в существующих публикациях](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md).|  
|Изменение параметров схемы.|**sp_changemergearticle**|**schema_option**|Создание моментального снимка.|  
|Изменение детализации отслеживания изменений от уровня столбцов до уровня строк (обратное изменение не требует дополнительных действий).|**sp_changemergearticle**|Значение **false** для **column_tracking**|Создание моментального снимка.<br /><br /> Повторная инициализация подписок.|  
|Изменение режима, определяющего, будут ли проверяться разрешения до применения на издателе инструкций, созданных на подписчике.|**sp_changemergearticle**|**check_permissions**|Создание моментального снимка.<br /><br /> Повторная инициализация подписок.|  
|Включение или выключение подписок, доступных только для загрузки (изменение других параметров отгрузки не требует каких-либо особых действий).|**sp_changemergearticle**|Изменения в или из значение **2** для **subscriber_upload_options**|Повторная инициализация подписок.|  
|Изменение владельца целевой таблицы.|**sp_changemergearticle**|**destination_owner**|Создание моментального снимка.<br /><br /> Повторная инициализация подписок.|  
  
## См. также:  
 [Администрирование и #40; Репликация & #41;](../../../relational-databases/replication/administration/administration-replication.md)   
 [Создание и применение моментального снимка](../../../relational-databases/replication/create-and-apply-the-snapshot.md)   
 [Повторная инициализация подписок](../../../relational-databases/replication/reinitialize-subscriptions.md)   
 [sp_addmergefilter & #40; Transact-SQL и #41;](../../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md)   
 [sp_articlecolumn & #40; Transact-SQL и #41;](../../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)   
 [sp_articlefilter & #40; Transact-SQL и #41;](../../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md)   
 [sp_changearticle & #40; Transact-SQL и #41;](../../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [sp_changearticlecolumndatatype & #40; Transact-SQL и #41;](../../../relational-databases/system-stored-procedures/sp-changearticlecolumndatatype-transact-sql.md)   
 [sp_changedistpublisher & #40; Transact-SQL и #41;](../../../relational-databases/system-stored-procedures/sp-changedistpublisher-transact-sql.md)   
 [sp_changemergearticle & #40; Transact-SQL и #41;](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)   
 [sp_changemergefilter & #40; Transact-SQL и #41;](../../../relational-databases/system-stored-procedures/sp-changemergefilter-transact-sql.md)   
 [sp_changemergepublication & #40; Transact-SQL и #41;](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)   
 [sp_changepublication & #40; Transact-SQL и #41;](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)   
 [sp_droparticle & #40; Transact-SQL и #41;](../../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)   
 [sp_dropmergearticle & #40; Transact-SQL и #41;](../../../relational-databases/system-stored-procedures/sp-dropmergearticle-transact-sql.md)   
 [sp_dropmergefilter & #40; Transact-SQL и #41;](../../../relational-databases/system-stored-procedures/sp-dropmergefilter-transact-sql.md)   
 [sp_mergearticlecolumn & #40; Transact-SQL и #41;](../../../relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql.md)  
  
  