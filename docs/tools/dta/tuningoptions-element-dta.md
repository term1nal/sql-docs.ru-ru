---
title: "Элемент TuningOptions (DTA) | Документы Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- XML
helpviewer_keywords:
- TuningOptions element
ms.assetid: 58a22ba1-8e03-411f-bd46-85e4540f217a
caps.latest.revision: 12
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c8fcdfd21cdbc923bc92e06aca42c7495f5d35e9
ms.contentlocale: ru-ru
ms.lasthandoff: 08/02/2017

---
# <a name="tuningoptions-element-dta"></a>Элемент TuningOptions (DTA)
  Содержит параметры конкретного сеанса настройки.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
<DTAInput>  
    <Server>  
...code removed...  
    <Workload>...</Workload>  
    <TuningOptions>...</TuningOptions>  
```  
  
## <a name="element-characteristics"></a>Характеристики элемента  
  
|Характеристика|Описание|  
|--------------------|-----------------|  
|**Тип данных и длина**|Нет.|  
|**Значение по умолчанию**|Нет.|  
|**Применяемость**|Необязательно. В случае использования может применяться только один раз для каждого элемента **DTAInput** .|  
  
## <a name="element-relationships"></a>Связи элемента  
  
|Связь|Элементы|  
|------------------|--------------|  
|**Родительский элемент**|[Элемент DTAInput &#40; DTA &#41;](../../tools/dta/dtainput-element-dta.md)|  
|**Дочерние элементы**|Элемент**ReportSet** . Дополнительные сведения см. в статье [XML-схема помощника по настройке ядра СУБД](http://go.microsoft.com/fwlink/?linkid=43100).<br /><br /> Элемент**TuningLogTable** . Дополнительные сведения см. в статье [XML-схема помощника по настройке ядра СУБД](http://go.microsoft.com/fwlink/?linkid=43100).<br /><br /> Элемент**NumberOfEvents** . Дополнительные сведения см. в статье [XML-схема помощника по настройке ядра СУБД](http://go.microsoft.com/fwlink/?linkid=43100).<br /><br /> [Элемент TuningTimeInMin &#40; DTA &#41;](../../tools/dta/tuningtimeinmin-element-dta.md)<br /><br /> [Элемент StorageBoundInMB (DTA)](../../tools/dta/storageboundinmb-element-dta.md)<br /><br /> Элемент**MaxKeyColumnsInIndex** . Дополнительные сведения см. в статье [XML-схема помощника по настройке ядра СУБД](http://go.microsoft.com/fwlink/?linkid=43100).<br /><br /> Элемент**MaxColumnsInIndex** . Дополнительные сведения см. в статье [XML-схема помощника по настройке ядра СУБД](http://go.microsoft.com/fwlink/?linkid=43100).<br /><br /> Элемент**MinPercentageImprovement** . Дополнительные сведения см. в статье [XML-схема помощника по настройке ядра СУБД](http://go.microsoft.com/fwlink/?linkid=43100)<br /><br /> [Элемент TestServer &#40; DTA &#41;](../../tools/dta/testserver-element-dta.md)<br /><br /> [Элемент FeatureSet &#40; DTA &#41;](../../tools/dta/featureset-element-dta.md)<br /><br /> [Секционирование элемент &#40; DTA &#41;](../../tools/dta/partitioning-element-dta.md)<br /><br /> [Элемент DropOnlyMode &#40; DTA &#41;](../../tools/dta/droponlymode-element-dta.md)<br /><br /> [Элемент KeepExisting &#40; DTA &#41;](../../tools/dta/keepexisting-element-dta.md)<br /><br /> [Элемент OnlineIndexOperation &#40; DTA &#41;](../../tools/dta/onlineindexoperation-element-dta.md)<br /><br /> [Элемент DatabaseToConnect (DTA)](../../tools/dta/databasetoconnect-element-dta.md)<br /><br /> Элемент**IgnoreConstantsInWorkload** . Дополнительные сведения см. в статье [XML-схема помощника по настройке ядра СУБД](http://go.microsoft.com/fwlink/?linkid=43100).<br /><br /> Элемент**RetainShellDB** . Дополнительные сведения см. в статье [XML-схема помощника по настройке ядра СУБД](http://go.microsoft.com/fwlink/?linkid=43100).|  
  
## <a name="example"></a>Пример  
 Примеры элемента **TuningOptions** см. в разделе [Образцы входных XML-файлов (DTA)](../../tools/dta/xml-input-file-samples-dta.md).  
  
## <a name="see-also"></a>См. также:  
 [Справочник по входным XML-файлам (помощник по настройке ядра СУБД)](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  