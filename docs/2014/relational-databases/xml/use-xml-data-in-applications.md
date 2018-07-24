---
title: Использование данных XML в приложениях | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- parameters [XML in SQL Server]
- XML [SQL Server], ADO
- columns [XML in SQL Server], ADO.NET
- ADO [XML in SQL Server]
- columns [XML in SQL Server], SQL Server Native Client
- xml data type [SQL Server], ADO
- SQLNCLI, XML
- xml data type [SQL Server], SQL Server Native Client
- SQL Server Native Client, XML
- ADO.NET [XML in SQL Server]
- XML [SQL Server], ADO.NET
- columns [XML in SQL Server], ADO
- xml data type [SQL Server], ADO.NET
- XML [SQL Server], SQL Server Native Client
ms.assetid: 5dabf7e0-c6df-451d-a070-4661f84607fd
caps.latest.revision: 26
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 13440d6941d05fd02c1c98c8a75d538adbf749de
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2018
ms.locfileid: "37293954"
---
# <a name="use-xml-data-in-applications"></a>Использование XML-данных в приложениях
  В этом разделе приведены параметры, доступные для работы с `xml` тип данных в приложении. Он содержит следующие сведения:  
  
-   Обработка XML в столбцах типа `xml` с помощью ADO и собственного клиента [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   Обработка XML в `xml` столбец типа с помощью ADO.NET  
  
-   Обработка типа `xml` в параметрах с помощью ADO.NET  
  
## <a name="handling-xml-from-an-xml-type-column-by-using-ado-and-sql-server-native-client"></a>Обработка XML в столбцах типа xml с помощью ADO и собственного клиента SQL Server  
 Чтобы при помощи компонентов MDAC получить доступ к типам и возможностям, появившимся в [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], в строке соединения ADO необходимо указать свойство инициализации, DataTypeCompatibility.  
  
 Например, в следующем примере Visual Basic Scripting Edition (VBScript) показаны результаты запросов `xml` столбца типа `Demographics`в `Sales.Store` таблицу `AdventureWorks2012` образца базы данных. В частности, запрос производит поиск значения столбца для строки, в которой значение `CustomerID` равно `3`.  
  
```  
Const DS = "MyServer"  
Const DB = "AdventureWorks2012"  
  
Set objConn = CreateObject("ADODB.Connection")  
Set objRs = CreateObject("ADODB.Recordset")  
  
CommandText = "SELECT Demographics" & _  
              " FROM Sales.Store" & _  
              " INNER JOIN Sales.Customer" & _  
              " ON Sales.Store.BusinessEntityID = sales.customer.StoreID" & _  
              " WHERE Sales.Customer.CustomerID = 3" & _  
              " OR Sales.Customer.CustomerID = 4"  
  
ConnectionString = "Provider=SQLNCLI11" & _  
                   ";Data Source=" & DS & _  
                   ";Initial Catalog=" & DB & _  
                   ";Integrated Security=SSPI;" & _  
                   "DataTypeCompatibility=80"  
  
'Connect to the data source.  
objConn.Open ConnectionString  
  
'Execute command through the connection and display  
Set objRs = objConn.Execute(CommandText)  
  
Dim rowcount  
rowcount = 0  
Do While Not objRs.EOF  
   rowcount = rowcount + 1  
   MsgBox "Row " & rowcount & _  
           vbCrLf & vbCrLf & objRs(0)  
   objRs.MoveNext  
Loop  
  
'Clean up.  
objRs.Close  
objConn.Close  
Set objRs = Nothing  
Set objConn = Nothing  
```  
  
 В этом примере показано, как настроить свойство совместимости типов данных. По умолчанию, при использовании собственного клиента [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] это свойство принимает значение 0. Если этому свойству присвоить значение 80, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] поставщик Native Client `xml` и столбцы определяемого пользователем типа отображаются как [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] типов данных. то есть DBTYPE_WSTR и DBTYPE_BYTES соответственно.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] должен быть установлен на клиентском компьютере, а в строке соединения он должен быть указан в качестве поставщика данных: "`Provider=SQLNCLI11;...`".  
  
