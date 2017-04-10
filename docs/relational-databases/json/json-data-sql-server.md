---
title: "Данные JSON (SQL Server) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "01/31/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-json"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
helpviewer_keywords: 
  - "JSON"
  - "JSON, встроенная поддержка"
ms.assetid: c9a4e145-33c3-42b2-a510-79813e67806a
caps.latest.revision: 47
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 44
---
# Данные JSON (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  JSON — это популярный формат текстовых данных, который используется для обмена данными в современных веб- и мобильных приложениях. Кроме того, JSON используется для хранения неструктурированных данных в файлах журналов или в базах данных NoSQL, таких как Microsoft Azure DocumentDB. Многие веб-службы REST возвращают результаты в формате текста JSON или принимают данные в формате JSON. Большинство служб Azure, таких как поиск Azure, хранилище Azure и Azure DocumentDb, имеют конечные точки REST, которые возвращают или принимают JSON. JSON — это также основной формат обмена данными между веб-страницами и веб-серверами с помощью вызовов AJAX.  
  
 Вот пример текста JSON:  
  
```json  
[   
   { "name": "John", "skills":["SQL","C#","Azure"] },  
   { "name": "Jane", "surname": "Doe" }  
]  
```  
  
 SQL Server предоставляет встроенные функции и операторы, позволяющие выполнять указанные ниже действия.  
  
-   Синтаксический анализ текста JSON, а также считывание и изменение значений.  
  
-   Преобразования массивов объектов JSON в табличный формат.  
  
-   Применение любого запроса Transact SQL к преобразованным объектам JSON.  
  
-   Форматирование результатов запросов Transact-SQL в формате JSON.  
  
 ![Overview of built-in JSON support](../../relational-databases/json/media/jsonslides1overview.png "Overview of built-in JSON support")  
  
 Рассмотрим основные возможности, предоставляемые SQL Server.  
  
 **Извлечение значений из текста JSON и их использование в запросах.** Если у вас есть текст JSON, который хранится в таблицах базы данных, используйте встроенные функции для чтения или измените значения в тексте JSON.  
  
-   Функция **JSON_VALUE** позволяет извлечь скалярное значение из строки JSON.  
  
-   Функция **JSON_QUERY** позволяет извлечь объект или массив.  
  
-   Используйте функцию **ISJSON** для проверки строки на наличие допустимых данных JSON.  
  
 В следующем примере представлен запрос, в котором используются реляционные данные и данные JSON (хранятся в столбце jsonCol) из таблицы:  
  
```tsql  
  
SELECT Name, Surname,     
    JSON_VALUE(jsonCol, '$.info.address.PostCode') as PostCode,  
    JSON_VALUE(jsonCol, '$.info.address."Address Line 1"') +  ' ' + JSON_VALUE(jsonCol, '$.info.address."Address Line 2"') AS Address,  
    JSON_QUERY(jsonCol, '$.info.skills') as Skills  
FROM PeopleCollection  
WHERE ISJSON(jsonCol) > 0   
  AND JSON_VALUE(jsonCol, '$.info.address.town') = 'Belgrade'  
  AND Status = 'Active'  
ORDER BY JSON_VALUE(@jsonInfo, '$.info.address.PostCode')  
  
```  
  
 Приложения и средства не видят разницы между значениями, взятыми из скалярных столбцов таблицы, и значениями, взятыми из столбца JSON. Значения из текста JSON можно использовать в любой части запроса Transact-SQL (включая предложения WHERE, ORDER BY, GROUP BY, агрегатные операции с окнами и т. д.). Для ссылок на значения в тексте JSON функции JSON используют синтаксис типа JavaScript. Дополнительные сведения см. в статьях [Проверка, построение запросов и изменение данных JSON с помощью встроенных функций (SQL Server)](../../relational-databases/json/validate-query-and-change-json-data-with-built-in-functions-sql-server.md), [JSON_VALUE (Transact-SQL)](../../t-sql/functions/json-value-transact-sql.md) и [JSON_QUERY (Transact-SQL)](../../t-sql/functions/json-query-transact-sql.md).  
  
 **Изменение значений JSON.** Если вам нужно изменить части текста JSON, используйте функцию **JSON_MODIFY**, чтобы обновить значение свойства в строке JSON и получить обновленную строку JSON. В следующем примере показано, как изменить значение свойства в переменной, которая содержит данные в формате JSON.  
  
