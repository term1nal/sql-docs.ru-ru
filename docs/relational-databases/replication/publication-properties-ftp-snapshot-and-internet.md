---
title: "Свойства публикации, страница &#171;Моментальный снимок — FTP и Интернет&#187; | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.newpubwizard.pubproperties.internetsynchronization.f1"
ms.assetid: 8e0198c3-5e4e-418c-9920-78ccbbfc1323
caps.latest.revision: 25
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 25
---
# Свойства публикации, страница &#171;Моментальный снимок — FTP и Интернет&#187;
  Эта страница позволяет:  
  
-   Устанавливать свойства доставки моментального снимка по протоколу FTP. Дополнительные сведения см. в разделе [передачи моментальные снимки через FTP](../../relational-databases/replication/transfer-snapshots-through-ftp.md). Для использования FTP в качестве протокола доставки моментальных снимков необходимо настроить FTP-сервер. Дополнительные сведения см. в документации по [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows.  
  
    > [!NOTE]  
    >  Изменения любых настроек FTP требуют создания нового моментального снимка.  
  
-   Устанавливать свойства веб-синхронизации для репликации слиянием в [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] и более поздних версиях, что позволяет синхронизировать подписки по протоколу HTTPS (безопасному протоколу передачи гипертекста). Для использования веб-синхронизации необходимо настроить сервер [!INCLUDE[msCoName](../../includes/msconame-md.md)] IIS. Дополнительные сведения см. в статье [Web Synchronization for Merge Replication](../../relational-databases/replication/web-synchronization-for-merge-replication.md).  
  
## Параметры  
 **Доступ к файлам моментальных снимков при помощи FTP**  
 Выберите **разрешить подписчикам загружать файлы моментальных снимков с помощью FTP (File Transfer Protocol)**, и укажите **имя FTP-сервера**, **номер порта**, **путь из корневой папки FTP**, **входа**, и **пароль**, чтобы разрешить подписчикам использовать FTP для доставки моментальных снимков.  
  
 Этот параметр позволяет подписчикам использовать FTP для получения файлов моментальных снимков, но не требует от них это делать. Если этот параметр выбран, мастер создания подписки будет настроен по умолчанию на получение подписчиком файлов моментальных снимков по протоколу FTP. Чтобы изменить этот параметр, используйте диалоговое окно **Свойства подписки** . Если подписчикам разрешается доступ к файлам моментальных снимков по протоколу FTP, задайте FTP-папку в качестве местонахождения файлов моментальных снимков на странице **Снимок** диалогового окна **Свойства публикации** . При этом агент моментальных снимков будет обновлять файлы в FTP-папке автоматически при создании нового моментального снимка. Если в качестве местонахождения не указана FTP-папка, необходимо будет обновлять файлы вручную при создании новых моментальных снимков. Дополнительные сведения см. в разделе [Доставка моментального снимка через FTP](../../relational-databases/replication/publish/deliver-a-snapshot-through-ftp.md).  
  
 **Веб-синхронизация**  
 Только репликация слиянием. Выберите **Разрешить синхронизацию подписчиков с помощью соединения с веб-сервером**задайте адрес веб-сервера, чтобы разрешить подписчикам слияний использовать веб-синхронизацию. Веб-сервер должен использовать протокол Secure Sockets Layer (SSL), а веб-адрес должен быть введен в полной форме, например https://server.domain.com/synchronize. Дополнительные сведения см. в разделе [Configure Web Synchronization](../../relational-databases/replication/configure-web-synchronization.md).  
  
## См. также:  
 [Создание публикации](../../relational-databases/replication/publish/create-a-publication.md)   
 [Просмотр и изменение свойств публикации](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Просмотр и изменение свойств подписки по запросу](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)   
 [Просмотр и изменение свойств принудительной подписки](../../relational-databases/replication/view-and-modify-push-subscription-properties.md)   
 [Создание и применение исходного моментального снимка](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)   
 [Публикация данных и объектов базы данных](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  