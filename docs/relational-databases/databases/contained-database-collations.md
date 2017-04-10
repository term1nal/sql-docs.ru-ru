---
title: "Параметры сортировки автономной базы данных | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "автономная база данных, параметры сортировки"
ms.assetid: 4b44f6b9-2359-452f-8bb1-5520f2528483
caps.latest.revision: 12
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 12
---
# Параметры сортировки автономной базы данных
  На порядок сортировки и семантику сравнения текстовых данных влияют различные свойства, в том числе учет регистра, учет диакритических знаков и используемый базовый язык. Эти характеристики выражаются в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] посредством выбора параметров сортировки для данных. Подробное обсуждение параметров сортировки см. в разделе [Поддержка параметров сортировки и Юникода](../../relational-databases/collations/collation-and-unicode-support.md).  
  
 Параметры сортировки применяются не только к данным, хранящимся в пользовательских таблицах, но и ко всему тексту, обрабатываемому [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], включая метаданные, временные объекты, имена переменных и т. д. Обработка таких объектов в автономных и неавтономных базах данных различается. Это изменение коснется небольшого числа пользователей и обеспечит независимость и единообразие экземпляров. При этом возможны некоторые затруднения, а также проблемы в сеансах, которые обращаются и к автономным и к неавтономным базам данных.  
  
 В этом разделе поясняется суть изменения и рассматриваются области, в которых оно может вызвать проблемы.  
  
## Неавтономные базы данных  
 Все базы данных имеют параметры сортировки по умолчанию (их можно задать во время создания или изменения базы данных). Эти параметры сортировки используются для всех метаданных в базе данных, а также по умолчанию для всех строковых столбцов в базе данных. Пользователи могут выбрать другие параметры сортировки для любого столбца с помощью предложения **COLLATE** .  
  
### Пример 1  
 Например, для работы в Пекине можно использовать параметры сортировки китайского языка:  
  
```tsql  
ALTER DATABASE MyDB COLLATE Chinese_Simplified_Pinyin_100_CI_AS;  
```  
  
 Теперь для создаваемого столбца по умолчанию будут применяться параметры сортировки китайского языка, но в случае необходимости можно выбрать другие параметры.  
  
```tsql  
CREATE TABLE MyTable  
      (mycolumn1 nvarchar,  
      mycolumn2 nvarchar COLLATE Frisian_100_CS_AS);  
GO  
SELECT name, collation_name  
FROM sys.columns  
WHERE name LIKE 'mycolumn%' ;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```tsql  
name            collation_name  
--------------- ----------------------------------  
mycolumn1       Chinese_Simplified_Pinyin_100_CI_AS  
mycolumn2       Frisian_100_CS_AS  
```  
  
 Это выглядит довольно простым, однако возникают некоторые проблемы. Поскольку параметры сортировки для столбца зависят от базы данных, в которой создается таблица, возникают проблемы с использованием временных таблиц, которые хранятся в базе данных **tempdb**. Параметры сортировки **tempdb** обычно совпадают с параметрами сортировки для экземпляра, которые не обязательно совпадают с параметрами сортировки базы данных.  
  
### Пример 2  
 Например, пусть база данных с китайскими параметрами сортировки (упомянутая выше) используется в экземпляре с параметрами сортировки **Latin1_General**:  
  
```tsql  
CREATE TABLE T1 (T1_txt nvarchar(max)) ;  
GO  
CREATE TABLE #T2 (T2_txt nvarchar(max)) ;  
GO  
```  
  
 На первый взгляд кажется, что две таблицы имеют одинаковую схему, однако из-за различия в параметрах сортировки баз данных значения оказываются несовместимыми.  
  
```  
SELECT T1_txt, T2_txt  
FROM T1   
JOIN #T2   
    ON T1.T1_txt = #T2.T2_txt  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 Сообщение 468, уровень 16, состояние 9, строка 2  
  
 Не удается разрешить конфликт параметров сортировки Latin1_General_100_CI_AS_KS_WS_SC и Chinese_Simplified_Pinyin_100_CI_AS в операции равенства.  
  
 Чтобы исправить эту проблему, можно явно задать параметры сортировки временной таблицы. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] эта задача несколько упрощается благодаря наличию ключевого слова **DATABASE_DEFAULT** для предложения **COLLATE**.  
  
