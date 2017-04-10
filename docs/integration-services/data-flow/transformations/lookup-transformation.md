---
title: "Преобразование &#171;Уточняющий запрос&#187; | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.lookuptrans.f1"
helpviewer_keywords: 
  - "Преобразование «Уточняющий запрос»"
  - "соединение столбцов [службы Integration Services]"
  - "кэш [службы Integration Services]"
  - "точно соответствовать [службы Integration Services]"
  - "уточняющие запросы [службы Integration Services]"
  - "точные соответствия [службы Integration Services]"
ms.assetid: de1cc8de-e7af-4727-b5a5-a1f0a739aa09
caps.latest.revision: 106
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 106
---
# Преобразование &#171;Уточняющий запрос&#187;
  Преобразование «Уточняющий запрос» выполняет уточняющие запросы, объединяя данные во входных столбцах со столбцами в ссылочном наборе данных. Уточняющие запросы используются для доступа к дополнительной информации в связанной таблице, основанной на значениях в общих столбцах.  
  
 Эталонным набором данных может быть файл кэша, существующая таблица или представление, новая таблица или результат SQL-запроса. Преобразование «Уточняющий запрос» использует для подключения к эталонному набору данных диспетчер соединений OLE DB или диспетчер соединений с кэшем. Дополнительные сведения см. в разделах [OLE DB Connection Manager](../../../integration-services/connection-manager/ole-db-connection-manager.md) и [Cache Connection Manager](../../../integration-services/data-flow/transformations/cache-connection-manager.md).  
  
 Можно настроить преобразование «Уточняющий запрос» следующими способами.  
  
-   Выбрать необходимый диспетчер соединений. Если необходимо подключится к базе данных, выберите диспетчер соединений OLE DB. Если необходимо подключится к файлу кэша, выберите диспетчер соединений с кэшем.  
  
-   Указать таблицу или представление, содержащие эталонный набор данных.  
  
-   Создать эталонный набор данных, указав инструкцию SQL.  
  
-   Указать соединения между входом и эталонным набором данных.  
  
-   Добавить столбцы из эталонного набора данных к выходу преобразования «Уточняющий запрос».  
  
-   Настроить параметры кэширования.  
  
 Преобразование «Уточняющий запрос» поддерживает следующие поставщики базы данных для диспетчера соединений OLE DB:  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  
  
-   Oracle;  
  
-   DB2  
  
 Преобразование «Уточняющий запрос» пытается выполнить эквивалентное соединение значений на входе преобразования и значений в эталонном наборе данных. Эквивалентное соединение означает, что каждая строка на входе преобразования должна соответствовать, по крайней мере, одной строке из эталонного набора данных. Если эквивалентное соединение невозможно, преобразование «Уточняющий запрос» выполняет одно из следующих действий.  
  
-   Если в эталонном наборе данных не существует совпадающих записей, то соединения не происходит. По умолчанию преобразование «Уточняющий запрос» обрабатывает все строки без совпадающих записей как ошибки. Однако можно настроить преобразование «Уточняющий запрос» так, чтобы эти строки перенаправлялись на выход несовпадающих строк. Дополнительные сведения см. в разделах [Редактор преобразования "Уточняющий запрос" (страница "Общие")](../../../integration-services/data-flow/transformations/lookup-transformation-editor-general-page.md) и [Редактор преобразования "Уточняющий запрос" (страница "Вывод ошибок")](../../../integration-services/data-flow/transformations/lookup-transformation-editor-error-output-page.md).  
  
