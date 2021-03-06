---
title: 64-разрядные целочисленные структуры | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- C data types [ODBC], 64-bit integer structures
- data types [ODBC], C data types
- 64-bit integer structures [ODBC]
ms.assetid: ac80c798-d9b2-4430-85ed-bd2461db0ac7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ac1a80e94d225b26cf879b27bdb0e138e0b0d1d9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/01/2018
ms.locfileid: "47692202"
---
# <a name="64-bit-integer-structures"></a>64-разрядные целочисленные структуры
_Int64 принадлежит к типу C SQL_C_SBIGINT и SQL_C_UBIGINT идентификаторы типа данных на компиляторы Microsoft C. При использовании компилятора, отличный от компилятора Microsoft® C тип C может отличаться. Если компилятор имеет встроенную поддержку 64-разрядных целых чисел, драйвера или приложения следует определить ODBCINT64 как тип собственного 64-разрядное целое число. Если компилятор не поддерживает 64-разрядных целых чисел, приложения или драйвера можно определить следующие структуры, чтобы гарантировать, что доступ к этим данным:  
  
```  
typedef struct{  
SQLUINTEGER dwLowWord;  
SQLUINTEGER dwHighWord;  
} SQLUBIGINT  
  
typedef struct{  
SQLUINTEGER dwLowWord;  
SQLINTEGER sdwHighWord;  
} SQLBIGINT  
```  
  
 Эти структуры должны быть выровнены для 8-байтовой границе, так как 64-разрядное целое число выравнивается по 8-байтовой границе.