```tsql  
CREATE TABLE T1 (T1_txt nvarchar(max)) ;  
GO  
CREATE TABLE #T2 (T2_txt nvarchar(max) COLLATE DATABASE_DEFAULT);  
GO  
SELECT T1_txt, T2_txt  
FROM T1   
JOIN #T2   
    ON T1.T1_txt = #T2.T2_txt ;  
```  
  
 Теперь операция работает без ошибки.  
  
 Различия параметров сортировки также проявляются в обработке переменных. Рассмотрим следующую функцию:  
  
```  
CREATE FUNCTION f(@x INT) RETURNS INT  
AS BEGIN   
      DECLARE @I INT = 1  
      DECLARE @İ INT = 2  
      RETURN @x * @i  
END;  
```  
  
 Это довольно необычная функция. В параметрах сортировки с учетом регистра конструкцию @i в предложении возврата нельзя привязать к @I или @İ. В параметрах сортировки Latin1_General без учета регистра конструкция @i привязывается к @I и функция возвращает значение 1. При этом в параметрах сортировки для турецкого языка без учета регистра конструкция @i привязывается к @İ и функция возвращает значение 2. Это может негативно отразиться на базе данных, которая перемещается между экземплярами с различными параметрами сортировки.  
  
## Автономные базы данных  
 Поскольку задачей проектирования автономных баз данных является обеспечение их независимости, необходимо исключить зависимость от параметров сортировки экземпляра и базы данных **tempdb**. Для этого в автономных базах данных реализовано основное понятие параметров сортировки каталога. Параметры сортировки каталога используются для метаданных системы и временных объектов. Далее даны подробности.  
  
 В автономной базе данных используются параметры сортировки каталога **Latin1_General_100_CI_AS_WS_KS_SC**. Эти параметры сортировки одинаковы для всех автономных баз данных во всех экземплярах [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], и их нельзя изменить.  
  
 Параметры сортировки базы данных сохраняются, но используются только в качестве параметров сортировки по умолчанию для пользовательских данных. По умолчанию параметры сортировки базы данных совпадают с параметрами сортировки базы данных model, однако пользователь может их изменить командой **CREATE** или **ALTER DATABASE**, как и в случае с неавтономными базами данных.  
  
 Новое ключевое слово **CATALOG_DEFAULT** доступно в предложении **COLLATE**. Оно служит ярлыком для текущих параметров сортировки метаданных и в автономных и в неавтономных базах данных. Это значит, что в неавтономной базе данных конструкция **CATALOG_DEFAULT** возвращает текущие параметры сортировки базы данных, поскольку в метаданных применяются параметры сортировки базы данных. В автономной базе данных эти два значения могут различаться, поскольку пользователь может изменить параметры сортировки базы данных так, чтобы они отличались от параметров сортировки каталога.  
  
 В данной таблице представлен порядок обработки различных объектов в автономных и неавтономных базах данных.  
  
||||  
|-|-|-|  
|**Элемент**|**Неавтономная база данных**|**Автономная база данных**|  
|Пользовательские данные (по умолчанию)|DATABASE_DEFAULT|DATABASE_DEFAULT|  
|Временные данные (по умолчанию)|Параметры сортировки TempDB|DATABASE_DEFAULT|  
|Метаданные|DATABASE_DEFAULT / CATALOG_DEFAULT|CATALOG_DEFAULT|  
|Временные метаданные|Параметры сортировки TempDB|CATALOG_DEFAULT|  
|Переменные|Параметры сортировки экземпляра|CATALOG_DEFAULT|  
|Метки перехода|Параметры сортировки экземпляра|CATALOG_DEFAULT|  
|Имена курсоров|Параметры сортировки экземпляра|CATALOG_DEFAULT|  
  
 В ранее описанном примере с временной таблицей видно, что такой принцип работы параметров сортировки исключает необходимость явно задавать предложение **COLLATE** в большинстве случаев использования временной таблицы. В автономной базе данных этот код теперь работает без ошибок, даже в случае, когда параметры сортировки различаются для базы данных и для экземпляра.  
  
```tsql  
CREATE TABLE T1 (T1_txt nvarchar(max)) ;  
GO  
CREATE TABLE #T2 (T2_txt nvarchar(max));  
GO  
SELECT T1_txt, T2_txt  
FROM T1   
JOIN #T2   
    ON T1.T1_txt = #T2.T2_txt ;  
```  
  
 Так происходит потому, что для `T1_txt` и `T2_txt` используются параметры сортировки автономной базы данных.  
  
