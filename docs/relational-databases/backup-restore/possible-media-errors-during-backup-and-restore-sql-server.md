---
title: "Возможные ошибки носителей во время резервного копирования и восстановления (SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "03/15/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-backup-restore"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "ошибки носителя [SQL Server]"
  - "CONTINUE_AFTER_ERROR, параметр"
  - "ошибки [SQL Server], резервные копии"
  - "резервные копии [SQL Server], ошибки"
  - "RESTORE VERIFYONLY, инструкция"
  - "резервные носители [SQL Server], управление обработкой ошибок"
  - "контрольные суммы страниц [SQL Server]"
  - "контрольные суммы резервных копий [SQL Server]"
  - "резервное копирование [SQL Server], ошибки носителя"
  - "инструкция RESTORE, ошибки носителя"
  - "NO_CHECKSUM, параметр"
  - "контрольные суммы [SQL Server]"
ms.assetid: 83a27b29-1191-4f8d-9648-6e6be73a9b7c
caps.latest.revision: 37
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 36
---
# Возможные ошибки носителей во время резервного копирования и восстановления (SQL Server)
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] позволяет восстанавливать базу данных, несмотря на обнаруженные ошибки. Новый важный механизм обнаружения ошибок состоит в возможном создании контрольной суммы резервной копии, которую можно создать операцией резервного копирования и проверить операцией восстановления. Можно управлять тем, будет ли операция проверять наличие ошибок и будет ли она останавливаться или продолжаться при обнаружении ошибки. Если резервная копия содержит контрольную сумму, инструкции RESTORE и RESTORE VERIFYONLY могут выполнять проверку на наличие ошибок.  
  
> [!NOTE]  
>  Зеркальные резервные копии могут содержать до четырех копий (зеркал) наборов носителей, предоставляя другие копии для исправления ошибок, вызванных повреждением носителей. Дополнительные сведения см. в разделе [Зеркальные наборы носителей резервных копий (SQL Server)](../../relational-databases/backup-restore/mirrored-backup-media-sets-sql-server.md).  
  
 **В этом разделе.**  
  
