---
title: "Приложение sqllogship | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "sqllogship"
ms.assetid: 8ae70041-f3d9-46e4-8fa8-31088572a9f8
caps.latest.revision: 10
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 10
---
# Приложение sqllogship
  Приложение **sqllogship** выполняет операции резервного копирования, обычного копирования и восстановления, а также связанные с ними задачи очистки для конфигурации доставки журналов. Операция выполняется на определенном экземпляре [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] для определенной базы данных.  
  
 ![Значок ссылки на раздел](../database-engine/configure-windows/media/topic-link.png "Значок ссылки на раздел") Соглашения о синтаксисе см. в [Справочнике по программе командной строки (Database Engine)](../tools/command-prompt-utility-reference-database-engine.md).  
  
## Синтаксис  
  
```  
  
sqllogship -server instance_name { -backup primary_id | -copy secondary_id | -restore secondary_id } [ –verboselevel level ] [ –logintimeout timeout_value ] [ -querytimeout timeout_value ]  
```  
  
## Аргументы  
 **-server** *имя_экземляра*  
 Указывает экземпляр [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], где будет выполняться операция. Указываемый экземпляр сервера зависит от того, на каком сервере задается операция доставки журналов. Для операции **-backup** в качестве аргумента *имя_сервера* должно быть указано имя сервера-источника, заданное в конфигурации доставки журналов. Для операции **-copy** или **-restore** в качестве аргумента *имя_сервера* указывается имя сервера-получателя, заданное в конфигурации доставки журналов.  
  
 **-backup** *primary_id*  
 Выполняет операцию резервного копирования для базы данных-источника, основной идентификатор которой определяется аргументом *primary_id*. Этот идентификатор можно получить из системной таблицы [log_shipping_primary_databases](../relational-databases/system-tables/log-shipping-primary-databases-transact-sql.md) или хранимой процедурой [sp_help_log_shipping_primary_database](../relational-databases/system-stored-procedures/sp-help-log-shipping-primary-database-transact-sql.md).  
  
 Операция резервного копирования создает резервную копию журналов в каталоге резервного копирования. Затем приложение **sqllogship** удаляет все старые файлы резервной копии на основе срока их хранения. Приложение записывает журнал для операции резервного копирования на сервер-источник и сервер мониторинга. Наконец, оно запускает хранимую процедуру [sp_cleanup_log_shipping_history](../relational-databases/system-stored-procedures/sp-cleanup-log-shipping-history-transact-sql.md), которая удаляет старые данные в журнале на основе срока их хранения.  
  
 **-copy** *secondary_id*  
 Выполняет операцию копирования резервных копий с указанного сервера-получателя для базы данных-получателя или баз данных со вторичным идентификатором, указываемым аргументом *secondary_id*. Этот идентификатор можно получить из системной таблицы [log_shipping_secondary](../relational-databases/system-tables/log-shipping-secondary-transact-sql.md) или хранимой процедурой [sp_help_log_shipping_secondary_database](../relational-databases/system-stored-procedures/sp-help-log-shipping-secondary-database-transact-sql.md).  
  
 Операция выполняет копирование файлов резервной копии из каталога резервного копирования в целевой каталог. Затем приложение **sqllogship** записывает журнал для операции копирования на сервер-получатель и сервер мониторинга.  
  
 **-restore** *secondary_id*  
 Выполняет операцию восстановления на указанный сервер-получатель для базы данных-получателя или баз данных со вспомогательным идентификатором, указываемым аргументом *secondary_id*. Этот идентификатор можно получить хранимой процедурой **sp_help_log_shipping_secondary_database**.  
  
 Все файлы резервной копии в целевом каталоге, созданные после самой последней точки восстановления, восстанавливаются в базы данных-получатели. Затем приложение **sqllogship** удаляет все старые файлы резервной копии на основе срока их хранения. Приложение записывает журнал для операции восстановления на сервер-получатель и сервер мониторинга. Наконец, оно запускает хранимую процедуру **sp_cleanup_log_shipping_history**, которая удаляет старые данные в журнале на основе срока их хранения.  
  
 **–verboselevel** *level*  
 Определяет уровень сообщений, добавляемых в журнал доставки журналов. *level* может быть одним из следующих целочисленных значений:  
  
