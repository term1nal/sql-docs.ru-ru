---
title: "Редактор источника &#171;ODBC&#187; (страница &#171;Столбцы&#187;) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.ssis.designer.odbcsource.columns.f1"
ms.assetid: 565984eb-8318-4be7-bebc-262209cf5065
caps.latest.revision: 7
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 7
---
# Редактор источника &#171;ODBC&#187; (страница &#171;Столбцы&#187;)
  Страница **Столбцы** диалогового окна **Редактор источника ODBC** используется для сопоставления выходного столбца с каждым внешним (исходным) столбцом.  
  
 Дополнительные сведения об источнике ODBC см. в разделе [ODBC Source](../../integration-services/data-flow/odbc-source.md).  
  
## Список задач  
 **Открытие страницы «Столбцы» редактора источника ODBC**  
  
1.  В среде [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]откройте пакет служб [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] , содержащий источник ODBC.  
  
2.  На вкладке **Поток данных** дважды щелкните источник ODBC.  
  
3.  В окне **Редактор источника ODBC**нажмите кнопку **Столбцы**.  
  
## Параметры  
  
### Доступные внешние столбцы  
 Список доступных внешних столбцов источника данных. В этой таблице нельзя добавлять или удалять столбцы. Выберите используемые столбцы источника. Выбранные столбцы добавляются в список **Внешний столбец** в порядке выбора.  
  
 Чтобы выбрать все столбцы, установите флажок **Выделить все** .  
  
### Внешний столбец  
 Представление внешних (исходных) столбцов в порядке, заданном при настройке компонентов, которые обрабатывают данные из источника ODBC.  
  
### Выходной столбец  
 Введите уникальное имя для каждого выходного столбца. По умолчанию используется имя выбранного внешнего (исходного) столбца, однако можно выбрать любое уникальное описательное имя. Введенное имя отображается в конструкторе служб SSIS.  
  
## См. также  
 [Редактор источника ODBC (страница "Диспетчер соединений")](../../integration-services/data-flow/odbc-source-editor-connection-manager-page.md)   
 [Редактор источника ODBC (страница "Вывод ошибок")](../../integration-services/data-flow/odbc-source-editor-error-output-page.md)  
  
  