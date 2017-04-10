---
title: "Управление запущенным процессом | Microsoft Docs"
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
  - "обработка отчетов [службы Reporting Services], сведения о состоянии"
  - "задания [службы Reporting Services]"
  - "просмотр заданий"
  - "отмена заданий"
  - "пользовательские задания [службы Reporting Services]"
  - "системные задания [службы Reporting Services]"
  - "обработка отчетов [службы Reporting Services], управление запущенными процессами"
  - "процессы [службы Reporting Services]"
  - "сканирование процессов [службы Reporting Services]"
  - "сведения о состоянии [службы Reporting Services]"
  - "обработка отчета [службы Reporting Services]"
  - "отмена подписок"
  - "серверы отчетов [службы Reporting Services], задания"
  - "управляемая данными подписка"
  - "отображение заданий"
  - "подписки [службы Reporting Services], запущенные процессы"
ms.assetid: 473e574e-f1ff-4ef9-bda6-7028b357ac42
caps.latest.revision: 53
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 53
---
# Управление запущенным процессом
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] наблюдают за состоянием заданий, работающих на сервере отчетов. Через регулярные интервалы времени сервер отчетов просматривает внутрипроцессные задания и записывает сведения о состоянии в базу данных сервера отчетов или в базы данных приложения служб для режима интеграции с SharePoint. Задание находится в процессе выполнения, если запущены следующие процессы: выполнение запроса на удаленном или локальном сервере базы данных, обработка отчета и подготовка отчета к просмотру.  
  
 Можно управлять как *пользовательскими заданиями* , так и *системными заданиями*.  
  
-   Пользовательские задания инициируются отдельным пользователем или подпиской. Это включает запуск отчета по запросу, запрос моментального снимка журнала отчета, ручное создание моментального снимка отчета и обработку стандартной подписки.  
  
-   Системные задания инициируются сервером отчетов. Они включают запланированные снимки состояния выполнения отчета, запланированные моментальные снимки журнала отчета и управляемые данными подписки.  
  
 Время обработки отчета и используемые ресурсы в значительной степени зависят от самого отчета, сложности запроса, объема данных и формата просмотра, который указан для отчета. Отчеты с простыми запросами к локальному источнику данных часто завершаются в течение нескольких миллисекунд и не требуют управления или тонкой настройки. В отличие от них большой отчет, который должен просматриваться в формате PDF или Excel, может потребовать достаточно много времени для обработки в зависимости от ресурсов оборудования, параметров доставки и существования одновременно выполняющихся процессов. На сервере отчетов большинство ресурсоемких процессов относится к операциям подготовки отчетов к просмотру и процессам, ожидающим завершения обработки запросов. Иногда, если нужно перевести компьютер в режим «вне сети» или остановить работающее задание, требующее слишком много времени, может понадобиться отменить обработку отчета.  
  
 Можно остановить следующие процессы.  
  
-   Обработка отчетов по запросу.  
  
-   Обработка запланированных отчетов.  
  
-   Стандартные подписки, принадлежащие отдельным пользователям.  
  
 Отмена задания означает лишь остановку процессов, работающих на сервере отчетов. Поскольку сервер отчетов не управляет обработкой данных на других компьютерах, необходимо вручную остановить процессы запросов, потерянные при этом на других системах. Можно указать значения времени ожидания запросов, чтобы автоматически закрыть те запросы, для выполнения которых требуется слишком много времени. Дополнительные сведения см. в разделе [Задание значений времени ожидания при обработке отчетов и общих наборов данных (SSRS)](../../reporting-services/report-server/setting-time-out-values-for-report-and-shared-dataset-processing-ssrs.md). Дополнительные сведения о временной остановке обработки отчета см. в разделе [Отключение или приостановка обработки отчетов и подписок](../../reporting-services/subscriptions/disable-or-pause-report-and-subscription-processing.md).  
  
