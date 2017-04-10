---
title: "Импорт и экспорт данных с помощью мастера импорта и экспорта SQL Server | Microsoft Docs"
ms.custom: ""
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "экспорт данных"
  - "файлы сопоставлений [службы Integration Services]"
  - "мастер импорта и экспорта SQL Server"
  - "пакеты служб SSIS, создание"
  - "пакеты [службы Integration Services], копирование"
  - "пакеты служб Integration Services, создание"
  - "пакеты [службы Integration Services], создание"
  - "пакеты служб SQL Server Integration Services, создание"
  - "мастер импорта и экспорта"
  - "копирование данных [службы Integration Services]"
  - "импорт данных, пакеты служб SSIS"
  - "источники [службы Integration Services], копирование данных"
ms.assetid: c0e4d867-b2a9-4b2a-844b-2fe45be88f81
caps.latest.revision: 160
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 134
---
# Импорт и экспорт данных с помощью мастера импорта и экспорта SQL Server
 Мастер импорта и экспорта [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] предоставляет простой способ копирования данных из источника в целевой объект. Для запуска мастера наличие SQL Server не обязательно. В этом обзоре рассматриваются источники данных, из которых можно импортировать данные (или в которые можно экспортировать данные) при помощи мастера, а также разрешения, необходимые для использования мастера.

Данный раздел содержит только **общее описание** мастера.
-   Если вы готовы запустить мастер и хотите знать, как это сделать, см. раздел [Запуск мастера экспорта и импорта SQL Server](../../integration-services/import-export-data/start-the-sql-server-import-and-export-wizard.md).
-   Если вам нужна информация о процедурах, выполняемых в мастере, выберите нужную страницу в меню навигации по контенту. Каждой странице мастера соответствует отдельная страница документации. Вы можете также нажать клавишу F1 при просмотре любой страницы или диалогового окна, чтобы открыть документацию по текущей странице мастера.

