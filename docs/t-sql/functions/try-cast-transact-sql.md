---
title: "TRY_CAST (Transact-SQL) | Документы Microsoft"
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
- TRY_CAST_TSQL
- TRY_CAST
dev_langs:
- TSQL
helpviewer_keywords:
- TRY_CAST function
ms.assetid: ea3a16de-995b-415c-b5f0-9355cf7bb401
caps.latest.revision: 10
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 09c5b6060798f28541f61e763954ed44920cf83d
ms.contentlocale: ru-ru
ms.lasthandoff: 09/01/2017

---
# <a name="trycast-transact-sql"></a>TRY_CAST (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Возвращает значение, приведенное к указанному типу, если приведение проходит успешно; в противном случае возвращает NULL.  
  
 ![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
TRY_CAST ( expression AS data_type [ ( length ) ] )  
```  
  
## <a name="arguments"></a>Аргументы  
 *expression*  
 Приводимое значение. Любое допустимое выражение.  
  
 *Тип данных*  
 Тип данных, к которому следует привести *выражение*.  
  
 *length*  
 Необязательное целое число, обозначающее длину целевого типа данных.  
  
 Диапазон допустимых значений определяется по значению *data_type*.  
  
## <a name="return-types"></a>Типы возвращаемых значений  
 Возвращает значение, приведенное к указанному типу, если приведение проходит успешно; в противном случае возвращает NULL.  
  
## <a name="remarks"></a>Замечания  
 **TRY_CAST** принимает переданное значение и пытается привести его в указанный *data_type*. Если приведение выполнено успешно, **TRY_CAST** возвращает значение, что и заданный *data_type*; при возникновении ошибки возвращается значение null. Однако если запрашивается преобразования, которая явно не разрешена, затем **TRY_CAST** завершается с ошибкой.  
  
 **TRY_CAST** не новые зарезервированным ключевым словом и доступно на всех уровнях совместимости. **TRY_CAST** имеет ту же семантику, что **TRY_CONVERT** при соединении с удаленными серверами.  
  
## <a name="examples"></a>Примеры  
  
### <a name="a-trycast-returns-null"></a>A. TRY_CAST возвращает NULL  
 В следующем примере показано, что TRY_CAST возвращает значение NULL, если не удается выполнить приведение.  
  
```tsql  
SELECT   
    CASE WHEN TRY_CAST('test' AS float) IS NULL   
    THEN 'Cast failed'  
    ELSE 'Cast succeeded'  
END AS Result;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
------------  
Cast failed  
  
(1 row(s) affected)  
```  
  
 В следующем примере показано, что выражение должно иметь ожидаемый формат.  
  
```tsql  
SET DATEFORMAT dmy;  
SELECT TRY_CAST('12/31/2010' AS datetime2) AS Result;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
----------------------  
NULL  
  
(1 row(s) affected)  
```  
  
### <a name="b-trycast-fails-with-an-error"></a>Б. TRY_CAST завершается с ошибкой  
 В следующем примере показано, что TRY_CAST возвращает ошибку, если явное приведение недопустимо.  
  
```tsql  
SELECT TRY_CAST(4 AS xml) AS Result;  
GO  
```  
  
 Результатом выполнения этой инструкции будет ошибка, так как целое число не может быть приведено к типу данных XML.  
  
```  
Explicit conversion from data type int to xml is not allowed.  
```  
  
### <a name="c-trycast-succeeds"></a>В. TRY_CAST выполнено успешно  
 В этом примере показано, что выражение должно иметь ожидаемый формат.  
  
```  
SET DATEFORMAT mdy;  
SELECT TRY_CAST('12/31/2010' AS datetime2) AS Result;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
----------------------------------  
2010-12-31 00:00:00.0000000  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>См. также:  
 [TRY_CONVERT &#40; Transact-SQL &#41;](../../t-sql/functions/try-convert-transact-sql.md)   
 [Функции CAST и CONVERT (Transact-SQL)](../../t-sql/functions/cast-and-convert-transact-sql.md)  
  
  