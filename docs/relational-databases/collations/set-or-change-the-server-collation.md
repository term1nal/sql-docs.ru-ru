---
title: "Задание или изменение параметров сортировки сервера | Microsoft Docs"
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
  - "параметры сортировки сервера [SQL Server]"
  - "параметры сортировки [SQL Server], сервер"
ms.assetid: 3242deef-6f5f-4051-a121-36b3b4da851d
caps.latest.revision: 34
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 34
---
# Задание или изменение параметров сортировки сервера
  Параметры сортировки сервера применяются по умолчанию для всех установленных системных баз данных с экземпляром [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], а также для новых пользовательских баз данных. Параметры сортировки сервера задаются во время установки [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Дополнительные сведения см. в статье [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md).  
  
## Изменение параметров сортировки сервера  
 Чтобы изменить параметры сортировки по умолчанию для экземпляра [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (эта операция может оказаться сложной), выполните следующие шаги:  
  
-   Проверьте наличие данных и скриптов, необходимых для повторного создания пользовательской базы данных и всех ее объектов.  
  
-   Экспортируйте все данные с помощью такого средства, как [bcp Utility](../../tools/bcp-utility.md). Дополнительные сведения см. в разделе [Массовый импорт и экспорт данных (SQL Server)](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md).  
  
-   Удалите все пользовательские базы данных.  
  
-   Перестройте базу данных master, указав новые параметры сортировки в свойстве SQLCOLLATION команды **setup**. Например:  
  
    ```  
    Setup /QUIET /ACTION=REBUILDDATABASE /INSTANCENAME=InstanceName   
    /SQLSYSADMINACCOUNTS=accounts /[ SAPWD= StrongPassword ]   
    /SQLCOLLATION=CollationName  
    ```  
  
     Дополнительные сведения см. в статье [Перестроение системных баз данных](../../relational-databases/databases/rebuild-system-databases.md).  
  
-   Создайте все базы данных и все их объекты.  
  
-   Импортируйте все данные.  
  
> [!NOTE]  
>  Вместо изменения параметров сортировки по умолчанию для всего экземпляра [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] можно указывать параметры сортировки по умолчанию для каждой новой базы данных.  
  
## См. также:  
 [Поддержка параметров сортировки и Юникода](../../relational-databases/collations/collation-and-unicode-support.md)   
 [Установка и изменение параметров сортировки базы данных](../../relational-databases/collations/set-or-change-the-database-collation.md)   
 [Задание или изменение параметров сортировки столбца](../../relational-databases/collations/set-or-change-the-column-collation.md)   
 [Перестроение системных баз данных](../../relational-databases/databases/rebuild-system-databases.md)  
  
  