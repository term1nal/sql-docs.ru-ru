---
title: "Выбор серверов для настройки (мастер настройки безопасности зеркального отображения баз данных) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.swb.configdbmsecurwiz.choosesrvrs.f1"
ms.assetid: 59e23ff3-d7ee-4e32-9629-0b54d3a258f7
caps.latest.revision: 25
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 25
---
# Выбор серверов для настройки (мастер настройки безопасности зеркального отображения баз данных)
  Используйте данную страницу для задания экземпляров сервера, которые нужно настроить в текущий момент. Перед продолжением выполнения мастера необходимо выбрать хотя бы один экземпляр сервера.  
  
 При снятии флажка для экземпляра сервера мастер не внесет в него никаких изменений. Мастер, однако, выдаст приглашение для ввода данных о данном экземпляре и сохранит эти данные в составе конфигурации других экземпляров сервера. Например, если снять этот флажок для экземпляра следящего сервера, мастер выдаст запрос на ввод учетной записи службы [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] свидетеля, поскольку имя входа для этой учетной записи необходимо создать как часть конфигурации безопасности, сохраненной в экземплярах основного и зеркального сервера.  
  
 **Настройка зеркального отображения базы данных в среде SQL Server Management Studio**  
  
-   [Создание сеанса зеркального отображения базы данных с использованием проверки подлинности Windows (среда SQL Server Management Studio)](../../database-engine/database-mirroring/establish database mirroring session - windows authentication.md)  
  
-   [Запуск мастера настройки безопасности зеркального отображения баз данных (среда SQL Server Management Studio)](../../database-engine/database-mirroring/start the configuring database mirroring security wizard.md)  
  
## Параметры  
 **Экземпляр основного сервера**  
 Выберите этот пункт для настройки безопасности основного сервера.  
  
 **Экземпляр зеркального сервера**  
 Выберите этот пункт для настройки безопасности зеркального сервера.  
  
 **Экземпляр следящего сервера**  
 Выберите этот пункт для настройки безопасности следящего сервера (при его наличии).  
  
## См. также:  
 [Свойства базы данных (страница "Зеркальное отображение")](../../relational-databases/databases/database-properties-mirroring-page.md)   
 [Зеркальное отображение базы данных (SQL Server)](../../database-engine/database-mirroring/database-mirroring-sql-server.md)  
  
  