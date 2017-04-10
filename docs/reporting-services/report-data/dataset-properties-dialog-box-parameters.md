---
title: "Диалоговое окно &#171;Свойства набора данных&#187; — &#171;Настройки&#187; | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "reference"
f1_keywords: 
  - "10150"
  - "sql13.rtp.rptdesigner.datasetproperties.parameters.f1"
  - "10023"
ms.assetid: 43b00aab-e2c3-4e85-abe1-a2b5a21efeed
caps.latest.revision: 40
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 40
---
# Диалоговое окно &#171;Свойства набора данных&#187; — &#171;Настройки&#187;
  Для добавления, изменения и удаления параметров запроса, включая те, которые связаны с параметрами отчета, используется вкладка **Параметры** диалогового окна **Свойства набора данных** .  
  
 Каждый раз при изменении запроса на вкладке запросов выполняется синтаксический анализ команды запроса. Для каждого параметра запроса, определенного здесь, создается параметр отчета с идентичным именем с учетом регистра. По умолчанию параметр запроса автоматически добавляется к списку параметров запроса и связывается с соответствующим параметром отчета.  
  
 Если значение по умолчанию одного параметра отчета зависит от значения по умолчанию другого параметра отчета, связанного с параметром запроса, порядок параметров отчета (тот, в котором они перечислены в диалоговом окне **Свойства параметров отчета**) важен. Параметр, расположенный ближе к концу списка, может зависеть от параметров, расположенных ближе к началу. Дополнительные сведения о параметрах отчета см. в разделе [Параметры отчета (построитель отчетов и конструктор отчетов)](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md).  
  
## Параметры  
 **Добавить**  
 Добавить в список новый параметр.  
  
 **Delete**  
 Удалить выбранный параметр из списка.  
  
 **Имя параметра**  
 Введите имя параметра запроса, добавленного к набору данных на вкладке **Запрос** диалогового окна **Свойства набора данных**.  
  
 **Значение параметра**  
 Введите значение параметра запроса. Это может быть статическое значение или выражение, которое может ссылаться на объект в отчете, но не на любой элемент или поле отчета. По умолчанию в поле **Значение** содержится выражение, указывающее параметр отчета.  
  
 **Стрелка вверх**  
 Переместить выбранный параметр вверх по списку.  
  
 **Стрелка вниз**  
 Переместить выбранный параметр вниз по списку.  
  
## См. также  
 [Параметры отчета (построитель отчетов и конструктор отчетов)](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [Наборы данных отчетов (службы SSRS)](../../reporting-services/report-data/report-datasets-ssrs.md)   
 [Изменение порядка параметров отчета (построитель отчетов и службы SSRS)](../../reporting-services/report-design/change-the-order-of-a-report-parameter-report-builder-and-ssrs.md)  
  
  