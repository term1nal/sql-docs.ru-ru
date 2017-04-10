---
title: "Добавление логики измерений к измерению | Microsoft Docs"
ms.custom: ""
ms.date: "03/23/2017"
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
  - "расширения бизнес-аналитики [службы Analysis Services], логика операций с измерениями"
  - "измерения [службы Analysis Services], расширения бизнес-аналитики"
  - "логика измерений [службы Analysis Services]"
  - "Type, свойство"
ms.assetid: b64fa386-eac2-4286-a320-0631a1887aac
caps.latest.revision: 32
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Добавление логики измерений к измерению
  Добавьте расширение логики измерений к кубу или измерению, чтобы задать для измерения стандартный бизнес-тип. Данное расширение также указывает соответствующие типы атрибутов измерения. Клиентские приложения могут использовать эти характеристики типа при анализе данных.  
  
 Чтобы добавить логику измерений, используйте мастер бизнес-аналитики и выберите параметр **Определить логику операций с измерениями** на странице **Выбор расширения** . После этого мастер проведет по шагам, позволяющим выбрать измерение, к которому необходимо применить логику измерений, а также определить атрибуты для выбранного измерения.  
  
## Выбор измерения  
 На первой странице **Параметры логики операций с измерениями** мастера указывается измерение, к которому необходимо применить логику измерений. Добавление расширения логики измерений к выбранному измерению приведет к изменениям измерения. Эти изменения будут наследоваться всеми кубами, включающими выбранное измерение.  
  
> [!NOTE]  
>  При выборе пункта **Счет** в качестве измерения указывается логика операций со счетами для измерения. Дополнительные сведения см. в разделе [Добавление логики операций со счетами к измерению](../../analysis-services/multidimensional-models/add-account-intelligence-to-a-dimension.md).  
  
## Указание атрибутов измерения  
 Выбор, сделанный на странице **Определение логики операций с измерениями** в списке **Тип измерения** , задает свойство измерения **Type** . Свойство **Type** предоставляет данные серверам и клиентским приложениям о содержании измерения. Некоторые параметры предоставляют клиентским приложениям только справочные сведения; такие параметры необязательны. Другие параметры, такие как Accounts или Time, определяют конкретные режимы и могут быть востребованы для реализации конкретных расширений бизнес-аналитики. Например, среда SQL Server Management Studio использует тип измерения для определения измерения «Валюта» и установки соответствующих правил конвертации валюты. Параметром по умолчанию, устанавливаемым для **Тип измерения** , является **Обычный**, что не дает представления о содержимом измерения.  
  
 Выбрав тип измерения, во вкладке **Атрибуты измерения**столбца **Включить** установите флажок рядом с каждым стандартным типом атрибута, которому соответствует определенный атрибут в измерении. В столбце **Атрибут измерения** разверните раскрывающийся список и выберите атрибут в измерении, соответствующий выбранному типу атрибута. При выборе атрибута из этого списка устанавливается свойство атрибута **Type** для атрибутов.  
  
 Например, необходимо добавить логику измерений к измерению «Учетные записи». В списке **Тип измерения**выберите пункт **Учетные записи**. Затем, если у измерения есть атрибуты **Тип учетной записи** и **Описание учетной записи** , в столбце **Включить** установите флажки напротив типов учетной записи **Имя учетной записи** и **Тип учетной записи** . В столбце **Атрибут измерения** свяжите эти типы учетной записи с атрибутами измерения **Описание учетной записи** и **Тип учетной записи** соответственно.  
  
## См. также  
 [Определение вычислений логики операций со временем с использованием мастера бизнес-аналитики](../../analysis-services/multidimensional-models/define-time-intelligence-calculations-using-the-business-intelligence-wizard.md)  
  
  