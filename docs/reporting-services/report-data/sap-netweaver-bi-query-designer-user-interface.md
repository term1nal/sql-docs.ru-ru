---
title: "Пользовательский интерфейс конструктора запросов BI SAP NetWeaver | Microsoft Docs"
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
f1_keywords: 
  - "sql13.rtp.rptdesigner.dataview.sapbwquerydesigner.f1"
  - "10014"
helpviewer_keywords: 
  - "источники данных [службы Reporting Services], SAP NetWeaver Business Intelligence"
  - "SAP NetWeaver Business Intelligence [службы Reporting Services], конструктор запросов"
  - "конструкторы запросов [службы Reporting Services]"
ms.assetid: 102da66e-ca31-41aa-ab4b-c9b5ab752a72
caps.latest.revision: 38
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 38
---
# Пользовательский интерфейс конструктора запросов BI SAP NetWeaver
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] предоставляют графический конструктор запросов, предназначенный для построения запросов многомерных выражений к источнику данных SAP NetWeaver® Business Intelligence. Графический конструктор запросов многомерных выражений имеет два режима: режим конструктора и режим запросов. В каждом режиме имеется панель «Метаданные», из которой можно перетащить элементы из InfoCube, MultiProvider или запроса с поддержкой веб-доступа, определенного на источнике данных, для построения запроса многомерных выражений, получающего данные при обработке отчета.  
  
> [!IMPORTANT]  
>  При создании и выполнении запросов пользователи получают доступ к источникам данных. Следует предоставить минимальные разрешения на источники данных, например разрешение только на чтение.  
  
 Дополнительные сведения о работе с многомерными источниками данных SAP см. в разделе [Тип соединения SAP NetWeaver BI (службы SSRS)](../../reporting-services/report-data/sap-netweaver-bi-connection-type-ssrs.md).  
  
 В этом разделе описываются кнопки панели инструментов и области конструктора запросов для каждого режима работы графического конструктора запросов.  
  
## Графический конструктор запросов в режиме конструктора  
 При изменении запроса набора данных, в котором используется источник данных [!INCLUDE[SAP_DPE_BW_1](../../includes/sap-dpe-bw-1-md.md)] , графический конструктор запросов открывается в режиме конструктора. На следующем рисунке отмечены панели в режиме конструктора.  
  
 ![Конструктор запросов с использованием многомерных выражений в режиме конструктора](../../reporting-services/report-data/media/rsqd-dssapbw-mdx-designmode.gif "Конструктор запросов с использованием многомерных выражений в режиме конструктора")  
  
 В следующей таблице приводится список панелей в этом режиме.  
  
|Панель|Функция|  
|----------|--------------|  
|Кнопка «Выбрать куб»|Отображается текущий выбранный InfoCube, MultiProvider или запрос с поддержкой веб-доступа.|  
|Панель «Метаданные»|Отображается иерархический список InfoCube, MultiProvider и запросов. Запросы, созданные в источнике данных, появляются под соответствующим кубом.|  
|Панель «Вычисляемые элементы»|Отображает вычисляемые элементы, определенные на данный момент и доступные для использования в запросе.|  
|Панель «Данные»|Отображает результаты выполнения запроса.|  
  
 На панель «Данные» можно перетаскивать измерения и ключевые элементы с панели «Метаданные» и вычисляемые элементы с панели «Вычисляемые элементы». Если переключатель **Автовыполнение** на панели инструментов включен, конструктор запросов выполняет запрос каждый раз при перетаскивании объекта в область «Данные». Если переключатель **Автовыполнение** выключен, конструктор запросов не выполняет запрос при любых изменениях в панели «Данные». Запрос можно выполнить вручную, нажав кнопку **Запуск** на панели инструментов.  
  
### Панель инструментов графического конструктора запросов в режиме конструктора  
 Панель инструментов конструктора запросов содержит кнопки, которые помогают создавать запросы многомерных выражений с помощью графического интерфейса. В следующей таблице перечислены кнопки и описаны их функции.  
  