|Level|Описание|  
|-----------|-----------------|  
|0|Не выводить сообщения трассировки и отладки.|  
|1|Выводить сообщения обработки ошибок.|  
|2|Выводить предупреждения и сообщения обработки ошибок.|  
|**3**|Выводить информационные сообщения, предупреждения и сообщения обработки ошибок. Это значение по умолчанию.|  
|4|Выводить все сообщения отладки и трассировки.|  
  
 **–logintimeout** *timeout_value*  
 Определяет период времени, достаточного для попытки подключения к экземпляру сервера. Значение по умолчанию составляет 15 секунд. *timeout_value* — **int***.*  
  
 **-querytimeout** *timeout_value*  
 Определяет период времени, достаточного для запуска определенной операции. Значение по умолчанию — до бесконечности. *timeout_value* — **int***.*  
  
## Замечания  
 Рекомендуется по возможности применять для выполнения резервирования, копирования и восстановления соответствующие задания. Их запуск производится через вызов хранимой процедуры [sp_start_job](../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md).  
  
 Журнал доставки журналов, созданный программой **sqllogship**, смешивается с журналом, создаваемым заданиями доставки журналов. При частом использовании программы **sqllogship** в конфигурациях доставки журналов стоит рассмотреть отключение заданий доставки журналов. Дополнительные сведения см. в статье [Disable or Enable a Job](../ssms/agent/disable-or-enable-a-job.md).  
  
 Приложение **sqllogship** устанавливается в каталог x:\Program Files\Microsoft SQL Server\130\Tools\Binn.  
  
## Разрешения  
 **sqllogship** использует проверку подлинности Windows. Учетной записи Windows, от которой выполняется команда, необходимы доступ к каталогу Windows и разрешения [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Это требование зависит от того, какой параметр задается командой **sqllogship**: **-backup**, **-copy** или **-restore**.  
  
|Параметр|Доступ к каталогу|Разрешения|  
|------------|----------------------|-----------------|  
|**-backup**|Требует доступа по чтению и записи в каталог резервной копии.|Необходимы те же разрешения, что и для инструкции BACKUP. Дополнительные сведения см. в разделе [BACKUP (Transact-SQL)](../t-sql/statements/backup-transact-sql.md).|  
|**-copy**|Требует доступа на чтение к каталогу резервной копии и доступа на запись в каталог копии.|Требует таких же разрешений, что и хранимая процедура [sp_help_log_shipping_secondary_database](../relational-databases/system-stored-procedures/sp-help-log-shipping-secondary-database-transact-sql.md).|  
|**-restore**|Требует доступа на чтение-запись в каталог копирования.|Требует тех же разрешений, что и инструкция RESTORE. Дополнительные сведения см. в разделе [RESTORE (Transact-SQL)](../Topic/RESTORE%20\(Transact-SQL\).md).|  
  
> [!NOTE]  
>  Чтобы выяснить пути к каталогам резервной копии и копии, необходимо запустить хранимую процедуру **sp_help_log_shipping_secondary_database** или просмотреть таблицу **log_shipping_secondary** в базе данных **msdb**. Пути к каталогам резервной копии и назначения находятся в столбцах **backup_source_directory** и **backup_destination_directory** соответственно.  
  
## См. также:  
 [Сведения о доставке журналов (SQL Server)](../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [log_shipping_primary_databases (Transact-SQL)](../relational-databases/system-tables/log-shipping-primary-databases-transact-sql.md)   
 [log_shipping_secondary (Transact-SQL)](../relational-databases/system-tables/log-shipping-secondary-transact-sql.md)   
 [sp_cleanup_log_shipping_history (Transact-SQL)](../relational-databases/system-stored-procedures/sp-cleanup-log-shipping-history-transact-sql.md)   
 [sp_help_log_shipping_primary_database (Transact-SQL)](../relational-databases/system-stored-procedures/sp-help-log-shipping-primary-database-transact-sql.md)   
 [sp_help_log_shipping_secondary_database (Transact-SQL)](../relational-databases/system-stored-procedures/sp-help-log-shipping-secondary-database-transact-sql.md)   
 [sp_start_job (Transact-SQL)](../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md)  
  
  