---
title: "Настройки сведений об устройстве ATOM | Microsoft Docs"
ms.custom: ""
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: fe4a56a4-5552-423c-85c1-895e2e212fee
caps.latest.revision: 7
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 7
---
# Настройки сведений об устройстве ATOM
  Настройки сведений об устройстве для модуля подготовки отчетов Atom включают параметры отправки имени веб-канала Atom и используемую кодировку.  
  
 В следующей таблице перечислены настройки сведений об устройстве для подготовки к просмотру в документе службы данных.  
  
|Настройка|Значение|  
|-------------|-----------|  
|**DataFeed**|Если указано, веб-канал Atom подготавливается к просмотру в соответствии с именем канала, указанным в этой настройке. В противном случае производится подготовка к просмотру сервисного документа Atom для отчета. Уникальный автоматически сформированный идентификатор канала данных. Это значение используется для внутренних целей и не подлежит изменению.|  
|**Кодировка**|Определенное комитетом по цифровым адресам в Интернете (IANA) название кодировки символов, поддерживаемой платформой .NET Framework. Значение по умолчанию — **UTF-8**. В качестве примеров других значений можно привести ASCII, UTF-7 и UTF-16.|  
  
## См. также  
 <xref:ReportExecution2005.ReportExecutionService.Render%2A>   
 [Передача настроек сведений об устройстве модулям подготовки отчетов к просмотру](../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [Настройка параметров модулей подготовки отчетов в RSReportServer.Config](../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [Технический справочник (службы SSRS)](../reporting-services/technical-reference-ssrs.md)  
  
  