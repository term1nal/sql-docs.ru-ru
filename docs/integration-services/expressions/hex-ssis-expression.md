---
title: "HEX (выражение служб SSIS) | Microsoft Docs"
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
  - "шестнадцатеричные данные"
  - "HEX, функция"
ms.assetid: f5d471ee-aeef-421c-b6e1-55b9676c3842
caps.latest.revision: 36
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 36
---
# HEX (выражение служб SSIS)
  Возвращает строку, представляющую собой шестнадцатеричное значение целого числа.  
  
## Синтаксис  
  
```  
  
HEX(integer_expression)  
```  
  
## Аргументы  
 *integer_expression*  
 Целое со знаком или беззнаковое целое.  
  
## Типы результата  
 DT_WSTR  
  
## Замечания  
 HEX возвращает значение null, если *integer_expression* имеет значение NULL.  
  
 Аргумент *integer_expression* должен выдавать целое число. Дополнительные сведения см. в статье [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
 Возвращаемый результат не включает квалификаторы, например префикс 0х. Для включения префикса используйте оператор + (сцепление). Дополнительные сведения см. в разделе [+ (Объединение) (выражение SSIS)](../../integration-services/expressions/concatenate-ssis-expression.md).  
  
 Буквы A — F, используемые в шестнадцатеричной нотации, записываются в верхнем регистре.  
  
 Длина возвращаемой строки для целых типов данных:  
  
-   DT_I1 и DT_UI1 возвращают строку не более 2 символов.  
  
-   DT_I2 и DT_UI2 возвращают строку не более 4 символов.  
  
-   DT_I4 и DT_UI4 возвращают строку не более 8 символов.  
  
-   DT_I8 и DT_UI8 возвращают строку длиной не более 16 символов.  
  
## Примеры выражений  
 В этом примере используется числовой литерал. Функция возвращает значение 190.  
  
```  
HEX(400)   
```  
  
 Этот пример использует столбец **ReorderPoint** . Тип данных этого столбца — **smallint**. Если значение **ReorderPoint** равно 750, функция возвращает 2EE.  
  
```  
HEX(ReorderPoint)   
```  
  
 Этот пример использует системную переменную **LocaleID**. Если значение **LocaleID** равно 1049, функция возвращает 419.  
  
```  
HEX(@LocaleID)  
```  
  
## См. также  
 [Функции (выражение служб SSIS)](../../integration-services/expressions/functions-ssis-expression.md)  
  
  