---
title: "Контейнер последовательности | Microsoft Docs"
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
  - "sql13.dts.designer.sequencecontainer.f1"
helpviewer_keywords: 
  - "контейнер последовательности"
  - "группирование потоков управления"
  - "контейнеры [службы Integration Services], последовательность"
  - "подмножество потока управления [службы Integration Services]"
ms.assetid: 7731f91e-b8b3-4d96-a0d9-73f568547cb3
caps.latest.revision: 48
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 48
---
# Контейнер последовательности
  Контейнер последовательности определяет поток управления, являющийся подмножеством потока управления пакета. Контейнер последовательности группирует пакет в несколько отдельных потоков управления, каждый из которых содержит одну или более задач и контейнеров, выполняющихся в общем потоке управления.  
  
 Помимо других контейнеров, контейнер последовательности может включать несколько задач. Добавление задач и контейнеров к контейнеру последовательности аналогично их добавлению к пакету, за исключением случаев, когда вместо контейнера пакетов задачи и контейнеры перетаскиваются в контейнер последовательности. Если контейнер последовательности включает более одной задачи или контейнера, то их можно соединить с помощью управлений очередностью так же, как и в пакете. Дополнительные сведения см. в разделе [Precedence Constraints](../../integration-services/control-flow/precedence-constraints.md).  
  
 Применение контейнера последовательности дает множество преимуществ:  
  
-   Отключение групп задач, если нужно сосредоточить отладку пакета на одном подмножестве потока управления пакета;  
  
-   Управление свойствами нескольких задач одновременно путем определения этих свойств в контейнере последовательности, а не в каждой отдельной задаче.  
  
     Например, свойству **Disable** контейнера последовательности можно присвоить значение **True** , что позволит отключить все задачи и контейнеры в контейнере последовательности.  
  
-   Создание области видимости для переменных, которыми может пользоваться группа связанных задач и контейнеров.  
  
-   Следует группировать такое количество задач, чтобы ими можно было легче управлять, сворачивая и разворачивая контейнер последовательности.  
  
     Помимо этого, с помощью окна **Группа** можно создать группы задач, способные разворачиваться и сворачиваться. Окно **Группа** появляется только во время проектирования, во время выполнения у него нет свойств или поведения. Дополнительные сведения см. в разделе [Группирование или разгруппирование компонентов](../../integration-services/group-or-ungroup-components.md).  
  
-   Задайте атрибут транзакции для контейнера последовательности, чтобы определить транзакцию для подмножества потока управления пакета. Таким образом, возможно выполнение транзакции на более детальном уровне.  
  
     Например, если в контейнере последовательности находятся две связанные задачи: одна удаляет данные из таблицы, а вторая вставляет данные в таблицу, можно настроить транзакцию так, чтобы гарантировать, что удаление будет отменено, если произойдет ошибка во время операции вставки. Дополнительные сведения см. в разделе [Транзакции служб Integration Services](../../integration-services/integration-services-transactions.md).  
  
## Настройка контейнера последовательности  
 У контейнера последовательности нет отдельного интерфейса пользователя, его можно настроить только в окне **Свойства** среды [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] или программно.  
  
 Дополнительные сведения о задании этих свойств программными средствами см. в документации по классу **T:Microsoft.SqlServer.Dts.Runtime.Sequence** в руководстве для разработчиков.  
  
## Связанные задачи  
 Дополнительные сведения о настройке свойств этого компонента [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] см. в разделе [Задание свойств задач или контейнеров](../Topic/Set%20the%20Properties%20of%20a%20Task%20or%20Container.md).  
  
## См. также  
 [Добавление задачи или контейнера в поток управления или удалить их из него](../../integration-services/control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)   
 [Соединение задач и контейнеров с помощью элементов управления очередностью по умолчанию](../Topic/Connect%20Tasks%20and%20Containers%20by%20Using%20a%20Default%20Precedence%20Constraint.md)   
 [Контейнеры служб Integration Services](../../integration-services/control-flow/integration-services-containers.md)  
  
  