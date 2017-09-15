---
title: "Открытие средства просмотра журналов | Документация Майкрософт"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Log File Viewer, opening
ms.assetid: a86b89cb-0432-4648-895a-05ecc5450e45
caps.latest.revision: 29
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 902e26657bb71799af5e006c9a1842edda4f783d
ms.contentlocale: ru-ru
ms.lasthandoff: 06/22/2017

---
# <a name="open-log-file-viewer"></a>открыть средство просмотра журнала
  Средство просмотра журнала используется в среде [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] для доступа к сведениям об ошибках и событиях, записываемых в следующие журналы.  
  
-   Коллекция аудита  
  
-   Сбор данных  
  
-   Database Mail  
  
-   Журнал заданий  
  
-   SQL Server  
  
-   SQL Server, агент  
  
-   События Windows (К ним можно получить доступ с помощью программы просмотра событий Windows.)  
  
 Начиная с [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], в списке «Зарегистрированные серверы» можно просматривать файлы журналов [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] на локальных и удаленных экземплярах [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. В списке «Зарегистрированные серверы» можно просматривать файлы журнала как для экземпляров в сети, так и для экземпляров вне сети. Дополнительные сведения о доступе в сети см. далее в разделе «Просмотр файлов журнала в сети с зарегистрированных серверов». Дополнительные сведения о доступе к автономным файлам журнала [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] см. в разделе [Просмотр автономных файлов журнала](../../relational-databases/logs/view-offline-log-files.md).  
  
 Открыть средство просмотра журнала можно несколькими способами (в зависимости от того, какие сведения нужно просмотреть).  
  
##  <a name="BeforeYouBegin"></a> Разрешения  
 Чтобы получить доступ к файлам журнала для экземпляров [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , которые находятся в сети, требуется членство в предопределенной роли сервера securityadmin.  
  
 Чтобы получить доступ к файлам журнала для экземпляров [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , которые находятся вне сети, необходим доступ на чтение к пространству WMI **Root\Microsoft\SqlServer\ComputerManagement10** , а также к папке, в которой хранятся файлы журнала. Дополнительные сведения см. в подразделе "Безопасность" раздела [Просмотр автономных файлов журнала](../../relational-databases/logs/view-offline-log-files.md).  
  
### <a name="security"></a>Безопасность  
 Требуется членство в предопределенной роли сервера securityadmin.  
  
### <a name="view-log-files"></a>Просмотр файлов журнала  
  
##### <a name="to-view-logs-that-are-related-to-general-sql-server-activity"></a>Просмотр журналов, связанных с общими операциями SQL Server  
  
1.  В обозревателе объектов разверните узел **Управление**.  
  
2.  Выполните любое из следующих действий.  
  
    -   Щелкните правой кнопкой мыши **Журналы SQL Server**, выберите **Просмотр**, а затем **Журнал SQL Server** или **Журнал SQL Server и Windows**.  
  
    -   Разверните узел **Журналы SQL Server**, щелкните правой кнопкой мыши любой файл журнала и выберите **Просмотреть журнал SQL Server**. Можно также дважды щелкнуть любой файл журнала.  
  
     Доступны журналы **Компонент Database Mail**, **SQL Server**, **Агент SQL Server**и **Windows NT**.  
  
##### <a name="to-view-logs-that-are-related-to-jobs"></a>Просмотр журналов, связанных с заданиями  
  
-   В обозревателе объектов откройте **Агент SQL Server**, щелкните правой кнопкой мыши **Задания**и выберите **Просмотр журнала**.  
  
     Доступны журналы **Компонент Database Mail**, **Журнал заданий**и **Агент SQL Server**.  
  
##### <a name="to-view-logs-that-are-related-to-maintenance-plans"></a>Просмотр журналов, связанных с планами обслуживания  
  
-   В обозревателе объектов раскройте узел **Управление**, щелкните правой кнопкой мыши **Планы обслуживания**и выберите **Просмотр журнала**.  
  
     Доступны журналы **Компонент Database Mail**, **Журнал заданий**, **Планы обслуживания**, **План удаленного обслуживания**и **Агент SQL Server**.  
  
##### <a name="to-view-logs-that-are-related-to-data-collection"></a>Просмотр журналов, связанных с коллекциями данных  
  
-   В обозревателе объектов раскройте узел **Управление**, щелкните правой кнопкой мыши **Сбор данных**и выберите команду **Просмотреть журналы**.  
  
     Доступны журналы **Сбор данных**, **Журнал заданий**и **Агент SQL Server**.  
  
##### <a name="to-view-logs-that-are-related-to-database-mail"></a>Просмотр журналов, связанных с компонентом Database Mail  
  
-   В обозревателе объектов раскройте узел **Управление**, щелкните правой кнопкой мыши **Компонент Database Mail**и выберите команду **Просмотреть журнал компонента Database Mail**.  
  
     Доступны журналы **Компонент Database Mail, Журнал заданий**, **Планы обслуживания**, **Планы удаленного обслуживания**, **SQL Server**, **Агент SQL Server**и **Windows NT**.  
  
##### <a name="to-view-logs-that-are-related-to-audits-collections"></a>Просмотр журналов, связанных с коллекциями аудитов  
  
-   В обозревателе объектов разверните узел **Безопасность**, затем узел **Аудиты**, щелкните правой кнопкой мыши аудит и выберите команду **Просмотреть журналы**.  
  
     Доступны журналы **Коллекция аудитов** и **Windows NT**.  
  
##### <a name="to-view-logs-that-are-related-to-audits-collections"></a>Просмотр журналов, связанных с коллекциями аудитов  
  
-   В обозревателе объектов разверните узел **Безопасность**, затем узел **Аудиты**, щелкните правой кнопкой мыши аудит и выберите команду **Просмотреть журналы**.  
  
     Доступны журналы **Коллекция аудитов** и **Windows NT**.  
  
## <a name="see-also"></a>См. также:  
 [Средство просмотра файлов журнала](../../relational-databases/logs/log-file-viewer.md)   
 [Подсистема аудита SQL Server (компонент Database Engine)](../../relational-databases/security/auditing/sql-server-audit-database-engine.md)   
 [Просмотр автономных файлов журнала](../../relational-databases/logs/view-offline-log-files.md)  
  
  