-   Если в ссылочной таблице содержится несколько соответствующих записей, преобразование «Уточняющий запрос» возвращает только первое соответствие, возвращаемое уточняющим запросом. Если было найдено несколько совпадений, преобразование «Уточняющий запрос» формирует ошибку или предупреждение только в том случае, если оно было настроено для загрузки всего эталонного набора данных в кэш. В этом случае преобразование «Уточняющий запрос» формирует ошибку, если оно обнаруживает несколько совпадений во время заполнения кэша.  
  
 Соединение может быть составным. Это значит, что можно объединить несколько столбцов на входе преобразования со столбцами в эталонном наборе данных. Преобразование поддерживает соединение столбцов с любыми типами данных, кроме DT_R4, DT_R8, DT_TEXT, DT_NTEXT и DT_IMAGE. Дополнительные сведения см. в статье [Integration Services Data Types](../../../integration-services/data-flow/integration-services-data-types.md).  
  
 Обычно значения из эталонного набора данных добавляются к выходу преобразования. Например, преобразование «Уточняющий запрос» может извлечь название продукта из таблицы, используя значение из входного столбца, затем добавить название продукта в выход преобразования. Значения из ссылочной таблицы могут заменить значения столбца или могут быть добавлены в новый столбец.  
  
 Уточняющие запросы выполняются преобразованием «Уточняющие запросы» с учетом регистра. Чтобы избежать сбоев поиска, вызванных различиями регистра в данных, можно предварительно преобразовать данные в верхний или нижний регистр с помощью преобразования «Таблица символов». Затем следует включить функции UPPER или LOWER в инструкцию SQL, создающую ссылочную таблицу. Дополнительные сведения см. в разделах [Преобразование "Таблица символов"](../../../integration-services/data-flow/transformations/character-map-transformation.md), [UPPER (Transact-SQL)](../../../t-sql/functions/upper-transact-sql.md) и [LOWER (Transact-SQL)](../../../t-sql/functions/lower-transact-sql.md).  
  
 Преобразование «Уточняющий запрос» имеет следующие входы и выходы.  
  
-   Вход.  
  
-   Выход совпадающих строк. Выход совпадающих строк обрабатывает строки во входе преобразования, которые не совпадают, по крайней мере, с одной из записей ссылочного набора данных.  
  
-   Выход несовпадающих строк. Выход несовпадающих строк обрабатывает строки во входе, которые не совпадают ни с одной записью эталонного набора данных. Если преобразование «Уточняющий запрос» было настроено для обработки строк без совпадающих записей как ошибок, строки будут перенаправлены в вывод ошибок на выходе. В противном случае преобразование перенаправит эти строки в выход несовпадающих строк.  
  
-   Вывод ошибок на выходе.  
  
## Кэширование эталонного набора данных  
 В кэше в памяти хранится эталонный набор данных и хэш-таблица, индексирующая данные. Кэш остается в памяти, пока не завершится выполнение пакета. Можно сохранить кэш в кэш-файле (CAW).  
  
 Если кэш был сохранен в файл, система загружает его быстрее. Это повышает производительность преобразования «Уточняющий запрос» и пакета. Помните, что при использовании кэш-файла работа идет с данными, которые менее актуальны, чем данные в базе данных.  
  
 Сохранение кэша в файл имеет следующие преимущества.  
  
-   ***Совместное использование файла кэша несколькими пакетами. Дополнительные сведения см в разделе *** [Реализация преобразования "Уточняющий запрос" в режиме полного кэширования с помощью преобразования диспетчера соединений с кэшем](../../../integration-services/data-flow/transformations/lookup transformation full cache mode - cache connection manager.md) ***.***  
  
-   Развертывание кэш-файла с пакетом. ***Затем эти данные можно использовать на нескольких компьютерах.*** Дополнительные сведения см. в разделе [Создание или развертывание кэша для преобразования "Уточняющий запрос"](../../../integration-services/data-flow/transformations/create-and-deploy-a-cache-for-the-lookup-transformation.md).  
  
-   Чтобы считывать данные из кэш-файла можно использовать источник «Необработанный файл». Затем можно использовать другие компоненты потока данных, чтобы преобразовать или переместить данные. Дополнительные сведения см. в статье [Raw File Source](../../../integration-services/data-flow/raw-file-source.md).  
  
    > [!NOTE]  
    >  Диспетчер соединений с кэшем не поддерживает кэш-файлы, которые были созданы или изменены с помощью назначения «Необработанный файл».  
  
-   Чтобы совершать операции и задавать атрибуты кэш-файлов, можно использовать задачу «Файловая система». Дополнительные сведения см. в разделе [File System Task](../../../integration-services/control-flow/file-system-task.md).  
  
 Далее приводятся режимы кэширования.  
  
-   Эталонный набор данных создается с помощью таблицы, представления или SQL-запроса и загружается в кэш до запуска преобразования «Уточняющий запрос». Для доступа к набору данных можно использовать диспетчер соединений OLE DB.  
  
     Этот режим кэширования совместим с параметром полного кэширования, доступным для преобразования «Уточняющий запрос» в службах [!INCLUDE[ssISversion2005](../../../includes/ssisversion2005-md.md)].  
  
