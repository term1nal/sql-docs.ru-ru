---
title: "Разрешения для папок и файлов (службы Master Data Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "безопасность [службы Master Data Services], файл и папка"
  - "папки [службы Master Data Services]"
  - "файлы [службы Master Data Services]"
ms.assetid: 6402d81d-7349-47b1-95ca-99b0c0f4f373
caps.latest.revision: 10
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 10
---
# Разрешения для папок и файлов (службы Master Data Services)
  При установке [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]папки и файлы устанавливаются по указанному для общих компонентов [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] пути установки в файловой системе. При использовании пути установки общих компонентов [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] по умолчанию, путем установки для [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] будет *диск*:\Program Files\Microsoft SQL Server\130\Master Data Services. Хотя путь установки общих компонентов можно изменить, следует учитывать разрешения, наследуемые от родительской папки, а также явно заданные для [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]разрешения.  
  
## Наследуемые разрешения  
 Папка **Microsoft SQL Server** , папка **Master Data Services** , а также большинство вложенных папок и файлов наследуют разрешения родительской папки, заданной в программе установки [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Если было выбрано расположение установки по умолчанию, то родительской папкой, от которой наследуются разрешения, будет *диск*:\Program Files. В приведенной далее таблице описаны разрешения по умолчанию для папки **Program Files**.  
  
> [!NOTE]  
>  Если изменить разрешения по умолчанию для **Program Files** или выбрать другое расположение для установки, то папки и файлы [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] унаследуют разрешения соответствующей родительской папки, и эти разрешения могут отличаться от приведенных в таблице ниже.  
  
###### Разрешения по умолчанию для папки Program Files  
  
|Имя группы или учетной записи|Разрешения|  
|---------------------------|-----------------|  
|CREATOR OWNER|Специальные разрешения|  
|SYSTEM|Специальные разрешения|  
|Администраторы|Специальные разрешения|  
|Пользователи|Чтение и выполнение, Просмотр содержимого папки, Чтение|  
|TrustedInstaller|Просмотр содержимого папки, Специальные разрешения|  
  
## Явные разрешения  
 Папка **MDSTempDir** и файл [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] Web.config (в папке **WebApplication**) не наследуют разрешения. Для них разрешения задаются явно при установке [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], независимо от выбранного пути установки. Изменять эти разрешения не следует.  
  
###### Разрешения MDSTempDir  
  
|Имя группы или учетной записи|Permissions|  
|---------------------------|-----------------|  
|SYSTEM|Изменение, Чтение и выполнение, Просмотр содержимого папки, Чтение, Запись|  
|Администраторы|Изменение, Чтение и выполнение, Просмотр содержимого папки, Чтение, Запись|  
|MDS_ServiceAccounts|Изменение, Чтение и выполнение, Просмотр содержимого папки, Чтение, Запись|  
  
###### Разрешения Web.config  
  
|Имя группы или учетной записи|Permissions|  
|---------------------------|-----------------|  
|SYSTEM|Полный доступ, Изменение, Чтение и выполнение, Чтение, Запись|  
|Администраторы|Полный доступ, Изменение, Чтение и выполнение, Чтение, Запись|  
|MDS_ServiceAccounts|Чтение и выполнение, Чтение|  
  
 Дополнительные сведения о содержимом файла [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] Web.config см. в разделе [Раздел "Веб-конфигурация" (службы Master Data Services)](../master-data-services/web-configuration-reference-master-data-services.md).  
  
## См. также:  
 [Установка служб Master Data Services](../master-data-services/install-windows/install-master-data-services.md)  
  
  