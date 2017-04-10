---
title: "Параллельная установка служб Reporting Services и служб IIS (собственный режим SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/23/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "развертывание [службы Reporting Services], службы IIS"
ms.assetid: 9b651fa5-f582-4f18-a77d-0dde95d9d211
caps.latest.revision: 40
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
---
# Параллельная установка служб Reporting Services и служб IIS (собственный режим SSRS)
  Службы [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] (SSRS) и IIS могут быть установлены и запущены на одном и том же компьютере. От используемой версии служб IIS будет зависеть, какие возникнут проблемы совместимости.  
  
||  
|-|  
|[!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Основной режим|  
  
|Версия служб IIS|Проблемы|Описание|  
|-----------------|------------|-----------------|  
|8.0, 8.5|Запросы, предназначенные для одного приложения, принимаются другим приложением.<br /><br /> Компонент HTTP.SYS предписывает правила приоритета для резервирования URL-адресов. Запросы, передаваемые в приложения, которые имеют одинаковое имя виртуального каталога и совместно отслеживают запросы, поступающие через порт 80, могут не достичь намеченной цели, если применяемое резервирование URL-адресов слабее резервирования URL-адресов другого приложения.|При определенных условиях зарегистрированная конечная точка, URL-адрес которой предшествует URL-адресу другой конечной точки в схеме резервирования URL-адресов, может получать HTTP-запросы, предназначенные для другого приложения.<br /><br /> Использование уникальных имен виртуальных каталогов для таких компонентов, как веб-служба сервера отчетов и [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)], поможет избежать этого конфликта.<br /><br /> Подробные сведения об этом сценарии приведены в этом разделе.|  
  
## Правила приоритета для резервирования URL-адресов  
 Прежде чем приступать к устранению проблем совместимости служб IIS и [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], необходимо понять правила приоритета резервирования URL-адресов. Правила приоритета можно обобщить следующим образом: резервирование URL-адресов, более явно определяющих значения, становится первым в очереди на получение запросов по соответствующим URL-адресам.  
  
-   Резервирование URL-адресов, указывающее виртуальный каталог, является более явным по сравнению с тем, в котором виртуальный каталог не задан.  
  
-   Резервирование URL-адресов, в котором указан единственный адрес (в виде IP-адреса, полного доменного имени, сетевого имени компьютера или имени узла), является более явным по сравнению с резервированием, в котором указан шаблон.  
  
-   Резервирование URL-адресов, в котором указан сильный шаблон, является более явным по отношению к резервированию со слабым шаблоном.  
  
 В следующих примерах приведен ряд резервирований URL-адресов, начиная от наиболее явного и заканчивая наименее явным:  
  
|Пример|Запрос|  
|-------------|-------------|  
|http://123.234.345.456:80/reports|Получает все запросы, которые передаются по адресу http://123.234.345.456/reports или http://\<имя_компьютера>/reports, если служба доменных имен способна разрешить этот IP-адрес в это имя узла.|  
|http://+:80/reports|Получает любые запросы, отправленные любому IP-адресу или имени узла, являющимся допустимыми для этого компьютера, при условии, что URL-адрес содержит имя виртуального каталога reports.|  
|http://123.234.345.456:80|Получает любой запрос, в котором указан адрес http://123.234.345.456 или http://\<имя_компьютера>, при условии, что служба доменных имен способна разрешить этот IP-адрес в это имя узла.|  
|http://+:80|Получает запросы, которые еще не получены другими приложениями, применительно к любым конечным точкам приложений, сопоставленным со значением **Все назначенные**.|  
|http://*:80|Получает запросы, которые еще не получены другими приложениями, применительно к любым конечным точкам приложений, сопоставленным со значением **Все неназначенные**.|  
  
 Одним из признаков конфликта портов является следующее сообщение об ошибке: "System.IO.FileLoadException. Процесс не может получить доступ к файлу, так как этот файл занят другим процессом. (Исключение в HRESULT: 0x80070020)".  
  
