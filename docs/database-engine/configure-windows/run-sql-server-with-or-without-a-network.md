---
title: "Запуск SQL Server при наличии и отсутствии сети | Microsoft Docs"
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
  - "проверка запуска службы SQL Server"
  - "net start, команда [SQL Server]"
  - "командная строка [SQL Server], подключения"
  - "службы SQL Server, сети"
  - "сведения о состоянии [SQL Server], служба Server"
  - "запуск SQL Server"
  - "работа в сети [SQL Server], SQL Server при наличии или отсутствии сети"
  - "службы [SQL Server], сети"
  - "запуск службы SQL Server"
  - "SQL Server, запуск"
ms.assetid: 54eac961-5c7a-4481-982d-f93a64b5c2f4
caps.latest.revision: 26
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 26
---
# Запуск SQL Server при наличии и отсутствии сети
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] может работать в сети или без подключения к ней.  
  
## Запуск SQL Server при подключении к сети  
 Чтобы сервер [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] мог взаимодействовать с клиентами и другими серверами в сети, должна быть запущена служба [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. По умолчанию [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows автоматически запускает встроенную службу [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Чтобы определить, была ли запущена служба [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], в командной строке введите следующее:  
  
 **net start**  
  
 Если службы, связанные с [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], запущены, следующие службы отобразятся в выходных данных команды **net start**:  
  
-   Службы Analysis Services (MSSQLSERVER)  
  
-   SQL Server (MSSQLSERVER)  
  
-   SQL Server Agent (MSSQLSERVER)  
  
## Запуск SQL Server без подключения к сети  
 При запуске экземпляра [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] без подключения к сети нет необходимости запускать встроенную службу [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Поскольку [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], диспетчер конфигураций SQL Server и команды **net start** и **net stop** могут работать даже без подключения к сети, процедуры запуска и остановки экземпляра [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] аналогичны при работе в сети и автономной работе.  
  
 При подключении к изолированному экземпляру [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] из локального клиента, например **sqlcmd**, осуществляется обход сети и подключение к экземпляру [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] напрямую через локальный канал. Разница между локальным и сетевым каналами заключается в использовании сети. И локальный, и сетевой каналы устанавливают соединение с экземпляром [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] через стандартный канал (\\\\.\pipe\sql\query), если не указано другое.  
  
 При подключении к локальному экземпляру [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] без указания имени сервера используется локальный канал. При подключении к локальному экземпляру [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] с явным указанием имени сервера используется или сетевой канал, или другой механизм сетевого межпроцессного взаимодействия (IPC), например через протоколы межсетевого и последовательного обмена пакетами (IPX/SPX), если [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] настроен для работы с несколькими сетями. Так как отдельный сервер [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] не поддерживает сетевые каналы, при соединении с экземпляром [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] из клиента ненужный аргумент **/***\<имя_сервера>* необходимо опустить. Например, для подключения к отдельному экземпляру [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] из **osql** введите:  
  
 **osql /Usa /P** *\<saPassword>*  
  
  