```tsql  
SET @jsonInfo = JSON_MODIFY(@jsonInfo, '$.info.address[0].town', 'London')  
```  
  
 **Преобразование коллекций JSON в набор строк.** Для выполнения запросов JSON в SQL Server никакой особый язык запросов не требуется. Для запроса данных JSON можно использовать стандартные инструкции T-SQL. Если вам нужно создать запрос или отчет по данным JSON, вы можете легко конвертировать данные JSON в строки и столбцы, вызвав функцию набора строк **OPENJSON**. Используйте функцию **OPENJSON** для импорта данных JSON в SQL Server или для преобразования данных JSON в строки и столбцы. Дополнительные сведения см. в статье [Преобразование данных JSON в строки и столбцы с помощью функции OPENJSON (SQL Server)](../../relational-databases/json/convert-json-data-to-rows-and-columns-with-openjson-sql-server.md).  
  
 В следующем примере вызывается функция **OPENJSON** , которая преобразует массив объектов, хранящийся в переменной **@json** , в набор строк, который можно запросить с помощью стандартной инструкции SQL SELECT:  
  
```tsql  
SET @json =  
N'[  
      { "id" : 2,"info": { "name": "John", "surname": "Smith" }, "age": 25 },  
      { "id" : 5,"info": { "name": "Jane", "surname": "Smith" }, "dob": "2005-11-04T12:00:00" }  
]'  
  
SELECT *  
FROM OPENJSON(@json)  
 WITH (id int 'strict $.id',  
       firstName nvarchar(50) '$.info.name', lastName nvarchar(50) '$.info.surname',  
       age int, dateOfBirth datetime2 '$.dob')  
  
```  
  
 **Результаты**  
  
|идентификатор|firstName|lastName|age|dateOfBirth|  
|--------|---------------|--------------|---------|-----------------|  
|2|Джон|Смит|25||  
|5|Джейн|Смит||2005-11-04T12:00:00|  
  
 **OPENJSON** преобразует массив объектов JSON в таблицу, где каждый объект представлен в отдельной строке, а пары ключ:значение возвращаются как ячейки. **OPENJSON** конвертирует значения JSON в указанные типы. **OPENJSON** может обрабатывать плоские пары ключ:значение, а также вложенные объекты с иерархической организацией. Все поля в тексте JSON возвращать необязательно. **OPENJSON** возвращает пустые значения, если значений JSON нет. Путь, размещаемый после указания типа, можно использовать для ссылки на вложенное свойство или просто для ссылки на свойство с другим именем. Необязательный префикс **strict** в пути означает, что значения указанных свойств должны присутствовать в тексте JSON. Дополнительные сведения см. в статьях [Преобразование данных JSON в строки и столбцы с помощью функции OPENJSON (SQL Server)](../../relational-databases/json/convert-json-data-to-rows-and-columns-with-openjson-sql-server.md) и [OPENJSON (Transact-SQL)](../../t-sql/functions/openjson-transact-sql.md).  
  
 **Преобразуйте данные SQL Server в JSON или экспортируйте JSON.** Данные из SQL Server в формате JSON или результаты запросов SQL можно отформатировать как JSON, добавив предложение **FOR JSON** к инструкции **SELECT**. FOR JSON позволяет делегировать форматирование выходных данных JSON из клиентских приложений в SQL Server. Дополнительные сведения см. в статье [Форматирование результатов запроса как JSON с помощью предложения FOR JSON (SQL Server)](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md).  
  
 В следующем примере используется режим PATH с предложением FOR JSON.  
  
```tsql  
SELECT id, firstName AS "info.name", lastName AS "info.surname", age, dateOfBirth as dob  
FROM People  
FOR JSON PATH  
```  
  
 Это   
Предложение     **FOR JSON** отформатирует результаты SQL как текст JSON, который можно предоставить любому приложению, которое понимает JSON. Параметр PATH содержит псевдонимы, разделенные точками, в предложении SELECT для вложения объектов в результаты запросов.  
  
 **Результаты**  
  