## Резервирование URL-адресов для служб IIS 8.0, 8.5 со службами [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Reporting Services  
 Изучение правил приоритета, приведенных в предыдущем разделе, позволяет разобраться, как резервирования URL-адресов, определенные для служб Reporting Services и IIS, поддерживают совместимость. Службы Reporting Services получают запросы, в которых явно указаны имена виртуальных каталогов для их приложений; службы IIS получают все остальные запросы, которые могут затем быть направлены приложениям, запущенным в рамках модели процесса IIS.  
  
|Приложение|Резервирование URL-адресов|Описание|Прием запроса|  
|-----------------|---------------------|-----------------|---------------------|  
|Сервер отчетов|http://+:80/ReportServer|Сильный шаблон для доступа к порту 80, с указанием виртуального каталога сервера отчетов.|Получает все запросы на порт 80, в которых указан виртуальный каталог сервера отчетов. Веб-служба сервера отчетов получает все запросы с адресом http://\<имя_компьютера>/reportserver.|  
|Веб-портал|http://+:80/Reports|Сильный шаблон для доступа к порту 80, с указанием виртуального каталога Reports.|Получает все запросы на порт 80, в которых указан виртуальный каталог reports. [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)] получает все запросы, отправленные по адресу http://\<имя_компьютера>/reports.|  
|IIS|http://*:80/|Слабый шаблон для доступа к порту 80.|Получает любые оставшиеся запросы на порт 80, которые не получены другим приложением.|  
  
## Параллельное развертывание [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] и служб SQL Server 2016 Reporting Services в службах IIS 8.0, 8.5  
 Если веб-сайты IIS имеют имена виртуальных каталогов, идентичные используемым в службах Reporting Services, возникают проблемы функциональной совместимости служб IIS и служб Reporting Services. Например, предположим, что имеется следующая конфигурация.  
  
-   Веб-сайт в службах IIS, который назначен на порт 80 и виртуальный каталог с именем Reports.  
  
-   Экземпляр сервера отчетов [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], установленный в конфигурации по умолчанию, где в резервировании URL-адресов также указан порт 80, а в приложении ресурса "[!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)]" также используется Reports в качестве имени виртуального каталога.  
  
 В такой конфигурации запрос, отправленный по адресу http://\<имя_компьютера>:80/reports, принимает [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)]. Приложение, доступ к которому предоставляется с помощью виртуального каталога Reports в службах IIS, после установки экземпляра сервера отчетов [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] больше не будет получать запросы.  
  
 При работе развернутых параллельно старой и новой версии служб [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], по всей вероятности будут обнаруживаться только что описанные проблемы маршрутизации. Это связано с тем, что во всех версиях служб [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] в качестве имен виртуальных каталогов для приложений таких компонентов, как сервер отчетов и [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)], используются ReportServer и Reports, в результате чего повышается вероятность наличия виртуальных каталогов reports и reportserver в службах IIS.  
  
 Чтобы обеспечить получение всеми приложениями направленных к ним запросов, руководствуйтесь следующими рекомендациями.  
  
-   Для установок служб Reporting Services используйте имена виртуальных каталогов, которые не используются ни одним веб-сайтом IIS на том же порте, что и в службе Reporting Services. Если возникает конфликт, установите службы Reporting Services в режиме «только файлы» (с помощью программы установки, но не настраивая параметры сервера в мастере установки), чтобы иметь возможность настроить виртуальные каталоги после завершения установки. Одним из признаков конфликта конфигурации является следующее сообщение об ошибке: "System.IO.FileLoadException. Процесс не может получить доступ к файлу, так как этот файл занят другим процессом. (Исключение в HRESULT: 0x80070020)".  
  
-   Для установок, настраиваемых вручную, применяйте предусмотренные по умолчанию соглашения об именах в настраиваемых URL-адресах. Если службы [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] устанавливаются в качестве именованного экземпляра, включите имя экземпляра при создании виртуального каталога.  
  
## См. также:  
 [Настройка URL-адресов сервера отчетов (диспетчер конфигурации служб SSRS)](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)   
 [Настройка URL-адреса (диспетчер конфигурации служб SSRS)](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)   
 [Установка сервера отчетов служб Reporting Services в собственном режиме](../../reporting-services/install-windows/install-reporting-services-native-mode-report-server.md)  
  
  