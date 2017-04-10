---
title: "Использование OPENJSON со схемой по умолчанию (SQL Server) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "06/02/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-json"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "OPENJSON, со схемой по умолчанию"
ms.assetid: 8e28a8f8-71a8-4c25-96b8-0bbedc6f41c4
caps.latest.revision: 11
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 10
---
# Использование OPENJSON со схемой по умолчанию (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Использование **OPENJSON** со схемой по умолчанию возвращает таблицу, содержащую одну строку для каждого свойства объекта или для каждого элемента в массиве.  
  
 Ниже приведены несколько примеров использования **OPENJSON** со схемой по умолчанию. Дополнительные сведения и другие примеры см. в разделе [OPENJSON (Transact-SQL)](../../t-sql/functions/openjson-transact-sql.md).  
  
## Пример. Возвращение каждого свойства объекта  
 **Запрос**  
  
```tsql  
SELECT * FROM OPENJSON('{"name":"John","surname":"Doe","age":45}')  
```  
  
 **Результаты**  
  
|Key|Значение|  
|---------|-----------|  
|имя|Джон|  
|surname|Doe|  
|age|45|  
  
## Пример. Возвращение каждого элемента массива  
 **Запрос**  
  
```tsql  
SELECT [key], value FROM OPENJSON('["en-GB", "en-UK","de-AT","es-AR","sr-Cyrl"]')  
```  
  
 **Результаты**  
  
|Key|Значение|  
|---------|-----------|  
|0|en-GB|  
|1|en-UK|  
|2|de-AT|  
|3|es-AR|  
|4|sr-Cyrl|  
  
## Пример. Преобразование JSON во временную таблицу  
 Следующий запрос возвращает все свойства объекта **info** .  
  
```tsql  
SET @json = N'{  
    "info":{    
      "type":1,  
      "address":{    
        "town":"Bristol",  
        "county":"Avon",  
        "country":"England"  
      },  
      "tags":["Sport", "Water polo"]  
   },  
   "type":"Basic"  
}'  
  
SELECT * FROM OPENJSON(@json, N'lax $.info')  
```  
  
 **Результаты**  
  
|Key|Значение|Тип|  
|---------|-----------|----------|  
|type|1|0|  
|address|{ "town":"Bristol", "county":"Avon", "country":"England" }|5|  
|tags|[ "Sport", "Water polo" ]|4|  
  
## Пример. Объединение реляционных данных и данных JSON  
 В следующем примере таблица SalesOrderHeader имеет текстовый столбец SalesReason, содержащий массив SalesOrderReasons в формате JSON. Объекты SalesOrderReasons содержат такие свойства, как "Manufacturer" и "Quality". Пример создает отчет, который соединяет каждую строку заказа на продажу со связанными причинами покупки, развернув массив JSON причин покупки, как если бы причины хранились в отдельной дочерней таблице.  
  
```tsql  
SELECT SalesOrderID, OrderDate, value AS Reason  
FROM Sales.SalesOrderHeader  
    CROSS APPLY OPENJSON (SalesReasons)  
  
```  
  
 В этом примере OPENJSON возвращает таблицу причин покупки, в которой причины отображаются как столбец значений. Оператор CROSS APPLY соединяет каждую строку заказа на продажу со строками, возвращенными функцией с табличным значением OPENJSON.  
  
## См. также:  
 [OPENJSON (Transact-SQL)](../../t-sql/functions/openjson-transact-sql.md)  
  
  