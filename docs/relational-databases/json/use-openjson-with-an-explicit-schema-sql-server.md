---
title: "Использование функции OPENJSON с явной схемой (SQL Server) | Microsoft Docs"
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
  - "OPENJSON с явной схемой"
ms.assetid: 9c1c3bfb-e1ad-4659-b94f-722b0848d5a2
caps.latest.revision: 13
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 12
---
# Использование функции OPENJSON с явной схемой (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  **OPENJSON** можно использовать с явной схемой, чтобы вернуть таблицу, отформатированную, как указано в предложении WITH.  
  
 Ниже приведены несколько примеров использования **OPENJSON** с явной схемой. Дополнительные сведения и примеры см. в статье [OPENJSON (Transact-SQL)](../../t-sql/functions/openjson-transact-sql.md).  
  
## Пример использования предложения WITH для форматирования выходных данных  
 Следующий запрос возвращает результаты, показанные в таблице ниже. Обратите внимание, что при использовании предложения AS JSON значения возвращаются в виде объектов JSON, а не скалярных значений в col5 и array_element.  
  
```tsql  
DECLARE @json NVARCHAR(MAX) =
N'{"someObject":   
   {"someArray":  
     [  
         {"k1": 11, "k2": null, "k3": "text"},  
         {"k1": 21, "k2": "text2", "k4": { "data": "text4" }},  
         {"k1": 31, "k2": 32},  
         {"k1": 41, "k2": null, "k4": { "data": false }}     
      ]  
   }  
}'  
  
SELECT * FROM  
OPENJSON(@json, N'lax $.someObject.someArray')  
WITH ( k1 int,   
       k2 varchar(100),  
       col3 varchar(6) N'$.k3',  
       col4 varchar(10) N'lax $.k4.data',  
       col5 nvarchar(MAX) N'lax $.k4' AS JSON, 
       array_element nvarchar(MAX) N'$' AS JSON  
)  
```  
  
 **Результаты**  
  
|k1|k2|col3|col4|col5|array_element|  
|--------|--------|----------|----------|----------|--------------------|  
|11|*NULL*|"text"|*NULL*|*NULL*|{"k1": 11, "k2": null, "k3": "text"}|  
|21|"text2"|*NULL*|"text4"|{ "data": "text4" }|{"k1": true, "k2": "text2", "k4": { "data": "text4" } }|  
|31|"32"|*NULL*|*NULL*|*NULL*|{"k1": 31, "k2": 32 }|  
|41|*NULL*|*NULL*|false|{ "data": false }|{"k1": 41, "k2": null,       "k4": { "data": false }    }|  
  
## Пример загрузки объекта JSON в таблицу [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
 В следующем примере весь объект JSON загружается в таблицу [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```tsql  
declare @json nvarchar(max) = '{  
 "id" : 2,  
 "firstName": "John",  
 "lastName": "Smith",  
 "isAlive": true,  
 "age": 25,  
 "dateOfBirth": "2015-03-25T12:00:00",  
 "spouse": null  
 }';  
  
 INSERT INTO Person  
 SELECT *   
 FROM OPENJSON(@json)  
 WITH (id int,  
       firstName nvarchar(50), lastName nvarchar(50),   
       isAlive bit, age int,  
       dateOfBirth datetime2, spouse nvarchar(50))  
  
```  
  
## См. также:  
 [OPENJSON (Transact-SQL)](../../t-sql/functions/openjson-transact-sql.md)  
  
  