---
title: "Преобразование &#171;Подсчет строк&#187; | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.rowcounttrans.f1"
helpviewer_keywords: 
  - "обновление переменных"
  - "преобразование «Подсчет строк»"
  - "число строк"
  - "переменные [службы Integration Services], обновление"
  - "подсчет строк"
ms.assetid: b68293b9-a68c-40be-9d81-77342da1be29
caps.latest.revision: 43
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 43
---
# Преобразование &#171;Подсчет строк&#187;
  Преобразование «Подсчет строк» подсчитывает строки по мере прохождения их в потоке данных и сохраняет конечный результат в переменной.  
  
 A [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] может обновлять значения переменных, используемых в скриптах, выражениях и выражениях свойств. (Например, переменная, используемая для подсчета строк, может обновить текстовое сообщение электронной почты, добавив количество строк.) Переменная, используемая преобразованием «Подсчет строк», должна существовать и находиться в области задачи потока данных, к которой относится поток данных с преобразованием «Подсчет строк».  
  
 Преобразование сохраняет значение подсчета строк таблицы в переменной только после прохождения последней строки через преобразование. Поэтому значение переменной не обновляется сразу, чтобы использовать обновленное значение в потоке данных, содержащем преобразование «Подсчет строк». Можно использовать обновленную переменную в отдельном потоке данных.  
  
 Это преобразование имеет один вход и один выход. Вывод ошибок не поддерживается.  
  
## Настройка преобразования «Подсчет строк»  
 Значения свойств можно задавать с помощью конструктора [!INCLUDE[ssIS](../../../includes/ssis-md.md)] или программными средствами.  
  
 Диалоговое окно **Расширенный редактор** содержит свойства, которые можно установить с помощью программных средств. Дополнительные сведения о свойствах, которые вы можете задать в диалоговом окне **Расширенный редактор** или программными средствами, см. в следующих разделах.  
  
-   [Общие свойства](../Topic/Common%20Properties.md)  
  
-   [Пользовательские свойства преобразований](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
## Связанные задачи  
 Дополнительные сведения о настройке свойств компонента см. в разделе [Установление свойств компонента потока данных](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## См. также  
 [Переменные в службах Integration Services (SSIS)](../../../integration-services/integration-services-ssis-variables.md)   
 [Поток данных](../../../integration-services/data-flow/data-flow.md)   
 [Преобразования служб Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  