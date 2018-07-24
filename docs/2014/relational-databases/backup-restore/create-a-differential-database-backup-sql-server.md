---
title: Создание разностной резервной копии базы данных (SQL Server) | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: backup-restore
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- full differential backups [SQL Server]
- database backups [SQL Server], full differential backups
- backing up databases [SQL Server], full differential backups
- backups [SQL Server], creating
ms.assetid: 70f49794-b217-4519-9f2a-76ed61fa9f99
caps.latest.revision: 32
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 595470b98b16cf955d2456891dac2284a94508c9
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2018
ms.locfileid: "37160935"
---
# <a name="create-a-differential-database-backup-sql-server"></a>Создание разностной резервной копии базы данных (SQL Server)
  В этом разделе описано, как создать разностную резервную копию базы данных в [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] с помощью среды [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] или [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **В этом разделе**  
  
-   **Перед началом работы**  
  
     [Ограничения](#Restrictions)  
  
     [Предварительные требования](#Prerequisites)  
  
     [Рекомендации](#Recommendations)  
  
     [безопасность](#Security)  
  
-   **Создание разностной резервной копии**  
  
     [Среда SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Перед началом  
  
###  <a name="Restrictions"></a> Ограничения  
  
-   Инструкция BACKUP не разрешена в явных и неявных транзакциях.  
  
###  <a name="Prerequisites"></a> Предварительные требования  
  
-   Для создания разностной резервной копии базы данных необходимо наличие ранее созданной полной резервной копии. Если для выбранной базы данных резервное копирование еще не производилось, то перед созданием разностной резервной копии выполните полное резервное копирование. Дополнительные сведения см. в разделе [Создание полной резервной копии базы данных (SQL Server)](create-a-full-database-backup-sql-server.md).  
  
###  <a name="Recommendations"></a> Рекомендации  
  
-   Поскольку разностные резервные копии увеличиваются в размере, восстановление разностной резервной копии может значительно увеличить время, которое необходимо для восстановления базы данных. Поэтому рекомендуется через некоторое время выполнить создание новой полной резервной копии, чтобы получить новую базовую копию для разностного копирования. Например, можно выполнять полное резервное копирование всей базы данных один раз в неделю, а затем в течение недели регулярно создавать разностные резервные копии.  
  
###  <a name="Security"></a> безопасность  
  
####  <a name="Permissions"></a> Permissions  
 Разрешения BACKUP DATABASE и BACKUP LOG назначены по умолчанию членам предопределенной роли сервера **sysadmin** и предопределенным ролям базы данных **db_owner** и **db_backupoperator** .  
  
 Проблемы, связанные с владельцем и разрешениями у физических файлов на устройстве резервного копирования, могут помешать операции резервного копирования. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] должен иметь возможность считывать и записывать данные на устройстве; учетная запись, от имени которой выполняется служба [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , должна иметь разрешения на запись. Однако процедура [sp_addumpdevice](/sql/relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql), добавляющая запись для устройства резервного копирования в системные таблицы, не проверяет разрешения на доступ к файлу. Проблемы физического файла устройства резервного копирования могут не проявляться до момента доступа к физическому ресурсу во время операции резервного копирования или восстановления.  
  
##  <a name="SSMSProcedure"></a> Использование среды SQL Server Management Studio  
  
#### <a name="to-create-a-differential-database-backup"></a>Создание разностной резервной копии  
  
1.  После соединения с соответствующим экземпляром компонента [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]в обозревателе объектов разверните дерево сервера, щелкнув его имя.  
  
2.  Раскройте узел **Базы данных**и в зависимости от типа восстанавливаемой базы данных выберите пользовательскую базу данных или раскройте узел **Системные базы данных** и выберите системную базу данных.  
  
3.  Щелкните правой кнопкой мыши базу данных, выберите пункт **Задачи**, а затем команду **Создать резервную копию**. Откроется диалоговое окно **Резервное копирование базы данных** .  
  
4.  В списке **База данных** проверьте имя базы данных. При необходимости можно выбрать другую базу данных из списка.  
  
     Разностное резервное копирование можно выполнить для любой модели восстановления (полная, с неполным протоколированием или простая).  
  
5.  В списке **Тип резервной копии** выберите **Разностная**.  
  
    > [!IMPORTANT]  
    >  При **разностные** — флажок установлен, убедитесь, что **резервная копия только для копирования** флажок установлен.  
  
6.  В разделе **Компонент резервного копирования**выберите **База данных**.  
  
7.  Оставьте имя резервного набора данных, предложенное по умолчанию в текстовом поле **Имя** , или введите другое имя резервного набора данных.  
  
8.  При необходимости можно ввести описание резервного набора данных в текстовом поле **Описание** .  
  
9. Укажите, когда истекает срок действия резервного набора данных.  
  
    -   Чтобы задать срок действия резервного набора данных, выберите пункт **После** (параметр по умолчанию) и введите срок действия набора в днях с момента его создания. Это значение может быть задано в диапазоне от 0 до 99 999 дней. Значение 0 означает, что срок действия резервного набора данных не ограничен.  
  
         Значение по умолчанию задается в параметре **Срок хранения носителей резервных копий по умолчанию (дней):** диалогового окна **Свойства сервера** (страница**Параметры базы данных** ). Чтобы получить доступ к этому параметру, щелкните правой кнопкой мыши имя сервера в обозревателе объектов и выберите пункт "Свойства", а затем выберите страницу **Настройки базы данных** .  
  
    -   Чтобы указать дату истечения срока действия резервного набора данных, выберите пункт **На**и введите дату истечения срока действия резервного набора данных.  
  
10. Чтобы выбрать тип назначения резервной копии, выберите пункт **Диск** или **Лента**. Чтобы выбрать путь к 64 (или менее) дискам или накопителям на магнитной ленте, содержащим один набор носителей, нажмите кнопку **Добавить**. Выбранные пути отображаются в списке **Создать резервную копию в** .  
  
     Чтобы удалить носитель резервной копии, выберите его и нажмите кнопку **Удалить**. Чтобы просмотреть содержимое носителя резервной копии, выберите его и щелкните **Содержимое**.  
  
11. Чтобы просмотреть или выбрать дополнительные параметры, нажмите кнопку **Параметры** на панели **Выбор страницы** .  
  
12. Выберите параметр **Переписать носитель** , указав один из следующих вариантов:  
  
    -   **Создать резервную копию в существующем наборе носителей**  
  
         Для этого параметра выберите вариант **Добавить в существующий резервный набор данных** или **Перезаписать все существующие резервные наборы данных**. При необходимости установите флажок **Проверить имя набора носителей и срок действия резервного набора данных** и, при необходимости, введите имя в текстовое поле **Имя набора носителей** . Если имя не указано, создается набор носителей с пустым именем. Если указать имя набора носителей, носитель (ленточный или дисковый) проверяется на совпадение введенного и существующего имени.  
  
         Если оставить имя носителя пустым и установить рядом с ним флажок для проверки, имя носителя при успешном завершении также станет пустым.  
  
    -   **Создать резервную копию в новом наборе носителей и удалить все существующие резервные наборы данных**  
  
         Для этого параметра введите имя в текстовом поле **Имя нового набора носителей** и при необходимости введите описание набора носителей в текстовое поле **Описание нового набора носителей** .  
  
13. В разделе **Надежность** можно установить следующие флажки.  
  
    -   **Проверить резервную копию после завершения**.  
  
    -   **Рассчитать контрольную сумму перед записью на носитель**и, при необходимости, **Продолжить при ошибке контрольной суммы**. Дополнительные сведения о контрольных суммах см. в разделе [Возможные ошибки носителей во время резервного копирования и восстановления (SQL Server)](possible-media-errors-during-backup-and-restore-sql-server.md).  
  
14. При резервном копировании на накопитель на магнитной ленте (как указано в разделе **Назначение** страницы **Общие** ) активен параметр **Выгрузить ленту после резервного копирования** . Щелкните этот параметр, чтобы активировать параметр **Перемотать ленту перед выгрузкой** .  
  
    > [!NOTE]  
    >  Параметры в разделе **Журнал транзакций** доступны, только если создается резервная копия журнала транзакций (это можно указать в разделе **Тип резервной копии** вкладки **Общие** ).  
  
15. [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] и более поздние версии поддерживают [сжатие резервных копий](backup-compression-sql-server.md). По умолчанию сжатие резервных копий зависит от значения параметра конфигурации сервера **backup-compression default** . Однако независимо от текущего значения по умолчанию на уровне сервера можно сжать резервные копии, установив параметр **Сжимать резервные копии**, или отказаться от сжатия резервных копий, установив параметр **Не сжимать резервные копии**.  
  
     **Просмотр текущих значений параметров по умолчанию для сжатия резервных копий**  
  
    -   [Параметр конфигурации сервера «Просмотр или настройка параметра сжатия резервных копий по умолчанию»](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)  
  
    > [!NOTE]  
    >  Для создания разностных резервных копий баз данных можно также воспользоваться мастером планов обслуживания базы данных.  
  
##  <a name="TsqlProcedure"></a> Использование Transact-SQL  
  
#### <a name="to-create-a-differential-database-backup"></a>Создание разностной резервной копии  
  
1.  Выполните инструкцию BACKUP DATABASE для создания разностной резервной копии базы данных, указав следующее:  
  
    -   имя базы данных для создания резервной копии;  
  
    -   устройство резервного копирования, на которое записывается полная резервная копия базы данных.  
  
    -   предложение DIFFERENTIAL. Оно обозначает, что копируются только части базы данных, измененные с момента последнего полного резервного копирования базы данных.  
  
     Необходимый синтаксис выглядит следующим образом:  
  
     BACKUP DATABASE *имя_базы_данных* TO <устройство_резервного_копирования> WITH DIFFERENTIAL  
  
###  <a name="TsqlExample"></a> Примеры (Transact-SQL)  
 В этом примере показано создание полной и разностной резервной копии базы данных `MyAdvWorks` .  
  
```tsql  
-- Create a full database backup first.  
BACKUP DATABASE MyAdvWorks   
   TO MyAdvWorks_1   
   WITH INIT;  
GO  
-- Time elapses.  
-- Create a differential database backup, appending the backup  
-- to the backup device containing the full database backup.  
BACKUP DATABASE MyAdvWorks  
   TO MyAdvWorks_1  
   WITH DIFFERENTIAL;  
GO  
```  
  
## <a name="see-also"></a>См. также  
 [Разностные резервные копии (SQL Server)](differential-backups-sql-server.md)   
 [Создание полной резервной копии базы данных (SQL Server)](create-a-full-database-backup-sql-server.md)   
 [Создание резервных копий файлов и файловых групп (SQL Server)](back-up-files-and-filegroups-sql-server.md)   
 [Восстановление разностной резервной копии базы данных (SQL Server)](restore-a-differential-database-backup-sql-server.md)   
 [Восстановление резервной копии журнала транзакций (SQL Server)](restore-a-transaction-log-backup-sql-server.md)   
 [Планы обслуживания](../maintenance-plans/maintenance-plans.md)   
 [Полные резервные копии файлов (SQL Server)](full-file-backups-sql-server.md)  
  
  