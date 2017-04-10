---
title: "Резервные копии заключительного фрагмента журнала (SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "08/01/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-backup-restore"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "резервное копирование [SQL Server], заключительный фрагмент журнала"
  - "резервные копии журналов [SQL Server], резервные копии заключительного фрагмента журнала"
  - "NO_TRUNCATE, предложение"
  - "резервные копии [SQL Server], резервные копии журналов"
  - "резервные копии заключительного фрагмента журнала"
  - "резервные копии [SQL Server], резервные копии заключительного фрагмента журнала"
ms.assetid: 313ddaf6-ec54-4a81-a104-7ffa9533ca58
caps.latest.revision: 55
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 55
---
# Резервные копии заключительного фрагмента журнала (SQL Server)
  В данном разделе рассматриваются вопросы резервного копирования и восстановления только тех баз данных [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], которые используют модель полного восстановления или модель восстановления с неполным протоколированием.  
  
 В *резервную копию заключительного фрагмента журнала* попадают все записи, резервная копия которых еще не была создана (*заключительный фрагмент журнала*), что позволяет предотвратить потерю работы и сохранить неповрежденную цепочку журналов. Для восстановления базы данных [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] на последний момент времени необходимо предварительно выполнить резервное копирование заключительного фрагмента журнала ее транзакций. Заключительный фрагмент журнала является становится последней рассматриваемой частью резервной копии в плане восстановления базы данных.  
  
> **ПРИМЕЧАНИЕ.** Не для всех сценариев восстановления требуется резервная копия заключительного фрагмента журнала. Резервная копия заключительного фрагмента журнала не нужна, если точка восстановления содержится в более ранней резервной копии журнала. Кроме того, резервная копия заключительного фрагмента журнала не требуется при перемещении или замещении (перезаписи) базы данных, при котором не нужно восстанавливать ее на определенный момент времени после создания ее последней резервной копии.  
  
   ##  <a name="TailLogScenarios"></a> Сценарии, в которых требуется резервная копия заключительного фрагмента журнала.  
 Рекомендуется формировать резервную копию заключительного фрагмента журнала в следующих сценариях.  
  
-   Если база данных находится в режиме «в сети» и следующим действием над базой данных должна быть операция восстановления, то прежде необходимо выполнить резервное копирование заключительного фрагмента журнала. Во избежание ошибок для оперативной базы данных необходимо использовать параметр WITH NORECOVERY инструкции [BACKUP](../../t-sql/statements/backup-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   Если база данных, работающая в режиме «вне в сети», не запускается и необходимо восстановить базу данных, то в первую очередь необходимо выполнить резервное копирование заключительного фрагмента журнала. Так как в это время никакие транзакции не выполняются, параметр WITH NORECOVERY использовать не обязательно.  
  
-   Если база данных повреждена, попытайтесь получить резервную копию заключительного фрагмента журнала, используя параметр WITH CONTINUE_AFTER_ERROR инструкции BACKUP.  
  
     Резервное копирование заключительного фрагмента журнала поврежденной базы данных может быть успешно выполнено только в том случае, если файлы журнала не повреждены, а база данных находится в режиме, который поддерживает резервное копирование заключительного фрагмента журнала, и не содержит какие-либо изменения с неполным протоколированием. Если резервная копия заключительного фрагмента журнала не может быть создана, то любые транзакции, зафиксированные после создания последней резервной копии журнала, будут потеряны.  
  
 В следующей таблице представлена сводка параметров BACKUP NORECOVERY и CONTINUE_AFTER_ERROR.  
  
|Параметр BACKUP LOG|Комментарии|  
|-----------------------|--------------|  
|NORECOVERY|Если планируется продолжить операцию восстановления базы данных, используйте параметр NORECOVERY. NORECOVERY переводит базу данных в состояние восстановления. Это гарантирует, что после создания резервной копии заключительного фрагмента журнала база данных не изменится. Если параметры NO_TRUNCATE или COPY_ONLY не заданы, журнал усекается.<br /><br /> **\*\* Важно! \*\***Рекомендуется использовать параметр NO_TRUNCATE исключительно в том случае, если база данных повреждена.|  
|CONTINUE_AFTER_ERROR|Параметр CONTINUE_AFTER_ERROR следует указывать только в том случае, если создается резервная копия заключительного фрагмента журнала поврежденной базы данных.<br /><br /> При резервном копировании заключительного фрагмента журнала поврежденной базы данных, некоторые метаданные, захватываемые обычно в резервные копии журналов, могут быть недоступны. Дополнительные сведения см. в подразделе [Резервное копирование заключительного фрагмента журнала с неполными метаданными резервной копии](#IncompleteMetadata) этого раздела.|  
  
##  <a name="IncompleteMetadata"></a> Резервное копирование заключительного фрагмента журнала с неполными метаданными резервной копии  
 Резервное копирование заключительного фрагмента журнала захватывает конец журнала даже в тех случаях, когда база данных работает вне сети, повреждена или в ней не хватает файлов данных. В результате этого метаданные команд восстановления данных и базы данных **msdb**могут быть неполными. Однако несмотря на неполноту метаданных, захваченный журнал будет полным и готовым к использованию.  
  
 Если резервная копия заключительного фрагмента журнала содержит неполные метаданные, то параметр **has_incomplete_metadata** в таблице [backupset](../../relational-databases/system-tables/backupset-transact-sql.md) принимает значение **1**. Кроме того, выходной аргумент [HasIncompleteMetadata](../Topic/RESTORE%20HEADERONLY%20\(Transact-SQL\).md)инструкции **RESTORE HEADERONLY** принимает значение **1**.  
  
 Если метаданные в резервной копии заключительного фрагмента журнала неполные, то в таблице [backupfilegroup](../../relational-databases/system-tables/backupfilegroup-transact-sql.md) большая часть сведений о файловых группах того времени в резервной копии заключительного фрагмента журнала будет утеряна. Большинство столбцов таблицы **backupfilegroup** содержит значение NULL, другие значения имеют следующие столбцы:  
  
-   **backup_set_id**  
  
-   **filegroup_id**  
  
-   **type**  
  
-   **type_desc**  
  
-   **is_readonly**  
  
##  <a name="RelatedTasks"></a> Связанные задачи  
 Инструкции по созданию резервной копии журнала транзакций см. в разделе [Резервное копирование журнала транзакций при повреждении базы данных (SQL Server)](../../relational-databases/backup-restore/back-up-the-transaction-log-when-the-database-is-damaged-sql-server.md).  
  
 Инструкции по восстановлению резервной копии журнала транзакций см. в разделе [Восстановление резервной копии журнала транзакций (SQL Server)](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md).  
    
## См. также:  
 [BACKUP (Transact-SQL)](../../t-sql/statements/backup-transact-sql.md)   
 [RESTORE (Transact-SQL)](../Topic/RESTORE%20\(Transact-SQL\).md)   
 [Резервное копирование и восстановление баз данных SQL Server](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [Резервные копии только для копирования (SQL Server)](../../relational-databases/backup-restore/copy-only-backups-sql-server.md)   
 [Резервные копии журналов транзакций (SQL Server)](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md)   
 [Применение резервных копий журналов транзакций (SQL Server)](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)  
  
  