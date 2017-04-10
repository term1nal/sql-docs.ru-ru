---
title: "Удаление источника данных в обозревателе решений (многомерные службы SSAS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.asvs.deleteobjects.f1"
helpviewer_keywords: 
  - "источники данных [службы Analysis Services], удаление"
  - "удаление источников данных"
  - "удаление источников данных"
ms.assetid: b45441ef-f909-4736-98b9-cc80d0acac99
caps.latest.revision: 46
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 46
---
# Удаление источника данных в обозревателе решений (многомерные службы SSAS)
  Удалив объект источника данных, можно окончательно исключить его из проекта многомерной модели служб Analysis Services.  
  
 В службах [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]источники данных представляют собой основу для построения представлений источников данных, которые в свою очередь используются для определения измерений, кубов и структур интеллектуального анализа данных в проекте или базе данных служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Таким образом, удаление источника данных может сделать недействительными другие объекты служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] в проекте служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Перед тем как удалить объект, необходимо всегда проверять список зависимых объектов, открываемый до удаления.  
  
> [!IMPORTANT]  
>  Источники данных, от которых зависят другие объекты, не могут быть удалены из базы данных служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , открытых в среде [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] в режиме в сети. Следует удалить все объекты в базе данных служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , которые зависят от источника данных, до удаления его самого. Дополнительные сведения о режиме в сети см. в разделе [Connect in Online Mode to an Analysis Services Database](../../analysis-services/multidimensional-models/connect-in-online-mode-to-an-analysis-services-database.md).  
  
### Удаление источника данных  
  
1.  Откройте проект в среде [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]или подключитесь к базе данных, из которой необходимо удалить источник данных.  
  
2.  В **обозревателе решений**откройте папку **Источники данных** .  
  
3.  Щелкните правой кнопкой мыши источник данных и выберите пункт **Удалить**. Появится диалоговое окно **Удаление объектов**  со списком объектов, которые станут недействительными при удалении этого источника данных. Внимательно просмотрите список, прежде чем нажать кнопку **ОК** и удалить источник данных.  
  
4.  Сохраните проект.  
  
     После удаления источника данных из проекта служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] необходимо сохранить в проекте изменения, чтобы не получить сообщение об ошибке при следующем его открытии, так как при обработке XML-файла для удаленного источника данных будет выдана ошибка.  
  
## См. также  
 [Источники данных в многомерных моделях](../../analysis-services/multidimensional-models/data-sources-in-multidimensional-models.md)   
 [Поддерживаемые источники данных (службы SSAS — многомерные базы данных)](../../analysis-services/multidimensional-models/supported-data-sources-ssas-multidimensional.md)  
  
  