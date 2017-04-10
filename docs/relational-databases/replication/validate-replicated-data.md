---
title: "Проверка реплицированных данных | Microsoft Docs"
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
  - "встроенная проверка данных [репликация SQL Server]"
  - "управление репликацией, проверка данных"
  - "репликация [SQL Server], проверка данных"
  - "репликация транзакций, проверка данных"
  - "проверка данных"
  - "проверка данных репликации слиянием [репликация SQL Server]"
  - "проверка данных репликации слиянием [репликация SQL Server], о проверке данных"
  - "проверка реплицированных данных"
ms.assetid: f7500a2b-61cb-41b5-816d-27609a6c58e7
caps.latest.revision: 45
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 45
---
# Проверка реплицированных данных
  Репликация транзакций, а также репликация слиянием позволяет проверять соответствие данных подписчика данным издателя. Проверку можно выполнять как для определенных подписок, так и для всех подписок в публикации. Задайте один из следующих типов проверки и агент распространителя или агент слияния проверят данные при следующем запуске.  
  
-   Только подсчет строк. При проверке этого типа проверяется совпадение числа строк таблицы на подписчике с числом строк таблицы на издателе, но не проверяется содержимое строк на совпадение. Проверка количества строк обеспечивает упрощенный подход к проверке, который может уведомить о проблемах с данными.  
  
-   Подсчет количества строк и двоичной контрольной суммы. Кроме подсчета количества строк на подписчике и на издателе, вычисляется контрольная сумма всех данных с помощью алгоритма подсчета контрольной суммы. Если количество строк не совпадает, то контрольная сумма не проверяется.  
  
 Кроме проверки совпадения данных на подписчике и издателе, репликация слиянием предоставляет возможность удостовериться, правильно ли данные секционированы для каждого подписчика. Дополнительные сведения см. в разделе [проверки сведений о секции для слияния подписчика](../../relational-databases/replication/validate-partition-information-for-a-merge-subscriber.md).  
  
 **Проверка данных**  
  
 Чтобы проверить все статьи в подписке, используйте среду [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], хранимые процедуры или объекты RMO. Дополнительные сведения см. в статье [Validate Data at the Subscriber](../../relational-databases/replication/validate-data-at-the-subscriber.md). Чтобы проверить отдельные статьи в публикациях моментальных снимков и публикациях транзакций, следует использовать хранимые процедуры.  
  
## Результаты проверки данных  
 Когда проверка заканчивается, агент распространителя или агент слияния заносит в журнал сообщения касательно успеха или неудачи (репликация не сообщает, на каких строках возникла ошибка). Эти сообщения можно просмотреть в среде [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], мониторе репликации и в системных таблицах репликации. В перечисленных выше разделах руководства описывается, как запустить проверку и просмотреть ее результаты.  
  
 Чтобы обработать ошибки проверки, рассмотрите следующее.  
  
-   Настройте предупреждение репликации под названием **Репликация: ошибка проверки данных подписчиком** , чтобы получать уведомление об ошибке. Дополнительные сведения см. в разделе [Настройка предопределенных предупреждений репликации & #40; SQL Server Management Studio & #41;](../../relational-databases/replication/administration/configure-predefined-replication-alerts-sql-server-management-studio.md).  
  
-   Является ли неудачная проверка данных проблемой для приложения? Если неудачная проверка данных представляет собой проблему, обновите данные вручную, чтобы они были синхронизированы, или повторно инициализируйте подписку.  
  
    -   Данные можно обновить с помощью [программы tablediff](../../tools/tablediff-utility.md). Дополнительные сведения об использовании этой программы см. в разделе [сравнения реплицированных таблицах для различия & #40; Программирование репликации на & #41;](../../relational-databases/replication/administration/compare-replicated-tables-for-differences-replication-programming.md).  
  
    -   Дополнительные сведения о повторной инициализации см. в разделе [повторно инициализировать подписки](../../relational-databases/replication/reinitialize-subscriptions.md).  
  
## Аспекты проверки данных  
 При проверке данных учитывайте следующие соображения.  
  
-   Перед проверкой данных следует остановить все действия по обновлению на подписчиках (при выполнении проверки нет необходимости останавливать действия на издателе).  
  
-   Ввиду того что простые и двоичные контрольные суммы могут требовать больших вычислительных мощностей при проверке большого количества данных, следует назначать проверку на время, когда активность используемых в репликации серверов минимальна.  
  
-   Репликация проверяет только таблицы; она не проверяет, совпадают ли в схеме на издателе и подписчике только статьи (например, хранимые процедуры).  
  
-   Двоичная контрольная сумма может использоваться с любой опубликованной таблицей. С помощью контрольной суммы нельзя проверить таблицы с фильтрацией по столбцам, или логические структуры таблиц, отличающиеся смещением столбцов (из-за инструкций ALTER TABLE, удаляющих или добавляющих столбцы).  
  
-   Проверка репликации использует **контрольной суммы** и **binary_checksum** функции. Сведения об их поведении см. в разделе  [контрольной СУММЫ & #40; Transact-SQL & #41;](../../t-sql/functions/checksum-transact-sql.md) и [BINARY_CHECKSUM & #40; Transact-SQL & #41;](../../t-sql/functions/binary-checksum-transact-sql.md).  
  
-   Проверка с использованием двоичной контрольной суммы может неверно сообщить об отказе, если типы данных на подписчике и издателе отличаются. К этому может привести выполнение одного из следующих действий.  
  
    -   Явная установка параметров схемы для соответствия типам данных в ранних версиях [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
    -   Установка уровня совместимости публикации для публикации слиянием в соответствии с более ранней версией [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], в то время как опубликованные таблицы содержат один или несколько типов данных, которые должны соответствовать текущей версии.  
  
    -   Инициализация подписки вручную при использовании разных типов данных на подписчике.  
  
-   Проверки двоичной контрольной суммы и простой контрольной суммы не поддерживаются трансформируемыми подписками для репликации транзакций.  
  
-   Также не поддерживается проверка данных, реплицированных на подписчики, отличные от [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## Как работает проверка данных  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] проверяет данные путем подсчета числа строк или контрольной суммы на издателе и последующего сравнения этих значений с соответствующими значениями числа строк и контрольной суммы, вычисленными на подписчике. Одно значение вычисляется для всей таблицы публикации, одно — для всей таблицы подписки, но данные в столбцах типа **text**, **ntext**и **image** в вычислении не участвуют.  
  
 При выполнении вычислений временно устанавливаются совместные блокировки таблиц, для которых производится подсчет числа строк или контрольных сумм, однако вычисления вскоре завершаются и общие блокировки снимаются, обычно в течение нескольких секунд.  
  
 При использовании двоичных контрольных сумм выполняется последовательная проверка столбцов избыточным 32-разрядным кодом (CRC) вместо проверки циклическим избыточным кодом (CRC) физической строки на странице данных. Это позволяет столбцам таблицы располагаться физически в любом порядке на странице данных, и при этом CRC-код для строки будет оставаться прежним. Проверка по двоичной контрольной сумме может использоваться при наличии у публикации фильтров по строкам или столбцам.  
  
## См. также:  
 [Рекомендации по администрированию репликации](../../relational-databases/replication/administration/best-practices-for-replication-administration.md)  
  
  