-   [Контрольные суммы резервных копий](#BckChecksums)  
  
-   [Реакция на ошибки контрольной суммы страниц при операциях резервного копирования или восстановления](#ResponsetoPageChecksumErrors)  
  
-   [Связанные задачи](#RelatedTasks)  
  
##  <a name="BckChecksums"></a> Контрольные суммы резервных копий  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] поддерживает три типа контрольных сумм: на страницах, в блоках журналов и резервных копиях. При создании контрольной суммы резервной копии инструкция BACKUP проверяет согласованность данных, считанных из базы данных, со всеми контрольными суммами или признаками обрыва страниц в этой базе.  
  
 Инструкция BACKUP может также вычислять контрольную сумму резервной копии для потока резервирования. Если на данной странице есть контрольная сумма или данные о разрыве страниц, то при резервном копировании инструкция BACKUP также проверяет для страницы контрольную сумму, идентификатор и состояние разрыва страницы. При создании контрольной суммы резервной копии операция резервного копирования не добавляет никаких контрольных сумм к страницам. Страницы копируются так, как они существуют в базе данных, они не изменяются операцией резервного копирования.  
  
 Из-за дополнительной нагрузки при проверке и создании контрольных сумм резервных копий их использование может ухудшить производительность. Может пострадать как рабочая нагрузка, так и пропускная способность резервного копирования. Поэтому использование контрольных сумм резервных копий необязательно. При принятии решения о создании контрольных сумм резервных копий необходимо тщательно проконтролировать соответствующую дополнительную загрузку ЦП и влияние на остальную рабочую нагрузку системы.  
  
 Инструкция BACKUP никогда не изменяет исходную страницу на диске и ее содержимое.  
  
 Если контрольные суммы резервных копий включены, операция резервного копирования выполняет следующие шаги:  
  
1.  Перед записью страницы на резервный носитель операция резервного копирования проверяет сведения на уровне страницы (контрольную сумму или обнаружение разрыва страницы), если они имеются. Если они отсутствуют, операция резервного копирования не может проверить страницу. Непроверенные страницы включаются «как есть», а их содержимое добавляется в общую контрольную сумму резервной копии.  
  
     Если во время проверки операция резервного копирования обнаруживает ошибку страницы, резервное копирование прерывается с ошибкой.  
  
    > [!NOTE]  
    >  Дополнительные сведения о контрольной сумме страниц и обнаружении разрывов страниц см. в описании параметра PAGE_VERIFY инструкции ALTER DATABASE. Дополнительные сведения см. в разделе [Параметры ALTER DATABASE SET (Transact-SQL)](../Topic/ALTER%20DATABASE%20SET%20Options%20\(Transact-SQL\).md).  
  
2.  Независимо от того, присутствует ли контрольная сумма страницы или нет, инструкция BACKUP создает отдельные контрольные суммы резервных копий для потока резервных файлов. Дополнительно операции восстановления могут использовать контрольные суммы резервных копий для проверки наличия повреждений в резервных файлах. Контрольная сумма резервной копии хранится на носителе резервных файлов, а не на страницах базы данных. Контрольную сумму резервной копии также можно использовать во время восстановления.  
  
3.  Резервный набор данных помечен как содержащий контрольные суммы резервных копий (в столбце **has_backup_checksums** таблицы **msdb..backupset**). Дополнительные сведения см. в разделе [backupset (Transact-SQL)](../../relational-databases/system-tables/backupset-transact-sql.md).  
  
 Во время операции восстановления, если на резервном носителе имеются контрольные суммы, по умолчанию и инструкция RESTORE, и инструкция RESTORE VERIFYONLY проверяют контрольные суммы резервных копий и страниц. Если у резервной копии нет контрольной суммы, все операции восстановления продолжаются без проверок. Данное поведение объясняется тем, что без контрольной суммы резервной копии операция восстановления не может достоверно проверять контрольные суммы страниц.  
  
## Реакция на ошибки контрольной суммы страниц при операциях резервного копирования или восстановления  
 По умолчанию после обнаружения ошибки контрольной суммы страницы операция BACKUP или RESTORE прерывается, а операция RESTORE VERIFYONLY продолжает работу. Однако вы можете определить, будет ли та или иная операция прерываться при возникновении ошибки или пытаться продолжать работу.  
  
 Если операция BACKUP продолжает работу при возникновении ошибок, она производит следующие действия:  
  
1.  Помечает резервный набор данных на резервном носителе как содержащий ошибки и отслеживает эту страницу в таблице **suspect_pages** в базе данных **msdb**. Дополнительные сведения см. в разделе [suspect_pages (Transact-SQL)](../../relational-databases/system-tables/suspect-pages-transact-sql.md).  
  
2.  Записывает эту ошибку в журнал ошибок SQL Server.  
  
3.  Помечает резервный набор данных как содержащий данный тип ошибок (в столбце **is_damaged** таблицы **msdb.backupset**). Дополнительные сведения см. в разделе [backupset (Transact-SQL)](../../relational-databases/system-tables/backupset-transact-sql.md).  
  
4.  Выдает сообщение о том, что резервная копия успешно создана, но содержит ошибки страниц.  
  
##  <a name="RelatedTasks"></a> Связанные задачи  
 **Включение или отключение контрольных сумм резервных копий**  
  
-   [Включение или отключение вычисления контрольных сумм резервных копий во время резервного копирования или восстановления (SQL Server)](../../relational-databases/backup-restore/enable-or-disable-backup-checksums-during-backup-or-restore-sql-server.md)  
  
 **Управление реакцией на ошибку во время операции резервного копирования**  
  
-   [Определение, продолжает ли операция резервного копирования или восстановления работу после возникновения ошибки (SQL Server)](../../relational-databases/backup-restore/specify if backup or restore continues or stops after error.md)  
  
## См. также:  
 [ALTER DATABASE (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql.md)   
 [BACKUP (Transact-SQL)](../../t-sql/statements/backup-transact-sql.md)   
 [backupset (Transact-SQL)](../../relational-databases/system-tables/backupset-transact-sql.md)   
 [Зеркальные наборы носителей резервных копий (SQL Server)](../../relational-databases/backup-restore/mirrored-backup-media-sets-sql-server.md)   
 [RESTORE (Transact-SQL)](../Topic/RESTORE%20\(Transact-SQL\).md)   
 [RESTORE VERIFYONLY (Transact-SQL)](../Topic/RESTORE%20VERIFYONLY%20\(Transact-SQL\).md)  
  
  