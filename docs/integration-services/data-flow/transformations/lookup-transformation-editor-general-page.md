---
title: "Редактор преобразования &#171;Уточняющий запрос&#187; (страница &#171;Общие&#187;) | Microsoft Docs"
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
  - "sql13.dts.designer.lookuptransformation.general.f1"
ms.assetid: 4bd15e48-0feb-4f95-be91-5df58105dbfb
caps.latest.revision: 18
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 18
---
# Редактор преобразования &#171;Уточняющий запрос&#187; (страница &#171;Общие&#187;)
  Используйте страницу **Общие** в диалоговом окне «Редактор преобразования "Уточняющий запрос"», чтобы выбрать режим кэширования, выбрать тип соединения и указать метод обработки строк без совпадающих записей.  
  
 Дополнительные сведения о преобразовании «Уточняющий запрос» см. в разделе [Lookup Transformation](../../../integration-services/data-flow/transformations/lookup-transformation.md).  
  
## Параметры  
 **Полное кэширование**  
 Формировать и загружать эталонный набор данных в кэш до запуска преобразования «Уточняющий запрос».  
  
 **Частичное кэширование**  
 При выполнении преобразования «Уточняющий запрос» — создать эталонный набор данных. Загружать в кэш строки с совпадающими записями в эталонном наборе данных и строки без совпадающих записей в наборе данных.  
  
 **Без кэширования**  
 При выполнении преобразования «Уточняющий запрос» — создать эталонный набор данных. Данные в кэш не загружаются.  
  
 **диспетчер соединений с кэшем**  
 Настроить преобразование «Уточняющий запрос» на использование диспетчера соединений с кэшем. Этот параметр доступен только в случае, если выбран параметр «Полное кэширование».  
  
 **диспетчер соединений OLE DB**  
 Настроить преобразование «Уточняющий запрос» на использование диспетчера соединений OLE DB.  
  
 **Метод обработки строк без совпадающих элементов**  
 Выбрать режим для обработки строк, не имеющих совпадения ни с одной из записей в эталонном наборе данных.  
  
 При выборе режима **Перенаправлять строки в выход несовпадающих строк**строки будут перенаправлены в выход несовпадающих строк и не будут обрабатываться как ошибки. Параметр **Ошибка** недоступен на странице **Вывод ошибок** в диалоговом окне **Редактор преобразования «Уточняющий запрос»** .  
  
 При выборе любого другого параметра в списке **Метод обработки строк без совпадающих элементов** , строки будут обрабатываться как ошибки. Параметр **Ошибка** доступен на странице **Вывод ошибок** .  
  
## Внешние ресурсы  
 Запись в блоге [Режимы кэша уточняющих запросов](http://go.microsoft.com/fwlink/?LinkId=219518) на сайте blogs.msdn.com  
  
## См. также  
 [Диспетчер соединений с кэшем](../../../integration-services/data-flow/transformations/cache-connection-manager.md)   
 [Редактор преобразования "Уточняющий запрос" (страница "Соединение")](../../../integration-services/data-flow/transformations/lookup-transformation-editor-connection-page.md)   
 [Редактор преобразования "Уточняющий запрос" (страница "Столбцы")](../../../integration-services/data-flow/transformations/lookup-transformation-editor-columns-page.md)   
 [Редактор преобразования "Уточняющий запрос" (страница "Дополнительно")](../../../integration-services/data-flow/transformations/lookup-transformation-editor-advanced-page.md)   
 [Редактор преобразования "Уточняющий запрос" (страница "Вывод ошибок")](../../../integration-services/data-flow/transformations/lookup-transformation-editor-error-output-page.md)  
  
  