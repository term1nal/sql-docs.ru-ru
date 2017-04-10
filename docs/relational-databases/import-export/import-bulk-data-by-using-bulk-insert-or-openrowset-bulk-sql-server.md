---
title: "Массовый импорт данных при помощи инструкции BULK INSERT или OPENROWSET(BULK...) (SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "07/26/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-bulk-import-export"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "инструкция BULK INSERT, импорт данных из удаленного файла данных"
  - "массовый импорт [SQL Server], методы"
  - "массовый экспорт [SQL Server], методы"
  - "функция OPENROWSET, BULK INSERT"
  - "массовый импорт [SQL Server], безопасность"
  - "поставщики больших наборов строк [SQL Server]"
  - "массовый экспорт [SQL Server], инструкция BULK INSERT"
  - "удаленный доступ к данным [SQL Server], массовый импорт"
  - "массовый импорт [SQL Server], инструкция BULK INSERT"
  - "операции массового экспорта-импорта в языке Transact-SQL"
ms.assetid: 18a64236-0285-46ea-8929-6ee9bcc020b9
caps.latest.revision: 45
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 44
---
# Массовый импорт данных при помощи инструкции BULK INSERT или OPENROWSET(BULK...) (SQL Server)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Этот раздел содержит общие сведения об использовании инструкций [!INCLUDE[tsql](../../includes/tsql-md.md)] BULK INSERT и INSERT...SELECT * FROM OPENROWSET(BULK...) для массового импорта данных из файла данных в таблицу [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. В разделе также описываются вопросы безопасности при использовании BULK INSERT и OPENROWSET(BULK…), а также применение этих методов для массового импорта из удаленного источника данных.  
  