|Кнопка|Description|  
|------------|-----------------|  
|**Редактировать как текст**|Переключиться из текстового конструктора запросов в графический и обратно. Недоступен для этого типа источника данных.|  
|**Импорт**|Импортировать существующий запрос из файла определения отчета (RDL), расположенного в файловой системе. Дополнительные сведения см. в разделе [Внедренные и общие наборы данных отчета (построитель отчетов и службы SSRS)](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md).|  
|![Refresh dataset fields](../../reporting-services/report-data/media/rsqdicon-refreshfields.gif "Refresh dataset fields")|Обновление метаданных из источника данных.|  
|![Добавление вычисляемого элемента](../../reporting-services/report-data/media/rsqdicon-addcalculatedmember.png "Добавление вычисляемого элемента")|Отображение диалогового окна **Построитель вычисляемых элементов** .|  
|![Переключатель для просмотра пустых ячеек](../../reporting-services/report-data/media/rsqdicon-showemptycells.png "Переключатель для просмотра пустых ячеек")|Переключение между режимами отображения и скрытия пустых ячеек в панели «Данные». (Это эквивалентно использованию предложения NON EMPTY в многомерном выражении).|  
|![Автоматическое выполнение запроса](../../reporting-services/report-data/media/rsqdicon-autoexecute.png "Автоматическое выполнение запроса")|Автоматическое выполнение запроса и вывод результатов после каждого изменения, например после удаления столбца на панели «Данные». Результаты отображаются в панели «Данные».|  
|![Удалить](../../reporting-services/report-data/media/rsqdicon-delete.png "Удалить")|Удалить выбранный на панель «Данные» столбец из запроса.|  
|![Значок диалогового окна «Параметры запроса»](../../reporting-services/report-data/media/iconqueryparameter.png "Значок диалогового окна «Параметры запроса»")|Отобразить диалоговое окно **Переменные** . Эта кнопка включена, только если выбранный куб является кубом запроса (так как переменные поддерживаются только в кубах запросов). При присвоении переменной значения по умолчанию создается соответствующий параметр в отчете.|  
|![Выполнение запроса](../../reporting-services/report-data/media/rsqdicon-run.png "Выполнение запроса")|Выполнить запрос и показать результаты на панели «Данные».|  
|![Cancel the query](../../reporting-services/report-data/media/rsqdicon-cancel.gif "Cancel the query")|Отмена запроса.|  
|![Переключение в режим конструктора](../../reporting-services/media/rsqdicon-designmode.png "Переключение в режим конструктора")|Переключение между режимом конструктора и режимом запросов.|  
  
## Графический конструктор запросов в режиме запросов  
 Для переключения графического конструктора запросов в режим запросов щелкните переключатель **Режим конструктора** на панели инструментов.  
  
 На следующем рисунке показаны части конструктора запросов в режиме запросов.  
  
 ![Конструктор запросов многомерных выражений SAP BW в режиме запроса](../../reporting-services/report-data/media/rsqd-dssapbw-mdx-querymode.gif "Конструктор запросов многомерных выражений SAP BW в режиме запроса")  
  
 В следующей таблице описываются функции каждой панели.  
  
|Панель|Функция|  
|----------|--------------|  
|Кнопка «Выбрать куб»|Отображает текущий выбранный InfoCube, MultiProvider или другой куб.|  
|Панель «Метаданные/Функции»|Отображает окно с вкладками, содержащее список доступных метаданных и функций, которые можно использовать при создании текста запроса.|  
|Панель «Переменные»|Отображает определенные в настоящее время переменные, которые можно использовать в запросе.|  
|Панель запросов|Отображает текст текущего запроса.|  
|Панель результатов|Отображает результаты запроса.|  
  
 С панели «Метаданные» можно перетаскивать ключевые элементы и измерения с вкладки **Метаданные** на панель запроса многомерных выражений. Техническое имя метаданных вставляется в то место, где находится курсор. Функции можно перетаскивать в панель «Запросы многомерных выражений» с вкладки **Функции** . При выполнении запроса в панели «Результат» отображаются результаты текущего запроса многомерных выражений.  
  
 Если выбранный куб является запросом с поддержкой веб-доступа, будет предложено задать статические значения по умолчанию для существующих переменных. После этого можно будет перетащить переменные на панель запроса многомерных выражений.  
  
 На панелях метаданных и переменных выводятся понятные имена. При перетаскивании объектов на панель запроса многомерных выражений выводятся технические имена, необходимые источнику данных, введенному в запрос многомерных выражений.  
  
### Панель инструментов графического конструктора запросов в режиме запросов  
 Панель инструментов конструктора запросов содержит кнопки, которые помогают создавать запросы многомерных выражений с помощью графического интерфейса. Кнопки на панели инструментов в режиме конструктора ничем не отличаются от кнопок в режиме запроса, однако в режиме запроса недоступны следующие кнопки.  
  
-   **Редактировать как текст**  
  
-   **Добавить вычисляемый элемент** (![Добавление вычисляемого элемента](../../reporting-services/report-data/media/rsqdicon-addcalculatedmember.png "Добавление вычисляемого элемента"))  
  
-   **Показывать пустые ячейки** (![Переключатель для просмотра пустых ячеек](../../reporting-services/report-data/media/rsqdicon-showemptycells.png "Переключатель для просмотра пустых ячеек"))  
  
-   **Автовыполнение** (![Автоматическое выполнение запроса](../../reporting-services/report-data/media/rsqdicon-autoexecute.png "Автоматическое выполнение запроса"))  
  
-   **Удалить** (![Удалить](../../reporting-services/report-data/media/rsqdicon-delete.png "Удалить"))  
  
## См. также  
 [Создание общего или внедренного набора данных (построитель отчетов и службы SSRS)](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)   
 [Файл конфигурации RSReportDesigner](../../reporting-services/report-server/rsreportdesigner-configuration-file.md)  
  
  