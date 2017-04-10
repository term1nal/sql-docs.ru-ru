---
title: "Репликация SQL Server | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "репликация [SQL Server], сведения"
  - "репликация [SQL Server]"
ms.assetid: 3a5f4592-3c61-4b4d-9ceb-39716aeeba41
caps.latest.revision: 58
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 58
---
# Репликация SQL Server
  Репликация представляет собой набор технологий копирования и распространения данных и объектов баз данных между базами данных, а также синхронизации баз данных для поддержания согласованности. Используя репликацию, можно распространять данные в различные расположения, а также удаленным или мобильным пользователям по локальным или глобальным сетям посредством коммутируемого соединения, по беспроводным соединениям и через Интернет.  
  
 Репликация транзакций обычно используется в сценариях «сервер-сервер», для которых необходима высокая пропускная способность, в том числе улучшение масштабируемости и доступности, хранение и протоколирование данных, интеграция данных с нескольких сайтов, объединение разнородных данных, автономная обработка пакетов. Репликация слиянием разработана в основном для мобильных приложений или распределенных серверных приложений, в которых возможно возникновение конфликтов данных. Обычные сценарии включают обмен данными с мобильными пользователями, клиентские приложения точки продажи (POS) и интеграцию данных с нескольких сайтов. Репликация моментальных снимков используется для обеспечения начального набора данных для репликации транзакций и репликации слиянием; она также может применяться при необходимости выполнения полного обновления данных. Располагая этими тремя типами репликации, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] представляет собой мощную и гибкую систему для синхронизации данных уровня предприятия. Репликация на SQLCE 3.5 и SQLCE 4.0 поддерживается и для [!INCLUDE[win8srv](../../includes/win8srv-md.md)] , и для [!INCLUDE[win8](../../includes/win8-md.md)].  
  
 Альтернативой для репликации является синхронизация баз данных с помощью Microsoft Sync Framework. Sync Framework включает в себя компоненты и интуитивно понятный и гибкий API, облегчающий синхронизацию баз данных SQL Server, SQL Server Express, SQL Server Compact и SQL Azure. Sync Framework также включает в себя классы, которые можно адаптировать для синхронизации базы данных SQL Server и любой другой базы данных, совместимой с ADO.NET. Подробную документацию по компонентам синхронизации баз данных Sync Framework см. в статье [Синхронизация баз данных](http://go.microsoft.com/fwlink/?LinkId=209079). Общие сведения о платформе Sync Framework см. в [Центре разработчиков Microsoft Sync Framework](http://go.microsoft.com/fwlink/?LinkId=209078). Сравнение между Sync Framework и репликацией слиянием приведено в статье [Обзор синхронизации баз данных](http://msdn.microsoft.com/library/bb902818\(SQL.110\).aspx)  
  
 **Просмотр содержимого по области**  
 ![Маленький значок папки](../../analysis-services/media/filefolder-small.png "Маленький значок папки") [Новые возможности](../../relational-databases/replication/what-s-new-replication.md)  
  
 ![Маленький значок папки](../../analysis-services/media/filefolder-small.png "Маленький значок папки") [Обратная совместимость](../../relational-databases/replication/replication-backward-compatibility.md)  
  
 ![Маленький значок папки](../../analysis-services/media/filefolder-small.png "Маленький значок папки") [Функции и задачи репликации](../../relational-databases/replication/replication-features-and-tasks.md)  
  
 ![Маленький значок папки](../../analysis-services/media/filefolder-small.png "Маленький значок папки") [Технический справочник](../../relational-databases/replication/technical-reference-replication.md)  
  
  