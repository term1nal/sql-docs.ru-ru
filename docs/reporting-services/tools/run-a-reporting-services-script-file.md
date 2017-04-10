---
title: "Запустить файл скрипта служб Reporting Services | Microsoft Docs"
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
helpviewer_keywords: 
  - "скрипты [службы Reporting Services], выполнение"
ms.assetid: 0de4995c-85ec-4d4c-aaef-fbd30edfb20f
caps.latest.revision: 36
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 36
---
# Запустить файл скрипта служб Reporting Services
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Файлы скриптов служб [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] выполняются из командной строки с помощью среды скриптов служб (программа rs.exe). В программе rs.exe доступно множество аргументов командной строки. Дополнительные сведения о параметрах командной строки см. в разделе [Служебная программа RS.exe (службы SSRS)](../../reporting-services/tools/rs-exe-utility-ssrs.md). Образцы скриптов см. на странице [Образцы продуктов служб SQL Server Reporting Services](http://go.microsoft.com/fwlink/?LinkId=177889).  
  
## Образцы команд в командной строке  
  
-   Запустите файл Script.rss в среде выполнения скриптов, при этом укажите целевой сервер отчетов. По умолчанию применяется проверка подлинности Windows.  
  
    ```  
    rs –i Script.rss -s http://servername/reportserver  
    ```  
  
-   Запустите файл Script.rss в среде выполнения скриптов, при этом задайте имя пользователя и пароль для ответа на вызовы веб-службы.  
  
    ```  
    rs –i Script.rss -s http://servername/reportserver -u myusername -p mypassword  
    ```  
  
-   Запустите файл Script.rss в среде выполнения скриптов, задайте лимит времени ожидания для сервера в 30 секунд.  
  
    ```  
    rs –i Script.rss -s http://servername/reportserver -l 30  
    ```  
  
-   Запустите файл Script.rss в среде выполнения скриптов, при этом укажите глобальную переменную скрипта с именем *report*.  
  
    ```  
    rs –i Script.rss -s http://servername/reportserver -v report="Company Sales"  
    ```  
  
-   Запустите файл Script.rss в среде выполнения скриптов, при этом укажите, что операции веб-службы в файле скриптов должны выполняться в виде пакета.  
  
    ```  
    rs –i Script.rss -s http://servername/reportserver -b  
    ```  
  
## См. также  
 [Технический справочник (службы SSRS)](../../reporting-services/technical-reference-ssrs.md)  
  
  