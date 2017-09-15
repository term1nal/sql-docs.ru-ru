---
title: "Меры | Документы Microsoft"
ms.custom: 
ms.date: 04/10/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 27ec8f99-e9ef-44c9-a83f-f7c88e128ad3
caps.latest.revision: 19
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 38b7467cd4ad765d651ea0ebe4ad57c278c987a1
ms.contentlocale: ru-ru
ms.lasthandoff: 09/01/2017

---
# <a name="measures"></a>меры
  В табличных моделях мера представляет собой вычисление, созданное при помощи формулы DAX, специально созданной для использования в клиенте отчетов. Меры оцениваются на основании полей, фильтров и срезов, которые пользователи выбирают в клиентском приложении создания отчетов.  
  
##  <a name="bkmk_understanding"></a> Преимущества  
 Меры могут быть основаны на стандартных агрегатных функциях, например AVERAGE, COUNT или SUM, либо на пользовательских формулах на языке выражений анализа данных (DAX). В дополнение к формуле каждая мера имеет свойства, определенные типом данных меры, например «Имя», «Сведения о таблице», «Формат» и «Десятичные разряды».  
  
 Когда меры были определены в модели, пользовали могут добавлять их в отчет или сводную таблицу. В зависимости от перспектив и ролей, меры появляются в списке полей со связанной с ними таблицей и доступны всем пользователям модели. Меры обычно создаются в таблицах фактов. Однако меры могут не зависеть от связанной с ними таблицы.  
  
 Важно понять фундаментальные различия между вычисляемым столбцом и мерой. В вычисляемом столбце формула имеет результатом значение для каждой строки в столбце. Например, в таблице «FactSales» вычисляемый столбец под названием «TotalProfit» со следующей формулой вычисляет значение для общей прибыли для каждой строки (одна строка на факт продажи) в таблице «FactSales»:  
  
```  
=[SalesAmount] - [TotalCost] - [ReturnAmount]  
```  
  
 Вычисляемый столбец «TotalProfit», как и любой другой столбец данных, можно использовать в клиенте отчетов.  
  
 С другой стороны, значение меры вычисляется на основании выбора пользователя, который представляет собой контекст фильтра в сводной таблице или отчете. Например, мера в таблице «FactSales» создана по следующей формуле:  
  
```  
Sum of TotalProfit: =SUM([TotalProfit])  
```  
  
 Аналитик продаж с помощью Excel желает знать итоговые продажи для некой категории продуктов. Каждая категория состоит из нескольких продуктов. Аналитик продаж выбирает столбец ProductCategoryName и добавляет его в окно фильтра «Метки строк». После этого в сводной таблице будет показана строка для каждой категории продукта. Затем пользователь выбирает сумму меры TotalProfit. Мера по умолчанию добавляется в окне фильтра «Значения». Мера вычисляет сумму итоговой прибыли и показывает результат для каждой категории продукта. Аналитик продаж затем может отфильтровать сумму итоговой прибыли для каждой категории продукта с помощью среза, например добавляя CalendarYear в качестве среза для просмотра суммы итоговой прибыли для каждой категории продукта по годам.  
  
|ProductCategoryName|Сумма TotalProfit|  
|-------------------------|------------------------|  
|Аудио|$2,731,061,308.69|  
|Фотоаппараты и видеокамеры|$620,623,675.75|  
|Компьютеры|$392,999,044.59|  
|ТВ и видео|$946,989,702.51|  
|**Grand Total**|**$4,691,673,731.53**|  
  
##  <a name="bkmk_def_mg"></a> Defining measures by using the measure grid  
 Меры создаются во время разработки с помощью сетки мер в конструкторе моделей. В каждой таблице есть сетка мер. По умолчанию она отображается под каждой таблицей в конструкторе моделей. Для конкретной таблицы просмотр сетки мер можно отключить. Чтобы включить отображение сетки мер таблицы, в меню **Таблица** выберите команду **Показать сетку мер**.  
  
 В сетке мер вы можете создавать меры одним из следующих способов.  
  
-   Щелкните пустую ячейку в сетке мер, а затем наберите формулу DAX в строке формул. При нажатии клавиши ВВОД для завершения формулы мера появится в ячейке в сетке мер.  
  
