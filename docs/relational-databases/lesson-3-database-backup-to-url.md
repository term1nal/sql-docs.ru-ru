---
title: "Занятие&#160;3. резервное копирование базы данных по URL-адресу | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-backup-restore"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: a9ae1501-b614-49d3-b975-6569da8350b2
caps.latest.revision: 16
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 16
---
# Занятие&#160;3. резервное копирование базы данных по URL-адресу
На этом занятии выполняется резервное копирование базы данных AdventureWorks2014 в локальном экземпляре SQL Server 2016 в контейнер Azure, созданный на [занятии 1: создание хранимой политики доступа и подписанного URL-адреса в контейнере Azure](../relational-databases/lesson-1-create-stored-access-policy-and-shared-access-signature.md).  
  
> [!NOTE]  
> Если необходимо выполнить резервное копирование базы данных SQL Server 2012 с пакетом обновления 1 (SP1) и накопительным пакетом обновления 2 или более поздней версии либо базы данных SQL Server 2014 в этот контейнер Azure, можно воспользоваться устаревшим синтаксисом, который описывается [здесь](https://technet.microsoft.com/en-US/library/dn435916(v=sql.120).aspx). Таким образом можно выполнить резервное копирование по URL-адресу с помощью синтаксиса WITH CREDENTIAL.  
  
Чтобы выполнить резервное копирование в хранилище BLOB-объектов, выполните указанные ниже действия.  
  
1.  Подключитесь к среде Microsoft SQL Server Management Studio.  
  
2.  Откройте новое окно запроса и подключитесь к экземпляру SQL Server 2016 ядра СУБД в виртуальной машине Azure.  
  
3.  Скопируйте и вставьте приведенный ниже скрипт Transact-SQL в окне запроса. Измените URL-адрес в соответствии с именем учетной записи хранения и контейнером, которые были указаны на занятии 1, а затем выполните этот скрипт.  
  
    ```  
  
    -- To permit log backups, before the full database backup, modify the database to use the full recovery model.  
    USE master;  
    ALTER DATABASE AdventureWorks2014  
       SET RECOVERY FULL;  
  
    -- Back up the full AdventureWorks2014 database to the container that you created in Lesson 1  
    BACKUP DATABASE AdventureWorks2014   
       TO URL = 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/AdventureWorks2014_onprem.bak'  
  
    ```  
  
4.  Откройте обозреватель объектов и подключитесь к хранилищу Azure с помощью учетной записи хранения и ключа учетной записи.  
  
5.  Разверните узел "Контейнеры", разверните контейнер, созданный на занятии 1, и убедитесь в том, что резервная копия из шага 3 отображается в нем.  
  
    ![On-premises backup file appears as blob in Azure container](../relational-databases/media/0d060e51-012f-4c61-ab8d-16d461d0ffad.JPG "On-premises backup file appears as blob in Azure container")  
  
**Следующее занятие:**  
  
[Занятие 4. Восстановление базы данных в виртуальной машине с URL-адреса](../relational-databases/lesson-4-restore-database-to-virtual-machine-from-url.md)  
  