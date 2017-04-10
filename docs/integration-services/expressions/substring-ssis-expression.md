---
title: "SUBSTRING (выражение служб SSIS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "SUBSTRING, функция"
  - "часть возвращенного выражения [службы Integration Services]"
ms.assetid: 3a46748a-f5f8-4a6c-9108-673666754068
caps.latest.revision: 34
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 34
---
# SUBSTRING (выражение служб SSIS)
  Возвращает часть символьного выражения, начинающегося с указанной позиции и имеющего указанную длину. Параметр *position* и параметр *length* должны иметь значение, выраженное целым числом.  
  
## Синтаксис  
  
```  
  
SUBSTRING(character_expression, position, length)  
```  
  
## Аргументы  
 *character_expression*  
 Символьное выражение, из которого извлекаются символы.  
  
 *position*  
 Является целым числом, указывающим, где начинается подстрока.  
  
 *длина*  
 Является целым числом, указывающим длину подстроки в виде числа символов.  
  
## Типы результата  
 DT_WSTR  
  
## Замечания  
 SUBSTRING использует однобазовый индекс. Если параметр *position* имеет значение 1, то подстрока начинается с первого символа в значении параметра *character_expression*.  
  
 Функция SUBSTRING работает только типом данных DT_WSTR. Аргумент *character_expression*, являющийся строковым литералом или столбцом данных с типом данных DT_STR, неявно приведен к типу данных DT_WSTR до выполнения функции SUBSTRING. Прочие типы данных должны быть явно приведены к типу данных DT_WSTR. Дополнительные сведения см. в разделах [Типы данных служб Integration Services](../../integration-services/data-flow/integration-services-data-types.md) и [Приведение (выражение служб SSIS)](../../integration-services/expressions/cast-ssis-expression.md).  
  
 Функция SUBSTRING возвращает нулевой результат при нулевом аргументе.  
  
 Переменные и столбцы могут использовать все аргументы выражения.  
  
 Аргумент *length* может превышать длину строки. В этом случае функция возвращает остаток строки.  
  
## Примеры выражений  
 Этот пример возвращает из строкового литерала два символа, начинающихся с 4. Возвращаемый результат — «ph».  
  
```  
SUBSTRING("elephant",4,2)  
```  
  
 Этот пример возвращает остаток строкового литерала, начиная с четвертого символа. Возвращаемый результат — «phant». Превышение аргументом *length* размера строки не является ошибкой.  
  
```  
SUBSTRING ("elephant",4,50)  
```  
  
 Этот пример возвращает первую букву из столбца **MiddleName** .  
  
```  
SUBSTRING(MiddleName,1,1)  
```  
  
 Этот пример использует переменные в аргументах *position* и *length* . Если **Start** равно 1, и **Length** равно 5, то функция возвращает первые пять символов столбца **Name** .  
  
```  
SUBSTRING(Name,@Start,@Length)  
```  
  
 Этот пример возвращает четыре последних символа переменной **PostalCode** , начиная с шестого символа.  
  
```  
SUBSTRING (@PostalCode,6,4)  
```  
  
 Этот пример возвращает строку с нулевой длиной из строкового литерала.  
  
```  
SUBSTRING ("Redmond",4,0)  
```  
  
## См. также  
 [Функции (выражение служб SSIS)](../../integration-services/expressions/functions-ssis-expression.md)  
  
  