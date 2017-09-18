---
title: "Команда потоки | Документы Microsoft"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- command streams [ADO]
- streams [ADO], command
ms.assetid: 0ac09dbe-2665-411e-8fbb-d1efe6c777be
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1be2cc9528e62e548feb242b06686ad50a1753c8
ms.contentlocale: ru-ru
ms.lasthandoff: 09/09/2017

---
# <a name="command-streams"></a>Команда потоков
ADO всегда поддерживается ввода команды в строку формата, заданного в **CommandText** свойство. Кроме того, при использовании ADO 2.7 или более поздней версии, также можно потока данных для ввода команды путем назначения потока **CommandStream** свойство. Можно назначить ADO **поток** объекта или любым объектом, поддерживающим COM **IStream** интерфейса.  
  
 Содержимого потока команды просто передается от ADO с поставщиком, поэтому поставщик должен поддерживать ввода команды потоком для работы этой функции. Например SQL Server поддерживает запросы в виде XML-шаблоны или расширения OpenXML языка Transact-SQL.  
  
 Поскольку сведения о потоке, должна интерпретироваться поставщиком, необходимо указать диалект команды, задав **диалект** свойство. Значение **диалект** является строка, содержащая GUID, который определяется поставщиком. Дополнительные сведения о допустимых значениях для **диалект** поддерживается поставщиком, обратитесь к документации поставщика.  
  
## <a name="xml-template-query-example"></a>Пример запросов XML-файла шаблона  
 Следующий пример написан на языке VBScript в базу данных "Борей".  
  
 Во-первых, инициализации и запуска **поток** объект, который будет использоваться для хранения в поток запроса:  
  
```  
Dim adoStreamQuery  
Set adoStreamQuery = Server.CreateObject("ADODB.Stream")  
adoStreamQuery.Open  
```  
  
 Содержимое потока запроса будет шаблона XML-запрос.  
  
 Шаблон запроса требует ссылки на пространства имен XML с sql: префикс \<sql:query > тег. Инструкции SQL SELECT включается как содержимое XML-шаблон и присваивается переменной строки следующим образом:  
  
```  
sQuery = "<ROOT xmlns:sql='urn:schemas-microsoft-com:xml-sql'>  
<sql:query> SELECT * FROM PRODUCTS ORDER BY PRODUCTNAME </sql:query>  
</ROOT>"  
```  
  
 Затем напишите строку в поток:  
  
```  
adoStreamQuery.WriteText sQuery, adWriteChar  
adoStreamQuery.Position = 0  
```  
  
 Назначьте adoStreamQuery для **CommandStream** свойство ADO **команда** объекта:  
  
```  
Dim adoCmd  
Set adoCmd  = Server.CreateObject("ADODB.Command"")  
adoCmd.CommandStream = adoStreamQuery  
```  
  
 Укажите командный язык **диалект**, которое указывает, как интерпретировать поток команды SQL Server поставщик OLE DB. Диалект, указанный GUID поставщика:  
  
```  
adoCmd.Dialect = "{5D531CB2-E6Ed-11D2-B252-00C04F681B71}"  
```  
  
 Наконец, выполните запрос и возвращают результаты **записей** объекта:  
  
```  
Set objRS = adoCmd.Execute  
```