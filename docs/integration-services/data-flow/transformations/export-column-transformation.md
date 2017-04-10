---
title: "Преобразование &#171;Экспорт столбца&#187; | Microsoft Docs"
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
  - "sql13.dts.designer.exportcolumntrans.f1"
helpviewer_keywords: 
  - "экспорт данных"
  - "параметры дозаписи [службы Integration Services]"
  - "преобразование «Экспорт столбца» [службы Integration Services]"
  - "столбцы [службы Integration Services], экспорт"
  - "вставка данных"
  - "параметры усечения [службы Integration Services]"
ms.assetid: 678d2dfc-e40c-4fbb-b2cc-42fffc44478a
caps.latest.revision: 45
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 45
---
# Преобразование &#171;Экспорт столбца&#187;
  Преобразование «Экспорт столбца» считывает данные из потока и вставляет их в файл. Например, если поток данных содержит сведения о продукте, такие как изображения каждого продукта, можно применить преобразование «Экспорт столбца» для сохранения изображений в файлы.  
  
## Параметры присоединения и усечения  
 Следующая таблица описывает, как изменение настроек присоединения и усечения влияет на результаты.  
  
|Append|Усечение|Файл существует|Результаты|  
|------------|--------------|-----------------|-------------|  
|False|False|Нет|Это преобразование создает новый файл и записывает в него данные.|  
|True|False|Нет|Это преобразование создает новый файл и записывает в него данные.|  
|False|True|Нет|Это преобразование создает новый файл и записывает в него данные.|  
|True|True|Нет|Преобразованию не удается провести проверку времени разработки. Оба этих свойства не могут быть установлены для **true**.|  
|False|False|Да|Возникает ошибка во время выполнения. Файл существует, но преобразование не имеет к нему доступа для записи.|  
|False|True|Да|Преобразование удаляет файл, затем создает новый и записывает в него данные.|  
|True|False|Да|Преобразование открывает файл и записывает данные в конец файла.|  
|True|True|Да|Преобразованию не удается провести проверку времени разработки. Оба этих свойства не могут быть установлены для **true**.|  
  
## Настройка преобразования «Экспорт столбца»  
 Можно настроить преобразование «Экспорт столбца» следующим образом:  
  
-   Обозначьте столбцы данных и столбцы, содержащие путь к файлам, в которые будут записаны данные.  
  
-   Обозначьте, следует ли операции вставки данных перезаписывать файлы или дописывать к ним.  
  
-   Укажите, будет ли записана в файл отметка порядка байтов (BOM).  
  
    > [!NOTE]  
    >  Отметка порядка байтов будет записана только в том случае, если данные не были добавлены в конец уже существующего файла и если эти данные типа DT_NTEXT.  
  
 Преобразование использует пару входных столбцов: первый содержит имя файла, второй — данные. Каждая строка в наборе данных может указывать отдельный файл. По мере обработки строк преобразованием данные записываются в указанный файл. Во время выполнения преобразование создает файлы, если они до этого не существовали, и записывает в них данные. Записываемые данные должны иметь тип DT_TEXT, DT_NTEXT или DT_IMAGE. Дополнительные сведения см. в статье [Integration Services Data Types](../../../integration-services/data-flow/integration-services-data-types.md).  
  
 Это преобразование имеет один вход, один выход и один выход ошибок.  
  
 Значения свойств можно задавать с помощью конструктора [!INCLUDE[ssIS](../../../includes/ssis-md.md)] или программными средствами.  
  
 Дополнительные сведения о свойствах, которые можно установить в диалоговом окне **Редактор преобразования "Экспорт столбца"**, см. в разделе [Редактор преобразования "Экспорт столбца" (страница "Столбцы")](../../../integration-services/data-flow/transformations/export-column-transformation-editor-columns-page.md).  
  
 Диалоговое окно **Расширенный редактор** содержит свойства, которые можно установить с помощью программных средств. Дополнительные сведения о свойствах, которые вы можете задать в диалоговом окне **Расширенный редактор** или программными средствами, см. в следующих разделах.  
  
-   [Общие свойства](../Topic/Common%20Properties.md)  
  
-   [Пользовательские свойства преобразований](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 Дополнительные сведения о настройке свойств см. в разделе [Установление свойств компонента потока данных](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
  