## Переход между автономными и неавтономными контекстами  
 Пока сеанс в автономной базе данных остается автономным, он должен оставаться в пределах базы данных, с которой установлено соединение. В этом случае работа ведется очевидным образом. Однако если сеанс переходит между автономными и неавтономными контекстами, то его обработка усложняется, поскольку требуется организовать связь между двумя наборами правил. Такое может случаться в частично автономной базе данных, поскольку пользователь может передать команду **USE** в другую базу данных. В этом случае различия в правилах параметров сортировки обрабатываются следующим образом.  
  
-   Правило параметров сортировки для пакета определяется базой данных, в которой начинается пакет.  
  
 Заметьте, что это решение принимается до обработки команд, включая первоначальную команду **USE**. Это значит, что если пакет начинается в автономной базе данных, но первая команда **USE** ссылается на неавтономную базу данных, то для пакета будут использоваться параметры сортировки для автономной базы данных. В отношении переменных это может приводить к различным результатам.  
  
-   Ссылка может обнаружить ровно одно соответствие. В этом случае ссылка будет работать без ошибок.  
  
-   Ссылка может не найти соответствия в текущих параметрах сортировки на прежней позиции. В этом случае происходит ошибка, показывающая, что переменная не существует, хотя очевидно, что она была создана.  
  
-   Ссылка может обнаружить несколько соответствий, которые прежде были различными. В этом случае также происходит ошибка.  
  
 Это показано в следующих примерах. Пусть имеется частично автономная база данных с именем `MyCDB`, для которой используются параметры сортировки каталога **Latin1_General_100_CI_AS_WS_KS_SC**. Мы предполагаем, что используются следующие параметры сортировки экземпляра: **Latin1_General_100_CS_AS_WS_KS_SC**. Таким образом, два набора параметров сортировки различаются только учетом регистра.  
  
### Пример 1  
 В следующем примере показан вариант, где ссылка обнаруживает ровно одно совпадение.  
  
```  
USE MyCDB;  
GO  
  
CREATE TABLE #a(x int);  
INSERT INTO #a VALUES(1);  
GO  
  
USE master;  
GO  
  
SELECT * FROM #a;  
GO  
  
Results:  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
x  
-----------  
1  
```  
  
 В данном случае конструкция #a привязывается к параметрам сортировки каталога (без учета регистра) и к параметрам сортировки экземпляра (с учетом регистра) и код работает.  
  
### Пример 2  
 В следующим примере показан вариант, где ссылка не обнаруживает соответствие в текущих параметрах сортировки на прежней позиции.  
  
```  
USE MyCDB;  
GO  
  
CREATE TABLE #a(x int);  
INSERT INTO #A VALUES(1);  
GO  
```  
  
 Здесь конструкция #A привязывается к #a в параметрах сортировки по умолчанию (без учета регистра) и операция вставки работает.  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
(1 row(s) affected)  
```  
  
 Однако если работа скрипта продолжается...  
  
```  
USE master;  
GO  
  
SELECT * FROM #A;  
GO  
```  
  
 Возникает ошибка во время привязки к #A в параметрах сортировки экземпляра (с учетом регистра).  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 Сообщение 208, уровень 16, состояние 0, строка 2  
  
 Недопустимое имя объекта «#A».  
  
### Пример 3  
 В следующем примере показан вариант, где ссылка обнаруживает несколько соответствий, которые прежде были различными. Сначала в базе данных **tempdb**, параметры сортировки которой (с учетом регистра) совпадают с параметрами сортировки экземпляра, выполняются следующие инструкции.  
  
```  
USE tempdb;  
GO  
  
CREATE TABLE #a(x int);  
GO  
CREATE TABLE #A(x int);  
GO  
INSERT INTO #a VALUES(1);  
GO  
INSERT INTO #A VALUES(2);  
GO  
```  
  
 Он завершается успешно, поскольку в данных параметрах сортировки таблицы различны.  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
(1 row(s) affected)  
(1 row(s) affected)  
```  
  
 Однако если перейти в автономную базу данных, то окажется, что привязка к этим таблицам уже невозможна.  
  
```  
USE MyCDB;  
GO  
SELECT * FROM #a;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 Сообщение 12800, уровень 16, состояние 1, строка 2  
  
 Не удается разрешить неоднозначную ссылку на временную таблицу с именем «#a». Возможные варианты: «#a» и «#A».  
  
## Заключение  
 Работа параметров сортировки в автономных базах данных несколько отличается от неавтономных баз данных. В целом эти изменения упрощают работу и обеспечивают независимость от экземпляра. У некоторых пользователей могут возникать проблемы, особенно если сеанс обращается и к автономным и к неавтономным базам данных.  
  
## См. также:  
 [Автономные базы данных](../../relational-databases/databases/contained-databases.md)  
  
  