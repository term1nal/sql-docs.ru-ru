---
title: "Столбцы с именем | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-xml"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "имена [SQL Server], столбцы с"
ms.assetid: c994e089-4cfc-4e9b-b7fc-e74f6014b51a
caps.latest.revision: 8
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 8
---
# Столбцы с именем
  Ниже приведены условия, при которых столбцы наборов строк с соответствующим именем сопоставляются с итоговым XML-документом с учетом регистра:  
  
-   имя столбца начинается с символа @;  
  
-   имя столбца не начинается с символа @;  
  
-   имя столбца не начинается с символа @ и содержит косую черту (/);  
  
-   несколько столбцов имеют одинаковый префикс;  
  
-   один из столбцов имеет другое имя.  
  
## Имя столбца начинается с символа @  
 Если имя столбца начинается с символа @ и не содержит косую черту (/), создается атрибут элемента <`row`>, имеющий соответствующее значение столбца. Например, следующий запрос возвращает набор строк с двумя столбцами (@PmId, Name). В итоговом XML-документе атрибут **PmId** добавляется к соответствующему элементу <`row`>, и ему присваивается значение столбца ProductModelID.  
  
```  
  
SELECT ProductModelID as "@PmId",  
       Name  
FROM Production.ProductModel  
WHERE ProductModelID=7  
FOR XML PATH   
go  
  
```  
  
 Результат:  
  
```  
<row PmId="7">  
  <Name>HL Touring Frame</Name>  
</row>  
```  
  
 Обратите внимание, что на одном уровне атрибуты должны располагаться перед любыми другими типами узлов, например, перед узлами элементов и текстовыми узлами. Следующий запрос возвращает ошибку:  
  
```  
SELECT Name,  
       ProductModelID as "@PmId"  
FROM Production.ProductModel  
WHERE ProductModelID=7  
FOR XML PATH   
go  
```  
  
## Имя столбца не начинается с символа @  
 Если имя столбца, начинающееся с символа @, не является одной из XPath-функций проверки узла и не содержит косую черту (/), по умолчанию создается элемент XML <`row`>, который представляет собой вложенный элемент элемента строки.  
  
 В результате следующего запроса указывается имя столбца. Дочерний элемент <`result`> добавляется к элементу <`row`>.  
  
```  
SELECT 2+2 as result  
for xml PATH  
```  
  
 Результат:  
  
```  
<row>  
  <result>4</result>  
</row>  
```  
  
 Следующий запрос указывает имя столбца ManuWorkCenterInformation для XML-данных, возвращенных запросом XQuery, указанным по отношению к столбцу Instructions типа **xml** . Элемент <`ManuWorkCenterInformation`> добавляется в качестве дочернего к элементу <`row`>.  
  
```  
SELECT   
       ProductModelID,  
       Name,  
       Instructions.query('declare namespace MI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
                /MI:root/MI:Location   
              ') as ManuWorkCenterInformation  
FROM Production.ProductModel  
WHERE ProductModelID=7  
FOR XML PATH   
go  
```  
  
 Результат:  
  
```  
<row>  
  <ProductModelID>7</ProductModelID>  
  <Name>HL Touring Frame</Name>  
  <ManuWorkCenterInformation>  
    <MI:Location ...LocationID="10" ...></MI:Location>  
    <MI:Location ...LocationID="20" ...></MI:Location>  
     ...  
  </ManuWorkCenterInformation>  
</row>  
```  
  
## Имя столбца не начинается с символа @ и содержит косую черту (/)  
 Если имя столбца не начинается с символа @, но содержит косую черту (/), оно является признаком иерархии XML. Например, если столбец имеет имя "Имя1/Имя2/Имя3.../Имя***n***", каждое Имя***i*** представляет имя элемента, вложенного в элемент текущей строки (для i=1) или расположенного под элементом Имя***i-1***. Если Имя***n*** начинается с символа @, оно сопоставляется с атрибутом элемента Имя***n-1***.  
  
 Например, следующий запрос возвращает идентификатор работника и имя, представленное сложным элементом EmpName, который включает в себя имя, отчество и фамилию работника.  
  
```  
SELECT EmployeeID "@EmpID",   
       FirstName  "EmpName/First",   
       MiddleName "EmpName/Middle",   
       LastName   "EmpName/Last"  
FROM   HumanResources.Employee E, Person.Contact C  
WHERE  E.EmployeeID = C.ContactID  
AND    E.EmployeeID=1  
FOR XML PATH  
```  
  
 Имена столбцов используются в качестве пути при построении XML-документа в режиме PATH. Имя столбца, содержащего значения идентификатора работника, начинается с символа @. Поэтому атрибут **EmpID** добавляется к элементу <`row`>. Имена всех других столбцов содержат символ косой черты (/), являющийся признаком иерархии. В итоговом XML-документе будет присутствовать дочерний элемент <`EmpName`> внутри элемента <`row`>, а элемент <`EmpName`> будет в свою очередь содержать дочерние элементы <`First`>, <`Middle`> и <`Last`>.  
  
