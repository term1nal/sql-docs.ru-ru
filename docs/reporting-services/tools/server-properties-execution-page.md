---
title: "Свойства сервера (страница &#171;Выполнение&#187;) | Microsoft Docs"
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
f1_keywords: 
  - "sql13.swb.reportserver.serverproperties.execution.f1"
ms.assetid: 53b77db1-b013-4dac-82dd-30c0de276639
caps.latest.revision: 32
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 32
---
# Свойства сервера (страница &#171;Выполнение&#187;)
  Используйте данную страницу для установки значения времени ожидания для выполнения отчета. Это значение применяется ко всем отчетам, обрабатываемым текущим экземпляром сервера отчетов. Для отдельных отчетов это значение можно заменить. Указанное значение должно охватывать все операции по обработке отчета, выполняемые на сервере отчетов, с учетом обработки запросов, выполняемой на сервере базы данных в то время, когда сервер отчетов получает данные, используемые в отчете.  
  
 Чтобы открыть эту страницу, в среде [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] подключитесь к экземпляру сервера отчетов, щелкните его правой кнопкой мыши и выберите пункт **Свойства**. Нажмите кнопку **Выполнение** , чтобы открыть эту страницу.  
  
## Параметры  
 **Не задавать время ожидания для выполнения отчета**  
 Допускать неограниченное время на сервере отчетов для завершения обработки отчета.  
  
 **Ограничить выполнение отчета следующим количество секунд**  
 Установить ограничение по продолжительности выполнения отчета. Этот период времени начинается во время запрашивания отчета. Если этот период времени заканчивается до полной обработки отчета, то сервер отчетов отменяет процесс и все связанные с ним запросы к внешним источникам данных.  
  
## См. также  
 [Установка свойств сервера отчетов (среда Management Studio)](../../reporting-services/tools/set-report-server-properties-management-studio.md)   
 [Подключение к серверу отчетов в среде Management Studio](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
 [Установка свойств обработки отчетов](../../reporting-services/report-server/set-report-processing-properties.md)   
 [Задание значений времени ожидания при обработке отчетов и общих наборов данных (SSRS)](../../reporting-services/report-server/setting-time-out-values-for-report-and-shared-dataset-processing-ssrs.md)   
 [Справка F1 по использованию сервера отчетов среде Management Studio](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)  
  
  