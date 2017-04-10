---
title: "Резервное копирование базы данных с оптимизированными для памяти таблицами | Microsoft Docs"
ms.custom: ""
ms.date: "03/20/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine-imoltp"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 83d47694-e56d-4dae-b54e-14945bf8ba31
caps.latest.revision: 18
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 18
---
# Резервное копирование базы данных с оптимизированными для памяти таблицами
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Резервные копии оптимизированных для памяти таблиц создаются в составе обычных резервных копий баз данных. Что же касается таблиц на дисках, то для обнаружения повреждений CHECKSUM пар файлов данных и разностных файлов проверяется в процессе резервного копирования базы данных.  
  
> [!NOTE]  
>  Если во время архивации обнаружится ошибка контрольной суммы одного или нескольких файлов в файловой группе, оптимизированной для памяти, произойдет сбой архивации. В этом случае потребуется восстановить базу данных из последней корректной резервной копии.  
>   
>  Если нет резервной копии, можно проэкспортировать данные из таблиц, оптимизированных для памяти, и таблиц на диске, после чего загрузить их обратно после удаления и повторного создания базы данных.  
  
 Полная резервная копия базы данных с одной или несколькими оптимизированными для памяти таблицами состоит из хранилища, выделенного для таблиц, находящихся на диске (если таковые имеются), активного журнала транзакций и пар файлов данных и разностных файлов (их также называют парами файлов контрольных точек) для оптимизированных для памяти таблиц. Однако, как описано в разделе [Устойчивость таблиц, оптимизированных для памяти](../../relational-databases/in-memory-oltp/durability-for-memory-optimized-tables.md), объем хранилища, используемый оптимизированными для памяти таблицами, может быть значительно больше, чем размер таблиц в памяти. Это оказывает влияние на размер резервной копии базы данных.  
  
## Полная резервная копия базы данных  
 В этом описании основное внимание уделяется архивации баз данных только с устойчивыми, оптимизированными для памяти таблицами, так как архивация таблиц, записанных на диск, ничем не отличается. Пары файлов контрольных точек из оптимизированной для памяти файловой группы могут находиться в различных состояниях. В приведенной далее таблице указано, какая часть файлов добавляется в резервную копию.  
  
|Состояние пары файлов контрольных точек|Резервное копирование|  
|--------------------------------|------------|  
|PRECREATED|Только метаданные файла|  
|UNDER CONSTRUCTION|Только метаданные файла|  
|ACTIVE|Метаданные файла и используемые байты|  
|MERGE TARGET|Только метаданные файла|  
|WAITING FOR LOG TRUNCATION|Метаданные файла и используемые байты|  
  
 Описание состояний пар файлов контрольных точек см. в разделе [sys.dm_db_xtp_checkpoint_files (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-checkpoint-files-transact-sql.md) и соответствующем столбце state_desc.  
  
 Размер резервных копий баз данных, в которых есть одна или несколько оптимизированных для памяти таблиц, обычно больше, чем размер в памяти, но меньше, чем объем, занимаемый на диске. Кроме всего прочего, дополнительный объем зависит от числа удаленных строк.  
  
### Оценка размера полной резервной копии базы данных  
  
> [!IMPORTANT]  
>  Не рекомендуется использовать значение BackupSizeInBytes для оценки размера резервной копии In-Memory OLTP.  
  
 Первый сценарий рабочей нагрузки предназначен (главным образом) для вставки. В этом случае большинство файлов данных находятся в состоянии Active, полностью загружены и из них удалено очень небольшое число строк. Размер резервной копии базы данных близок к размеру данных в памяти.  
  
 Второй сценарий рабочей нагрузки предназначен для частого выполнения операций вставки, удаления и обновления. В худшем случае каждая из пар файлов контрольных точек после учета удаленных строк загружена на 50 %. Размер резервной копии базы данных будет по крайней мере в два раза больше размера данных в памяти.  
  
## Разностные резервные копии баз данных с таблицами, оптимизированными для памяти  
 Хранилище оптимизированных для памяти таблиц состоит из файлов данных и разностных файлов, как описано в разделе [Устойчивость таблиц, оптимизированных для памяти](../../relational-databases/in-memory-oltp/durability-for-memory-optimized-tables.md). Разностная резервная копия базы данных с таблицами, оптимизированными для памяти, содержит следующие данные.  
  
-   Присутствие оптимизированный для памяти таблицы не влияет разностное резервное копирование файловых групп для хранения дисковых таблиц.  
  
-   Журнал активной транзакции тот же, что и в полной резервной копии базы данных.  
  
-   Для файловой группы, оптимизированной для памяти, разностная резервная копия для определения данных и разностных файлов, подлежащих резервному копированию, использует тот же алгоритм, что и полная резервная копия, но затем отфильтровывает подмножество файлов следующим образом.  
  
    -   Файл данных содержит новые вставленные строки, и после его заполнения он закрывается и помечается как файл только для чтения. Файл данных копируется только в том случае, если он был закрыт после создания последней полной резервной копии базы данных. В разностную резервную копию добавляются только файлы данных со строками, вставленными с момента создания последней полной резервной копии. Исключение — это сценарий обновления и удаления, допускающий, что некоторые вставленные строки могли быть помечены для сборки мусора или уже были обработаны этой операцией.  
  
    -   Разностный файл хранит ссылки на удаленные строки данных. Поскольку любая будущая транзакция может удалить строку, а разностный файл может измениться в любой момент своего существования, он не закрываются никогда. Разностный файл всегда сохраняется в резервную копию. Разностные файлы обычно используют менее 10 % хранилища, поэтому они оказывают минимальное влияние на размер разностной резервной копии.  
  
 Если таблицы, оптимизированные для памяти, являются значительной частью размера базы данных, то разностная резервная копии может значительно уменьшить размер резервной копии. Для типичных рабочих нагрузок OLTP разностные резервные копии будут намного меньше, чем полные резервные копии баз данных.  
  
## См. также:  
 [Резервное копирование и восстановление оптимизированных для памяти таблиц](../Topic/Backup,%20Restore,%20and%20Recovery%20of%20Memory-Optimized%20Tables.md)  
  
  