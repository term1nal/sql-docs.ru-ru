---
title: "Защищаемые объекты | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "10/18/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.swb.roleproperties.selectobject.f1"
helpviewer_keywords: 
  - "защищаемые объекты [SQL Server]"
  - "схемы [SQL Server], защищаемые объекты"
  - "защищаемые объекты базы данных [SQL Server]"
  - "иерархии [SQL Server], защищаемые объекты"
  - "защищаемые объекты сервера [SQL Server]"
ms.assetid: bfa748f0-70b0-453c-870a-04b7b205b9ff
caps.latest.revision: 41
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 41
---
# Защищаемые объекты
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  К защищаемым объектами относятся ресурсы, доступ к которым регулируется системой авторизации компонента [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] . Например, защищаемым объектом является таблица. Некоторые защищаемые объекты могут храниться внутри других, создавая иерархии «областей», которые сами могут защищаться. К областям защищаемых объектов относятся **сервер**, **база данных**и **схема**.  
  
## Область защищаемых объектов: сервер  
 Область защищаемых объектов **сервера** содержит следующие защищаемые объекты:  
  
-   Группа доступности  
  
-   Конечная точка  
  
-   Имя входа  
  
-   Роль сервера  
  
-   база данных  
  
## Область защищаемых объектов: база данных  
 Область защищаемых объектов **базы данных** содержит следующие защищаемые объекты:  
  
-   Роль приложения  
  
-   Сборка  
  
-   Асимметричный ключ  
  
-   Сертификат  
  
-   Контракт  
  
-   Полнотекстовый каталог  
  
-   Полнотекстовый список стоп-слов  
  
-   тип сообщений;  
  
-   Привязка удаленной службы  
  
-   Роль (база данных)  
  
-   Маршрут  
  
-   схема  
  
-   Поиск в списке свойств  
  
-   Служба  
  
-   Симметричный ключ  
  
-   Пользователь  
  
## Область защищаемых объектов: схема  
 Область защищаемых объектов **схемы** содержит следующие защищаемые объекты:  
  
-   Тип  
  
-   Коллекция схем XML  
  
-   Объект — к классу объекта относятся следующие элементы:  
  
    -   Статистическое  
  
    -   Функция  
  
    -   Процедура  
  
    -   Очередь  
  
    -   Синоним  
  
    -   Таблица  
  
    -   Просмотр 
    
    -   Внешняя таблица 
  
## Управление доступом к защищаемому объекту  
 Сущность, которая получает разрешение на доступ к защищаемому объекту, именуется участником. Наиболее часто в роли участников выступают имена входа и пользователи базы данных. Управление доступом к защищаемым объектам осуществляется путем предоставления или отзыва разрешений либо путем добавления имен входа и пользователей к ролям, имеющим доступ. Сведения об управлении разрешениями см. в разделах [GRANT (Transact-SQL)](../../t-sql/statements/grant-transact-sql.md), [REVOKE (Transact-SQL)](../../t-sql/statements/revoke-transact-sql.md), [DENY (Transact-SQL)](../../t-sql/statements/deny-transact-sql.md), [Хранимая процедура sp_addrolemember (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md) и [sp_droprolemember (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md).  
  
> [!CAUTION]  
>  Разрешения по умолчанию, которые предоставляются системным объектам во время установки, тщательно оцениваются на предмет возможных угроз, и их не нужно будет изменять для защиты установки [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Любые изменения разрешений в системных объектах могут ограничить или нарушить функциональность, а также перевести установку [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] в неподдерживаемое состояние.  
  
## См. также  
 [Приступая к работе с разрешениями Database Engine](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)  
  
 [Обеспечение безопасности SQL Server](../../relational-databases/security/securing-sql-server.md)  
  
 [sys.database_principals (Transact-SQL)](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)  
  
 [sys.database_role_members (Transact-SQL)](../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)  
  
 [sys.server_principals (Transact-SQL)](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)  
  
 [sys.server_role_members (Transact-SQL)](../../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md)  
  
 [sys.sql_logins (Transact-SQL)](../../relational-databases/system-catalog-views/sys-sql-logins-transact-sql.md)  
  
  