**Запустите мастер.** Если вы хотите запустить мастер, но на вашем компьютере не установлен [!INCLUDE[msCoName] (../Token/msCoName_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], мастер импорта и экспорта [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] можно установить с помощью SQL Server Data Tools (SSDT). Дополнительные сведения см. в разделе [Скачивание SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx).

> [!TIP] Если вам нужно скопировать несколько баз данных или объекты базы данных, отличные от таблиц и представлений, вместо мастера импорта и экспорта используйте мастер копирования базы данных. Дополнительные сведения см. в разделе [Использование мастера копирования базы данных](../../relational-databases/databases/use-the-copy-database-wizard.md).

## <a name="example-of-a-common-use-case---exporting-data-to-excel-video"></a>Пример распространенного варианта использования — экспорт данных в Excel (видео)  
Обычно мастер используется для экспорта данных в Excel. В этом четырехминутном видео на YouTube объясняется, как это сделать с помощью мастера и понятных и простых инструкций, — [Using the SQL Server Import and Export Wizard to Export to Excel](https://go.microsoft.com/fwlink/?linkid=829049) (Использование мастера импорта и экспорта SQL Server для экспорта в Excel).

##  <a name="a-namewizardsourcesa-what-data-sources-and-destinations-can-i-use"></a><a name="wizardSources"></a> Какие источники данных и назначения можно использовать?  
 Мастер импорта и экспорта [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] может копировать данные из следующих источников данных. Для использования некоторых из этих источников данных может потребоваться скачать и установить дополнительные файлы.

| Источник данных | Нужно ли скачивать дополнительные файлы? |
|-------------|-----------------------------------------|
|**Базы данных корпоративного класса**<br/>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Oracle и др.|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] устанавливает файлы, необходимые для подключения к [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] и Oracle, но не устанавливает файлы, необходимые для подключения к другим корпоративным базам данных, например IBM DB2 или Informix.<br/>Если для корпоративной системы баз данных уже установлено клиентское программное обеспечение, то, как правило, у вас есть все необходимое для установки соединения.<br/>Если клиентское программное обеспечение не установлено, обратитесь к администратору базы данных по поводу установки лицензионной копии.|
|**Базы данных с открытым исходным кодом**<br/>MySql, PostgreSQL, SQLite и др.|Для подключения к этим источникам данных необходимо загрузить дополнительные файлы.<br/><br/>В случае **MySql** см. [Соединители MySQL](http://dev.mysql.com/downloads/connector/).<br/>В случае **PostgreSQL** см. [psqlODBC — драйвер ODBC для PostgreSQL](https://odbc.postgresql.org/) и продукты сторонних производителей, такие как [Npgsql — поставщик данных .NET для PostgreSQL](http://www.npgsql.org/).<br/>В случае **SQLite** выберите подходящий продукт среди нескольких поставщиков, а также драйвер, доступный в Интернете.|
|**Текстовые** (неструктурированные) файлы.|Никакие дополнительные файлы не требуются.|
|**Файлы Microsoft Excel и Microsoft Access**|Microsoft Office не устанавливает все файлы, необходимые для подключения к файлам Excel и Access в качестве источников данных. Скачайте [среду выполнения Microsoft Access 2016](https://www.microsoft.com/download/details.aspx?id=50040).|
|**Источники данных Azure**<br/>В настоящее время доступно только хранилище BLOB-объектов Azure.|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] не устанавливает файлы, необходимые для подключения к хранилищу BLOB-объектов Azure как к источнику данных. Скачайте [пакет дополнительных компонентов служб SQL Server Integration Services 2016 для Azure](https://www.microsoft.com/download/details.aspx?id=49492).|
|**Любой другой источник данных, для которого доступен соединитель**.|Обычно для подключения к указанным ниже источникам данных требуется скачать дополнительные файлы.<br/><br/>Любой источник, для которого доступен **драйвер ODBC**. Установите подключение ODBC (Open Database Connectivity), выбрав поставщик .Net Framework для Odbc на странице мастера **Выбор источника данных** или **Выбор назначения**, а затем укажите строку подключения или существующее имя источника данных, которое ссылается на драйвер ODBC.<br/>Любой источник, для которого доступен **поставщик OLE DB**.<br/>Любой источник, для которого доступен **поставщик данных .NET Framework**.<br/>Другие источники данных, для которых **компоненты независимых производителей** предоставляют возможности источника и назначения. Обычно эти сторонние продукты продаются как дополнительные компоненты для служб SQL Server Integration Services (SSIS).|
  
> [!TIP] Если для источника данных требуется строка подключения, см. примеры на стороннем сайте [The Connection Strings Reference](https://www.connectionstrings.com/) (Справочник по строкам подключения).  
  
## <a name="what-permissions-do-i-need-to-run-the-wizard"></a>Разрешения, необходимые для запуска мастера  
 Чтобы успешно запустить мастер импорта и экспорта служб [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], нужно иметь по крайней мере одно из указанных ниже разрешений. Если вы уже работаете с источником данных и назначением, вероятно, у вас уже есть нужные разрешения.
  
|Задачи, для выполнения которых требуются разрешения|Разрешения, необходимые при подключении к SQL Server |  
|-------------------------|----------------------------------------------------|  
|Подключение к исходным и целевым базам данных, а также к общим папкам.|Права на вход в систему сервера и базы данных.|  
|Экспорт или считывание данных из исходной базы данных или файла.|Разрешения SELECT на исходные таблицы и представления.|  
|Импорт или запись данных в целевую базу данных или файл.|Разрешения INSERT для целевых таблиц.|  
|Создание целевой базы данных или файла, если это применимо.|Разрешения CREATE DATABASE или CREATE TABLE.|  
|Сохранение пакета служб SSIS, созданного с помощью мастера, если применимо.|Если вы хотите сохранить пакет в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], достаточно разрешений для сохранения пакета в базу данных **msdb**.|  
  
##  <a name="a-namewizardssisa-the-wizard-uses-sql-server-integration-services-ssis"></a><a name="wizardSSIS"></a> Мастер использует службы SQL Server Integration Services  
 Мастер использует службы SQL Server Integration Services (SSIS) для копирования данных. Службы SSIS — это средство для извлечения, преобразования и загрузки данных (ETL). Страницы мастера используют некоторые фрагменты языка служб SSIS.
  
 В службах SSIS основной единицей является **пакет**. По мере перемещения по страницам и указания параметров мастер создает пакет служб SSIS в памяти.    
  
Если установлен [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Standard Edition или более поздний выпуск, можно при необходимости сохранить пакет SSIS. В дальнейшем при помощи конструктора служб [!INCLUDE[ssIS](../../includes/ssis-md.md)] можно повторно использовать пакет или расширить его, включив дополнительные задачи, преобразования и логику обработки событий. Мастер импорта и экспорта [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] является простейшим методом создания базового пакета служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], копирующего данные из источника в назначение.

Дополнительные сведения о службах SSIS см. в разделе [Службы SQL Server Integration Services](../../integration-services/sql-server-integration-services.md).

## <a name="get-help-while-the-wizard-is-running"></a>Получение справки во время работы мастера
> [!TIP] Нажмите клавишу F1 при просмотре любой страницы или диалогового окна, чтобы открыть документацию по текущей странице мастера.   
  
## <a name="whats-next"></a>Дальнейшие действия  
 Запустите мастер. Дополнительные сведения см. в разделе [Запуск мастера импорта и экспорта SQL Server](../../integration-services/import-export-data/start-the-sql-server-import-and-export-wizard.md).  
  
## <a name="see-also"></a>См. также:
[Сопоставление типов данных в мастере импорта и экспорта SQL Server](../../integration-services/import-export-data/data-type-mapping-in-the-sql-server-import-and-export-wizard.md)