```json  
[  
      { "id" : 2,"info": { "name": "John", "surname": "Smith" }, "age": 25 },  
      { "id" : 5,"info": { "name": "Jane", "surname": "Smith" }, "dob": "2005-11-04T12:00:00" }  
]  
```  
  
 Дополнительные сведения см. в статьях [Форматирование результатов запроса как JSON с помощью предложения FOR JSON (SQL Server)](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md) и [Предложение FOR (Transact-SQL)](../Topic/FOR%20Clause%20\(Transact-SQL\).md).  
  
## Способы применения  
 SQL Server предоставляет гибридную модель для хранения и обработки реляционных данных и данных JSON с использованием стандартного языка Transact-SQL. Это позволяет формировать коллекции документов JSON по таблицам, устанавливать отношения между ними, комбинировать строго типизированные скалярные столбцы, которые хранятся в таблицах с гибкими парами ключ:значение, хранящимися в столбцах JSON, и запрашивает скалярные значения и значения JSON в одной или нескольких таблицах с использованием полного Transact-SQL. Текст JSON обычно хранится в столбцах varchar или nvarchar и индексируется как обычный текст. Любая функция или компонент SQL Server, которые поддерживают текст, поддерживают и JSON, поэтому в обмене данных между JSON и другими компонентами SQL Server нет практически никаких ограничений. JSON можно хранить во временных таблицах или в таблицах в памяти, применять к тексту JSON предикаты безопасности на уровне строк и т. д. Если у вас есть чистые рабочие нагрузки JSON, в которых вы хотите использовать язык запросов, настроенный для обработки документов JSON, подумайте о Microsoft Azure [DocumentDB](https://azure.microsoft.com/services/documentdb/).  
  
 Рассмотрим несколько способов применения встроенной поддержки JSON в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## Возврат данных из таблицы SQL Server в формате JSON  
 Если у вас есть веб-служба, которая получает данные с уровня базы данных и возвращает их в формате JSON, либо платформы или библиотеки JavaScript, которые принимают данные в формате JSON, вы можете отформатировать результаты прямо в запросе SQL. Вместо написания кода или включения библиотеки для преобразования объектов результатов табличных запросов и последующей сериализации объектов в формате JSON вы можете передать форматирование в SQL Server с помощью FOR JSON.  
  
 Например, можно сформировать выходные данные JSON, совместимые со спецификацией OData. Веб-служба ожидает запрос и ответ в указанном ниже формате.  
  
-   Запрос: `/Northwind/Northwind.svc/Products(1)?$select=ProductID,ProductName`  
  
-   Ответ: `{"@odata.context":"http://services.odata.org/V4/Northwind/Northwind.svc/$metadata#Products(ProductID,ProductName)/$entity","ProductID":1,"ProductName":"Chai"}`  
  
 URL-адрес OData представляет запрос столбцов ProductID и ProductName для продукта с идентификатором 1. FOR JSON можно использовать для форматирования выходных данных для SQL Server.  
  
```tsql  
SELECT 'http://services.odata.org/V4/Northwind/Northwind.svc/$metadata#Products(ProductID,ProductName)/$entity' AS '@odata.context',   
ProductID, Name as ProductName   
FROM Production.Product  
WHERE ProductID = 1  
FOR JSON AUTO  
  
```  
  
 Результат этого запроса — текст JSON, который полностью соответствует спецификации OData. Форматирование и экранирование выполняются SQL Server. SQL Server может выдать результаты запроса в любом формате, таком как OData JSON или GeoJSON. См. статью [Возврат пространственных данных в формате GeoJSON](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/01/05/returning-spatial-data-in-geojson-format-part-1).  
  
## Анализ данных JSON с помощью запросов SQL  
 Если вам нужно отфильтровать или вычислить данные JSON для целей отчетности, JSON можно преобразовать в реляционный формат с помощью OPENJSON. Затем подготовьте отчеты, используя стандартный [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
```tsql  
SELECT Tab.Id, SalesOrderJsonData.Customer, SalesOrderJsonData.Date  
FROM   SalesOrderRecord AS Tab  
         CROSS APPLY  
    OPENJSON (Tab.json, N'$.Orders.OrdersArray')  
          WITH (  
             Number   varchar(200) N'$.Order.Number',   
             Date     datetime     N'$.Order.Date',  
             Customer varchar(200) N'$.AccountNumber',   
             Quantity int          N'$.Item.Quantity'  
          )  
 AS SalesOrderJsonData  
WHERE JSON_VALUE(Tab.json, '$.Status') = N'Closed'  
ORDER BY JSON_VALUE(Tab.json, '$.Group'), Tab.DateModified  
  
```  
  
 В одном и том же запросе можно использовать стандартные столбцы таблицы и значения из текста JSON. Для повышения эффективности запроса можно добавить индексы в выражение JSON_VALUE(Tab.json, '$.Status').  
  
## Импорт данных JSON в таблицы SQL Server  
 Если требуется загрузка данных JSON из внешней службы в SQL Server, можно импортировать данные в SQL Server с помощью OPENJSON вместо того, чтобы использовать синтаксический анализ данных на уровне приложения.  
  
```tsql  
INSERT INTO SalesReport  
SELECT SalesOrderJsonData.*  
FROM OPENJSON (@jsonVariable, N'$.Orders.OrdersArray')  
          WITH (  
             Number   varchar(200) N'$.Order.Number',   
             Date     datetime     N'$.Order.Date',  
             Customer varchar(200) N'$.AccountNumber',   
             Quantity int          N'$.Item.Quantity'  
          )  
 AS SalesOrderJsonData;  
  
```  
  
 Содержимое переменной JSON может быть предоставлено какой-либо внешней службой REST, прислано в виде параметра из какой-либо платформы JavaScript на стороне клиента или загружено из внешних файлов. Результаты можно легко вставить, обновить или объединить из текста JSON в таблицу SQL Server. Дополнительные сведения об этом сценарии см. в статье [Импорт данных JSON в SQL Server](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2015/09/22/openjson-the-easiest-way-to-import-json-text-into-table/), [Вставка документов JSON в SQL Server 2016](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/03/upsert-json-documents-in-sql-server-2016)и [Загрузка данных GeoJSON в SQL Server 2016](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/01/05/loading-geojson-data-into-sql-server/).  
  
## Загрузка файлов JSON в SQL Server  
 Сведения, которые хранятся в файлах, можно отформатировать как стандартный JSON или JSON с разбивкой на строки. SQL Server может импортировать содержимое файлов JSON, проанализировать его с помощью функций OPENJSON или JSON_VALUE и загрузить их в таблицы.  
  
 Если файлы JSON хранятся в локальных файлах, на общих сетевых дисках или в хранилище файлов Azure, доступном для SQL Server, данные JSON можно загрузить в SQL Server с помощью массового импорта. Дополнительные сведения об этом сценарии см. в статье [Импорт файлов JSON в SQL Server с помощью функции OPENROWSET (BULK)](http://blogs.msdn.com/b/sqlserverstorageengine/archive/2015/10/07/importing-json-files-into-sql-server-using-openrowset-bulk.aspx).  
  
 Если файлы JSON с разбивкой на строки хранятся в хранилище BLOB-объектов Azure или в файловой системе Hadoop, вы можете загрузить текст JSON с помощью Polybase, проанализировать его в коде Transact-SQL и загрузить в таблицы.  
  
## Проверка встроенной поддержки JSON  
 **Проверка встроенной поддержки JSON с образцом базы данных AdventureWorks.** Чтобы получить образец базы данных AdventureWorks, скачайте по крайней мере файл базы данных и примеры сценариев [здесь](https://www.microsoft.com/en-us/download/details.aspx?id=49502). После восстановления образца базы данных в экземпляре SQL Server 2016 распакуйте файлы образца и откройте файл JSON Sample Queries procedures views and indexes.sql в папке JSON. Выполните сценарии в этом файле, чтобы переформатировать некоторые данные как данные JSON, запустите образцы запросов и отчеты по данным JSON, индексируйте данные JSON, а затем импортируйте и экспортируйте JSON.  
  
 Вот, что делать с помощью скриптов, включенных в файл.  
  
1.  Выполнить денормализацию существующей схемы для создания столбцов данных JSON.  
  
    1.  Сохраните данные из SalesReasons, SalesOrderDetails, SalesPerson, Customer и других таблиц, которые содержат сведения, относящиеся к заказам на продажу, в столбцы JSON таблицы SalesOrder_json.  
  
    2.  Сохраните данные из таблиц EmailAddresses/PersonPhone в таблицу Person_json как массив объектов JSON.  
  
2.  Создайте процедуры и представления для запроса данных JSON.  
  
3.  Проиндексируйте данные JSON: создайте индексы свойств JSON и полнотекстовые индексы.  
  
4.  Выполните импорт и экспорт JSON: создайте и выполните процедуры для экспорта содержимого таблиц Person и SalesOrder как результатов JSON, а затем импортируйте и обновите таблицы Person и SalesOrder, используя входные данные JSON.  
  
5.  Выполните примеры запросов: выполните несколько запросов, вызывающих хранимые процедуры и представления, которые были созданы при выполнении шагов 2 и 4.  
  
6.  Очистите скрипты: не выполняйте это действие, если хотите оставить хранимые процедуры и представления, которые были созданы при выполнении шагов 2 и 4.  
  
## Дополнительные сведения о встроенной поддержке JSON  
  
### Разделы этой статьи  
 [Форматирование результатов запроса как JSON с помощью предложения FOR JSON (SQL Server)](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)  
 Предложение FOR JSON позволяет делегировать форматирование выходных данных JSON из клиентских приложений в SQL Server.  
  
 [Преобразование данных JSON в строки и столбцы с помощью функции OPENJSON (SQL Server)](../../relational-databases/json/convert-json-data-to-rows-and-columns-with-openjson-sql-server.md)  
 Предложение OPENJSON позволяет импортировать данные JSON в SQL Server или преобразовать данные JSON в реляционный формат для приложения или службы, которая сейчас не может использовать JSON напрямую, например для служб интеграции SQL Server.  
  
 [Проверка, построение запросов и изменение данных JSON с помощью встроенных функций (SQL Server)](../../relational-databases/json/validate-query-and-change-json-data-with-built-in-functions-sql-server.md)  
 Встроенные функции можно использовать для проверки текста JSON и получения скалярного значения, объекта или массива.  
  
 [Выражения пути JSON (SQL Server)](../../relational-databases/json/json-path-expressions-sql-server.md)  
 Выражение пути позволяет указать текст JSON, который нужно использовать.  
  
 [Индексирование данных JSON](../../relational-databases/json/index-json-data.md)  
 Вычисляемые столбцы можно использовать для создания индексов с учетом сортировки на основе свойств в документах JSON.  
  
 [Часто задаваемые вопросы о JSON в SQL Server](../Topic/Frequently%20Asked%20Questions%20about%20JSON%20in%20SQL%20Server.md)  
 Ответы на некоторые распространенные вопросы о встроенной поддержке JSON в SQL Server.  
  
### Публикации блога Майкрософт  
  
-   [Публикации блога Йована Поповича (Jovan Popovic), руководителя программы Microsoft](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)  
  
### Справочные разделы  
  
-   [Предложение FOR (Transact-SQL)](../Topic/FOR%20Clause%20\(Transact-SQL\).md) (FOR JSON)  
  
-   [OPENJSON (Transact-SQL)](../../t-sql/functions/openjson-transact-sql.md)  
  
-   [Функции JSON (Transact-SQL)](../../t-sql/functions/json-functions-transact-sql.md)  
  
    -   [ISJSON (Transact-SQL)](../../t-sql/functions/isjson-transact-sql.md)  
  
    -   [JSON_VALUE (Transact-SQL)](../../t-sql/functions/json-value-transact-sql.md)  
  
    -   [JSON_QUERY (Transact-SQL)](../../t-sql/functions/json-query-transact-sql.md)  
  
    -   [JSON_MODIFY (Transact-SQL)](../../t-sql/functions/json-modify-transact-sql.md)  
  
  