-   Эталонный набор данных создается с помощью подключенного источника данных в потоке данных или с помощью кэш-файла, а затем загружается в кэш до выполнения преобразования «Уточняющий запрос». Для доступа к набору данных можно использовать диспетчер соединений с кэшем и, дополнительно, преобразование «Кэш». Дополнительные сведения см. в разделах [Cache Connection Manager](../../../integration-services/data-flow/transformations/cache-connection-manager.md) и [Cache Transform](../../../integration-services/data-flow/transformations/cache-transform.md).  
  
-   Создание эталонного набора данных производится по таблице, представлению или SQL-запросу во время выполнения преобразования «Уточняющий запрос». Строки с совпадающими записями в эталонном наборе данных и строки без совпадающих записей в наборе данных загружаются в кэш.  
  
     Когда превышается объем памяти кэша, преобразование «Уточняющий запрос» автоматически удаляет из кэша строки, которые используются реже всего.  
  
     Этот режим кэширования совместим с параметром частичного кэширования, доступным для преобразования «Уточняющий запрос» в службах [!INCLUDE[ssISversion2005](../../../includes/ssisversion2005-md.md)].  
  
-   Создание эталонного набора данных производится по таблице, представлению или SQL-запросу во время выполнения преобразования «Уточняющий запрос». Данные не кэшируются.  
  
     Этот режим кэширования совместим с параметром отсутствия кэширования, доступным для преобразования «Уточняющий запрос» в службах [!INCLUDE[ssISversion2005](../../../includes/ssisversion2005-md.md)].  
  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] и [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] различается способ сравнения строк. Если преобразование «Уточняющий запрос» было настроено для загрузки эталонного набора данных в кэш до своего запуска, службы [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] проводят сравнение уточняющего запроса в кэше. В противном случае операция уточняющего запроса использует параметризованную инструкцию SQL, а [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] производит сравнение уточняющего запроса. Это означает, что преобразование «Уточняющий запрос» может возвращать различное количество результатов поиска из одной и той же таблицы подстановки в зависимости от типа кэша.  
  
## Связанные задачи  
 Значения свойств можно задавать с помощью конструктора [!INCLUDE[ssIS](../../../includes/ssis-md.md)] или программными средствами. Дополнительные сведения см. в следующих разделах.  
  
-   [Реализация уточняющего запроса в режиме «Частичное кэширование» или «Без кэширования»](../../../integration-services/data-flow/transformations/implement-a-lookup-in-no-cache-or-partial-cache-mode.md)  
  
-   [реализовать преобразование «Уточняющий запрос» в режиме полного кэширования с помощью диспетчера соединений с кэшем](../../../integration-services/data-flow/transformations/lookup transformation full cache mode - cache connection manager.md)  
  
-   [Реализация преобразования «Уточняющий запрос» в режиме полного кэширования с помощью диспетчера соединений OLE DB](../../../integration-services/data-flow/transformations/lookup transformation full cache mode - ole db connection manager.md)  
  
-   [Установление свойств компонента потока данных](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## См. также  
  
-   Видеоролик [Как реализовать преобразование «Уточняющий запрос» в режиме полного кэширования](http://go.microsoft.com/fwlink/?LinkId=131031)на сайте msdn.microsoft.com  
  
-   Запись в блоге, [Рекомендации по использованию режимов кэширования для преобразования «Уточняющий запрос»](http://go.microsoft.com/fwlink/?LinkId=146623), на сайте blogs.msdn.com  
  
-   Запись в блоге [Шаблон уточняющего запроса: без учета регистра символов](http://go.microsoft.com/fwlink/?LinkId=157782)на сайте blogs.msdn.com  
  
-   Образец, [Преобразование «Уточняющий запрос»](http://go.microsoft.com/fwlink/?LinkId=267528), на сайте msftisprodsamples.codeplex.com.  
  
     Дополнительные сведения об установке образцов продукта и баз данных служб [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] см. в разделе [Образцы продукта служб SQL Server Integration Services](http://go.microsoft.com/fwlink/?LinkId=267527).  
  
## См. также  
 [Преобразование «Нечеткий уточняющий запрос»](../../../integration-services/data-flow/transformations/fuzzy-lookup-transformation.md)   
 [Преобразование «Уточняющий запрос термина»](../../../integration-services/data-flow/transformations/term-lookup-transformation.md)   
 [Поток данных](../../../integration-services/data-flow/data-flow.md)   
 [Преобразования служб Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  