---
title: "Категория событий отчеты о состоянии | Документы Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- progress events [Analysis Services]
- Progress Reports event category
- event classes [Analysis Services], progress reports
ms.assetid: c130f160-28ef-49bc-9ee6-da47dc9aab2a
caps.latest.revision: 23
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3489d5176553ba8482646610a048955b93399043
ms.contentlocale: ru-ru
ms.lasthandoff: 09/01/2017

---
# <a name="progress-reports-event-category"></a>категория событий «Отчеты о состоянии»
  Категория событий «Отчеты о состоянии» содержит классы событий, описанные в следующей таблице.  
  
|Класс событий|Идентификатор события|Description|  
|-----------------|--------------|-----------------|  
|Начало отчета о состоянии|5|Позволяет собрать все события начала отчета о состоянии с момента запуска трассировки.|  
|Окончание отчета о состоянии|6|Собирает все события окончания отчета о состоянии с момента запуска трассировки.|  
|Текущий отчет о состоянии|7|Собирает все текущие события отчета о состоянии с момента запуска трассировки. Например, во время обработки текущие отчеты включают в себя данные, относящиеся к обрабатываемым объектам (измерения, секции, куб и т. д.).|  
|Ошибка отчета о состоянии|8|Собирает все события ошибки отчета о состоянии с момента запуска трассировки.|  
  
 Каждое событие начала отчета о состоянии начинается с потока событий состояния и завершается событием конца отчета о состоянии. В потоке может содержаться любое количество событий ошибки отчета о состоянии и текущих событий отчета о состоянии.  
  
 Дополнительные сведения о столбцах, связанных с каждым из классов событий «Отчеты о состоянии», см. в разделе [Progress Reports Data Columns](../../analysis-services/trace-events/progress-reports-data-columns.md).  
  
## <a name="see-also"></a>См. также  
 [События трассировки служб Analysis Services](../../analysis-services/trace-events/analysis-services-trace-events.md)  
  
  