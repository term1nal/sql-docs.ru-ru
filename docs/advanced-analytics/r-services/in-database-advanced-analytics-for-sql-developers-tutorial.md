---
title: "Дополнительные аналитические функции в базе данных для разработчиков SQL (учебник) | Microsoft Docs"
ms.custom: ""
ms.date: "04/19/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
dev_langs: 
  - "R"
  - "TSQL"
ms.assetid: c18cb249-2146-41b7-8821-3a20c5d7a690
caps.latest.revision: 15
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 15
---
# Дополнительные аналитические функции в базе данных для разработчиков SQL (учебник)
Цель этого пошагового руководства — предоставить разработчикам SQL практические рекомендации по созданию решений для расширенной аналитики с помощью [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]. В этом руководстве вы узнаете, как включить R в приложение или решение бизнес-аналитики, заключив код на языке R в хранимые процедуры.  
  
## Обзор  
Процесс построения законченного решения обычно состоит получения и очистки данных, изучения данных и формирования характеристик, обучения и настройки модели и, наконец, развертывания модели в рабочей среде. Разработку и тестирование кода на языке R лучше всего производить с помощью среды разработки, предназначенной для языка R, например RStudio или [!INCLUDE[rtvs-short](../../includes/rtvs-short-md.md)]. Однако после создания решения его можно легко развернуть в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] с помощью хранимых процедур [!INCLUDE[tsql](../../includes/tsql-md.md)] в знакомой среде [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
Поэтому в этом пошаговом руководстве предполагается, что весь необходимый для решения код на языке R уже имеется, и вы сосредоточитесь на создании и развертывании решения для расширенной аналитики с готовым кодом на языке R.  
  
-   [Шаг 1. Скачивание образца данных](../../advanced-analytics/r-services/step-1-download-the-sample-data-in-database-advanced-analytics-tutorial.md).    Скачайте образец набора данных и образцы файлов скриптов SQL на локальный компьютер.  
  
-   [Шаг 2. Импорт данных в SQL Server с помощью PowerShell](../../advanced-analytics/r-services/step-2-import-data-to-sql-server-using-powershell.md).  Выполните скрипт PowerShell, который создает базу данных и таблицу в экземпляре [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], а затем загружает образец данных в таблицу.  
  
-   [Шаг 3. Анализ и визуализация данных](../../advanced-analytics/r-services/step-3-explore-and-visualize-the-data-in-database-advanced-analytics-tutorial.md).   Выполните базовые действия по анализу и визуализации данных, вызвав пакеты и функции R из хранимых процедур [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   [Шаг 4. Создание функций данных с помощью T-SQL](../../advanced-analytics/r-services/step-4-create-data-features-using-t-sql-in-database-advanced-analytics-tutorial.md).  Сформируйте характеристики данных с помощью пользовательских функций SQL.  
  
-   [Шаг 5. Обучение и сохранение модели с помощью T-SQL](../../advanced-analytics/r-services/step-5-train-and-save-a-model-using-t-sql.md).  Создайте и сохраните модель машинного обучения с помощью хранимых процедур.  
  
-   [Шаг 6. Ввод модели в эксплуатацию](../../advanced-analytics/r-services/step-6-operationalize-the-model-in-database-advanced-analytics-tutorial.md).  Сохранив модель в базе данных, вызовите ее для прогнозирования из [!INCLUDE[tsql](../../includes/tsql-md.md)] с помощью хранимых процедур.  
  
> [!NOTE]  
> Мы рекомендуем не использовать [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] для написания или тестирования кода на языке R. Если в коде на языке R, внедренном в хранимую процедуру, есть проблемы, сведения, возвращаемые хранимой процедурой, обычно не позволяют установить причину ошибки.   
>   
> В целях отладки рекомендуется использовать такое средство, как RStudio или [!INCLUDE[rtvs-short](../../includes/rtvs-short-md.md)]. Скрипты R, предоставленные в этом учебнике, были разработаны и отлажены с помощью традиционных средств R.  
>   
> Если вы хотите узнать, как разрабатывать скрипты R, которые могут выполняться в [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], см. учебник [Пошаговое руководство по обработке и анализу данных](../../advanced-analytics/r-services/data-science-end-to-end-walkthrough.md).  
  
### Сценарий  
В этом пошаговом руководстве используется известный набор данных по работе такси в Нью-Йорке. Этот общедоступный набор данных состоит из файлов CSV объемом 20 ГБ в сжатом виде (приблизительно 48 ГБ в несжатом виде) и содержит сведения о более чем 173 миллионах отдельных поездках на такси в 2013 году, а также об оплате каждой поездки. Чтобы упростить и ускорить работу с этим пошаговым руководством, мы создали представительную выборку данных, которая включает приблизительно 1 % от общего объема исходных данных (1 703 957 строк и 23 столбца). В этом руководстве вы используете эти данные для построения модели двоичной классификации, которая прогнозирует получение чаевых за определенную поездку на основе значений таких столбцов, как время дня, расстояние и место посадки.  
  
  
### Требования  
Это пошаговое руководство предназначено для пользователей, которые уже знакомы с операциями с базами данных, такими как создание баз данных и таблиц, импорт данных в таблицы и создание запросов SQL. Весь необходимый код на языке R предоставляется, поэтому среда разработки R не требуется. Опытный программист SQL может пройти это руководство, используя [!INCLUDE[tsql](../../includes/tsql-md.md)] в [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] или выполняя предоставленные скрипты PowerShell.  
  
Однако перед началом работы с руководством следует выполнить указанные ниже подготовительные действия.  
  
-   Подключитесь к экземпляру [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] с включенными службами SQL Server R Services (требуется версия CTP 3 или более поздняя). Подробные сведения см. в инструкциях по установке: [Установка служб SQL Server R Services (в базе данных)](https://msdn.microsoft.com/library/mt696069.aspx).  
  
 -   Учетная запись, используемая для этого пошагового руководства, должна иметь разрешения на создание баз данных и других объектов, отправку данных, выбор данных и выполнение хранимых процедур.  
  
## Следующий шаг  
[Шаг 1. Скачивание образца данных](../../advanced-analytics/r-services/step-1-download-the-sample-data-in-database-advanced-analytics-tutorial.md)  
  
## См. также:  
[Учебники по службам SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md)  
[Службы R SQL Server](../../advanced-analytics/r-services/sql-server-r-services.md)  
  
  
  