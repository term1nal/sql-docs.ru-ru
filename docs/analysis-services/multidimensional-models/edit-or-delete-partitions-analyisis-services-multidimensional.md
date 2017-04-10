---
title: "Изменение и удаление секций (Analysis Services — многомерные данные) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
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
  - "изменение секций"
  - "секции [службы Analysis Services], изменение"
ms.assetid: fb7a64ca-d021-4926-b92d-83476fbc40a3
caps.latest.revision: 30
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 30
---
# Изменение и удаление секций (Analysis Services — многомерные данные)
  Секции куба редактируются с помощью вкладки **Секции** в конструкторе кубов в [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. На вкладке **Секции** перечислены секции для всех групп мер в кубе. А также секции обратной записи с включенной функцией обратной записи.  
  
 Чтобы изменить секции для любой группы мер, разверните группу мер на вкладке **Секции** . Секции группы мер указываются в списке, основанном на их порядковых номерах, в формате таблицы; перечисленные столбцы см. в следующей таблице.  
  
 Настройки связанной группы мер необходимо редактировать в исходном кубе.  
  
 Удаление секций производится автоматически при слиянии исходной секции с целевой. Секция, указанная как источник, после успешного слияния удаляется. Также можно вручную удалить секции в [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] или на вкладке «Секции» в [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. Щелкните правой кнопкой мыши и выберите команду **Удалить**. Помните, что при удалении секции также удаляются данные и агрегирования. В качестве меры предосторожности обязательно создайте резервную копию базы данных на тот случай, что понадобится отменить данное действие.  
  
> [!NOTE]  
>  Также можно использовать XMLA-скрипты, автоматизирующие задачи по построению, слиянию и удалению секций. XMLA-скрипт может быть создан и выполнен в [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]или в пользовательских SSIS-пакетах, выполняемых как задача по расписанию. Дополнительные сведения см. в статье [Automate Analysis Services Administrative Tasks with SSIS](../../analysis-services/instances/automate-analysis-services-administrative-tasks-with-ssis.md).  
  
## Источник секции  
 Указывает исходную таблицу или именованный запрос для секции. Чтобы изменить исходную таблицу, щелкните ячейку, а затем нажмите кнопку обзора (**...**).  
  
 ![Исходный столбец на панели секции](../../analysis-services/multidimensional-models/media/ssas-partitionsource.png "Исходный столбец на панели секции")  
  
 Если секция основывается на запросе, нажмите кнопку обзора (**...**), чтобы изменить запрос. Это изменит свойство **Source** секции. Дополнительные сведения см. в статье [Change a partition source to use a different fact table](../../analysis-services/multidimensional-models/change-a-partition-source-to-use-a-different-fact-table.md).  
  
 Можно указать таблицу в представлении источника данных, которая имеет такую же структуру, как исходная таблица источника (во внешнем источнике данных, из которого извлекаются данные). Источник может быть в любом из источников данных или представлений источников данных базы данных куба.  
  
## Параметры хранилища  
 В конструкторе кубов на вкладке секций можно щелкнуть **Параметры хранилища** , чтобы выбрать одну из стандартных настроек для реляционного хранилища ROLAP, гибридного HOLAP или многомерного MOLAP или установить пользовательские настройки для режима хранилища и упреждающего кэширования. По умолчанию используется хранилище MOLAP, поскольку оно обеспечивает наилучшую производительность запросов. Дополнительные сведения о каждом параметре см. в разделе [Определение хранилища секции (Analysis Services — многомерные данные)](../../analysis-services/multidimensional-models/set-partition-storage-analysis-services-multidimensional.md).  
  
 Хранилище можно настроить отдельно для каждой секции каждой группы мер в кубе. Также можно установить настройки хранилища по умолчанию для куба или группы мер. Хранилище настраивается на вкладке **Секции** мастера кубов.  
  
## См. также  
 [Создание локальной секции и управление ею (службы Analysis Services)](../../analysis-services/multidimensional-models/create-and-manage-a-local-partition-analysis-services.md)   
 [Проектирование агрегатов (службы Analysis Services — многомерные данные)](../../analysis-services/multidimensional-models/designing-aggregations-analysis-services-multidimensional.md)   
 [Объединение секций в службах Analysis Services (службы SSAS — многомерные данные)](../../analysis-services/multidimensional-models/merge-partitions-in-analysis-services-ssas-multidimensional.md)  
  
  