---
title: "INDEXKEY_PROPERTY (Transact-SQL) | Документы Microsoft"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- INDEXKEY_PROPERTY_TSQL
- INDEXKEY_PROPERTY
dev_langs:
- TSQL
helpviewer_keywords:
- index keys [SQL Server]
- INDEXKEY_PROPERTY function
- viewing index keys
- displaying index keys
- keys [SQL Server], index
ms.assetid: 87c0c385-6b2d-4716-ac8c-a3ce6e8d89e9
caps.latest.revision: 32
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a4d15a653fbc4954a37e5124a7a24436738ef5c1
ms.contentlocale: ru-ru
ms.lasthandoff: 09/01/2017

---
# <a name="indexkeyproperty-transact-sql"></a>INDEXKEY_PROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Возвращает сведения о ключах индекса, Возвращает NULL для XML-индексов.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Вместо этого используйте [sys.index_columns &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md).  
  
 ![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
INDEXKEY_PROPERTY ( object_ID ,index_ID ,key_ID ,property )  
```  
  
## <a name="arguments"></a>Аргументы  
 *object_id*  
 Идентификатор таблицы или индексированного представления. *object_id* — **int**.  
  
 *index_ID*  
 Идентификатор индекса. *index_ID* — **int**.  
  
 *Идентификатор key_ID*  
 Позиция ключевого столбца индекса. *key_ID* — **int**.  
  
 *Свойство*  
 Имя свойства, для которого будут возвращены сведения. *Свойство* представляет собой строку символов и может принимать одно из следующих значений.  
  
|Значение|Description|  
|-----------|-----------------|  
|**ColumnId**|Идентификатор столбца в *key_ID* позиции индекса.|  
|**IsDescending**|Порядок, в котором хранится индексированный столбец:<br /><br /> 1 = по убыванию; 0 = по возрастанию.|  
  
## <a name="return-types"></a>Типы возвращаемых значений  
 **int**  
  
## <a name="exceptions"></a>Исключения  
 Возвращает значение NULL в случае ошибки или если участник не имеет разрешений для просмотра объекта.  
  
 Пользователь может просматривать только метаданные защищаемых объектов, которыми он владеет или на которые пользователю были предоставлены разрешения. Это означает, что встроенные функции, создающие метаданные, такие как INDEXKEY_PROPERTY, могут вернуть значение NULL в случае, если пользователь не имеет разрешений на объект. Дополнительные сведения см. в разделе [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="examples"></a>Примеры  
 В следующем примере показано, как можно вернуть оба свойства для индекса с идентификатором `1` и ключевым столбцом `1` в таблице `Production.Location`.  
  
```tsql  
USE AdventureWorks2012;  
GO  
SELECT   
    INDEXKEY_PROPERTY(OBJECT_ID('Production.Location', 'U'),  
        1,1,'ColumnId') AS [Column ID],  
    INDEXKEY_PROPERTY(OBJECT_ID('Production.Location', 'U'),  
        1,1,'IsDescending') AS [Asc or Desc order];  
```  
  
 Результирующий набор:  
  
```  
Column ID   Asc or Desc order   
----------- -----------------   
1           0  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>См. также:  
 [INDEX_COL &#40; Transact-SQL &#41;](../../t-sql/functions/index-col-transact-sql.md)   
 [INDEXPROPERTY (Transact-SQL)](../../t-sql/functions/indexproperty-transact-sql.md)   
 [sys.Objects &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.indexes (Transact-SQL)](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns (Transact-SQL)](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)  
  
  