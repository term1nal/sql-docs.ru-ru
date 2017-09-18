---
title: "Append-метод (ADOX столбцы) | Документы Microsoft"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Columns::raw_Append
- Columns::Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 7a46d23c-efef-4ec7-815d-cd3ac86787dd
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7c6c9323dbc1e3c69445dc09ad06373856fb67bc
ms.contentlocale: ru-ru
ms.lasthandoff: 09/09/2017

---
# <a name="append-method-adox-columns"></a>Append-метод (ADOX столбцы)
Добавляет новый [столбца](../../../ado/reference/adox-api/column-object-adox.md) объект [столбцы](../../../ado/reference/adox-api/columns-collection-adox.md) коллекции.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
Columns.Append Column [,Type] [,DefinedSize]  
```  
  
#### <a name="parameters"></a>Параметры  
 *Столбец*  
 **Столбца** добавляемый объект или имя столбца для создания и добавления.  
  
 *Тип*  
 Необязательно. Объект **длинные** значение, которое указывает тип данных столбца. *Тип* параметр соответствует параметру [тип](../../../ado/reference/adox-api/type-property-column-adox.md) свойство **столбца** объекта.  
  
 *DefinedSize*  
 Необязательно. Объект **длинные** значение, указывающее размер столбца. *DefinedSize* параметр соответствует параметру [DefinedSize](../../../ado/reference/adox-api/definedsize-property-adox.md) свойство **столбца** объекта.  
  
> [!NOTE]
>  Произойдет ошибка при наращивании **столбца** для **столбцы** коллекцию [индекс](../../../ado/reference/adox-api/index-object-adox.md) Если **столбца** не существует в [Таблицы](../../../ado/reference/adox-api/table-object-adox.md) , добавляется к уже [таблиц](../../../ado/reference/adox-api/tables-collection-adox.md) коллекции.  
  
## <a name="applies-to"></a>Объект применения  
 [Коллекция столбцов (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)  
  
## <a name="see-also"></a>См. также:  
 [Столбцы и таблицы добавьте методы примера имя свойства (Visual Basic)](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [Ключи добавить метод, тип ключа, RelatedColumn, RelatedTable и UpdateRule-пример свойства (Visual Basic)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Пример свойства ParentCatalog (Visual Basic)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [Append-метод (ADOX группы)](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Append-метод (ADOX индексы)](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Append-метод (ADOX ключи)](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append-метод (ADOX процедур)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Append-метод (ADOX таблицы)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append-метод (ADOX пользователей)](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Append-метод (ADOX представления)](../../../ado/reference/adox-api/append-method-adox-views.md)