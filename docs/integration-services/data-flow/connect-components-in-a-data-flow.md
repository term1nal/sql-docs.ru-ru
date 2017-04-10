---
title: "Соединение компонентов в потоке данных | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "компоненты [службы Integration Services], подключения"
  - "подключения [службы Integration Services], компоненты потока данных"
ms.assetid: 70616a58-8921-4218-85bf-f3e90c5a9dbf
caps.latest.revision: 41
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 40
---
# Соединение компонентов в потоке данных
  Эта процедура описывает способ соединения выхода компонентов в потоке данных с другими компонентами того же потока.  
  
### Соединение компонентов в потоке данных  
  
1.  В среде [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]откройте проект служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , содержащий необходимый пакет.  
  
2.  Чтобы открыть пакет, дважды щелкните его в обозревателе решений.  
  
3.  Перейдите на вкладку **Поток управления**, затем дважды щелкните задачу потока данных, содержащую поток данных, в котором требуется соединить компоненты.  
  
4.  В области конструктора на вкладке **Поток данных** выберите преобразование или источник, который необходимо соединить.  
  
5.  Перетащите зеленую стрелку выхода преобразования или источника на преобразование или целевой объект. Некоторые компоненты потока данных могут иметь вывод ошибок, который можно соединять аналогичным образом.  
  
    > [!NOTE]  
    >  Некоторые компоненты могут иметь несколько выходов; следовательно, можно подключить каждый выход к отдельному преобразованию или целевому объекту.  
  
6.  Чтобы сохранить обновленный пакет, выберите пункт **Сохранить выбранные элементы** в меню **Файл** .  
  
## См. также  
 [Добавление или удаление компонента в потоке данных](../../integration-services/data-flow/add-or-delete-a-component-in-a-data-flow.md)   
 [Настройка вывода ошибок в компоненте потока данных](../../integration-services/troubleshooting/configure-an-error-output-in-a-data-flow-component.md)   
 [Поток данных](../../integration-services/data-flow/data-flow.md)  
  
  