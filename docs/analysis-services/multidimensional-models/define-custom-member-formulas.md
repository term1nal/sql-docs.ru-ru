---
title: "Определение нестандартных формул элементов | Microsoft Docs"
ms.custom: ""
ms.date: "03/23/2017"
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
  - "элементы [службы Analysis Services], настраиваемые"
  - "формулы пользовательской свертки [службы Analysis Services]"
  - "многомерные выражения [службы Analysis Services], формулы пользовательской свертки"
  - "нестандартные формулы элементов [службы Analysis Services]"
ms.assetid: 258304e2-d900-4013-97e3-871f51dfdce2
caps.latest.revision: 32
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Определение нестандартных формул элементов
  Нестандартные формулы элемента — это многомерные выражения, предоставляющие значения для элементов указанного атрибута. Столбец таблицы из представления источников данных содержит выражение для каждого элемента атрибута, предоставляющее значение для этого элемента.  
  
 Нестандартные формулы элементов определяют значения ячеек, которые связаны с элементами, и заменяют агрегатные функции мер. Нестандартные формулы элементов записаны в многомерных выражениях. Каждая нестандартная формула элемента применяется к одному элементу. Нестандартные формулы элементов хранятся в таблице измерения или в другой таблице, имеющей связь по внешнему ключу с таблицей измерения.  
  
 Свойство атрибута **CustomRollupColumn** указывает столбец, содержащий нестандартные формулы элементов для элементов атрибута. Если строка в столбце является пустой, значение ячейки для элемента возвращается обычным способом. Если формула в столбце не является допустимой, при извлечении значения ячейки, которая использует элемент, возникает ошибка времени выполнения.  
  
 Перед указанием нестандартной формулы элемента для атрибута убедитесь, что таблица измерения, содержащая атрибут, или непосредственно связанная таблица, содержит строковый столбец для хранения нестандартных формул элементов. Если это так, то можно либо установить свойство **CustomRollupColumn** вручную, либо использовать расширение установки нестандартных формул элементов мастера бизнес-аналитики для включения нестандартной формулы элемента для атрибута. Дополнительные сведения об использовании этой возможности см. в разделе [Настройка нестандартных формул элементов для атрибутов в измерении](../../analysis-services/multidimensional-models/set-custom-member-formulas-for-attributes-in-a-dimension.md).  
  
## Вычисление нестандартных формул элементов  
 Нестандартные формулы элементов отличаются от вычисляемых элементов. Нестандартные формулы элементов применяются к элементам, которые содержатся в таблице измерения, и только предоставляют значение для них. В отличие от пользовательских формул, вычисляемые элементы не хранятся в таблицах измерения, а выражения вычисляемых элементов определяют данные и метаданные дополнительных элементов измерения или иерархии.  
  
 Нестандартные формулы элементов заменяют агрегатные функции, связанные с мерами. Например, перед тем как была задана нестандартная формула элемента, мера, использующая агрегатную функцию **Sum** , принимала следующие значения для элементов измерения «Время»:  
  
-   2003: 2100  
  
    -   Квартал 1: 700  
  
    -   Квартал 2: 500  
  
    -   Квартал 3: 100  
  
    -   Квартал 4: 800  
  
-   2004: 1500  
  
    -   Квартал 1: 600  
  
    -   Квартал 2: 200  
  
    -   Квартал 3: 300  
  
    -   Квартал 4: 400  
  
 После задания нестандартной формулы элемента значение элемента стало определяться формулой пользовательской свертки. Например, следующая нестандартная формула элемента предоставляет значение 450 для дочернего элемента «Квартал 4» элемента «2004» измерения Time.  
  
```  
Time.[Quarter 3] * 1.5  
```  
  
 Нестандартные формулы элементов хранятся в столбце таблицы измерения. Чтобы включить формулы пользовательской свертки, необходимо установить свойство **CustomRollupColumn** нужного атрибута.  
  
 Чтобы применить многомерное выражение ко всем элементам атрибута, создайте в таблице измерения именованное вычисление, возвращающее многомерное выражение в виде символьной строки. Затем присвойте имя вычисления свойству **CustomRollupColumn** нужного атрибута. Именованное вычисление — это столбец в таблице представления источника дынных, который возвращает значения строк, определенные выражением SQL. Дополнительные сведения о составлении именованных вычислений см. в разделе [Определение именованных вычислений в представлении источника данных (службы Analysis Services)](../../analysis-services/multidimensional-models/define-named-calculations-in-a-data-source-view-analysis-services.md).  
  
> [!NOTE]  
>  Чтобы применить многомерное выражение не ко всем элементам атрибута, а только к членам определенного уровня, необходимо определить выражение в виде скрипта многомерного выражения для данного уровня. Дополнительные сведения см. в статье [Основные принципы создания скриптов многомерных выражений (службы Analysis Services)](../../analysis-services/multidimensional-models/mdx/mdx-scripting-fundamentals-analysis-services.md).  
  
 При одновременном использовании вычисляемых элементов и формул пользовательской свертки следует помнить о порядке вычислений. Вычисляемые элементы разрешаются до формул пользовательской свертки.  
  
## См. также  
 [Атрибуты и иерархии атрибутов](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)   
 [Настройка нестандартных формул элементов для атрибутов в измерении](../../analysis-services/multidimensional-models/set-custom-member-formulas-for-attributes-in-a-dimension.md)  
  
  