-   Создайте меру с помощью стандартной статистической функции щелкнув столбец, затем щелкнув кнопку автосуммирования (∑) на панели инструментов и щелкнув стандартную статистическую функцию. Стандартные статистические функции: Sum, Average, Count, DistinctCount, Max, Min. Меры, созданные с помощью кнопки автосуммирования, будут всегда отображаться в сетке мер под столбцом.  
  
 По умолчанию при использовании кнопки автосуммирования имя меры определяется именем связанного столбца с двоеточием, после которого следует формула. Имя можно изменить в строке формул в параметре свойства **Имя меры** в окне свойств. При создании меры с помощью пользовательской формулы можно ввести имя в строку формул, поставить после него двоеточие, за которым следует формула, или можно ввести имя в свойстве **Имя меры** в окне свойств.  
  
 Важно присваивать имена мерам аккуратно. Имя меры будет появляться в связанной таблице в списке полей клиента отчетов. Ключевой показатель эффективности также будет называться в соответствии с базовой мерой. Имя меры не может совпадать с именем столбца любой таблицы в модели.  
  
> [!TIP]  
>  Группы из разных таблиц можно сгруппировать в одну таблицу, создав пустую таблицу с последующим переносом в нее существующих мер или созданием новых. Возможно, имена таблиц придется включать в формулы DAX при указании ссылок на столбцы из других таблиц.  
  
 Если для модели были определены перспективы, то меры не будут автоматически добавлены к этим перспективам. Необходимо вручную добавить меры к перспективам с помощью диалогового окна «Перспективы». Дополнительные сведения см. в разделе [перспективы](../../analysis-services/tabular-models/perspectives-ssas-tabular.md).  
  
##  <a name="bkmk_properties"></a> Свойства мер  
 Каждая мера имеет определяющие ее свойства. Свойства меры вместе со связанными свойствами столбца можно изменить в окне «Свойства». Меры имеют следующие свойства:  
  
|Свойство|Параметр по умолчанию|Description|  
|--------------|---------------------|-----------------|  
|**Description**|Пусто|Описание меры. Описание не появится с мерой в клиенте отчетов.|  
|**Формат**|Автоматически определяется по типу данных столбца, на который есть ссылка в выражении формулы.|Формат меры. Например, валюта или процент.|  
|**Формула**|Формула, введенная в строке формул при создании меры.|Формула меры.|  
|**Имя меры**|Если используется автосуммирование, имя меры предшествует имени столбца и отделено двоеточием. Если введена пользовательская формула, введите имя и двоеточие, затем введите формулу.|Имя меры, как показано в списке полей клиента отчетов.|  
  
##  <a name="bkmk_KPI"></a> Использование меры в ключевом показателе эффективности  
 Ключевой показатель эффективности определяется *базовым* значением, определенным мерой, и *целевым* значением, также определяемым мерой или абсолютным значением. Ключевой показатель эффективности также включает *состояние*, которое представляет собой вычисление, где базовое значение сравнивается с целевым значением между пороговыми значениями в графическом формате. Ключевые показатели эффективности часто используются бизнесменами для определения трендов в критически важных бизнес-показателях.  
  
 Любая мера может служить базовой мерой для ключевого показателя эффективности. Для создания ключевого показателя эффективности в сетке мер щелкните правой кнопкой мыши меру и выберите **Создать ключевой показатель эффективности**. Появится диалоговое окно «Ключевой показатель эффективности», в котором можно указать целевое значение (определенное мерой или абсолютным значением) и определить пороговые значения состояния и графический тип. Дополнительные сведения см. в разделе [ключевые показатели эффективности](../../analysis-services/tabular-models/kpis-ssas-tabular.md).  
  
##  <a name="bkmk_rel_tasks"></a> Связанные задачи  
  
|Раздел|Description|  
|-----------|-----------------|  
|[Создание мер и управление ими](../../analysis-services/tabular-models/create-and-manage-measures-ssas-tabular.md)|Содержит описание порядка создания мер и управления мерами с помощью сетки мер в конструкторе моделей.|  
  
## <a name="see-also"></a>См. также:  
 [Ключевые показатели эффективности](../../analysis-services/tabular-models/kpis-ssas-tabular.md)   
 [Создание и управление ими ключевые показатели эффективности](../../analysis-services/tabular-models/create-and-manage-kpis-ssas-tabular.md)   
 [Вычисляемые столбцы](../../analysis-services/tabular-models/ssas-calculated-columns.md)  
  
  