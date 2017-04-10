---
title: "Задача &#171;Обработка средствами Analysis Services&#187; | Microsoft Docs"
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
  - "sql13.dts.designer.asprocessingtask.f1"
helpviewer_keywords: 
  - "задача «Обработка средствами Analysis Services»"
  - "обработка объектов [службы Integration Services]"
ms.assetid: e5748836-b4ce-4e17-ab6b-617a336f02f4
caps.latest.revision: 52
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 52
---
# Задача &#171;Обработка средствами Analysis Services&#187;
  Задача «Обработка службами [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] » обрабатывает объекты [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , такие как табличные модели, кубы, измерения и модели интеллектуального анализа данных.  
  
 При обработке табличных моделей имейте в виду следующее.  
  
-   Невозможно выполнить анализ влияния на табличных моделях.  
  
-   Не отображаются некоторые параметры обработки для табличного режима, такие как процесс дефрагментации и процесс повторного вычисления. Эти функции вы можете выполнить с помощью задачи «Выполнение инструкции DDL».  
  
-   Параметры «Обработка индексов» и «Обработка с обновлением» не подходят для табличной модели и не должны использоваться.  
  
-   Параметры пакетов не учитываются в табличных моделях.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] содержат множество задач, выполняющих операции бизнес-аналитики, такие как выполнение инструкций языка описания данных DDL и запросов прогноза интеллектуального анализа данных. Дополнительные сведения о задачах, связанных с бизнес-аналитикой, см. в следующих разделах:  
  
-   [Задача «Выполнение инструкции DDL служб Analysis Services»](../../integration-services/control-flow/analysis-services-execute-ddl-task.md)  
  
-   [Задача «Запрос интеллектуального анализа данных»](../../integration-services/control-flow/data-mining-query-task.md)  
  
## Обработка объектов  
 В одно и то же время могут обрабатываться множество объектов. При обработке множества объектов, определенные настройки применяются для обработки всех объектов в пакете.  
  
 В пакете объекты могут обрабатываться последовательно или параллельно. Если пакет не содержит объекты, для которых важна последовательная обработка, то параллельная обработка может увеличить скорость обработки. Если объекты в пакете обрабатываются параллельно, то можно настроить задачу так, чтобы позволить ей определять, сколько объектов обрабатывать параллельно, или можно вручную указать количество объектов, обрабатываемых одновременно. Если объекты обрабатываются последовательно, можно установить атрибут транзакции пакета: прикрепить все объекты к одной транзакции или использовать отдельную транзакцию для каждого объекта в пакете.  
  
 При обработке объектов аналитики, возможно, будет необходимо обработать объекты, зависимые от них. Задача «Обработка службами [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] » содержит параметр, указывающий на необходимость обработать любые зависимые объекты в дополнение к выбранным объектам.  
  
 Обычно таблицы измерений обрабатываются перед таблицами фактов. Попытка обработать таблицы фактов перед таблицами измерений может вызвыть ошибку.  
  
 Эта задача также позволяет настраивать обработку ошибок в ключах измерений. Например, задача может пропустить ошибки или остановиться, после того как произойдет определенное количество ошибок. Задача может использовать заданную по умолчанию конфигурацию ошибок или может создать пользовательскую конфигурацию ошибок. В пользовательской конфигурации ошибок можно указать, как задача обрабатывает ошибки, и условия возникновения ошибок. Например, можно указать, что задача должна прекращать выполнение, когда произошла четвертая ошибка, или указать, как задача должна обрабатывать ключевые значения **NULL** . Пользовательская конфигурация ошибок может также содержать путь к журналу ошибок.  
  
> [!NOTE]  
>  Задача «Обработка службами [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]» может обрабатывать только объекты аналитики, созданные с использованием средств [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Задача часто применяется вместе с задачей «Массовая вставка», которая загружает данные в таблицу [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , или задачей потока данных, которая выполняет поток данных, загружающий данные в таблицу. Например, задача потока данных может иметь поток данных, который извлекает данные из базы данных интерактивной обработки транзакций (OLTP) и загружает их в таблицу фактов хранилища данных, затем для обработки куба, основанного на хранилище данных, вызывается задача "Обработка службами [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]".  
  
 Задача «Обработка средствами [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] » использует диспетчер соединений служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] для подключения к экземпляру служб [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Дополнительные сведения см. в статье [Analysis Services Connection Manager](../../integration-services/connection-manager/analysis-services-connection-manager.md).  
  
## Обработка ошибок  
  
## Настройка задачи «Обработка средствами Analysis Services»  
 Значения свойств можно задавать с помощью конструктора [!INCLUDE[ssIS](../../includes/ssis-md.md)] или программными средствами.  
  
 Дополнительные сведения о свойствах, которые можно задать в конструкторе служб [!INCLUDE[ssIS](../../includes/ssis-md.md)] , см. в следующих разделах:  
  
-   [Редактор задачи "Обработка средствами Analysis Services" (страница "Общие")](../../integration-services/control-flow/analysis-services-processing-task-editor-general-page.md)  
  
-   [Редактор задачи "Обработка средствами Analysis Services" (страница "Службы Analysis Services")](../../integration-services/control-flow/analysis-services-processing-task-editor-analysis-services-page.md)  
  
-   [Страница «Выражения»](../../integration-services/expressions/expressions-page.md)  
  
 Дополнительные сведения об установке этих свойств в конструкторе служб [!INCLUDE[ssIS](../../includes/ssis-md.md)] см. в следующем разделе:  
  
-   [Задание свойств задач или контейнеров](../Topic/Set%20the%20Properties%20of%20a%20Task%20or%20Container.md)  
  
## Настройка задачи «Обработка средствами Analysis Services» программными средствами  
 Дополнительные сведения о программной настройке этих свойств см. в следующих разделах:  
  
-   <xref:Microsoft.DataTransformationServices.Tasks.DTSProcessingTask.DTSProcessingTask>  
  
  