---
title: "Просмотр куба | Microsoft Docs"
ms.custom: ""
ms.date: "02/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: 3819946e-d3fa-4c1d-afe3-599c938b1b2e
caps.latest.revision: 18
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Просмотр куба
После развертывания куба данные куба отображаются на вкладке **Обозреватель** конструктора кубов, а данные измерений отображаются на вкладке **Браузер** конструктора измерений. Просмотр данных куба и измерения позволяет постепенно проверять свою работу. Можно видеть, что небольшие изменения свойств, связей и других объектов оказывают нужный эффект после обработки объекта. Вкладка «Обозреватель» используется как для данных куба, так и для данных измерения, однако в зависимости от просматриваемого объекта она предлагает разные возможности.  
  
Для измерений вкладка «Обозреватель» позволяет просматривать элементы или осуществлять навигацию по иерархии вплоть до конечных узлов. Данные измерения можно просматривать на разных языках, если в модель были добавлены переводы.  
  
Для кубов вкладка «Обозреватель» предлагает два подхода для просмотра данных. С помощью встроенного конструктора запросов многомерных выражений можно создавать запросы, которые возвращают плоский набор строк из многомерной базы данных. Кроме того, можно использовать ярлык Excel. При запуске из среды [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]Excel открывается со сводной таблицей на листе и уже определенным подключением к базе данных рабочей области модели.  
  
Как правило, Excel предлагает более широкие возможности просмотра, поскольку позволяет исследовать данные куба в интерактивном режиме с использованием горизонтальной и вертикальной оси для анализа связей в данных. Напротив, конструктор запросов многомерных выражений ограничен одной осью. Более того, поскольку набор строк является плоским, получить углубленную детализацию, обеспечиваемую сводными таблицами Excel, невозможно. При добавлении новых измерений и иерархий в куб, что предстоит на следующих занятиях, Excel будет предпочтительным решением для просмотра данных.  
  
### Просмотр развернутого куба  
  
1.  В **конструкторе измерений** среды [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]откройте измерение «Продукт». Для этого дважды щелкните измерение **Продукт** в узле **Измерения** обозревателя решений.  
  
2.  Перейдите на вкладку **Браузер** , чтобы просмотреть элемент **Все** иерархии атрибутов **Product Key** . На третьем занятии будет определена пользовательская иерархия для измерения «Продукты», позволяющая просматривать это измерение.  
  
3.  Перейдите в **конструктор кубов** среды [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Чтобы сделать это, дважды щелкните куб **Учебник по службам Analysis Services**, который находится в узле **Кубы** в дереве обозревателя решений.  
  
4.  Перейдите на вкладку **Браузер** и на панели инструментов конструктора нажмите значок **Повторное соединение** .  
  
    Левая панель конструктора отображает объекты куба учебника по службам [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . В правой части вкладки **Браузер** находятся две панели: верхняя — панель **Фильтр** , нижняя — панель **Данные** . На следующем занятии будет выполнен анализ с помощью средства просмотра кубов.  
  
## Следующее занятие  
[Урок 3. Изменение мер, атрибутов и иерархий](../analysis-services/lesson-3-modifying-measures-attributes-and-hierarchies.md)  
  
## См. также:  
[Редактор запросов многомерных выражений (службы Analysis Services — многомерные данные)](../Topic/MDX%20Query%20Editor%20(Analysis%20Services%20-%20Multidimensional%20Data).md)  
  
  
  