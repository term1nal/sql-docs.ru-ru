---
title: Рекомендации по обработке исключений в службах Reporting Services | Документы Майкрософт
ms.date: 03/06/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-web-service-net-framework-exception-handling
ms.topic: reference
helpviewer_keywords:
- exceptions [Reporting Services], best practices
ms.assetid: 72fecf28-f02e-4338-b50f-0b21f520302d
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 0f9334a6a0e752770cc7d7504c025201beb6113c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/01/2018
ms.locfileid: "47789942"
---
# <a name="best-practices-for-reporting-services-exception-handling"></a>Рекомендации по обработке исключений в службах Reporting Services
  При разработке приложений служб [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] существует несколько методик, которые можно использовать для избежания возникновения исключений или сокращения их количества. При возникновении исключений пользователю следует выводить ясное и четкое сообщение об ошибке; кроме того, следует добавить обработку исключений, чтобы приложения не завершались неожиданно.  
  
 Приложение, посылающее запросы веб-службе сервера отчетов должно выполнять следующие действия.  
  
-   Оно должно избегать вызова исключений методом предотвращения создания как можно большего количества недопустимых запросов.  
  
-   Оно должно по возможности перехватывать исключения и предоставлять определенные коды обработки ошибок.  
  
-   Оно должно обрабатывать варианты ошибок, не выдающие исключений.  
  
## <a name="in-this-section"></a>в этом разделе  
  
|Раздел|Описание|  
|-----------|-----------------|  
|[Предотвращение использования недопустимых запросов](../../../reporting-services/report-server-web-service-net-framework-exception-handling/best-practices/preventing-invalid-requests.md)|Описывает методики предотвращения отправки недопустимых запросов на сервер отчетов.|  
|[Использование блоков Try-Catch](../../../reporting-services/report-server-web-service-net-framework-exception-handling/best-practices/using-try-and-catch-blocks.md)|Описывает, как можно увеличить надежность приложения с использованием блоков TRY и CATCH.|  
|[Обработка предупреждений и ситуаций, не вызывающих исключения](../../../reporting-services/report-server-web-service-net-framework-exception-handling/best-practices/handling-warnings-and-cases-that-do-not-cause-exceptions.md)|Объясняет, как следует обрабатывать ошибки, которые не приводят к формированию исключения службами [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].|  
|[Использование свойства Detail для обработки определенных ошибок](../../../reporting-services/report-server-web-service-net-framework-exception-handling/best-practices/using-the-detail-property-to-handle-specific-errors.md)|Описывает, как можно программным образом обрабатывать определенные ошибки с помощью свойства **Detail** объекта **SoapException**.|  
  
## <a name="see-also"></a>См. также:  
 [Свойство Detail](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/detail-property.md)   
 [Введение в обработку исключений в службах Reporting Services](../../../reporting-services/report-server-web-service-net-framework-exception-handling/introducing-exception-handling-in-reporting-services.md)   
 [Класс SoapException в службах Reporting Services](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/reporting-services-soapexception-class.md)  
  
  
