---
title: "LTRIM (выражение служб SSIS) | Microsoft Docs"
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
  - "начальные пробелы"
  - "LTRIM, функция"
ms.assetid: d082f42a-d7e7-49f5-a503-ac44ba630832
caps.latest.revision: 33
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 33
---
# LTRIM (выражение служб SSIS)
  Возвращает символьное выражение после удаления начальных пробелов.  
  
> [!NOTE]  
>  Функция LTRIM не удаляет такие пробельные символы, как табуляция или перевод строки. Юникод обеспечивает элементы кода для множества различных типов пробелов, однако данная функция распознает только элемент кода 0x0020 в Юникоде. Если строки двухбайтовой кодировки (DBCS) преобразованы в Юникод, они могут включать пробелы, отличные от 0x0020. Тогда функция не в состоянии удалить такие пробелы. Для удаления всех типов пробелов можно использовать метод LTrim Microsoft Visual Basic .NET в скрипте, запускаемом из компонента скриптов.  
  
## Синтаксис  
  
```  
  
LTRIM(character expression)  
```  
  
## Аргументы  
 *character_expression*  
 Символьное выражение, из которого удаляются пробелы.  
  
## Типы результата  
 DT_WSTR  
  
## Замечания  
 Функция LTRIM работает только с типом данных DT_WSTR. Аргумент *character_expression*, являющийся строковым литералом или столбцом данных с типом данных DT_STR, неявно приведен к типу данных DT_WSTR до выполнения функции LTRIM. Прочие типы данных должны быть явно приведены к типу данных DT_WSTR. Дополнительные сведения см. в разделах [Типы данных служб Integration Services](../../integration-services/data-flow/integration-services-data-types.md) и [Приведение (выражение служб SSIS)](../../integration-services/expressions/cast-ssis-expression.md).  
  
 Функция LTRIM возвращает значение NULL, если аргумент принимает значение NULL.  
  
## Примеры выражений  
 Этот пример удаляет начальные пробелы из строкового литерала. Возвращаемый результат — «Hello».  
  
```  
LTRIM("    Hello")  
```  
  
 Этот пример удаляет начальные пробелы из столбца **FirstName** .  
  
```  
LTRIM(FirstName)  
```  
  
 Этот пример удаляет начальные пробелы из переменной **FirstName** .  
  
```  
LTRIM(@FirstName)  
```  
  
## См. также  
 [RTRIM (выражение служб SSIS)](../../integration-services/expressions/rtrim-ssis-expression.md)   
 [TRIM (выражение служб SSIS)](../../integration-services/expressions/trim-ssis-expression.md)   
 [Функции (выражение служб SSIS)](../../integration-services/expressions/functions-ssis-expression.md)  
  
  