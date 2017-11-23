---
title: "sys.sp_xtp_checkpoint_force_garbage_collection (Transact-SQL) | Документы Microsoft"
ms.custom: 
ms.date: 08/02/2016
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
- sys.sp_xtp_checkpoint_force_garbage_collection_TSQL
- sys.sp_xtp_checkpoint_force_garbage_collection
dev_langs: TSQL
helpviewer_keywords: sys.sp_xtp_checkpoint_force_garbage_collection
ms.assetid: 82b35b2b-edbd-44ac-9fc8-80695f2fd1df
caps.latest.revision: "11"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 80b82684ab06f2ba9e748808a2286b38cee9d044
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/17/2017
---
# <a name="sysspxtpcheckpointforcegarbagecollection-transact-sql"></a>sys.sp_xtp_checkpoint_force_garbage_collection (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  Помечает исходные файлы, используемые при выполнении операции слияния, регистрационным номером транзакции в журнале (LSN), после чего файлы больше не требуются и их можно собирать как мусор. Кроме того, перемещает файлы, связанный номер LSN которых меньше точки усечения журнала, в сборку мусора файлового потока.  
  
 ![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
 
## <a name="syntax"></a>Синтаксис  
  
```  
sys.sp_xtp_checkpoint_force_garbage_collection [[ @dbname=database_name]  
```  
  
## <a name="arguments"></a>Аргументы  
 *database_name*  
 База данных, в которой будет выполняться сборка мусора. Значение по умолчанию — текущая база данных.  
  
## <a name="return-code-values"></a>Значения кода возврата  
 0 — успешное завершение. Ненулевое значение — ошибка.  
  
## <a name="result-set"></a>Результирующий набор  
 Возвращаемая строка содержит следующие сведения.  
  
|Столбец|Description|  
|------------|-----------------|  
|num_collected_items|Отображает число файлов, которые были перенесены в сборку мусора файлового потока. Это файлы, номер LSN которых меньше номера LSN точки усечения журнала.|  
|num_marked_for_collection_items|Указывает количество файлов данных и разностных файлов, номер LSN которых был обновлен с использованием blockID журнала с конечным номером LSN журнала.|  
|last_collected_xact_seqno|Возвращает последний соответствующий номер LSN, до которого файлы были перенесены в сборку мусора файлового потока.|  
  
## <a name="permissions"></a>Permissions  
 Необходимо разрешение владельца базы данных.  
  
## <a name="sample"></a>Образец  
  
```  
exec [sys].[sp_xtp_checkpoint_force_garbage_collection] hkdb1  
```  
  
## <a name="see-also"></a>См. также:  
 [Системные хранимые процедуры (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Выполняющаяся в памяти OLTP (оптимизация в памяти)](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  