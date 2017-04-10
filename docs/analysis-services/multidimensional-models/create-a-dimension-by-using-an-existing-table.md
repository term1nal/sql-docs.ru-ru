---
title: "Создание измерения с помощью существующей таблицы | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "иерархии [службы Analysis Services], измерения"
  - "главные таблицы измерений"
  - "измерения [службы Analysis Services], стандартные"
  - "стандартные измерения [службы Analysis Services]"
ms.assetid: edd96fbe-1b1c-445a-95d6-7a025e0ee868
caps.latest.revision: 52
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 52
---
# Создание измерения с помощью существующей таблицы
  Для создания измерения на основе существующей таблицы в службах [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]можно использовать мастер измерений среды [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] . Для этого на странице **Выберите метод создания** мастера измерений необходимо выбрать параметр **Использовать существующую таблицу** . Если выбран этот параметр, мастер сформирует структуру измерения на основе таблиц измерения, их столбцов и всех связей между этими столбцами в существующем представлении источника данных. Мастер делает выборку данных из исходной таблицы и связанных с ней таблиц. На основе этих данных он определяет столбцы атрибутов, основанные на столбцах таблиц измерения, а также иерархии атрибутов (называемые *пользовательскими* иерархиями). Создав измерение с помощью мастера измерений, можно использовать конструктор измерений для добавления, удаления и настройки атрибутов и иерархий в измерении.  
  
 Если измерение создается на основе существующей таблицы, мастер измерений проведет по следующим этапам:  
  
-   Определение исходных сведений  
  
-   Выбор связанных таблиц  
  
-   Выбор атрибутов измерения  
  
-   Определение логики операций со счетами  
  
> [!NOTE]  
>  Пошаговые инструкции, соответствующие представленной здесь информации, см. в разделе [Создание измерения с помощью мастера измерений](../../analysis-services/multidimensional-models/create-a-dimension-using-the-dimension-wizard.md).  
  
## Определение исходных сведений  
 Информация об источнике данных указывается на странице **Определение исходных сведений** . Процесс начинается с выбора представления источников данных, содержащего таблицу, на которой будет основано измерение. Затем следует выбрать основную таблицу определяемого измерения. Это таблица, которая напрямую связана с таблицей фактов. Например, укажите таблицу Product в качестве основной таблицы для измерения «Продукты» или таблицу Employee для измерения «Сотрудники». Мастер автоматически выбирает ключевой столбец, основанный на первичном ключе представления источников данных. Однако при необходимости можно выбрать другой ключевой столбец. Ключевой столбец определяет элементы измерения. Например, можно задать столбец ProductKey в качестве ключевого для измерения «Продукт».  
  
 При необходимости можно задать столбец, содержащий имя элемента. По умолчанию имя элемента, представляемое пользователю, будет значением из ключевого столбца. Значения в ключевом столбце (например, ProductID или EmployeeID) часто представляют собой уникальные ключи, сформированные системой и непонятные для пользователя. Можно предоставить пользователю более значимую информацию, изменив видимое имя на соответствующее значение из какого-либо другого столбца измерения. Например, можно определить столбец имени элемента, содержащий названия продуктов или имена сотрудников. Если изменить имя элемента, пользователи увидят более описательное имя, но запросы по-прежнему будут использовать значения из ключевых столбцов, чтобы правильно различать элементы с одинаковыми именами. Если для ключевого столбца задан составной ключ, необходимо также определить столбец, содержащий значения элементов для ключевого атрибута. Дополнительные сведения о настройке свойств атрибутов см. в разделе [Справочник по свойствам атрибута измерения](../../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md).  
  
## Выбор связанных таблиц  
  
> [!NOTE]  
>  Мастер пропускает этот шаг, если главная таблица измерения не имеет связей с другими таблицами измерения.  
  
 Если измерение создается по схеме «снежинка», необходимо задать связанные таблицы, из которых будут взяты дополнительные атрибуты, на странице **Выбор связанных таблиц** . Например, при создании измерения заказчиков нужно определить таблицу географического положения заказчиков. В этом случае таблица географического положения заказчиков будет указана как связанная.  
  
## Выбор атрибутов измерения  
 Выбрав таблицы измерения, на странице **Выбор атрибутов измерения** выберите атрибуты из этих таблиц для включения в измерение. Атрибутом измерения может стать любой базовый столбец любой из этих таблиц. Ключевой атрибут измерения должен быть выбран, и должен быть разрешен его просмотр.  
  
 По умолчанию мастер присваивает атрибуту тип **Regular**. Однако иногда лучше сопоставить некоторые атрибуты с другим типом атрибута, лучше представляющим данные. Например, таблица dbo.DimAccount в образце базы данных DW [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)] содержит столбец AccountCodeAlternateKey с номерами счетов. Вместо типа **Regular** можно присвоить этому атрибуту тип **Account Number** .  
  