#### <a name="to-test-this-example"></a>Проверка этого примера  
  
1.  Убедитесь, что на компьютере клиента установлен собственный клиент [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] и доступны компоненты MDAC 2.6.0 или более поздней версии.  
  
     Дополнительные сведения см. в статье [Программирование SQL Server Native Client](../native-client/sql-server-native-client-programming.md).  
  
2.  Убедитесь, что образец базы данных [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] установлен в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
     Для этого примера требуется образец базы данных [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
3.  Скопируйте код, приведенный ранее в этом подразделе, и вставьте его в текстовый редактор или редактор кода. Сохраните файл под именем HandlingXmlDataType.vbs.  
  
4.  Измените скрипт так, как необходимо для вашей установки [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , и сохраните изменения.  
  
     В частности, вместо `MyServer` необходимо указать либо `(local)` , либо действительное имя сервера, на котором установлен [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
5.  Запустите файл скрипта HandlingXmlDataType.vbs на выполнение.  
  
 Результат должен примерно соответствовать следующему:  
  
```  
Row 1  
  
<StoreSurvey xmlns="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/StoreSurvey">  
  <AnnualSales>1500000</AnnualSales>  
  <AnnualRevenue>150000</AnnualRevenue>  
  <BankName>Primary International</BankName>  
  <BusinessType>OS</BusinessType>  
  <YearOpened>1974</YearOpened>  
  <Specialty>Road</Specialty>  
  <SquareFeet>38000</SquareFeet>  
  <Brands>3</Brands>  
  <Internet>DSL</Internet>  
  <NumberEmployees>40</NumberEmployees>  
</StoreSurvey>  
  
Row 2  
  
<StoreSurvey xmlns="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/StoreSurvey">  
  <AnnualSales>300000</AnnualSales>  
  <AnnualRevenue>30000</AnnualRevenue>  
  <BankName>United Security</BankName>  
  <BusinessType>BM</BusinessType>  
  <YearOpened>1976</YearOpened>  
  <Specialty>Road</Specialty>  
  <SquareFeet>6000</SquareFeet>  
  <Brands>2</Brands>  
  <Internet>DSL</Internet>  
  <NumberEmployees>5</NumberEmployees>  
</StoreSurvey>  
```  
  
## <a name="handling-xml-from-an-xml-type-column-by-using-adonet"></a>Обработка XML-данных в столбцах типа xml с помощью ADO.NET  
 Для работы со `xml` столбец типа данных с помощью ADO.NET и [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] можно использовать стандартное поведение `SqlCommand` класса. Например `xml` данные столбца типа и его значения можно получить в одном, так и любые столбцы SQL извлекаются с помощью `SqlDataReader`. Тем не менее если вы хотите работать с содержимым `xml` столбец типа данных как XML, сначала необходимо связать содержимое с `XmlReader` типа.  
  
 Дополнительные сведения и примеры кода см. в разделе «Значения XML-столбцов в модуле чтения данных» в документации по пакету [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnlong](../../includes/dnprdnlong-md.md)] SDK.  
  
## <a name="handling-an-xml-type-column-in-parameters-by-using-adonet"></a>Обработка столбцов типа xml в параметрах с помощью ADO.NET  
 Для обработки XML-данных, переданных в качестве параметра в ADO.NET и [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], значение можно представить в виде экземпляра данных типа `SqlXml`. Специальная обработка не производится, поскольку `xml` типа данных столбцов в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] может принимать значения параметров в так же, как другие столбцы и типы данных, такие как `string` или `integer`.  
  
 Дополнительные сведения и примеры кода см. в разделе «XML-значения в качестве параметров» в документации по пакету [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnlong](../../includes/dnprdnlong-md.md)] SDK.  
  
## <a name="see-also"></a>См. также  
 [Данные XML (SQL Server)](xml-data-sql-server.md)  
  
  