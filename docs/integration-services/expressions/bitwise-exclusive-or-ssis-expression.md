---
title: "^ (битовое исключающее ИЛИ) (выражение служб SSIS) | Microsoft Docs"
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
  - "^ (оператор побитового исключающего ИЛИ)"
  - "побитовое исключающее ИЛИ (^)"
ms.assetid: 6ac53cab-29c4-4835-9f87-371b058b2f38
caps.latest.revision: 37
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 37
---
# ^ (битовое исключающее ИЛИ) (выражение служб SSIS)
  Выполняет побитовую исключающую операцию ИЛИ для двух целочисленных значений. Она сравнивает каждый бит первого операнда с соответствующим битом второго операнда. Если один из битов равен 0, а второй равен 1, соответствующий бит результата устанавливается в 1. Если оба бита равны 0 или оба бита равны 1, соответствующий бит результата равен 0.  
  
 Оба условия должны относиться либо к целым числам со знаком, либо к беззнаковым целым числам.  
  
## Синтаксис  
  
```  
  
integer_expression1 ^ integer_expression2  
  
```  
  
## Аргументы  
 *integer_expression1, integer_expression2*  
 Любое допустимое выражение: либо целое число со знаком, либо беззнаковое целое число. Дополнительные сведения см. в статье [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
## Типы результата  
 Определяются типами данных обоих аргументов. Дополнительные сведения см. в разделе [Integration Services Data Types in Expressions](../../integration-services/expressions/integration-services-data-types-in-expressions.md).  
  
## Замечания  
 Если значение любого из условий — NULL, то результат выражения тоже будет NULL.  
  
## Примеры выражений  
 Этот пример выполняет битовую монопольную операцию ИЛИ над переменными **NumberA** и **NumberB**. **NumberA** содержит 3 (00000011), а **NumberB** — 7 (00000111).  
  
```  
@NumberA ^ @NumberB  
```  
  
 Результатом вычисления выражения будет 4 (00000100).  
  
 00000011  
  
 00000111  
  
 ----------\-  
  
 00000100  
  
 Этот пример производит побитовую исключающую операцию ИЛИ между столбцами **ReorderPoint** и **SafetyStockLevel** .  
  
```  
ReorderPoint ^ SafetyStockLevel  
```  
  
 Если **ReorderPoint** имеет значение 10, а **SafetyStockLevel** — значение 8, результат вычисления выражения равен 2 (00000010).  
  
 00001010  
  
 00001000  
  
 ----------\-  
  
 00000010  
  
 Этот пример выполняет побитовую исключающую операцию ИЛИ между двумя целыми числами.  
  
```  
3 ^ 5   
```  
  
 Результатом выполнения выражения будет 6 (00000110).  
  
 00000011  
  
 00000101  
  
 ----------\-  
  
 00000110  
  
## См. также  
 [&#124;&#124; (логическое ИЛИ) (выражение служб SSIS)](../../integration-services/expressions/logical-or-ssis-expression.md)   
 [&#124; (битовое включающее ИЛИ) (выражение служб SSIS)](../../integration-services/expressions/bitwise-inclusive-or-ssis-expression.md)   
 [Очередность и ассоциативность операторов](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Операторы (выражение служб SSIS)](../../integration-services/expressions/operators-ssis-expression.md)  
  
  