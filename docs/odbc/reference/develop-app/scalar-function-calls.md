---
title: Вызовы скалярных функций | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- escape sequences [ODBC], scalar function calls
ms.assetid: 10cb4dcf-4cd8-4a56-8725-d080bd3ffe47
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 54615676558165e4044e99bf9452ce8e8a333170
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/01/2018
ms.locfileid: "47704302"
---
# <a name="scalar-function-calls"></a>Вызовы скалярных функций
Скалярные функции возвращают значение для каждой строки. Например скалярная функция абсолютное значение принимает числовой столбец в качестве аргумента и возвращает абсолютное значение каждого значения в столбце. Escape-последовательность для вызова скалярной функции  
  
 **{fn***скалярная функция* **}**   
  
 где *скалярная функция* — одна из функций, перечисленных в [скалярные функции в приложении E:](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md). Дополнительные сведения об escape-последовательность скалярной функции, см. в разделе [escape-последовательность скалярной функции](../../../odbc/reference/appendixes/scalar-function-escape-sequence.md) в грамматике SQL в C: приложение.  
  
 Например следующие инструкции SQL создать тот же результирующий набор в верхнем регистре клиента имена. В первой инструкции используется синтаксис escape последовательности. Вторая инструкция имеет собственный синтаксис для Ingres для OS/2 и не поддерживает взаимодействие.  
  
```  
SELECT {fn UCASE(Name)} FROM Customers  
  
SELECT uppercase(Name) FROM Customers  
```  
  
 Приложение можно смешивать вызовы скалярных функций, которые используют собственный синтаксис и вызовы скалярных функций, которые используют синтаксис ODBC. Например предположим, что имена в таблице сотрудников хранятся в виде фамилия, запятая и имя. Следующая инструкция SQL создает результирующий набор фамилий сотрудников в таблице сотрудников. В инструкции используется скалярная функция ODBC **ПОДСТРОКИ** и скалярную функцию SQL Server **CHARINDEX** и будет правильно выполняться только на сервере SQL Server.  
  
```  
SELECT {fn SUBSTRING(Name, 1, CHARINDEX(',', Name) – 1)} FROM Customers  
```  
  
 Для максимальной совместимости приложения должны использовать **преобразовать** скалярную функцию, чтобы убедиться в том, что результат скалярной функции будет требуемого типа. **Преобразовать** функция преобразует данные из одного типа данных SQL в указанный тип данных SQL. Синтаксис **преобразовать** функция  
  
 **ПРЕОБРАЗОВАНИЕ (** *value_exp* **,** *data_type ***)**  
  
 где *value_exp* является именем столбца, результат другой скалярной функцией, или значение литерала и *data_type* является ключевое слово, которое соответствует **#define** имя, используемое по Тип данных SQL идентификатором, как определено в [типы данных приложение D:](../../../odbc/reference/appendixes/appendix-d-data-types.md). Например, следующая инструкция SQL использует **преобразовать** функции, чтобы убедиться в том, что выходные данные **функция CURDATE** функция является датой, вместо данных отметки времени или символ:  
  
```  
INSERT INTO Orders (OrderID, CustID, OpenDate, SalesPerson, Status)  
   VALUES (?, ?, {fn CONVERT({fn CURDATE()}, SQL_DATE)}, ?, ?)  
```  
  
 Чтобы определить, скалярные функции, которые поддерживаются источником данных, приложение вызывает **SQLGetInfo** с SQL_CONVERT_FUNCTIONS, SQL_NUMERIC_FUNCTIONS, SQL_STRING_FUNCTIONS, SQL_SYSTEM_FUNCTIONS и SQL_TIMEDATE_ Параметры функции. Чтобы определить, какие операции преобразования поддерживаются **преобразовать** приложение вызывает функцию, **SQLGetInfo** с любой из параметров, которые начинаются с SQL_CONVERT.
