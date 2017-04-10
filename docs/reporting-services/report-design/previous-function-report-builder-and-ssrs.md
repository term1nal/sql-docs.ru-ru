---
title: "Функция Previous (построитель отчетов и службы SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/23/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 403a9384-6ca4-42e8-97ca-ac3f6fe4316b
caps.latest.revision: 8
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
---
# Функция Previous (построитель отчетов и службы SSRS)
  Возвращает значение или значение статистического выражения для предыдущего экземпляра элемента внутри заданной области.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## Синтаксис  
  
```  
  
Previous(expression, scope)  
```  
  
#### Параметры  
 *expression*  
 (**Variant** или **Binary**) Выражение, используемое для идентификации данных, для которого необходимо получить предыдущее значение, например `Fields!Fieldname.Value` или `Sum(Fields!Fieldname.Value)`.  
  
 *область*  
 (**String**) Необязательно. Имя группы или область данных либо значение NULL (**Nothing** в [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]), указывающее область, из которой необходимо получить предыдущее значение, заданное параметром *expression*.  
  
## Тип возвращаемых данных  
 Возвращает **Variant** или **Binary**.  
  
## Замечания  
 Функция **Previous** возвращает предыдущее значение для выражения, которое вычисляется в указанной области после применения всех операций сортировки и фильтрации.  
  
 Если параметр *expression* не содержит статистической функции, функция **Previous** по умолчанию относится к текущей области элемента отчета.  
  
 В группе подробностей используйте функцию **Previous** , чтобы задать ссылку на значение поля в предыдущем экземпляре строки детализации.  
  
> [!NOTE]  
>  Функция **Previous** поддерживает только ссылки на поля в группе подробных сведений. Например, для текстового поля в группе подробностей выражение `=Previous(Fields!Quantity.Value)` возвращает данные для поля `Quantity` из предыдущей строки. Это выражение в первой строке возвращает значение NULL (**Nothing** в [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]).  
  
 Если параметр *expression* содержит агрегатную функцию, использующую область по умолчанию, функция **Previous** выполняет статистическую обработку данных в пределах предыдущего экземпляра области, указанной в вызове агрегатной функции.  
  
 Если параметр *expression* содержит агрегатную функцию, задающую область, отличную от области по умолчанию, параметр *scope* для функции **Previous** должен включать область для области, указанной в вызове агрегатной функции.  
  
 Функции **Level**, **InScope**, **Aggregate** и **Previous** нельзя использовать в параметре *expression*. Параметр *recursive* для агрегатных функций не поддерживается.  
  
 Дополнительные сведения см. в разделах [Справочник по агрегатным функциям (построитель отчетов и службы SSRS)](../../reporting-services/report-design/aggregate-functions-reference-report-builder-and-ssrs.md) и [Область выражения для суммирования, агрегатных функций и встроенных коллекций (построитель отчетов и службы SSRS)](../../reporting-services/report-design/expression scope for totals, aggregates, and built-in collections.md).  
  
## Примеры  
  
### Description  
 Следующий пример кода, помещенный в строку данных по умолчанию для области данных, предоставляет значение для поля `LineTotal` в предыдущей строке.  
  
### код  
  
```  
=Previous(Fields!LineTotal.Value)  
```  
  
### Description  
 В следующем примере показано выражение, вычисляющее сумму продаж в указанный день месяца и предыдущее значение в тот же день месяца в прошлом году. Выражение добавляется в ячейку строки, относящуюся к дочерней группе `GroupbyDay`. Ее родительской группой является `GroupbyMonth`, которая имеет родительскую группу `GroupbyYear`. Выражение отображает результаты для группы GroupbyDay (область по умолчанию) и затем для группы `GroupbyYear` (родитель родительской группы `GroupbyMonth`).  
  
 Рассмотрим для примера область данных с родительской группой `Year` и ее дочерней группой `Month`, у которой имеется дочерняя группа `Day` (три вложенных уровня). Выражение `=Previous(Sum(Fields!Sales.Value,"Day"),"Year")` в строке, связанной с группой `Day` , возвращает значение продаж в тот же день и в тот же месяц прошлого года.  
  
### код  
  
```  
=Sum(Fields!Sales.Value) & " " & Previous(Sum(Fields!Sales.Value,"GroupbyDay"),"GroupbyYear")  
```  
  
## См. также  
 [Использование выражений в отчетах (построитель отчетов и службы SSRS)](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Примеры выражений (построитель отчетов и службы SSRS)](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Типы данных в выражениях (построитель отчетов и службы SSRS)](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [Область выражения для суммирования, агрегатных функций и встроенных коллекций (построитель отчетов и службы SSRS)](../../reporting-services/report-design/expression scope for totals, aggregates, and built-in collections.md)  
  
  