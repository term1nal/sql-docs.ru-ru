---
title: "Просмотр или изменение расположения по умолчанию для файлов данных и журнала (среда SQL Server Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "03/23/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "файлы журналов [SQL Server], изменение расположения по умолчанию"
  - "файлы данных [SQL Server], изменение расположения по умолчанию"
ms.assetid: 70a57fda-fcfe-490f-9cf6-5df620e32b2a
caps.latest.revision: 16
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
---
# Просмотр или изменение расположения по умолчанию для файлов данных и журнала (среда SQL Server Management Studio)
  Данный раздел описывает функции просмотра и изменения расположений по умолчанию для новых файлов данных и файлов журнала в [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] с помощью [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Путь по умолчанию берется из реестра. После изменения местоположения все новые базы данных, созданные в экземпляре [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , будут использовать это местоположение, если не указано другое местоположение.  
  
 
##  <a name="Recommendations"></a> Рекомендации  
 Рекомендуемым способом защиты файлов данных и журналов является защита с помощью списков управления доступом (ACL). Задайте в качестве расположения списков ACL корневой каталог, где создаются файлы.  
  
  
## Просмотр или изменение расположений по умолчанию для файлов базы данных  
  
1.  В обозревателе объектов щелкните правой кнопкой мыши сервер и выберите **Свойства**.  
  
2.  На странице "Свойства" левой панели откройте вкладку **Параметры базы данных**.  
  
3.  В области **Места хранения, используемые базой данных по умолчанию**можно просмотреть текущие расположения, используемые по умолчанию для новых файлов данных и файлов журнала. Чтобы изменить местоположение по умолчанию, введите новый путь по умолчанию в поле **Данные** или **Журнал** или нажмите кнопку обзора, перейдите к нужному пути и выберите его.  
  
>**ПРИМЕЧАНИЕ.** После смены расположений необходимо остановить и запустить службу SQL Server для завершения изменения.  
  
## См. также:  
 [CREATE DATABASE (SQL Server Transact-SQL)](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [Создание базы данных](../../relational-databases/databases/create-a-database.md)  
  
  