---
title: "Введите элемент (XMLA) | Документы Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Type Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.type
- http://schemas.microsoft.com/analysisservices/2003/engine#Type
- urn:schemas-microsoft-com:xml-analysis#Type
helpviewer_keywords:
- Type element
ms.assetid: 5d898123-a635-402a-be86-8249d7304fa4
caps.latest.revision: 15
author: jeannt
ms.author: jeannt
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 40a6b965ed031572b956814e65f95198671af48b
ms.contentlocale: ru-ru
ms.lasthandoff: 09/01/2017

---
# <a name="type-element-xmla"></a>Элемент Type (XML для аналитики)
  Определяет тип обработки, выполняемой по [процесс](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md) элемента.  
  
## <a name="syntax"></a>Синтаксис  
  
```xml  
  
<Process>  
...  
   <Type>...</Type>  
...  
</Process>  
```  
  
## <a name="element-characteristics"></a>Характеристики элемента  
  
|Характеристика|Описание|  
|--------------------|-----------------|  
|Тип данных и длина|String (перечисление)|  
|Значение по умолчанию|None|  
|Количество элементов|1-1: обязательный элемент, который встречается ровно один раз.|  
  
## <a name="element-relationships"></a>Связи элемента  
  
|Связь|Элемент|  
|------------------|-------------|  
|Родительские элементы|[Процесс](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)|  
|Дочерние элементы|None|  
  
## <a name="remarks"></a>Замечания  
 Дополнительные сведения о параметрах обработки, доступных для объектов в экземпляре [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], в разделе [обработка многомерной модели &#40; Службы Analysis Services &#41; ](../../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md).  
  
 Значение **тип** элемента ограничивается одной из строк, перечисленных в следующей таблице.  
  
|Значение|Description|  
|-----------|-----------------|  
|*ProcessFull*|Удаляет из задействованного объекта все данные, после чего выполняет обработку этого объекта.|  
|*ProcessAdd*|Добавляет к задействованному объекту новые данные.|  
|*ProcessUpdate*|Обновляет данные в задействованном объекте.|  
|*ProcessIndexes*|Создает или перестраивает индексы и агрегаты в задействованном объекте.|  
|*ProcessScriptCache*|Если куб обработан, сервер перестраивает кэш скрипта многомерных выражений. В противном случае возникнет ошибка.<br /><br /> **Примечание** применяется только к кубам.|  
|*ProcessData*|Выполняет обработку данных только в задействованном объекте.|  
|*ProcessDefault*|Определяет состояние задействованного объекта и выполняет обработку, соответствующую режиму этого объекта, с целью его полной оптимизации и перевода в полностью обработанное состояние.|  
|*ProcessClear*|Удаляет данные из задействованного объекта и всех связанных объектов.|  
|*ProcessStructure*|Выполняет обработку структуры только задействованного объекта.|  
|*ProcessClearStructureOnly*|Выполняет очистку данных только в задействованном объекте.|  
  
## <a name="see-also"></a>См. также:  
 [Свойства &#40; XML для Аналитики &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  