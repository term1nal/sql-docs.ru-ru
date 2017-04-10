---
title: "Настройка распространителя | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "репликация [SQL Server], распространение"
  - "конфигурация распространителя [репликация SQL Server]"
  - "удаленные распространители [репликация SQL Server]"
  - "репликация транзакций, настройка распространения"
  - "базы данных распространителя [репликация SQL Server], изменение размера"
  - "распространители [репликация SQL Server], настройка"
  - "базы данных распространителя [репликация SQL Server], о базах данных распространителя"
  - "база данных распространителя [репликация SQL Server]"
  - "репликация слиянием [репликация SQL Server], настройка распространения"
ms.assetid: 94d52169-384e-4885-84eb-2304e967d9f7
caps.latest.revision: 44
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 44
---
# Настройка распространителя
  Распространитель — это сервер, на котором находится база данных распространителя, хранящая метаданные и данные предыстории для всех типов репликации, а также транзакции репликации транзакций. Для настройки репликации, необходимо настроить распространитель. Каждый издатель может быть назначен только одному экземпляру распространителя, однако один распространитель может совместно использоваться несколькими издателями. Распространитель использует следующие дополнительные ресурсы на сервере, где он расположен.  
  
-   Дополнительное дисковое пространство, если файлы моментальных снимков для публикации хранятся на распространителе (где они обычно и хранятся).  
  
-   Дополнительное место на диске для хранения базы данных распространителя.  
  
-   Дополнительное использование процессора агентами репликации для принудительных подписок на распространителе.  
  
 Сервер, который был выбран в качестве распространителя, должен иметь достаточно места на диске и достаточно мощный процессор для поддержки репликации и других действий на данном сервере. При настройке распространителя указываются следующие параметры:  
  
-   Папку моментальных снимков, применяемую по умолчанию для всех издателей, которые используют этот распространитель. Убедитесь, что эта папка уже открыта для общего доступа и имеет соответствующий набор разрешений. Дополнительные сведения см. в разделе [Безопасность папки моментальных снимков](../../relational-databases/replication/security/secure-the-snapshot-folder.md).  
  
-   Имя и расположение файлов базы данных распространителя. База данных распространителя не может быть переименована после создания. Для использования иного имени для базы данных необходимо отключить распространение и установить конфигурацию заново.  
  
-   Любые издатели, наделенные правами использования распространителя. Если указываются издатели, отличные от экземпляра, на котором выполняется распространитель, необходимо также указать пароль для установки подключений издателей к удаленному распространителю.  
  
 Для репликации транзакций, после настройки распространения рекомендуется выполнить следующие действия:  
  
-   Установите надлежащий размер для базы данных распространителя. Проверьте репликацию с типовой нагрузкой системы, чтобы определить пространство, необходимое для хранения команд. Убедитесь в том, что база данных имеет достаточный размер для хранения команд без частого автоматического увеличения размера. Дополнительные сведения об изменении размера базы данных см. в разделе [ALTER DATABASE & #40; Transact-SQL & #41;](../../t-sql/statements/alter-database-transact-sql.md).  
  
-   Установите параметр **sync with backup** для базы данных распространителя. Дополнительные сведения см. в разделе [стратегии резервного копирования и восстановления моментальных снимков и репликации транзакций](../../relational-databases/replication/administration/strategies-for-backing-up-and-restoring-snapshot-and-transactional-replication.md) и [Включение скоординированного резервного копирования для репликации транзакций и #40; Программирование репликации Transact-SQL & #41;](../../relational-databases/replication/administration/enable coordinated backups for transactional replication.md).  
  
## Локальный и удаленный распространители  
 По умолчанию распространитель является тем же самым сервером, что и издатель (локальный распространитель), но он может быть также и отдельным сервером, отличным от сервера издателя (удаленный распространитель). Обычно удаленный распространитель используется в следующих случаях:  
  
-   Перенос обработки на другой компьютер, если требуется минимизировать влияние репликации на издатель (например, если издатель является сервером интерактивной обработки транзакций (OLTP)).  
  
-   Настройка централизованного распространителя для нескольких издателей.  
  
 Удаленные распространители чаще используются в репликации транзакций, чем в репликации слиянием по двум причинам:  
  
-   Распространитель играет большую роль в репликации транзакций, так как все реплицированные транзакции записываются в базу данных распространителя и считываются из нее.  
  
-   В топологиях репликации слиянием обычно используются подписки по запросу, так что все агенты выполняются на каждом подписчике вместо выполнения на распространителе. Дополнительные сведения см. в разделе [подписаться на публикации](../../relational-databases/replication/subscribe-to-publications.md). В большинстве случаев для репликации слиянием необходимо использовать локальный распространитель.  
  
 Чтобы настроить публикацию и распространение, см. раздел [Configure Publishing and Distribution](../../relational-databases/replication/configure-publishing-and-distribution.md).  
  
 Чтобы изменить свойства издателя и распространителя, см. раздел [View and Modify Distributor and Publisher Properties](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md).  
  
## См. также:  
 [Публикация данных и объектов базы данных](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Организация безопасности распространителя](../../relational-databases/replication/security/secure-the-distributor.md)  
  
  