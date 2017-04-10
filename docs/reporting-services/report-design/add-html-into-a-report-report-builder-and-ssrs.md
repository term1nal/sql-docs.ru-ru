---
title: "Добавление HTML в отчет (построитель отчетов и службы SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 30bd631a-f774-48e7-a13a-b6c2eb54d9bb
caps.latest.revision: 8
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 8
---
# Добавление HTML в отчет (построитель отчетов и службы SSRS)
  С помощью заполнителя можно импортировать HTML из поля в наборе данных, чтобы использовать в отчете. По умолчанию заполнитель представляет простой текст, поэтому нужно изменить тип разметки заполнителя на HTML. Дополнительные сведения см. в разделе [Импорт HTML в отчет (построитель отчетов и службы SSRS)](../../reporting-services/report-design/importing-html-into-a-report-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### Добавление HTML из поля набора данных в текстовое поле  
  
1.  На вкладке **Вставка** щелкните **Список**. Щелкните в области конструктора и перетащите указатель мыши, чтобы создать поле нужного размера.  
  
     Откроется диалоговое окно **Свойства набора данных** . Можно использовать общий набор данных или набор данных, внедренный в отчет. Чтобы получить дополнительные сведения, щелкните [Диалоговое окно "Свойства набора данных" — "Запрос" (построитель отчетов)](../../reporting-services/report-data/dataset-properties-dialog-box-query-report-builder.md) или [Диалоговое окно "Свойства набора данных" — "Запрос"](../Topic/Dataset%20Properties%20Dialog%20Box,%20Query.md).  
  
2.  На вкладке **Вставка** щелкните **Текстовое поле**. Щелкните в списке и перетащите указатель мыши, чтобы создать поле нужного размера.  
  
3.  Перетащите в текстовое поле HTML-поле из набора данных. Для поля создается заполнитель.  
  
4.  Щелкните правой кнопкой мыши заполнитель и выберите пункт **Свойства местозаполнителя**.  
  
5.  На вкладке **Общие** убедитесь, что поле **Значение** содержит выражение, которое оценивается как поле, перемещенное на шаге 3.  
  
6.  Установите флажок **HTML — интерпретировать теги HTML как стили**. Тем самым поля будут вычисляться как HTML.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## См. также  
 [Форматирование чисел и дат (построитель отчетов и службы SSRS)](../../reporting-services/report-design/formatting-numbers-and-dates-report-builder-and-ssrs.md)   
 [Форматирование линий, цветов и изображений (построитель отчетов и службы SSRS)](../../reporting-services/report-design/formatting-lines-colors-and-images-report-builder-and-ssrs.md)   
 [Диалоговое окно "Свойства заполнителя" — "Общие" (построитель отчетов и службы SSRS)](../Topic/Placeholder%20Properties%20Dialog%20Box,%20General%20\(Report%20Builder%20and%20SSRS\).md)  
  
  