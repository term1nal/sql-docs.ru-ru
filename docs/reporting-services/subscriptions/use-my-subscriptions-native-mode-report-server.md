---
title: "Использование страницы &quot;Мои подписки&quot; (сервер отчетов в основном режиме) | Microsoft Docs"
ms.custom: ""
ms.date: "07/01/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "подписки [службы Reporting Services], страница "Мои подписки""
  - "страница «Мои подписки» [службы Reporting Services]"
ms.assetid: e96623ba-677e-4748-8787-f32bed3b5c12
caps.latest.revision: 40
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 38
---
# Использование страницы &quot;Мои подписки&quot; (сервер отчетов в основном режиме)
На веб-портале [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] есть страница **Мои подписки**, которая представляет собой единое место для организации подписок. Страницу *Мои подписки* можно использовать для просмотра, изменения, включения, отключения и удаления существующих подписок. Однако ее нельзя использовать для создания подписок.  Страница «Мои подписки» показывает лишь созданные вами подписки. На ней не отображаются ни подписки, принадлежащие другим пользователям (даже если вы на них подписаны), ни управляемые данными подписки.
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] в основном режиме|  
  
При вводе запроса поле поиска динамически фильтрует список подписок. Выполнить поиск подписок по имени, по сведениям о триггерах, состоянию и т. д. нельзя. Дополнительные сведения см. в разделе [Создание подписок для работающих в основном режиме серверов отчетов и управление этими подписками](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md).
  
## Открытие страницы «Мои подписки»  
1. Откройте веб-портал [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)].
2. Щелкните параметр ![ssrs_portal_settings_gear](../../reporting-services/subscriptions/media/ssrs-portal-settings-gear.png) на панели инструментов.
3. Нажмите кнопку **Мои подписки**.

Дополнительные сведения см. в разделе [Веб-портал служб Reporting Services](../../reporting-services/web-portal-ssrs-native-mode.md).

## Использование Windows PowerShell для перечисления MySubscriptions  
 ![Содержимое, связанное с PowerShell](../../analysis-services/instances/install-windows/media/rs-powershellicon.png "Содержимое, связанное с PowerShell")  
  
 Следующий скрипт PowerShell возвращает список подписок и свойств подписок для текущего пользователя. Дополнительные сведения см. в разделе [Метод ReportingService2010.ListMySubscriptions](http://technet.microsoft.com/library/reportservice2010.reportingservice2010.listmysubscriptions.aspx).  
  
```  
#server -  all subscriptions of the current user at the given server or site  
$server="[server name]/reportserver"  
$rs2010 = New-WebServiceProxy -Uri "http://$server/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential;  
  
$subscriptions=ListMySubscriptions(ItemPathOrSiteURL)  
$subscriptions | select Path, report, Description, Owner, SubscriptionID, lastexecuted,Status  
#uncomment the following to list all the subscription properties  
#$subscriptions

```  
  
## См. также  
 [Подписки, управляемые данными](../../reporting-services/subscriptions/data-driven-subscriptions.md)   
 [Подписки и доставка (службы Reporting Services)](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [old_Создание подписок для работающих в основном режиме серверов отчетов и управление этими подписками](http://msdn.microsoft.com/ru-ru/7f46cbdb-5102-4941-bca2-5e0ff9012c6b)  
  
  