```  
<row EmpID="1">  
  <EmpName>  
    <First>Gustavo</First>  
    <Last>Achong</Last>  
  </EmpName>  
</row>  
```  
  
 Отчество работника имеет значение NULL, которое по умолчанию сопоставляется с отсутствием элемента или атрибута. Если необходимо сформировать элементы для значений NULL, укажите директиву ELEMENTS с ключевым словом XSINIL, как показано в данном запросе.  
  
```  
SELECT EmployeeID "@EmpID",   
       FirstName  "EmpName/First",   
       MiddleName "EmpName/Middle",   
       LastName   "EmpName/Last"  
FROM   HumanResources.Employee E, Person.Contact C  
WHERE  E.EmployeeID = C.ContactID  
AND    E.EmployeeID=1  
FOR XML PATH, ELEMENTS XSINIL  
```  
  
 Результат:  
  
```  
<row xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"   
      EmpID="1">  
  <EmpName>  
    <First>Gustavo</First>  
    <Middle xsi:nil="true" />  
    <Last>Achong</Last>  
  </EmpName>  
</row>  
```  
  
 По умолчанию в режиме PATH формируется элементно-ориентированный XML-документ. Поэтому указание директивы ELEMENTS в режиме PATH не имеет никакого смысла. Однако как показано в предыдущем примере, директива ELEMENTS с ключевым словом XSINIL может быть полезна при формировании элементов для значений NULL.  
  
 Следующий запрос кроме идентификатора и имени возвращает еще и адрес работника. В соответствии с путем, указанным в именах столбцов адресов, дочерний элемент <`Address`> добавляется к элементу <`row`>, а подробные сведения об адресе добавляются в качестве дочерних элементов к элементу <`Address`>.  
  
```  
SELECT EmployeeID   "@EmpID",   
       FirstName    "EmpName/First",   
       MiddleName   "EmpName/Middle",   
       LastName     "EmpName/Last",  
       AddressLine1 "Address/AddrLine1",  
       AddressLine2 "Address/AddrLIne2",  
       City         "Address/City"  
FROM   HumanResources.Employee E, Person.Contact C, Person.Address A  
WHERE  E.EmployeeID = C.ContactID  
AND    E.AddressID = A.AddressID  
AND    E.EmployeeID=1  
FOR XML PATH  
```  
  
 Результат:  
  
```  
<row EmpID="1">  
  <EmpName>  
    <First>Gustavo</First>  
    <Last>Achong</Last>  
  </EmpName>  
  <Address>  
    <AddrLine1>7726 Driftwood Drive</AddrLine1>  
    <City>Monroe</City>  
  </Address>  
</row>  
```  
  
## Несколько столбцов имеют одинаковый префикс пути  
 Если несколько последовательных столбцов имеют одинаковый префикс пути, производится их группировка под одним именем. Если используется одно и то же пространство имен, но разные префиксы пространства имен, путь считается отличающимся. В предыдущем запросе столбцы FirstName, MiddleName и LastName имеют один и тот же префикс EmpName. Поэтому они добавляются как дочерние элементы элемента <`EmpName`>. Это справедливо также для случая создания элемента <`Address`>, показанного в предыдущем примере.  
  
## Один из столбцов имеет другое имя  
 Если между столбцами встречается столбец с другим именем, группирование будет нарушено, как это показано в следующем измененном запросе. Добавляя столбцы с адресом между столбцами FirstName и MiddleName, данный запрос нарушает группирование столбцов FirstName, MiddleName и LastName, указанное в предыдущем запросе.  
  
```  
SELECT EmployeeID "@EmpID",   
       FirstName "EmpName/First",   
       AddressLine1 "Address/AddrLine1",  
       AddressLine2 "Address/AddrLIne2",  
       City "Address/City",  
       MiddleName "EmpName/Middle",   
       LastName "EmpName/Last"  
FROM   HumanResources.EmployeeAddress E, Person.Contact C, Person.Address A  
WHERE  E.EmployeeID = C.ContactID  
AND    E.AddressID = A.AddressID  
AND    E.EmployeeID=1  
FOR XML PATH  
```  
  
 В результате запрос создает два элемента <`EmpName`>. Первый элемент <`EmpName`> имеет дочерний элемент <`FirstName`>, а второй элемент <`EmpName`> имеет дочерние элементы <`MiddleName`> и <`LastName`>.  
  
 Результат:  
  
```  
<row EmpID="1">  
  <EmpName>  
    <First>Gustavo</First>  
  </EmpName>  
  <Address>  
    <AddrLine1>7726 Driftwood Drive</AddrLine1>  
    <City>Monroe</City>  
  </Address>  
  <EmpName>  
    <Last>Achong</Last>  
  </EmpName>  
</row>  
```  
  
## См. также:  
 [Использование режима PATH совместно с FOR XML](../../relational-databases/xml/use-path-mode-with-for-xml.md)  
  
  