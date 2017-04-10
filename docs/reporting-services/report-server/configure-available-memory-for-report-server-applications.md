---
title: "Настройка доступной памяти для приложений сервера отчетов | Microsoft Docs"
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
helpviewer_keywords: 
  - "память [службы Reporting Services]"
  - "пороговые значения памяти [службы Reporting Services]"
ms.assetid: ac7ab037-300c-499d-89d4-756f8d8e99f6
caps.latest.revision: 49
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 49
---
# Настройка доступной памяти для приложений сервера отчетов
  Хотя службы [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] могут использовать всю доступную память, можно переопределить поведение по умолчанию, настроив верхний предел ресурсов памяти, выделяемых серверным приложениям служб [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Можно также задать пороговые значения, которые изменяют способ назначения приоритета и обработки запросов сервером отчетов в зависимости от дефицита свободной памяти. При малом дефиците свободной памяти сервер отчетов назначает чуть более высокий приоритет интерактивной обработке отчетов или обработке отчетов по запросу. При серьезном дефиците свободной памяти сервер отчетов использует многочисленные приемы, чтобы сохранить работоспособность в условиях ограниченных доступных ресурсов.  
  
 В этом разделе описаны задаваемые пользователем параметры конфигурации и реакция сервера в случаях, когда при обработке запросов приходится учитывать недостаток свободной памяти.  
  
## Политики управления памятью  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] изменяют объем памяти, выделяемый определенным приложениям и типы обработки запросов. Приложения, которые выполняются в службе сервера отчетов и участвуют в управлении памятью.  
  
-   Диспетчер отчетов, клиентский веб-интерфейс для сервера отчетов.  
  
-   Веб-служба сервера отчетов, используемая для интерактивной обработки отчетов и запросов по требованию.  
  
-   Приложение фоновой обработки, используемое для обработки отчетов по расписанию, доставки подписок и обслуживания баз данных.  
  
 Политики управления памятью применяются к службе сервера отчетов в целом, а не к отдельным приложениям, выполняемым внутри процесса.  
  
 Если недостатка памяти нет, то каждое серверное приложение запрашивает некоторый объем памяти при запуске, не дожидаясь получения запросов, чтобы обеспечить оптимальную производительность, когда запросы будут, наконец, получены. По мере возникновения недостатка памяти, сервер отчетов корректирует модель процесса, как описано в следующей таблице.  
  
|Дефицит памяти|Реакция сервера|  
|---------------------|---------------------|  
|Низкий|Обработка текущих запросов продолжается. Новые запросы принимаются почти всегда. Запросы к приложениям, выполняющим обработку в фоновом режиме, имеют более низкий приоритет, чем запросы к веб-службе сервера отчетов.|  
|Средний|Обработка текущих запросов продолжается. Новые запросы могут быть приняты. Запросы к приложениям, выполняющим обработку в фоновом режиме, имеют более низкий приоритет, чем запросы к веб-службе сервера отчетов. Выделение памяти сокращается для всех трех серверных приложений, более всего сокращение касается фоновой обработки, чтобы выделить больше памяти для запросов веб-службы.|  
|Высокий|Выделение памяти сокращается еще больше. Запросы дополнительной памяти со стороны серверных приложений запрещены. Обработка текущих запросов замедляется и для их завершения требуется больше времени. Новые запросы не принимаются. Сервер отчетов выгружает файлы данных из памяти на диск.<br /><br /> Если ограничения памяти становятся критическими и отсутствует память для обработки новых запросов, то сервер отчетов возвращает ошибку HTTP 503, которая свидетельствует о недоступности сервера, пока завершается обработка текущих запросов. В некоторых случаях может быть выполнена очистка домена приложений, чтобы немедленно сократить недостаток свободной памяти.|  
  
 Нельзя настроить реакцию сервера отчетов для различных сценариев нехватки свободной памяти, но можно назначить параметры конфигурации, которые определяют границы, разделяющие реакцию на высокий, средний и низкий недостаток свободной памяти.  
  
## Когда следует настраивать параметры управления памятью  
 Параметры по умолчанию указывают неравные области для низкой, средней и высокой нехватки свободной памяти. По умолчанию область низкой нехватки свободной памяти больше, чем зоны средней и высокой нехватки свободной памяти. Такая конфигурация оптимальна для нагрузки, которая распределена равномерно, либо увеличивается или сокращается постепенно. В этом случае переход между зонами совершается постепенно, и у сервера отчетов есть время скорректировать реакцию.  
  
 Если нагрузка изменяется скачками, то полезно изменить параметры по умолчанию. Если нагрузка изменяется внезапными скачками, то сервер отчетов может очень быстро перейти от состояния без недостатка свободной памяти к отказам выделения памяти. Это может произойти, если имеется несколько экземпляров отчетов, требующих много памяти и запускаемых одновременно. Для обработки нагрузки такого типа рекомендуется как можно скорее перевести сервер отчетов в область средней или высокой нехватки памяти, чтобы замедлить обработку. Это позволит завершить больше запросов. Для этого нужно уменьшить значение для **MemorySafetyMargin** , чтобы уменьшить область низкой нехватки памяти относительно других областей. В результате реакция на среднюю и высокую нехватку памяти будет происходить раньше.  
  
## Параметры конфигурации для управления памятью  
 Параметры конфигурации, которые управляют распределением памяти для сервера отчетов — **WorkingSetMaximum**, **WorkingSetMinimum**, **MemorySafetyMargin**и **MemoryThreshold**.  
  
-   Параметры**WorkingSetMaximum** и **WorkingSetMinimum** определяют область доступной памяти. Настраивая эти параметры, можно установить область доступной памяти для приложений сервера отчетов. Это полезно, если несколько приложений размещаются на одном компьютере, и известно, что сервер отчетов использует непропорциональное количество системных ресурсов по сравнению с другими приложениями на том же компьютере.  
  
-   Параметры**MemorySafetyMargin** и **MemoryThreshold** set the boundaries for low, medium, и high levels of memory pressure. Для каждого состояния службы [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] предпринимают действие по исправлению, чтобы обработка отчетов и другие запросы выполнялись в соответствии с объемом памяти, доступной на компьютере. Можно указать параметры конфигурации, которые определяют разграничение между низким, средним и высоким уровнями нехватки свободной памяти.  
  
     Параметры конфигурации можно изменить, но это не улучшит производительность при обработке отчетов. Изменение параметров конфигурации полезно, только если запросы теряются прежде, чем будут завершены. Лучший способ повысить производительность сервера — развернуть сервер отчетов или его отдельные приложения на разных компьютерах.  
  
 На следующей иллюстрации показано, как параметры используются совместно, чтобы различить низкий, средний и высокий уровни нехватки свободной памяти:  
  
 ![Параметры конфигурации для состояния памяти](../../reporting-services/report-server/media/rs-memoryconfigurationzones.gif "Параметры конфигурации для состояния памяти")  
  
 В следующей таблице приведены описания параметров **WorkingSetMaximum**, **WorkingSetMinimum**, **MemorySafetyMargin**и **MemoryThreshold** . Параметры конфигурации задаются в файле [RSReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md).  
  
|Элемент|Description|  
|-------------|-----------------|  
|**WorkingSetMaximum**|Порог памяти, после которого больше не будут приниматься новые запросы на предоставление памяти от приложений сервера отчетов.<br /><br /> По умолчанию сервер отчетов устанавливает значение **WorkingSetMaximum** равным объему доступной памяти в компьютере. Это значение обнаруживается при запуске службы.<br /><br /> Этот параметр не появляется в файле конфигурации RSReportServer.config, если не добавить его вручную. Чтобы сервер отчетов использовал меньше памяти, можно изменить файл RSReportServer.config, добавив элемент и значение. Диапазон допустимых значений — от 0 до максимального целого числа. Значение указывается в килобайтах.<br /><br /> При достижении значения **WorkingSetMaximum** сервер отчетов прекращает принимать новые запросы. Обрабатываемые в это время запросы продолжают выполняться. Новые запросы принимаются лишь после того, как объем использованной памяти станет меньше значения, указанного параметром **WorkingSetMaximum**.<br /><br /> Если существующие запросы по-прежнему занимают дополнительную память по достижении значения **WorkingSetMaximum** , все домены приложений сервера отчетов будут очищены. Дополнительные сведения см. в статье [Application Domains for Report Server Applications](../../reporting-services/report-server/application-domains-for-report-server-applications.md).|  
|**WorkingSetMinimum**|Нижний предел потребления ресурсов; сервер отчетов не будет освобождать память, если общее использование памяти ниже этого предела.<br /><br /> Его значение по умолчанию рассчитывается при запуске службы. В соответствии с этим расчетом, запрашиваемый объем выделенной памяти составляет 60 процентов от **WorkingSetMaximum**.<br /><br /> Этот параметр не появляется в файле конфигурации RSReportServer.config, если не добавить его вручную. Чтобы изменить это значение, необходимо добавить элемент **WorkingSetMinimum** в файл RSReportServer.config. Диапазон допустимых значений — от 0 до максимального целого числа. Значение указывается в килобайтах.|  
|**MemoryThreshold**|Задает процент **WorkingSetMaximum** , определяющий границу между высоким и средним уровнями потребления памяти. Если процент использования памяти достиг этого значения, сервер отчетов замедляет обработку запросов и перераспределяет память, выделенную различным серверным приложениям. Значение по умолчанию равно 90. Это значение должно быть больше значения параметра **MemorySafetyMargin**.|  
|**MemorySafetyMargin**|Задает процент **WorkingSetMaximum** , определяющий границу между средним и низким уровнями потребления памяти. Это значение представляет собой процент доступной памяти, которая будет зарезервирована для системы и не сможет быть использована для работы сервера отчетов. Значение по умолчанию равно 80.|  
  
> [!NOTE]  
> Параметры  **MemoryLimit** и **MaximumMemoryLimit** в [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] и более поздних версиях являются устаревшими. Если обновить существующую установку или использовать файл RSReportServer.config с этими значениями, то сервер отчетов не будет их считывать.  
  
#### Пример параметров конфигурации памяти  
 Следующий пример показывает параметры конфигурации для компьютера серверов отчетов, в котором используются пользовательские значения конфигурации памяти. Чтобы добавить параметр **WorkingSetMaximum** или **WorkingSetMinimum**, необходимо вставить соответствующие элементы и значения в файл RSReportServer.config. Оба значения представляют собой целые числа, указывающие объем ОЗУ в килобайтах, выделяемый для серверных приложений. В следующем примере указывается, что общая память, выделенная для приложений сервера отчетов, не может превышать 4 гигабайт. Если значение параметра **WorkingSetMinimum** по умолчанию (60 % от значения **WorkingSetMaximum**) приемлемо, его можно опустить и задать в файле RSReportServer.config только параметр **WorkingSetMaximum**. Пример содержит параметр **WorkingSetMinimum** , чтобы показать, как выглядит этот параметр, если понадобится его добавить:  
  
```  
      <MemorySafetyMargin>80</MemorySafetyMargin>  
      <MemoryThreshold>90</MemoryThreshold>  
      <WorkingSetMaximum>4000000</WorkingSetMaximum>  
      <WorkingSetMinimum>2400000</WorkingSetMinimum>  
```  
  
#### О параметрах конфигурации памяти ASP.NET  
 Хотя веб-служба сервера отчетов и диспетчер отчетов представляют собой приложения [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)], ни одно из приложений не реагирует на параметры конфигурации памяти, указанные в разделе **processModel** файла machine.config для приложений [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)], работающих в режиме совместимости с IIS 5.0. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] считывают параметры конфигурации памяти только из файла RSReportServer.config.  
  
## См. также  
 [Файл конфигурации RsReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
 [Файл конфигурации RsReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
 [Изменение файла конфигурации служб Reporting Services (RSreportserver.config)](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)   
 [Домены приложений для приложений сервера отчетов](../../reporting-services/report-server/application-domains-for-report-server-applications.md)  
  
  