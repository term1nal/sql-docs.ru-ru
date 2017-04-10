---
title: "Работа с элементами, кортежами и наборами (многомерные выражения) | Microsoft Docs"
ms.custom: ""
ms.date: "03/13/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "многомерные выражения [службы Analysis Services], кортежи"
  - "ключи элементов [многомерные выражения]"
  - "многомерные выражения [службы Analysis Services], наборы"
  - "вычисляемые элементы [многомерные выражения]"
  - "элементы [многомерные выражения]"
  - "многомерные выражения [службы Analysis Services], элементы"
  - "именованные наборы [многомерные выражения]"
  - "многомерные выражения [службы Analysis Services], кортежи"
  - "функции элементов [многомерные выражения]"
  - "наборы [многомерные выражения]"
  - "многомерные выражения [службы Analysis Services], элементы"
  - "имена элементов [многомерные выражения]"
  - "многомерные выражения [службы Analysis Services], наборы"
  - "функции кортежей"
  - "кортежи"
  - "функции наборов [многомерные выражения]"
ms.assetid: b6ec2439-caef-46d3-9fd7-5f4526cee334
caps.latest.revision: 41
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 41
---
# Работа с элементами, кортежами и наборами (многомерные выражения)
  Многомерные выражения предоставляют функции, возвращающие один или более элементов, кортежей или наборов, или действуют на элемент, кортеж или набор.  
  
## Функции элементов  
 В языке многомерных выражений есть несколько функций для получения элементов из других многомерных сущностей, таких как измерения, уровни или кортежи. Например, функция [FirstChild](../../../mdx/firstchild-mdx.md) действует на элемент и возвращает элемент.  
  
 Чтобы найти первый потомок измерения времени, можно указать его явно, как показано в следующем примере.  
  
```  
SELECT [Date].[Calendar Year].[CY 2001] on 0  
FROM [Adventure Works]  
  
```  
  
 Или же можно найти этот же элемент с помощью функции **FirstChild** , как показано в следующем примере.  
  
```  
SELECT [Date].[Calendar Year].FirstChild on 0  
FROM [Adventure Works]  
  
```  
  
 Дополнительные сведения о функциях элементов в многомерных выражениях см. в разделе [Справочник по функциям многомерных выражений (многомерные выражения)](../../../mdx/mdx-function-reference-mdx.md).  
  
## Функции кортежей  
 В языке многомерных выражений есть несколько функций, возвращающих кортежи. Эти функции можно использовать в любом месте, где допускаются кортежи. Например, функция [Item (кортеж) (многомерные выражения)](../../../mdx/item-tuple-mdx.md) может использоваться для получения первого кортежа из набора, что удобно, если известно, что набор состоит из единственного кортежа, который нужно передать функции, требующей кортеж в качестве аргумента.  
  
 В следующем примере возвращается первый кортеж из набора кортежей по оси столбцов.  
  
```  
SELECT {  
   ([Measures].[Reseller Sales Amount]  
      ,[Date].[Calendar Year].[CY 2003]  
   )  
, ([Measures].[Reseller Sales Amount]  
      ,[Date].[Calendar Year].[CY 2004]  
   )  
}.Item(0)  
ON COLUMNS   
FROM [Adventure Works]  
```  
  
 Дополнительные сведения о функциях кортежей см. в разделе [Справочник по функциям многомерных выражений (многомерные выражения)](../../../mdx/mdx-function-reference-mdx.md).  
  
## Функции наборов  
 В языке многомерных выражений есть несколько функций, возвращающих наборы. Чтобы извлечь набор, не обязательно явно перечислять все кортежи в квадратных скобках. Дополнительные сведения о функциях элементов, возвращающих наборы, см. в разделе [Основные понятия многомерных выражений (службы Analysis Services)](../../../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md). Существует множество дополнительных функций над наборами.  
  
 Оператор «двоеточие» (:) позволяет использовать естественный порядок элементов для создания набора. Например, набор, представленный в следующем примере, содержит четыре кортежа: с первого по четвертый квартал календарного 2002 г.  
  
```  
SELECT   
   {[Calendar Quarter].[Q1 CY 2002]:[Calendar Quarter].[Q4 CY 2002]}   
ON 0  
FROM [Adventure Works]  
```  
  
 Такой же набор можно создать, не используя оператор двоеточия, а указав кортежи, как показано в следующем примере.  
  
```  
SELECT {  
   [Calendar Quarter].[Q1 CY 2002],   
   [Calendar Quarter].[Q2 CY 2002],   
   [Calendar Quarter].[Q3 CY 2002],   
   [Calendar Quarter].[Q4 CY 2002]  
   } ON 0  
FROM [Adventure Works]  
  
```  
  
 Оператор «двоеточие» (:) является инклюзивной функцией. Результирующий набор содержит элементы, указанные с обеих сторон оператора двоеточия.  
  
 Дополнительные сведения о функциях наборов см. в разделе [Справочник по функциям многомерных выражений (многомерные выражения)](../../../mdx/mdx-function-reference-mdx.md).  
  
## Функции массивов  
 Функции массивов обрабатывают набор и возвращают массив. Дополнительные сведения о функциях массивов см. в разделе [Справочник по функциям многомерных выражений (многомерные выражения)](../../../mdx/mdx-function-reference-mdx.md).  
  
## Функции иерархий  
 Функции иерархий возвращают иерархию, обрабатывая элемент, уровень, иерархию или строку. Дополнительные сведения о функциях иерархий см. в разделе [Справочник по функциям многомерных выражений (многомерные выражения)](../../../mdx/mdx-function-reference-mdx.md).  
  
## Функции уровней  
 Функции уровней возвращают уровень, обрабатывая элемент, уровень или строку. Дополнительные сведения о функциях уровней см. в разделе [Справочник по функциям многомерных выражений (многомерные выражения)](../../../mdx/mdx-function-reference-mdx.md).  
  
## Логические функции  
 Логическая функция обрабатывает многомерное выражение, возвращая информацию о кортежах, элементах или наборах в выражении. Например, функция [IsEmpty (многомерные выражения)](../../../mdx/isempty-mdx.md) оценивает, возвращает ли выражение значение пустой ячейки. Дополнительные сведения о логических функциях см. в разделе [Справочник по функциям многомерных выражений (многомерные выражения)](../../../mdx/mdx-function-reference-mdx.md).  
  
## Числовые функции  
 Числовая функция обрабатывает многомерное выражение, возвращая скалярную величину. Например, функция [Aggregate (многомерные выражения)](../../../mdx/aggregate-mdx.md) возвращает скалярную величину, вычисляемую с помощью статистической обработки мер по кортежам в заданном наборе. Дополнительные сведения о числовых функциях см. в разделе [Справочник по функциям многомерных выражений (многомерные выражения)](../../../mdx/mdx-function-reference-mdx.md).  
  
## Строковые функции  
 Строковая функция обрабатывает многомерное выражение, возвращая строку. Например, функция [UniqueName (многомерные выражения)](../../../mdx/uniquename-mdx.md) возвращает строковое значение, включающее в себя уникальное имя измерения, иерархии, уровня или элемента. Дополнительные сведения о строковых функциях см. в разделе [Справочник по функциям многомерных выражений (многомерные выражения)](../../../mdx/mdx-function-reference-mdx.md).  
  
## См. также  
 [Основные понятия многомерных выражений (службы Analysis Services)](../../../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md)   
 [Основные принципы запросов многомерных выражений (службы Analysis Services)](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)   
 [Справочник по функциям многомерных выражений (многомерные выражения)](../../../mdx/mdx-function-reference-mdx.md)  
  
  