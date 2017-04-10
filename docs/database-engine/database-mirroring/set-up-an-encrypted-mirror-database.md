---
title: "Настройка зашифрованной зеркальной базы данных | Microsoft Docs"
ms.custom: ""
ms.date: "03/06/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "криптография [SQL Server], зеркальное отображение базы данных"
  - "шифрование [SQL Server], зеркальное отображение базы данных"
  - "главный ключ базы данных [SQL Server], зеркальное отображение базы данных"
  - "зеркальная база данных [SQL Server]"
  - "зеркальное отображение базы данных [SQL Server], безопасность"
ms.assetid: 7329a575-be29-46e0-abc6-1344db37920c
caps.latest.revision: 24
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 24
---
# Настройка зашифрованной зеркальной базы данных
  Чтобы включить автоматическое шифрование главного ключа базы данных зеркальной базы данных, необходимо предоставить пароль, используемый для шифрования главного ключа экземпляра зеркального сервера. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] и более поздние версии включают в себя механизмы для передачи пароля. Перед началом зеркального отображения базы данных необходимо создать учетные данные для главного ключа базы данных с помощью хранимой процедуры **sp_control_dbmasterkey_password**. Необходимо повторить этот процесс для каждой базы данных, для которой будет создаваться зеркальное отображение. Дополнительные сведения см. в разделе [sp_control_dbmasterkey_password (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-control-dbmasterkey-password-transact-sql.md).  
  
> [!CAUTION]  
>  Не включайте дешифрование базы данных отработки отказа, оно не должно быть для **sa** и другим серверам-участникам с обширными правами доступа. База данных может быть настроена таким образом, чтобы иерархия ее ключей не могла быть расшифрована главным ключом службы. Эта возможность поддерживается для максимальной защиты баз данных, содержащих информацию, доступ к которой не может иметь **sa** или другие участники на уровне сервера с обширными правами доступа. Включение расшифровки отработки отказа для такой базы данных сводит на нет эту защиту, позволяя **sa** и другим привилегированным участникам на уровне сервера расшифровывать базу данных.  
  
## См. также:  
 [sp_control_dbmasterkey_password (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-control-dbmasterkey-password-transact-sql.md)   
 [CREATE MASTER KEY (Transact-SQL)](../../t-sql/statements/create-master-key-transact-sql.md)   
 [ALTER MASTER KEY (Transact-SQL)](../../t-sql/statements/alter-master-key-transact-sql.md)   
 [Иерархия средств шифрования](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [Настройка зеркального отображения базы данных (SQL Server)](../../database-engine/database-mirroring/setting-up-database-mirroring-sql-server.md)  
  
  