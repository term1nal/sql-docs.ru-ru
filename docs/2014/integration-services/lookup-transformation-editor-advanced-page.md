---
title: Редактор преобразования Уточняющий запрос (страница "Дополнительно") | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.lookuptransformation.advanced.f1
helpviewer_keywords:
- Lookup Transformation Editor
ms.assetid: f3395c65-0320-47f9-8d83-daaa082d8713
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: aa56e9366fdc60a5b411e19b200706f0404e7312
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/02/2018
ms.locfileid: "48209734"
---
# <a name="lookup-transformation-editor-advanced-page"></a>Редактор преобразования «Уточняющий запрос» (страница «Дополнительно»)
  Используйте вкладку **Дополнительно** диалогового окна **Редактор преобразования «Уточняющий запрос»** для настройки частичного кэширования и для изменения инструкции SQL для преобразования «Уточняющий запрос».  
  
 Дополнительные сведения о преобразовании «Уточняющий запрос» см. в разделе [Lookup Transformation](data-flow/transformations/lookup-transformation.md).  
  
## <a name="options"></a>Параметры  
 **Размер кэша (32-разрядная версия)**  
 Настройте размер кэша (в мегабайтах) для 32-разрядных компьютеров. Значение по умолчанию 5.  
  
 **Размер кэша (64-разрядная версия)**  
 Настройте размер кэша (в мегабайтах) для 64-разрядных компьютеров. Значение по умолчанию 5.  
  
 **Включить кэширование для строк с несовпадающими записями**  
 Кэшировать строки без совпадающих элементов в эталонном наборе данных.  
  
 **Размещение из кэша**  
 Задать долю кэша (в процентах), которую следует выделять для строк без совпадающих элементов в эталонном наборе данных.  
  
 **Изменить инструкцию SQL**  
 Изменить инструкцию SQL, которая используется для формирования эталонного набора данных.  
  
> [!NOTE]  
>  Дополнительная инструкция SQL, которую можно указать на этой странице, заменяет имя таблицы, указанное на странице **Соединение** **Редактора преобразования «Уточняющий запрос»**. Дополнительные сведения см. в разделе [Lookup Transformation Editor &#40;Connection Page&#41;](../../2014/integration-services/lookup-transformation-editor-connection-page.md).  
  
 **Задать параметры**  
 Сопоставить входные столбцы с параметрами, используя диалоговое окно **Установка параметров запроса** .  
  
## <a name="external-resources"></a>Внешние ресурсы  
 Запись в блоге [Режимы кэша уточняющих запросов](http://go.microsoft.com/fwlink/?LinkId=219518) на сайте blogs.msdn.com  
  
## <a name="see-also"></a>См. также  
 [Уточняющий &#40;страница "Общие"&#41;](general-page-of-integration-services-designers-options.md)   
 [Уточняющий &#40;страница "подключения"&#41;](../../2014/integration-services/lookup-transformation-editor-connection-page.md)   
 [Редактор преобразования "Уточняющий запрос" (страница "Столбцы")](../../2014/integration-services/lookup-transformation-editor-columns-page.md)   
 [Уточняющий &#40;странице вывода ошибок&#41;](../../2014/integration-services/lookup-transformation-editor-error-output-page.md)   
 [Integration Services Error and Message Reference](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Преобразование "Нечеткий уточняющий запрос"](data-flow/transformations/fuzzy-lookup-transformation.md)  
  
  
