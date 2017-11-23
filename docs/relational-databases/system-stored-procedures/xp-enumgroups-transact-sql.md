---
title: "xp_enumgroups (Transact-SQL) | Документы Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- xp_enumgroups_TSQL
- xp_enumgroups
dev_langs: TSQL
helpviewer_keywords: xp_enumgroups
ms.assetid: 0bd3ed36-e260-469c-a5ff-b033fb9ea59d
caps.latest.revision: "23"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 95f116674e5698ebf841f0731ef4a93566113e9a
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/21/2017
---
# <a name="xpenumgroups-transact-sql"></a>xp_enumgroups (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Предоставляет список локальных групп Microsoft Windows или список глобальных групп, определенных в указанном домене Windows.  
  
||  
|-|  
|**Область применения**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (с[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] до [текущей версии](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
xp_enumgroups [ 'domain_name' ]  
```  
  
## <a name="arguments"></a>Аргументы  
 **"** *имя_домена* **"**  
 Имя домена Windows, для которого перечисляется список глобальных групп. *имя_домена* — **sysname**, значение по умолчанию NULL.  
  
## <a name="return-code-values"></a>Значения кода возврата  
 0 (успешное завершение) или 1 (неуспешное завершение)  
  
## <a name="result-sets"></a>Результирующие наборы  
  
|Имя столбца|Тип данных|Description|  
|-----------------|---------------|-----------------|  
|**группы**|**sysname**|Имя группы Windows|  
|**комментарий**|**sysname**|Описание группы Windows, предоставленное Windows|  
  
## <a name="remarks"></a>Замечания  
 Если *имя_домена* имя компьютера под управлением Windows, экземпляр [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] находится под управлением, или имя домена не указано, **xp_enumgroups** перечисляет локальные группы с компьютера под управлением [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **xp_enumgroups** не может использоваться при создании экземпляра [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] работает в Windows 98.  
  
## <a name="permissions"></a>Permissions  
 Требуется членство в **db_owner** предопределенной роли базы данных в **master** базы данных или членство в **sysadmin** предопределенной роли сервера.  
  
## <a name="examples"></a>Примеры  
 В следующем примере перечисляются группы в домене `sales`.  
  
```  
EXEC xp_enumgroups 'sales';  
```  
  
## <a name="see-also"></a>См. также:  
 [Хранимая процедура sp_grantlogin (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [Хранимая процедура sp_revokelogin (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)   
 [Системные хранимые процедуры (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Общие расширенные хранимые процедуры &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)   
 [xp_loginconfig &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/xp-loginconfig-transact-sql.md)   
 [xp_logininfo &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/xp-logininfo-transact-sql.md)  
  
  