---
title: "Оптимизация производительности параметризованного фильтра с помощью предварительно вычисляемых секций | Microsoft Docs"
ms.custom: ""
ms.date: "03/23/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "предварительно вычисляемые секции [репликация SQL Server]"
  - "предварительно вычисляемые секции репликации слиянием [репликация SQL Server]"
  - "предварительно вычисляемые секции репликации слиянием [репликация SQL Server], о предварительно вычисляемых секциях"
ms.assetid: 85654bf4-e25f-4f04-8e34-bbbd738d60fa
caps.latest.revision: 45
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Оптимизация производительности параметризованного фильтра с помощью предварительно вычисляемых секций
  Предварительно вычисляемые секции — это способ оптимизации производительности, который может использоваться с фильтрованными публикациями слиянием. Предварительно вычисляемые секции необходимы также для использования логических записей в фильтрованных публикациях. Дополнительные сведения о логических записях см. в разделе [изменения группы связанных строк с логическими записями](../../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md).  
  
 При синхронизации подписчика с издателем издатель должен оценить фильтры подписчика, чтобы определить, какие строки принадлежат секции подписчика или его набору данных. Процесс определения принадлежности изменений секциям на издателе для каждого подписчика, получающего набор фильтрованных данных, называется *оценкой секции*. Без использования предварительно вычисляемых секций оценка секции должна выполняться для каждого изменения, вносимого в отфильтрованный столбец на издателе с момента последнего запуска агента слияния для определенного подписчика, и этот процесс необходимо повторить для каждого подписчика, синхронизируемого с издателем.  
  
 Однако если издатель и подписчик выполняются на [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] и более поздней версии, а также используются предварительно вычисляемые секции, членство в секциях для всех изменений на издателе вычисляется заранее и сохраняется во время выполнения изменений. В результате, когда подписчик синхронизируется с издателем, он может немедленно начать загрузку изменений, соответствующих его секции, без необходимости прохождения через процесс оценки секции. Такой принцип работы приводит к увеличению производительности, если публикация имеет большое количество изменений, подписчиков или статей.  
  
 В дополнение к использованию предварительно вычисляемых секций выполните предварительное создание моментальных снимков или разрешите подписчикам запрашивать создание и применение моментального снимка при первоначальной синхронизации. Используйте один или оба этих параметра, чтобы предоставить моментальные снимки публикациям, использующим параметризованные фильтры. Если не указать один из этих параметров, подписки будут инициализированы с помощью серии инструкций SELECT и INSERT, а не с использованием программы **bcp** . Этот процесс — гораздо более медленный. Дополнительные сведения см. в статье [Snapshots for Merge Publications with Parameterized Filters](../../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md).  
  
 **Использование предварительно вычисляемых секций**  
  
 Предварительно вычисляемые секции включены по умолчанию для всех новых и существующих публикаций, соответствующих описанным выше требованиям. Эту настройку можно изменить с помощью среды [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] или программно. Дополнительные сведения см. в разделе [Optimize Parameterized Row Filters](../../../relational-databases/replication/publish/optimize-parameterized-row-filters.md).  
  
## Требования к использованию предварительно вычисляемых секций  
 В случае соответствия следующим требованиям новые публикации слиянием создаются по умолчанию с включенными предварительно вычисляемыми секциями, а существующие публикации автоматически обновляются для использования этой функции. Если публикация не соответствует требованиям, включение предварительно вычисляемых секций возможно после изменения публикации. Если некоторые статьи соответствуют этим требованиям, а другие не соответствуют, рассмотрите возможность создания двух публикаций, в одной из которых будут включены предварительно вычисляемые секции.  
  
### Требования, предъявляемые к предложениям фильтра  
  
-   Любые функции, используемые в параметризованных фильтрах строк, например: HOST_NAME() и SUSER_SNAME() — должны находиться непосредственно в предложении параметризованного фильтра, а не быть вложенными в представление или динамическую функцию. Дополнительные сведения об этих функциях см. в разделе [HOST_NAME & #40; Transact-SQL & #41;](../../../t-sql/functions/host-name-transact-sql.md), [SUSER_SNAME & #40; Transact-SQL & #41;](../../../t-sql/functions/suser-sname-transact-sql.md), и [параметризованные фильтры строк](../../../relational-databases/replication/merge/parameterized-row-filters.md).  
  
-   Значения, возвращаемые каждому подписчику, не должны изменяться после создания секции. Например, если в фильтре используется HOST_NAME() (и при этом значение HOST_NAME() не переопределяется), не изменяйте имя компьютера подписчика.  
  
-   Фильтры соединения не должны содержать динамических функций (например, HOST_NAME() и SUSER_SNAME(), которые возвращают разные значения в зависимости от синхронизируемого подписчика). Динамические функции должны содержаться только в параметризованных фильтрах строк.  
  
-   В предложении фильтра нельзя использовать недетерминированные функции. Дополнительные сведения о недетерминированных функциях см. в разделе [Deterministic and Nondeterministic Functions](../../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).  
  
-   Представления, на которые имеются ссылки в предложениях фильтра соединения или параметризованного фильтра, не должны содержать динамические функции.  
  
-   В публикации не должно быть циклических связей фильтра соединения.  
  
### Параметры сортировки базы данных  
  
-   Если используются предварительно вычисляемые секции, то при сравнениях всегда применяются параметры сортировки базы данных, а не порядок сортировки таблицы или столбца. Рассмотрим следующий сценарий.  
  
    -   База данных с параметрами сортировки, учитывающими регистр символов, содержит таблицу с порядком сортировки не учитывающим регистр символов.  
  
    -   Таблица содержит столбец **ComputerName**, который сравнивается с именем узла размещения подписчика в параметризованном фильтре.  
  
    -   Таблица содержит одну строку со значением «МОЙКОМПЬЮТЕР» и одну строку со значением «мойкомпьютер» в том же столбце.  
  
     Если подписчик синхронизируется с узлом по имени «мойкомпьютер», подписчик получит только одну строку, потому что сравнение учитывает регистр символов (параметры сортировки базы данных). Если предварительно вычисляемые секции не используются, подписчик получит обе строки, поскольку таблица имеет параметры сортировки, не зависящие от регистра.  
  
## Производительность предварительно вычисляемых секций  
 При использовании предварительно вычисляемых секций имеет место определенная потеря производительности, когда изменения передаются с подписчика на издатель, но большая часть времени процесса слияния затрачивается на оценку секций и на загрузку изменений с издателя на подписчик, поэтому чистый выигрыш в производительности может быть довольно значительным. Увеличение производительности может быть разным в зависимости от числа одновременно синхронизирующихся подписчиков, а также от количества обновлений в синхронизации, в которых строки переносятся из одной секции в другую.  
  
## См. также:  
 [Параметризованные фильтры строк](../../../relational-databases/replication/merge/parameterized-row-filters.md)  
  
  