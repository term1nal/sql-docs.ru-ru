---
title: 'Занятие 2: Добавление моделей интеллектуального анализа данных к структуре интеллектуального анализа данных потребительской корзины | Документация Майкрософт'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: d96a7a7d-35d7-4b34-abb5-f0822c256253
caps.latest.revision: 34
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8d758ef319c61d7868c2114372f353a374c38230
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2018
ms.locfileid: "37159715"
---
# <a name="lesson-2-adding-mining-models-to-the-market-basket-mining-structure"></a>Занятие 2: Добавление моделей интеллектуального анализа данных к структуре интеллектуального анализа данных потребительской корзины
  На этом занятии будет добавлено две модели интеллектуального анализа данных к структуре интеллектуального анализа Market Basket, созданный в [занятии 1: Создание структуры интеллектуального анализа данных Market Basket](../../2014/tutorials/lesson-1-creating-the-market-basket-mining-structure.md). С помощью этих моделей интеллектуального анализа данных можно будет создавать прогнозы.  
  
 Для прогнозирования типов товара, которые клиент стремится заказать одновременно, необходимо создать две модели интеллектуального анализа данных с помощью [Microsoft Association Algorithm](../../2014/analysis-services/data-mining/microsoft-association-algorithm.md) и два разных значения *MINIMUM_PROBABILTY* параметра.  
  
 *MINIMUM_PROBABILTY* является [!INCLUDE[msCoName](../includes/msconame-md.md)] параметр алгоритма взаимосвязей, которая помогает определить количество правил, содержащих модель интеллектуального анализа данных, указав минимальную вероятность, что правило должно содержать. Например, установка этого параметра в значение 0,4 означает, что правило может быть сформировано только в том случае, если вероятность появления сочетания продуктов, описанного в нем, равняется, по крайней мере, сорока процентам.  
  
 Вы просмотрите эффект от изменения *MINIMUM_PROBABILTY* параметра в одном из следующих занятий.  
  
