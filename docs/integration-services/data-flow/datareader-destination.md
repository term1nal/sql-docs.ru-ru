---
title: "Назначение DataReader | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.datareaderdest.f1"
helpviewer_keywords: 
  - "назначение DataReader"
  - "назначения [службы Integration Services], поставщик DataReader"
ms.assetid: 56fcc4bf-c901-42c3-a71d-110039293431
caps.latest.revision: 30
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 30
---
# Назначение DataReader
  Назначение DataReader извлекает данные из потока данных с помощью интерфейса ADO.NET **DataReader** . Эти данные могут быть впоследствии использованы другими приложениями. Например, можно настроить источник данных из отчета служб [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] на использование результата выполнения пакета служб [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Для этого нужно создать поток данных, который реализует назначение DataReader.  
  
 Дополнительные сведения о доступе и чтении значений в назначении DataReader программным способом см. в разделе [Загрузка выхода локального пакета](../../integration-services/run-manage-packages-programmatically/loading-the-output-of-a-local-package.md).  
  
## Настройка назначения «DataReader»  
 Можно указать значение времени ожидания для назначения DataReader и установить, должно ли назначение завершиться неудачей по истечении времени ожидания. Время ожидания истекает, если приложение не требует данных в течение заданного промежутка времени.  
  
 Назначение DataReader имеет один вход. Вывод ошибок не поддерживается.  
  
 Значения свойств можно задавать с помощью конструктора [!INCLUDE[ssIS](../../includes/ssis-md.md)] или программными средствами.  
  
 Дополнительные сведения о свойствах, которые вы можете задать в диалоговом окне **Расширенный редактор** или программными средствами, см. в следующих разделах.  
  
-   [Общие свойства](../Topic/Common%20Properties.md)  
  
-   [Пользовательские свойства назначения «Модуль чтения данных»](../../integration-services/data-flow/datareader-destination-custom-properties.md)  
  
 Дополнительные сведения о настройке свойств см. в разделе [Установление свойств компонента потока данных](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
  