> [!NOTE]  
>  Если при создании измерения его тип и типы стандартных атрибутов не заданы, с помощью мастера бизнес-аналитики можно задать их позже. Дополнительные сведения см. в разделе [Добавление логики измерений к измерению](../../analysis-services/multidimensional-models/add-dimension-intelligence-to-a-dimension.md) или (для измерения типа "Учетные данные") [Добавление логики операций со счетами к измерению](../../analysis-services/multidimensional-models/add-account-intelligence-to-a-dimension.md).  
  
 Мастер автоматически устанавливает тип измерения на основе указанных типов атрибутов. Типы атрибутов, указанные в мастере, задают свойство **Type** для атрибутов. Установка свойства **Type** для измерения и его атрибутов обеспечивает данные о содержимом измерения серверу и клиентским приложениям. Иногда настройка **Type** обеспечивает клиентским приложениям только справочные сведения и необязательна. В других случаях (как для измерений времени, счетов и валют) эти настройки свойства **Type** определяют конкретное поведение, зависящее от сервера, и могут быть необходимы для реализации определенных характеристик куба.  
  
 Дополнительные сведения о типах измерений и атрибутов см. в разделах [Типы атрибутов](../Topic/Dimension%20Types.md) и [Настройка типов атрибутов](../../analysis-services/multidimensional-models/configure-attribute-types.md).  
  
## Определение логики операций со счетами  
  
> [!NOTE]  
>  Мастер измерений показывает этот шаг только в том случае, если на странице **Выбор атрибутов измерения** определен атрибут измерения **Тип счетов**.  
  
 Для создания измерения типа «Счет» используется страница **Определение логики операций со счетами** . Если создается измерение типа «Счет», необходимо сопоставить стандартные типы счетов, поддерживаемые службами [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , с элементами атрибута типа «Счет» в измерении. Сервер использует эти сопоставления для предоставления отдельных статистических функций и псевдонимов для каждого типа данных счета.  
  
 Для сопоставления этих типов счетов мастер предоставляет таблицу со следующими столбцами.  
  
-   Столбец **Типы счетов исходной таблицы** , где перечисляются типы счетов из таблицы источника данных.  
  
-   Столбец **Встроенные типы счетов**, где перечисляются соответствующие стандартные типы счетов, поддерживаемые сервером. Если в исходных данных используются стандартные имена, мастер автоматически связывает исходный тип с типом на сервере и заполняет этой информацией столбец **Встроенные типы счетов**. Если на сервере нет соответствующего типа или необходимо изменить привязку, выберите другой тип в столбце **Встроенные типы счетов**.  
  
> [!NOTE]  
>  Если при создании измерения «Счет» с помощью мастера между типами счетов не было установлено соответствие, то можно задать соответствие типов в мастере бизнес-аналитики после создания измерения. Дополнительные сведения см. в разделе [Добавление логики операций со счетами к измерению](../../analysis-services/multidimensional-models/add-account-intelligence-to-a-dimension.md).  
  
## Завершение работы мастера  
 Мастер просматривает таблицы измерений, чтобы выявить связи. Мастер автоматически создаст связи между ключевыми атрибутами в измерениях типа «снежинка».  
  
 Мастер также автоматически обнаруживает связь типа «родители-потомки», если она существует в измерении. Связь «родители-потомки» существует, когда родительский атрибут ссылается на элементы ключевого атрибута измерения. Эта связь определяет иерархические связи, а также пути статистических вычислений между конечными элементами измерения. Дополнительные сведения об иерархиях "родители-потомки" см. в разделе [Атрибуты в иерархиях типа "родители-потомки"](../../analysis-services/multidimensional-models/attributes-in-parent-child-hierarchies.md).  
  
 Чтобы завершить работу, на странице **Завершение работы мастера** введите имя для нового измерения и просмотрите структуру измерения.  
  
## См. также  
 [Создание измерения путем формирования в источнике данных таблицы, отличной от таблицы времени](../../analysis-services/multidimensional-models/create-a-dimension-by-generating-a-non-time-table-in-the-data-source.md)   
 [Создание измерения времени посредством формирования таблицы времени](../../analysis-services/multidimensional-models/create-a-time-dimension-by-generating-a-time-table.md)   
 [Справочник по свойствам атрибута измерения](../../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md)   
 [Создание измерения времени посредством формирования таблицы времени](../../analysis-services/multidimensional-models/create-a-time-dimension-by-generating-a-time-table.md)   
 [Создание измерения путем формирования в источнике данных таблицы, отличной от таблицы времени](../../analysis-services/multidimensional-models/create-a-dimension-by-generating-a-non-time-table-in-the-data-source.md)  
  
  