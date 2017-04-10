---
title: "Подписчики, отличные от подписчиков SQL Server | Microsoft Docs"
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
  - "подписки [репликация SQL Server], подписчики, отличные от подписчиков SQL Server"
  - "разнородные источники данных, подписчики, отличные от подписчиков SQL Server"
  - "разнородные источники данных"
  - "разнородная репликация базы данных, подписчики, отличные от подписчиков SQL Server"
  - "подписчики, отличные от подписчиков SQL Server, информация о подписчиках, отличных от подписчиков SQL Server"
  - "разнородные подписчики"
  - "разнородные подписчики, информация о разнородных подписчиках"
  - "подписчики [репликация SQL Server], подписчики, отличные от подписчиков SQL Server"
  - "подписчики, отличные от SQL Server"
ms.assetid: 831e7586-2949-4b9b-a2f3-7b0b699b23ff
caps.latest.revision: 55
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 55
---
# Подписчики, отличные от подписчиков SQL Server
  Следующие подписчики, не относящиеся к [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], могут подписаться на публикации моментальных снимков и публикации транзакций, используя принудительные подписки. Подписки поддерживаются для двух самых последних версий каждой из баз данных, приведенных в списке, с использованием самой последней версии поставщика OLE DB из приводимого списка.  
  
 Разнородная репликация на подписчики, отличные от подписчика SQL Server, устарела. Публикация Oracle устарела. Для перемещения данных создайте решения с помощью системы отслеживания измененных данных и служб [!INCLUDE[ssIS](../../../includes/ssis-md.md)].  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
|База данных|Операционная система|Поставщик|  
|--------------|----------------------|--------------|  
|Oracle;|Все платформы, поддерживаемые Oracle|Поставщик OLE DB для Oracle (поставляемый Oracle)|  
|IBM DB2|MVS, AS400, Unix, Linux, Windows, за исключением версии 9.x|Поставщик OLE DB для Microsoft Host Integration Server (HIS)|  
  
 Сведения о создании подписок для Oracle и IBM DB2 см. в разделе [подписчиков Oracle](../../../relational-databases/replication/non-sql/oracle-subscribers.md) и [подписчиков IBM DB2](../../../relational-databases/replication/non-sql/ibm-db2-subscribers.md).  
  
## Вопросы использования подписчиков, отличных от подписчиков SQL Server  
 При репликации на подписчики, не относящиеся к [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], необходимо помнить о следующем:  
  
### Общие рекомендации  
  
