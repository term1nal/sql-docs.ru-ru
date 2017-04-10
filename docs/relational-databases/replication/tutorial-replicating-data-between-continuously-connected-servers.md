---
title: "Учебник. Репликация данных между постоянно соединенными серверами | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
helpviewer_keywords: 
  - "учебники [репликация SQL Server]"
  - "репликация [SQL Server], учебники"
  - "мастера [репликация SQL Server]"
ms.assetid: 7b18a04a-2c3d-4efe-a0bc-c3f92be72fd0
caps.latest.revision: 21
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 21
---
# Учебник. Репликация данных между постоянно соединенными серверами
Репликация представляет собой хорошее решение проблемы перемещения данных между постоянно соединенными серверами. С помощью мастеров репликации можно легко настроить и администрировать топологию репликации. В этом учебники рассказывается о настройке топологии репликации для постоянно соединенных серверов.  
  
## Обзор учебника  
В этом учебнике рассказывается о публикации данных из одной базы данных в другую при помощи репликации транзакций. На первом занятии рассматривается, как создать публикацию при помощи среды [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] . На дальнейших занятиях разбирается создание и проверка подписки, а также измерение задержки.  
  
## Требования  
Этот учебник предназначен для пользователей, знакомых с основными операциями с базами данных, но имеющих ограниченный опыт в работе с репликацией. Для работы с этим учебником требуется завершить работу с предыдущим учебником, [Подготовка сервера для репликации](../../relational-databases/replication/tutorial-preparing-the-server-for-replication.md).  
  
Для работы с этим учебником должны быть установлены следующие компоненты.  
  
-   На сервере-издателе (источник):  
  
    -   Любой выпуск [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], за исключением Express ([!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]) или [!INCLUDE[ssEW](../../includes/ssew-md.md)]. Эти выпуски не могут быть издателями репликации.  
  
    -   [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] . В целях повышения безопасности образцы баз данных по умолчанию не устанавливаются.  
  
-   На сервере-подписчике (целевом):  
  
    -   Любой выпуск [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], за исключением [!INCLUDE[ssEW](../../includes/ssew-md.md)]. [!INCLUDE[ssEW](../../includes/ssew-md.md)] не может быть подписчиком в репликации транзакций.  
  
    > [!NOTE]  
    > Репликация не устанавливается по умолчанию на [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)].  
  
> [!NOTE]  
> В среде [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] необходимо подключиться к издателю и подписчику с помощью имени входа, которое является членом предопределенной роли сервера **sysadmin**.  
  
**Предполагаемое время для выполнения заданий данного учебника: 30 минут.**  
  
## Занятия этого учебника  
  
-   [Урок 1. Публикация данных с помощью репликации транзакций](../../relational-databases/replication/lesson-1-publishing-data-using-transactional-replication.md)  
  
-   [Занятие 2. Создание подписки на публикацию транзакций](../../relational-databases/replication/lesson-2-creating-a-subscription-to-the-transactional-publication.md)  
  
-   [Занятие 3. Проверка подписки и измерение задержки](../../relational-databases/replication/lesson-3-validating-the-subscription-and-measuring-latency.md)  
  
[Приступить к изучению](../../relational-databases/replication/lesson-1-publishing-data-using-transactional-replication.md)  
  
## См. также:  
[Основные понятия программирования репликации](../../relational-databases/replication/concepts/replication-programming-concepts.md)  
  
  
  