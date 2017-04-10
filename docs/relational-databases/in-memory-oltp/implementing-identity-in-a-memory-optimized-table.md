---
title: "Реализация IDENTITY в таблице, оптимизированной для памяти | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine-imoltp"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c0a704a3-3a31-4c2c-b967-addacda62ef8
caps.latest.revision: 11
author: "MightyPen"
ms.author: "genemi"
manager: "jhubbard"
caps.handback.revision: 11
---
# Реализация IDENTITY в таблице, оптимизированной для памяти
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

IDENTITY поддерживается в оптимизированной для памяти таблице, если и начальное значение, и шаг приращения равны 1 (по умолчанию). Столбцы идентификаторов с определением IDENTITY(x, y), где x != 1 или y != 1 в таблицах, оптимизированных для памяти, не поддерживаются.   
    
Чтобы увеличить начальное значение IDENTITY, вставьте новую строку с явным значением в столбце идентификаторов с помощью параметра сеанса `SET IDENTITY_INSERT table_name ON`. При вставке строки начальное значение IDENTITY меняется на явно добавленное значение плюс 1. Например, чтобы увеличить начальное значение до 1000, вставьте строку со значением 999 в столбце идентификаторов. Создаваемые значения идентификаторов будут начинаться с 1000.     
  
## См. также:  
 [Миграция в In-Memory OLTP](../../relational-databases/in-memory-oltp/migrating-to-in-memory-oltp.md)  
  
  