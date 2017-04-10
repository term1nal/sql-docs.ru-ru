---
title: "Настройка Reporting Services для использования альтернативного имени субъекта | Microsoft Docs"
ms.custom: ""
ms.date: "03/20/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ce458f9f-4b4f-4a58-aa75-9a90dda1e622
caps.latest.revision: 6
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 6
---
# Настройка Reporting Services для использования альтернативного имени субъекта
  В этом разделе объясняется, как настроить [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] (SSRS), чтобы использовать альтернативное имя субъекта (SAN), изменив файл rsreportserver.config и используя средство Netsh.exe.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] в основном режиме|  
  
 Инструкции применяются к URL-адресу службы отчетов, а также URL-адресу веб-службы.  
  
 Чтобы использовать SAN, SSL-сертификат должен быть зарегистрирован на сервере, подписан и иметь закрытый ключ. Самозаверяющий сертификат использовать невозможно.  
  
 URL-адреса в [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] можно настроить для использования SSL-сертификата. Обычно сертификат имеет только имя субъекта, которое позволяет ему использовать только один URL-адрес для сеанса SSL. SAN — это дополнительное поле в сертификате, которое позволяет службе SSL прослушивать и быть допустимой для многих URL-адресов, а также совместно использовать порт SSL с другими приложениями. SAN выглядит следующим образом: www.s2.com.  
  
 Дополнительные сведения о параметрах SSL см. в статье [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]Настройка соединений SSL для сервера отчетов, работающего в собственном режиме[](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md "Configure SSL Connections on a Native Mode Report Server").  
  
### Настройка SSRS для использования альтернативного имени субъекта для URL-адреса веб-службы  
  
1.  Запустите диспетчер конфигурации служб Reporting Services.  
  
     Дополнительные сведения см. в разделе [Диспетчер конфигурации служб Reporting Services (собственный режим)](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md).  
  
2.  Выберите на странице **URL-адрес веб-службы** порт SSL и SSL-сертификат.  
  
     ![Диспетчер конфигурации служб Reporting Services](../../reporting-services/report-server-sharepoint/media/reportingservices-configurationmanager.png "Диспетчер конфигурации служб Reporting Services")  
  
     Диспетчер конфигурации зарегистрирует SSL-сертификат для порта.  
  
3.  Откройте файл rsreportserver.config.  
  
     Файл для служб SSRS в собственном режиме находится в следующей папке по умолчанию.  
  
    ```  
    \Program Files\Microsoft SQL Server\MSRS11.MSSQLSERVER\Reporting Services\ReportServer  
    ```  
  
4.  Скопируйте раздел URL-адреса для приложения веб-службы сервера отчетов.  
  
     Например, далее указан исходный раздел URL-адреса.  
  
    ```  
        <URL>  
         <UrlString>https://localhost:443</UrlString>  
         <AccountSid>S-1-5-20</AccountSid>  
         <AccountName>NT Authority\NetworkService</AccountName>  
        </URL>  
  
    ```  
  
     Ниже указан измененный раздел URL-адреса.  
  
    ```  
    <URL>  
         <UrlString>https://www.s1.com:443</UrlString>  
         <AccountSid>S-1-5-20</AccountSid>  
         <AccountName>NT Authority\NetworkService</AccountName>  
        </URL>  
        <URL>  
         <UrlString>https://www.s2.com:443</UrlString>  
         <AccountSid>S-1-5-20</AccountSid>  
         <AccountName>NT Authority\NetworkService</AccountName>  
        </URL>  
  
    ```  
  
5.  Сохраните файл rsreportserver.config.  
  
6.  Откройте командную строку от имени администратора и запустите средство Netsh.exe.  
  
    ```  
    C:\windows\system32\netsh  
    ```  
  
7.  Переключитесь в контекст HTTP, введя следующее.  
  
    ```  
    Netsh>http  
    ```  
  
8.  Отобразите существующие urlacl, введя следующее.  
  
    ```  
    Netsh http>show urlacl  
    ```  
  
     Появится запись, аналогичная следующей.  
  
    ```  
    Reserved URL            : https:// www.s1.com:443/ReportServer/  
        User: NT SERVICE\ReportServer  
            Listen: Yes  
            Delegate: No  
            SDDL: D:(A;;GX;;;S-1-5-80-1234567890-123456789-123456789-123456789-1234567890)  
    ```  
  
     urlacl — это DACL (список управления доступом на уровне пользователей) для зарезервированного URL-адреса.  
  
9. Создайте альтернативное имя субъекта с тем же пользователем и SDDL как существующую запись, введя следующее.  
  
    ```  
    netsh http>add urlacl  url=https://www.s2.com:443/ReportServer    
    user="NT Service\ReportServer" sddl=D:(A;;GX;;;S-1-5-80-1234567980-12346579-123456789-123456789-1234567890)  
  
    ```  
  
10. Щелкните на странице **Состояние сервера отчетов** диспетчера конфигурации Reporting Services кнопку **Остановить** , а затем нажмите **Запустить** , чтобы перезапустить сервер отчетов.  
  
## См. также  
 [Файл конфигурации RsReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
 [Использование диспетчера конфигурации служб Reporting Services (собственный режим)](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)   
 [Изменение файла конфигурации служб Reporting Services (RSreportserver.config)](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)   
 [Настройка URL-адресов сервера отчетов (диспетчер конфигурации служб SSRS)](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)  
  
  