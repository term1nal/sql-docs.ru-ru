---
title: "Проектирование агрегатов (службы Analysis Services — многомерные данные) | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
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
  - "статистические выражения [службы Analysis Services], секции"
  - "секции [службы Analysis Services], агрегаты"
ms.assetid: 3072b7e0-6961-42ad-a287-16f391f2cec4
caps.latest.revision: 33
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 33
---
# Проектирование агрегатов (службы Analysis Services — многомерные данные)
  Агрегатами называются предварительно вычисленные сводки по данным куба, помогающие службам [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ускорить выполнение запросов.  
  
 Для настройки параметров хранения и проектирования статистических схем для секции применяется мастер статистических схем. Мастер работает с одной секцией группы мер, поэтому каждую секцию можно настроить по-своему. Мастер руководит настройкой хранилища и проектированием статистических схем для секции. Для получения дополнительных сведений о настройке хранилища см.  
  
 Выберите метод управления количеством статистических схем, которые будет строить мастер, и запустите проектирование.  
  
 Задача — спроектировать оптимальное количество статистических схем. Это количество должно не только обеспечивать приемлемое время ответа, но предотвращать лишний рост размеров сегмента. С увеличением количества статистических схем уменьшается время ответа, но увеличивается пространство, которое требуется для их хранения, и время вычисления. Кроме того, первые агрегаты, намного сильнее увеличивают производительность, чем последующие. Уменьшение количества менее полезных агрегатов так же может увеличить производительность. Для управления количеством агрегатов, которые проектирует мастер, можно использовать один из следующих методов.  
  
-   Укажите ограничение на размер пространства для хранения агрегатов.  
  
-   Укажите ограничение на увеличение производительности.  
  
-   Вручную остановите работу мастера, когда кривая производительности начнет снижаться до приемлемого уровня увеличения производительности.  
  
-   Отмените проектирование агрегатов.  
  
 Чтобы построить хранилище, мастер должен иметь возможность соединяться со службами [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] на целевом сервере. Если службы [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] не запущены на целевом сервере или процесс проектирования не может к нему подключиться, появится сообщение об ошибке.  
  
 Последний шаг мастера позволяет продолжить или отложить обработку. В первом случае будут созданы спроектированные агрегаты, а во втором они будут сохранены для будущей обработки. В зависимости от размеров секции, обработка может занять значительное время. При необходимости можно прервать обработку секции.  
  
## См. также  
 [Агрегаты и статистические схемы](../../analysis-services/multidimensional-models-olap-logical-cube-objects/aggregations-and-aggregation-designs.md)  
  
  