-   Репликация поддерживает публикацию таблиц и индексированных представлений в виде таблиц для подписчиков, не относящихся к [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (индексированные представления не могут быть реплицированы как индексированные представления).  
  
-   Если публикация создается в мастере создания публикаций, а затем включается для отличных от подписчиков SQL Server с помощью диалогового окна Свойства публикации, владелец всех объектов в базе данных подписки не указан для не -[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] подписчиков, тогда как для [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] подписчиков, ему присваивается владелец соответствующего объекта в базе данных публикации.  
  
-   Если публикация имеет подписчиков [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] и подписчиков, не относящихся к [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], то публикация должна быть включена для подписчиков, не относящихся к [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], перед тем как будут созданы какие-либо подписки для подписчиков [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   По умолчанию скрипты, создаваемые агентом моментальных снимков для подписчиков, не относящихся к [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], используют в синтаксисе инструкции CREATE TABLE идентификаторы без кавычек. Поэтому опубликованная таблица с именем 'test' реплицируется как 'TEST'. Чтобы использовать такой же регистр, как таблицы в базе данных публикации, используйте **- QuotedIdentifier** параметр для агента распространителя.  **- QuotedIdentifier** параметра также должен использоваться, если имена опубликованных объектов (например, таблицы, столбцы и ограничения) содержат пробелы или слова, которые являются зарезервированными словами в версии базы данных в отличном от[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] подписчика. Дополнительные сведения об этом параметре см. в разделе [агента распространителя репликации](../../../relational-databases/replication/agents/replication-distribution-agent.md).  
  
-   Учетная запись, под которой запускается агент распространителя, должна иметь доступ с правом на чтение к установочному каталогу поставщика OLE DB.  
  
-   По умолчанию для не -[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] подписчиков, агент распространителя использует значение [(адреса по умолчанию)] для базы данных подписки ( **- SubscriberDB** параметр для агента распространителя):  
  
    -   Для СУБД Oracle сервер имеет не более одной базы данных, поэтому нет необходимости указывать базу данных.  
  
    -   Для СУБД IBM DB2 база данных указывается в строке соединения с DB2. Дополнительные сведения см. в разделе [Создать подписку для подписчика не SQL Server](../../../relational-databases/replication/create-a-subscription-for-a-non-sql-server-subscriber.md).  
  
-   Если распространитель [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] выполняется на 64-разрядной платформе, необходимо использовать 64-разрядную версию соответствующего поставщика OLE DB.  
  
-   Репликация перемещает данные в формате Юникода независимо от параметров сортировки и кодовых страниц, используемых на издателе и подписчике. При репликации между издателями и подписчиками рекомендуется выбрать совместимые параметры сортировки и кодовую страницу.  
  
-   Если статья добавляется или удаляется из публикации, то подписки для подписчиков, не относящихся к [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], должны быть повторно инициализированы.  
  
-   Для всех подписчиков, не относящихся к [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], поддерживаются только ограничения NULL и NOT NULL. Ограничения первичного ключа реплицируются как уникальные индексы.  
  
-   В разных базах данных значение NULL обрабатывается по-разному, что влияет на представление пустых значений, пустых строк и значений NULL. Это в свою очередь влияет на поведение значений, вставляемых в столбцы с определяемыми уникальными ограничениями. Например, СУБД Oracle допускает существование нескольких значений NULL в столбце, который считается уникальным, тогда как [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] допускает наличие только одного значения NULL в уникальном столбце.  
  
     Дополнительным фактором, который следует учитывать, является порядок обработки значений NULL, пустых строк и пустых значений в случае, когда столбец определяется как NOT NULL. Сведения по этому вопросу для подписчиков Oracle см. в разделе [подписчиков Oracle](../../../relational-databases/replication/non-sql/oracle-subscribers.md).  
  
-   Связанные с репликацией метаданные (таблица последовательности транзакций) на поставщиках [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] не удаляются при удалении подписки.  
  
### Соответствие требованиям базы данных подписчика  
  
-   Опубликованные схема и данные должны соответствовать требованиям базы данных подписчика. Например, если база данных, не относящаяся к [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], имеет меньший максимальный размер строки, чем [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], то следует убедиться, что опубликованные схема и данные не превышают этот размер.  
  
-   Таблицы, которые реплицируются на подписчики, не относящиеся к [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], должны следовать соглашениям об именовании таблиц базы данных подписчика.  
  
-   DDL не поддерживается для подписчиков, отличных от подписчиков SQL Server. Дополнительные сведения об изменениях схем см. в разделе [внесение изменений схемы в базах данных публикаций](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md).  
  
### Поддержка возможности репликации  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] предлагает два типа подписок: push и pull. Подписчики, не относящиеся к [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], должны использовать принудительные подписки, для которых агент распространителя запускается на распространителе [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] предлагает два формата моментальных снимков: собственный bcp режим и символьный режим. Подписчики, не относящиеся к [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], требуют использования моментальных снимков символьного формата.  
  
-   Подписчики, не относящиеся к [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], не могут использовать подписки с немедленным обновлением или обновлением посредством очередей и не могут быть узлами одноранговой топологии.  
  
-   Подписчики, не относящиеся к [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], не могут быть автоматически инициализированы из резервной копии.  
  
## См. также:  
 [Разнородная репликация базы данных](../../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Подписка на публикации](../../../relational-databases/replication/subscribe-to-publications.md)  
  
  