## <a name="alter-mining-structure-statement"></a>Инструкция ALTER MINING STRUCTURE  
 Чтобы добавить модель интеллектуального анализа данных, которая содержит вложенную таблицу к структуре интеллектуального анализа данных, используйте [ALTER MINING STRUCTURE &#40;расширений интеллектуального анализа данных&#41;] (инструкция (~/dmx/alter-mining-structure-dmx.md). Код инструкции можно разбить на следующие части:  
  
-   Определение структуры интеллектуального анализа данных  
  
-   Указание имени модели интеллектуального анализа  
  
-   Определение ключевого столбца  
  
-   Определение столбцов исходных данных и прогнозируемых столбцов  
  
-   Определение столбцов вложенных таблиц  
  
-   Идентификация алгоритма и изменений параметра  
  
 Далее приведен общий пример инструкции `ALTER MINING STRUCTURE`, добавляющей в структуру модель интеллектуального анализа данных, содержащую столбцы вложенной таблицы:  
  
```  
ALTER MINING STRUCTURE [<Mining Structure Name>]  
ADD MINING MODEL [<Mining Model Name>]  
(  
    [<key column>],  
    <mining model column> <usage>,  
    <table columns>  
    (  [<nested key column>],  
       <nested mining model columns> )  
) USING <algorithm>( <algorithm parameters> )  
```  
  
 В первой строке кода идентифицируется существующая структура интеллектуального анализа данных, в которую будет добавлена модель интеллектуального анализа данных:  
  
```  
ALTER MINING STRUCTURE [<mining structure name>]  
```  
  
 В следующей строчке кода модели интеллектуального анализа данных, добавляемой к структуре интеллектуального анализа, присваивается имя:  
  
```  
ADD MINING MODEL [<mining model name>]  
```  
  
 Сведения о присвоении имени объекту в расширений интеллектуального анализа (DMX), см. в разделе [идентификаторы &#40;расширений интеллектуального анализа данных&#41;](/sql/dmx/identifiers-dmx).  
  
 Следующие строки кода задают столбцы из структуры интеллектуального анализа данных, которые будут использоваться моделью интеллектуального анализа данных:  
  
```  
[<key column>],  
<mining model columns> <usage>,  
```  
  
 Можно использовать только столбцы, которые уже существуют в структуре интеллектуального анализа данных.  
  
 Первым столбцом в списке столбцов модели интеллектуального анализа данных должен быть ключевой столбец структуры интеллектуального анализа данных. Тем не менее, у вас нет к типу `KEY` после ключевого столбца, чтобы задать его использование. При создании структуры интеллектуального анализа данных этот столбец уже был определен как ключевой.  
  
 В остальных строках задается использование столбцов новой модели интеллектуального анализа данных. С помощью следующего синтаксиса можно указать столбец модели интеллектуального анализа, который следует использовать для прогнозирования:  
  
```  
<column name> PREDICT,  
```  
  
 Если для столбца не было указано использование, то этот столбец можно не включать в структуру интеллектуального анализа данных. Все столбцы, которые используются в упоминаемой структуре интеллектуального анализа данных, автоматически доступны для использования в моделях интеллектуального анализа данных, основанных на этой структуре. Однако модель не будет использовать столбцы для обучения, если не было указано их использование.  
  
 В последней строке фрагмента кода задается алгоритм и параметры алгоритма, используемые для формирования модели интеллектуального анализа.  
  
```  
) USING <algorithm>( <algorithm parameters> )  
```  
  
## <a name="lesson-tasks"></a>Задачи занятия  
 На этом занятии будут выполнены следующие задачи.  
  
-   Добавление в структуру ассоциативной модели интеллектуального анализа данных, используя вероятность по умолчанию  
  
-   Добавление в структуру ассоциативной модели интеллектуального анализа данных, используя измененную вероятность  
  
## <a name="adding-an-association-mining-model-to-the-structure-using-the-default-minimumprobability"></a>Добавление модели интеллектуального анализа взаимосвязей к структуре с помощью параметра по умолчанию MINIMUM_PROBABILTY  
 Первой задачей является добавление новой модели интеллектуального анализа данных к структуре интеллектуального анализа данных потребительской корзины на основе [!INCLUDE[msCoName](../includes/msconame-md.md)] алгоритм взаимосвязей, используя значение по умолчанию для *MINIMUM_PROBABILITY*.  
  
#### <a name="to-add-an-association-mining-model"></a>Добавление ассоциативной модели интеллектуального анализа данных  
  
1.  В **обозревателя объектов**, щелкните правой кнопкой мыши экземпляр [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], пункты **новый запрос**, а затем нажмите кнопку **расширений интеллектуального анализа данных**.  
  
     Откроется редактор запросов, содержащий новый, пустой запрос.  
  
    > [!NOTE]  
    >  Чтобы создать запрос расширений интеллектуального анализа данных к определенной базе данных служб [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], щелкните правой кнопкой мыши базу данных, а не экземпляр.  
  
2.  Скопируйте общий пример инструкции `ALTER MINING STRUCTURE` в пустой запрос.  
  
3.  Вместо  
  
    ```  
    <mining structure name>   
    ```  
  
     вставьте  
  
    ```  
    [Market Basket]  
    ```  
  
4.  Вместо  
  
    ```  
    <mining model name>   
    ```  
  
     вставьте  
  
    ```  
    [Default Association]  
    ```  
  
5.  Вместо  
  
    ```  
    [<key column>],  
    <mining model columns>,  
    <table columns>  
    (  [<nested key column>],  
       <nested mining model columns> )  
    ```  
  
     вставьте  
  
    ```  
    OrderNumber,  
        [Products] PREDICT (  
            [Model]  
        )  
    ```  
  
     В этом случае в качестве прогнозируемого столбца была назначен столбец таблицы `[Products]` `.` Кроме того, в список столбцов вложенной таблицы был добавлен столбец `[Model]`, поскольку он является ключевым столбцом вложенной таблицы.  
  
    > [!NOTE]  
    >  Помните, что ключ вложенной таблицы отличается от ключа варианта. Ключ варианта — это уникальный идентификатор варианта, а ключ вложенной таблицы — атрибут, подлежащий моделированию.  
  
6.  Вместо  
  
    ```  
    USING <algorithm>( <algorithm parameters> )  
    ```  
  
     вставьте  
  
    ```  
    Using Microsoft_Association_Rules  
    ```  
  
     В результате инструкция должна выглядеть следующим образом:  
  
    ```  
    ALTER MINING STRUCTURE [Market Basket]  
    ADD MINING MODEL [Default Association]  
    (  
        OrderNumber,  
        [Products] PREDICT (  
            [Model]  
        )  
    )  
    Using Microsoft_Association_Rules  
    ```  
  
7.  В меню **Файл** щелкните **Сохранить DMXQuery1.dmx как**.  
  
8.  В **Сохранить как** диалоговом окне перейдите к соответствующей папке и присвойте файлу имя `Default_Association_Model.dmx`.  
  
9. На панели инструментов нажмите кнопку **Выполнить** .  
  
## <a name="adding-an-association-mining-model-to-the-structure-changing-the-default-minimumprobability"></a>Добавление модели интеллектуального анализа взаимосвязей к структуре путем изменения параметра MINIMUM_PROBABILITY  
 Следующей задачей является добавление новой модели интеллектуального анализа данных к структуре интеллектуального анализа данных потребительской корзины на основе [!INCLUDE[msCoName](../includes/msconame-md.md)] алгоритм взаимосвязей и изменить значение по умолчанию для параметра MINIMUM_PROBABILITY на 0,01. Изменение параметра приведет к [!INCLUDE[msCoName](../includes/msconame-md.md)] алгоритм взаимосвязей, чтобы создать дополнительные правила.  
  
#### <a name="to-add-an-association-mining-model"></a>Добавление ассоциативной модели интеллектуального анализа данных  
  
1.  В **обозревателя объектов**, щелкните правой кнопкой мыши экземпляр [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], пункты **новый запрос**, а затем нажмите кнопку **расширений интеллектуального анализа данных**.  
  
     Откроется редактор запросов, содержащий новый, пустой запрос.  
  
2.  Скопируйте общий пример инструкции `ALTER MINING STRUCTURE` в пустой запрос.  
  
3.  Вместо  
  
    ```  
    <mining structure name>   
    ```  
  
     вставьте  
  
    ```  
    Market Basket  
    ```  
  
4.  Вместо  
  
    ```  
    <mining model name>   
    ```  
  
     вставьте  
  
    ```  
    [Modified Association]  
    ```  
  
5.  Вместо  
  
    ```  
    <mining model columns>,  
    <table columns>  
    (  [<nested key column>],  
       <nested mining model columns> )  
    ```  
  
     вставьте  
  
    ```  
    OrderNumber,  
    [Products] PREDICT (  
            [Model]  
        )  
    ```  
  
     В этом случае таблица `[Products]` обозначается как прогнозируемый столбец. Столбец `[MODEL]` также включается в список, поскольку он является ключевым столбцом во вложенной таблице.  
  
6.  Вместо  
  
    ```  
    USING <algorithm>( <algorithm parameters> )  
    ```  
  
     вставьте  
  
    ```  
    USING Microsoft_Association_Rules (Minimum_Probability = 0.1)  
    ```  
  
     В результате инструкция должна выглядеть следующим образом:  
  
    ```  
    ALTER MINING STRUCTURE [Market Basket]  
    ADD MINING MODEL [Modified Assocation]  
    (  
        OrderNumber,  
        [Products] PREDICT (  
            [Model]  
        )  
    )  
    USING Microsoft_Association_Rules (Minimum_Probability = 0.1)  
    ```  
  
7.  В меню **Файл** щелкните **Сохранить DMXQuery1.dmx как**.  
  
8.  В **Сохранить как** диалоговом окне перейдите к соответствующей папке и присвойте файлу имя `Modified Association_Model.dmx`.  
  
9. На панели инструментов нажмите кнопку **Выполнить** .  
  
 На следующем занятии требуется обработать структуру интеллектуального анализа данных «Потребительская корзина» и связанные с ней модели интеллектуального анализа данных.  
  
## <a name="next-lesson"></a>Следующее занятие  
 [Урок 3. Обработка структуры интеллектуального анализа "Потребительская корзина"](../../2014/tutorials/lesson-3-processing-the-market-basket-mining-structure.md)  
  
  