> [!NOTE]  
>  В исключительном случае для остановки процесса, возможно, придется перезапустить сервер. Для режима интеграции с SharePoint может потребоваться перезапуск пула приложений, в котором размещается приложение служб [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Дополнительные сведения см. в статье [Запуск и остановка службы сервера отчетов](../../reporting-services/report-server/start-and-stop-the-report-server-service.md).  
  
 В этом разделе.  
  
-   [Просмотр и отмена заданий (собственный режим)](#bkmk_native)  
  
-   [Просмотр и отмена заданий (режим SharePoint)](#bkmk_sharepoint)  
  
-   [Программное управление заданиями](#bkmk_programmatically)  
  
##  <a name="bkmk_native"></a> Просмотр и отмена заданий (собственный режим)  
 Чтобы просмотреть или отменить задания, выполняющиеся на сервере отчетов, вы можете использовать среду [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] . Необходимо обновить страницу, чтобы получить список заданий, работающих в настоящее время на сервере отчетов, или получить текущее состояние заданий из базы данных сервера отчетов. После подключения к серверу отчетов в среде [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]можно открыть папку «Задания», чтобы просмотреть список отчетов, которые в настоящее время обрабатываются на компьютере сервера отчетов. Сведения о состоянии каждого задания отображаются на странице «Свойства заданий». Сведения о состоянии всех заданий можно просмотреть, открыв диалоговое окно «Отмена заданий сервера отчетов».  
  
 Чтобы просмотреть или отменить задания, выполняющиеся на сервере отчетов, вы можете использовать среду [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] . Необходимо обновить страницу, чтобы получить список заданий, работающих в настоящее время на сервере отчетов, или получить текущее состояние заданий из базы данных сервера отчетов. После подключения к серверу отчетов в среде [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]можно открыть папку «Задания», чтобы просмотреть список отчетов, которые в настоящее время обрабатываются на компьютере сервера отчетов. Сведения о состоянии каждого задания отображаются на странице «Свойства заданий». Сведения о состоянии всех заданий можно просмотреть, открыв диалоговое окно «Отмена заданий сервера отчетов».  
  
 Нельзя использовать среду [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], чтобы отобразить список создания моделей, обработки модели или управляемых данными подписок либо отменить их. Службы Reporting Services не позволяют отменить создание или обработку модели. Однако можно отменить управляемые данными подписки с помощью инструкций, приведенных в этом разделе.  
  
### Отмена обработки отчета или подписки  
  
1.  В среде [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]установите соединение с сервером отчетов. Инструкции см. в разделе [Подключение к серверу отчетов в среде Management Studio](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md).  
  
2.  Откройте папку **Задания** .  
  
3.  Щелкните правой кнопкой мыши отчет и выберите команду **Отменить задания**.  
  
### Отмена управляемой данными подписки  
  
1.  Откройте файл RSReportServer.config в текстовом редакторе.  
  
2.  Найдите параметр **IsNotificationService**.  
  
3.  Присвойте ему значение **False**.  
  
4.  Сохраните файл.  
  
5.  В диспетчере отчетов удалите управляемую данными подписку из вкладки "Подписки" отчета или из папки **Мои подписки**.  
  
6.  После удаления подписки в файле RSReportServer.config найдите параметр **IsNotificationService** и присвойте ему значение **True**.  
  
7.  Сохраните файл.  
  
### Настройка параметров частоты для получения состояния заданий  
 Работающая задача хранится во временной базе данных сервера отчетов. Можно изменять параметры конфигурации в файле RSReportServer.config, чтобы управлять периодичностью, с которой сервер отчетов просматривает внутрипроцессные задания, а также интервал времени, после которого состояние работающего задания меняется с нового на работающее. Параметр **RunningRequestsDbCycle** указывает периодичность, с которой сервер отчетов просматривает работающие задания. По умолчанию сведения о состоянии записываются каждые 60 секунд. Параметр **RunningRequestsAge** указывает период времени, после которого состояние выполняющегося задания меняется с «новое» на «выполняющееся».  
  
##  <a name="bkmk_sharepoint"></a> Просмотр и отмена заданий (режим SharePoint)  
 Управление заданиями в развертывании в режиме SharePoint осуществляется в центре администрирования SharePoint для каждого приложения службы [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
#### Управление заданиями в режиме SharePoint  
  
1.  В центре администрирования SharePoint выберите **Управление приложениями службы**.  
  
2.  Щелкните имя приложения службы [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , откроется страница управления приложением.  
  
3.  Нажмите кнопку **Управление заданиями**.  
  
4.  Нажмите кнопку **Идентификатор задания** , чтобы просмотреть сведения о задании.  
  
5.  Либо щелкните поле задания и нажмите кнопку **Удалить** , чтобы отменить задание. При удалении задания подписка не удаляется.  
  
##  <a name="bkmk_programmatically"></a> Программное управление заданиями  
 Заданиями можно управлять программно или с помощью скриптов. Дополнительные сведения см. в разделе <xref:ReportService2010.ReportingService2010.ListJobs%2A>, <xref:ReportService2010.ReportingService2010.CancelJob%2A>.  
  
## См. также  
 [Отмена заданий сервера отчетов (среда Management Studio)](../../reporting-services/tools/cancel-report-server-jobs-management-studio.md)   
 [Свойства задания (среда Management Studio)](../../reporting-services/tools/job-properties-management-studio.md)   
 [Изменение файла конфигурации служб Reporting Services (RSreportserver.config)](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)   
 [Файл конфигурации RsReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
 [Диспетчер отчетов (службы Reporting Services в основном режиме)](../Topic/Report%20Manager%20%20\(SSRS%20Native%20Mode\).md)   
 [Наблюдение за производительностью сервера отчетов](../../reporting-services/report-server/monitoring-report-server-performance.md)  
  
  