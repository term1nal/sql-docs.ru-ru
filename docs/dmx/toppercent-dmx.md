---
title: TopPercent (расширения интеллектуального анализа данных) | Документация Майкрософт
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 781b5c660826ff963497a5b89b7bc01a16eeb265
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2018
ms.locfileid: "38040402"
---
# <a name="toppercent-dmx"></a>TopPercent (расширения интеллектуального анализа данных)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  **TopPercent** функция возвращает значение, в порядке убывания ранга верхние строки таблицы, сумма которых, по крайней мере указанный процент.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
TopPercent(<table expression>, <rank expression>, <percent>)  
```  
  
## <a name="applies-to"></a>Объект применения  
 Выражение, возвращающее таблицу, такие как \<ссылка на столбец таблицы >, или функция, возвращающая таблицу.  
  
## <a name="return-type"></a>Тип возвращаемых данных  
 \<таблицы выражение >  
  
## <a name="remarks"></a>Примечания  
 **TopPercent** функция возвращает верхние строки в порядке убывания ранга на основе вычисленного значения \<rank expression > аргумент для каждой строки таким образом, чтобы сумма \<rank expression > значения по крайней мере заданному проценту, заданному по \<процентов > аргумент. **TopPercent** возвращает возможные наименьшее количество элементов, соответствующих указанному значению процента.  
  
## <a name="examples"></a>Примеры  
 В следующем примере создается прогнозирующий запрос к модели взаимосвязей, построенной с помощью [основам интеллектуального анализа данных](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c).  
  
 Чтобы понять, как работает TopPercent, возможно, будет сначала выполнить прогнозирующий запрос, который возвращает только вложенную таблицу.  
  
```  
SELECT Predict ([Association].[v Assoc Seq Line Items], INCLUDE_STATISTICS, 10)  
FROM   
     [Association]  
NATURAL PREDICTION JOIN  
SELECT (SELECT 'Women''s Mountain Shorts' as [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
> [!NOTE]  
>  В этом примере значение, заданное в качестве входных данных, содержит знак одинарной кавычки, а значит, его нужно экранировать и добавить перед ним еще один знак кавычки. При отсутствии уверенности в синтаксических конструкциях, используемых для вставки escape-символа, запросы можно создавать с помощью построителя прогнозирующих запросов. При выборе значения из раскрывающегося списка необходимый escape-символ вставляется автоматически. Дополнительные сведения см. в разделе [Создание одноэлементного запроса в конструкторе интеллектуального анализа данных](../analysis-services/data-mining/create-a-singleton-query-in-the-data-mining-designer.md).  
  
 Пример результатов:  
  
|Модель|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Sport-100|4334|0.291283016|0.252695851|  
|Фляга для воды|2866|0.192620472|0.175205052|  
|Ремонтный комплект|2113|0.142012232|0.132389356|  
|Камера шины для велосипеда Mountain|1992|0.133879965|0.125304948|  
|Велосипед Mountain-200|1755|0.117951475|0.111260823|  
|Камера шины для шоссейного велосипеда|1588|0.106727603|0.101229538|  
|Велосипедная шапочка|1473|0.098998589|0.094256014|  
|Набор крыльев для велосипеда Mountain|1415|0.095100477|0.090718432|  
|Держатель фляги для велосипеда Mountain|1367|0.091874454|0.087780332|  
|Держатель фляги для шоссейного велосипеда|1195|0.080314537|0.077173962|  
  
 Функция TopPercent принимает результаты этого запроса и возвращает строки с наибольшими значениями, сумма которых составляет заданную процентную долю.  
  
```  
SELECT   
TopPercent  
    (  
    Predict ([Association].[v Assoc Seq Line Items],INCLUDE_STATISTICS,10),  
    $SUPPORT,  
    50)  
FROM   
     [Association]  
NATURAL PREDICTION JOIN  
(SELECT (SELECT 'Women''s Mountain Shorts' as [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
 Первым аргументом функции TopPercent является имя столбца таблицы. В этом примере вложенной таблицы возвращается путем вызова функции Predict и использовать аргумент INCLUDE_STATISTICS.  
  
 Второй аргумент функции TopPercent является столбец во вложенной таблице, используемой для упорядочения результатов. В этом примере параметр INCLUDE_STATISTICS возвращает столбцы $SUPPORT, $PROBABILTY и $ADJUSTED PROBABILITY. В этом примере используется столбец $SUPPORT, поскольку значения в нем не являются дробными и их легче проверять.  
  
 Третий аргумент функции TopPercent указывает процент, имеет тип double. Чтобы получить строки для верхних продуктов, стоимость которых составляет 50 процентов от общей поддержки, необходимо ввести 50.  
  
 Пример результатов:  
  
|Модель|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Sport-100|4334|0.29…|0.25…|  
|Фляга для воды|2866|0.19…|0.17…|  
|Ремонтный комплект|2113|0.14…|0.13…|  
|Камера шины для велосипеда Mountain|1992|0.133…|0.12…|  
  
 **Примечание** этот пример приведен только для иллюстрации применения функции TopPercent. В зависимости от размера набора данных выполнение данного запроса может занять значительное время.  
  
> [!WARNING]  
>  Функции многомерных выражений для TOPPERCENT и BOTTOMPERCENT могут давать непредвиденные результаты, если значения, используемые для вычисления процентов, содержат отрицательные числа. Это не влияет на функции расширений интеллектуального анализа данных. Дополнительные сведения см. в разделе [BottomPercent &#40;многомерных Выражений&#41;](../mdx/bottompercent-mdx.md).  
  
## <a name="see-also"></a>См. также  
 [Расширения интеллектуального анализа данных &#40;расширений интеллектуального анализа данных&#41; справочнике по функциям](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Функции &#40;расширений интеллектуального анализа данных&#41;](../dmx/functions-dmx.md)   
 [Общие функции прогнозирования &#40;расширений интеллектуального анализа данных&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