> **ПРИМЕЧАНИЕ.** При использовании инструкции BULK INSERT или OPENROWSET(BULK…) важно понимать, каким образом выполняется олицетворение в версии [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Дополнительные сведения см. в подразделе «Вопросы безопасности» далее в этом разделе.  
  
## BULK INSERT, инструкция  
 Инструкция BULK INSERT загружает данные из файла данных в таблицу. Эти функциональные возможности аналогичны тем, которые предоставляются параметром **in** команды **bcp**, но чтение файла данных выполняется процессом [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Описание синтаксиса инструкции BULK INSERT см. в разделе [BULK INSERT (Transact-SQL)](../../t-sql/statements/bulk-insert-transact-sql.md).  
  
## Примеры BULK INSERT  
 
  
-   [BULK INSERT (Transact-SQL)](../../t-sql/statements/bulk-insert-transact-sql.md)  
  
-   [Примеры массового импорта и экспорта XML-документов (SQL Server)](../../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)  
  
-   [Сохранение значений идентификаторов при массовом импорте данных (SQL Server)](../../relational-databases/import-export/keep-identity-values-when-bulk-importing-data-sql-server.md)  
  
-   [Сохранение значений NULL или использование значений по умолчанию при массовом импорте данных (SQL Server)](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)  
  
-   [Определение признаков конца поля и строки (SQL Server)](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)  
  
-   [Использование файла форматирования для массового импорта данных (SQL Server)](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)  
  
-   [Использование символьного формата для импорта и экспорта данных (SQL Server)](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Использование собственного формата для импорта и экспорта данных (SQL Server)](../../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [Использование символьного формата Юникод для импорта и экспорта данных (SQL Server)](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Использование собственного формата Юникод для импорта и экспорта данных (SQL Server)](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
-   [Пропуск столбца таблицы с помощью файла форматирования (SQL Server)](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)  
  
-   [Использование файла форматирования для сопоставления столбцов таблицы с полями файла данных (SQL Server)](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
## Функция OPENROWSET(BULK…)  
 Доступ к поставщику больших наборов строк OPENROWSET осуществляется путем вызова функции OPENROWSET и задания параметра BULK. Функция OPENROWSET(BULK…) обеспечивает доступ к удаленным данным, производя соединение с удаленным источником данных, например файлу данных, через поставщик OLE DB.  
  
 Чтобы импортировать групповые данные, вызовите функцию OPENROWSET(BULK…) из предложения SELECT…FROM инструкции INSERT. Основной синтаксис массового импорта данных:  
  
 Инструкции INSERT ... SELECT * FROM OPENROWSET(BULK...).  
  
 При использовании инструкции INSERT функция OPENROWSET(BULK...) поддерживает табличные указания. Кроме обычных табличных указаний, например TABLOCK, предложение BULK может принимать следующие специальные табличные указания: IGNORE_CONSTRAINTS (игнорирует только ограничения CHECK), IGNORE_TRIGGERS, KEEPDEFAULTS и KEEPIDENTITY. Дополнительные сведения см. в разделе [Табличные указания (Transact-SQL)](../Topic/Table%20Hints%20\(Transact-SQL\).md).  
  
 Сведения о дополнительном использовании параметра BULK см. в разделе [OPENROWSET (Transact-SQL)](../../t-sql/functions/openrowset-transact-sql.md).  
  
## Инструкции INSERT...SELECT * FROM OPENROWSET(BULK...) — примеры:
  
-   [Примеры массового импорта и экспорта XML-документов (SQL Server)](../../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)  
  
-   [Сохранение значений идентификаторов при массовом импорте данных (SQL Server)](../../relational-databases/import-export/keep-identity-values-when-bulk-importing-data-sql-server.md)  
  
-   [Сохранение значений NULL или использование значений по умолчанию при массовом импорте данных (SQL Server)](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)  
  
-   [Использование файла форматирования для массового импорта данных (SQL Server)](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)  
  
-   [Использование символьного формата для импорта и экспорта данных (SQL Server)](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Пропуск столбца таблицы с помощью файла форматирования (SQL Server)](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)  
  
-   [Использование файла форматирования для пропуска поля данных (SQL Server)](../../relational-databases/import-export/use-a-format-file-to-skip-a-data-field-sql-server.md)  
  
-   [Использование файла форматирования для сопоставления столбцов таблицы с полями файла данных (SQL Server)](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
## Вопросы безопасности  
 Если пользователь использует имя входа [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], то применяется профиль безопасности учетной записи процесса [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. За пределами компонента Database Engine невозможно выполнить проверку подлинности имени входа, проходящего проверку подлинности SQL Server. Поэтому, если имя входа, использующее проверку подлинности SQL Server, инициирует команду BULK INSERT, подключение к данным устанавливается с помощью контекста безопасности учетной записи процесса SQL Server (учетной записи, которая используется службой SQL Server Database Engine). 
 
 Для того чтобы прочитать исходные данные, учетной записи, которая используется службой SQL Server Database Engine, необходимо предоставить доступ к этим исходным данным. Если пользователь [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] входит в систему с проверкой подлинности Windows, то ему доступны только те файлы, к которым имеет доступ учетная запись пользователя, независимо от профиля безопасности процесса [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Предположим, пользователь вошел в экземпляр [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] с проверкой подлинности Windows. Чтобы иметь возможность воспользоваться BULK INSERT или OPENROWSET для импорта данных из файла данных в таблицу [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], учетная запись должна иметь доступ на чтение этого файла данных. Если же пользователь имеет доступ к файлу данных, то он может импортировать данные из файла в таблицу даже в том случае, когда процесс [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] не имеет прав доступа к файлу. Пользователь не должен предоставлять процессу [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] права на доступ к файлу.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] и [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows могут быть настроены таким образом, чтобы экземпляр [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] мог выполнять соединение с другим экземпляром [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] посредством переадресации учетных данных пользователя Windows, прошедшего проверку подлинности. Такой подход называется *олицетворением* или *делегированием*. При использовании инструкции BULK INSERT или OPENROWSET очень важно понимать, каким образом в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] и более поздних версиях обеспечивается безопасность при олицетворении пользователя. Это позволяет хранить файл данных не на том компьютере, на котором вошел пользователь или работает процесс [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Например, если пользователь на **компьютере_A** имеет доступ к файлу данных на **компьютере_B** и делегирование учетных данных было соответствующим образом настроено, этот пользователь может подключиться к экземпляру [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], запущенному на **компьютере_C**, получить доступ к файлу данных на **компьютере_B** и выполнить массовый импорт данных из этого файла в таблицу на **компьютере_C**.  
  
## Массовый импорт из удаленного файла данных  
 Чтобы использовать инструкции BULK INSERT или INSERT...SELECT \* FROM OPENROWSET(BULK...) для массового импорта данных с другого компьютера, необходимо, чтобы файл данных был доступен на обоих компьютерах. Укажите общий файл данных в формате UNC, то есть в следующем формате: **\\\\***Имя сервера***\\***Общая папка***\\***Путь***\\***Имя файла*. Кроме того, используемая учетная запись должна обладать разрешениями, необходимыми для чтения этого файла на удаленном диске.  
  
 Например, инструкция `BULK INSERT` производит массовый импорт в таблицу `SalesOrderDetail` базы данных `AdventureWorks` из файла данных с именем `newdata.txt`. Этот файл данных находится в общей папке `\dailyorders`, расположенной в общем сетевом каталоге `salesforce` компьютера с именем `computer2`.  
  
```  
BULK INSERT AdventureWorks2012.Sales.SalesOrderDetail  
   FROM '\\computer2\salesforce\dailyorders\neworders.txt';  
GO  
```  
  
> **ПРИМЕЧАНИЕ.** Это ограничение не применяется к служебной программе **bcp**, потому что клиент считывает файл независимо от [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## См. также:  
 [INSERT (Transact-SQL)](../../t-sql/statements/insert-transact-sql.md)   
 [Предложение SELECT (Transact-SQL)](../../t-sql/queries/select-clause-transact-sql.md)   
 [Массовый импорт и экспорт данных (SQL Server)](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)   
 [OPENROWSET (Transact-SQL)](../../t-sql/functions/openrowset-transact-sql.md)   
 [SELECT (Transact-SQL)](../../t-sql/queries/select-transact-sql.md)   
 [FROM (Transact-SQL)](../../t-sql/queries/from-transact-sql.md)   
 [Программа bcp](../../tools/bcp-utility.md)   
 [BULK INSERT (Transact-SQL)](../../t-sql/statements/bulk-insert-transact-sql.md)  
  
  