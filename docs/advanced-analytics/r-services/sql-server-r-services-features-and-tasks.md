---
title: "Возможности и задачи служб R SQL Server | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "05/31/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 52ad3f10-6d24-477a-aeb6-110456b2ed1c
caps.latest.revision: 13
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 13
---
# Возможности и задачи служб R SQL Server
  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] объединяет мощность и гибкость с открытым исходным кодом языка R со средствами корпоративного уровня для хранения данных и управления, разработки рабочего процесса и отчетов и визуализации. Он поддерживает потребности специалистов по четыре различных данных и сценариев.  
  
## Специалисты по анализу данных: анализ, моделирование и оценка с помощью R и SQL Server  
 Специалистам по анализу данных доступны различные средства для анализа данных и машинного обучения — от знакомого приложения Excel и платформ с открытым исходным кодом до дорогих статистических наборов, для работы с которыми требуются глубокие технические познания. [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] предоставляют уникальные преимущества, так как они позволяют перенести вычисления в базу данных без перемещения данных и в соответствии с корпоративными политиками безопасности. Кроме того, код R, созданный специалистами по анализу данных, можно легко развернуть в рабочей среде и вызывать в знакомых корпоративных средствах и решениях: приложениях на основе баз данных [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , средствах создания отчетов бизнес-аналитики и панелях мониторинга. С помощью [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]специалисты по анализу данных могут развернуть и обновить аналитическое решение, выполнив стандартные требования к управлению корпоративными данными, такие как требования к безопасности, простоте развертывания, управлению, мониторингу и аудиту доступа.  
  
-   **Привычный пользовательский интерфейс.**  Разрабатывайте и тестируйте решение с помощью среды разработки R по своему выбору.  
  
-   **Обработка в базе данных.**  Выполняйте код R, при этом вычисления будут происходить на компьютере, где размещен экземпляр [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Это избавляет от необходимости перемещения данных.  
  
-   **Производительность и масштаб.**  Включает масштабируемые пакеты R и интерфейсы API, все больше не ограничены одним потоком, размещенному в оперативной памяти архитектура R. Можно работать с большими наборами данных и вычислений многопоточных, многоядерных процессоров, несколькими процессами.  
    
-   **Переносимость кода.**  Один и тот же код R, выполнить [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] данные можно легко использовать повторно для других источников данных, например Hadoop.  
  
 Подробные сведения о связанных задач и основные понятия в разделе [прогнозирующего моделирования с R и просмотр данных](../../advanced-analytics/r-services/data-exploration-and-predictive-modeling-with-r.md).  
  
## Разработчики приложений и баз данных: развертывание решений R  
 Разработчикам баз данных необходимо интегрировать несколько технологий и объединить результаты, чтобы их можно было совместно использовать на всем предприятии. Разработчик базы данных работает с разработчиками приложений, разработчиками SQL и специалистами по анализу данных для создания решений, методов управления данными, а также проектирования и развертывания решений. [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] предоставляют множество преимуществ для разработчиков, работающих со специалистами по анализу данных.  
  
-   **Взаимодействовать с помощью скриптов R [!INCLUDE[tsql](../../includes/tsql-md.md)].**  Разработчики отчетов, аналитики и разработчики баз данных могут вызывать сценарии R с помощью системных хранимых процедур. Если решение использует сложное агрегирование или включает большие наборы данных, может иметь вычислений выполнение в базе данных или использовать сочетание R и [!INCLUDE[tsql](../../includes/tsql-md.md)], в зависимости от того, что обеспечивает лучшую производительность. Легкая интеграция с  [!INCLUDE[tsql](../../includes/tsql-md.md)] особенно удобна, если вам необходимо многократно выполнять задачи на больших объемах данных, например формировать прогнозирующие оценки для производственных данных.  
  
     Интеграция с [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , кроме того, означает, что вы можете выполнять сценарии R из любого приложения, использующего [!INCLUDE[tsql](../../includes/tsql-md.md)]. Например, можно без труда вызвать хранимую процедуру из [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] отчета для вызова сценария R и создания построения, а также прогнозы в отчете.  
  
-   **Производительность и масштаб.**  Несмотря на то, что известно, что язык R с открытым исходным имеют ограничения, пакет RevoScaleR API-интерфейсы, предоставляемые [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] можно работать с большими наборами данных и использовать преимущества многопоточных, многоядерных процессоров, несколькими процессами вычислений в базе данных.  
  
-   **Стандартные инструменты разработки и управления**  Не требуются дополнительные средства для администрирования или развертывания. Все задания R можно вызывать с помощью хранимой процедуры. Кроме того, один и тот же код R, который применяется к данным [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , можно использовать повторно для других источников данных, например Hadoop.  
  
 Подробные сведения о связанных задач и основные понятия в разделе [операционализации код R](../../advanced-analytics/r-services/operationalizing-your-r-code.md).  
  
## Администраторы базы данных: управление решениями углубленной аналитики  
 Администраторам баз данных необходимо интегрировать конкурирующие проекты и приоритеты в единую точку контакта: сервер базы данных. Им необходимо предоставить доступ к данным не только специалистам по анализу, но и различным разработчикам отчетов, бизнес-аналитикам и потребителям бизнес-данных, поддерживая при этом работоспособность операционного хранилища данных и хранилища отчетов. На предприятии администратор базы данных — это важная часть процесса построения и развертывания эффективной инфраструктуры для обработки и анализа данных. [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] предоставляют администратору базы данных, который поддерживает роль обработки и анализа данных, множество преимуществ.  
  
-   **Безопасность.**  Архитектура [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] отслеживает безопасности баз данных и изолирует выполнение R сеансов работы экземпляра базы данных.  
  
     Можно указать, кто имеет право выполнять сценарии R и убедитесь, что данные, используемые в задания R управляется с помощью того же ролей безопасности, которые определены в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   **Надежность.**  Сеансы R выполняются в отдельном процессе, чтобы сервер продолжал работать как обычно даже при возникновении проблем в сеансе R.  
  
-   **Управление ресурсами.**  Можно управлять объемом ресурсов, выделяемых для среды выполнения R, чтобы предотвратить негативное влияние масштабных вычислений на общую производительность сервера.  
  
 Подробные сведения о связанных задачах и основных понятиях см. в разделе [Managing and Monitoring R Solutions](../../advanced-analytics/r-services/managing-and-monitoring-r-solutions.md).  
  
## Специалисты по архитектуре и проектировщики ETL: создание интегрированных рабочих процессов, охватывающих R и SQL Server  
 Специалисты по обработке данных проектируют и создают решения ETL. Специалисты по архитектуре разрабатывают платформы данных, выполняющие конкурирующие и дополняющие друг друга бизнес-задачи. Поскольку [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] тесно интегрированы с другими средствами Microsoft, например бизнес-аналитики и стек хранилища данных облака enterprise и средства мобильности и Hadoop, он предоставляет множество преимуществ данных инженер или системных архитекторов, желающий повысить уровень расширенной аналитики.  
  
-   **Широкий набор хорошо знакомых средств разработки.**  При разработке решений на языке R используйте [!INCLUDE[tsql](../../includes/tsql-md.md)] и системные хранимые процедуры для заполнения наборов данных, выполнения заданий R и прогнозирования. Больше не требуется создавать параллельные рабочие процессы в средствах обработки и анализа данных — создавать конвейеры данных в знакомой среде [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
     Необходимо использовать облачные данные? Поддержка фабрики данных Azure и базы данных SQL Azure упрощает преобразование данных и управления ими, и использование источников данных облака в рабочих процессах точно так же, как для локальных [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] данных.  
  
-   **Создание рабочих процессов и управление ими.**  Планирование заданий и создания рабочих процессов, содержащая скрипты R, с помощью системных хранимых процедур.  
  
 Подробные сведения о связанных задач и основные понятия в разделе [Создание рабочих процессов, когда использование R в SQL Server](../../advanced-analytics/r-services/creating-workflows-that-use-r-in-sql-server.md).  
  
## См. также:  
 [Приступая к работе со службами SQL Server R Services](../../advanced-analytics/r-services/getting-started-with-sql-server-r-services.md)  
  
  