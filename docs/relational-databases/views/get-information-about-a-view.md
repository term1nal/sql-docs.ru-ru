---
title: "Получение сведений о представлении | Документация Майкрософт"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-views
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.viewproperties.general.f1
helpviewer_keywords:
- views [SQL Server], status information
- metadata [SQL Server], views
- dependencies [SQL Server], views
- displaying view information
- views [SQL Server], metadata
- viewing view information
- status information [SQL Server], views
- view dependencies
ms.assetid: 05a73e33-8f85-4fb6-80c1-1b659e753403
caps.latest.revision: 30
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: f2a981d28720713387dd5b593f037662b9b6b654
ms.contentlocale: ru-ru
ms.lasthandoff: 06/22/2017

---
# <a name="get-information-about-a-view"></a>Получение сведений о представлении
  Получить сведения об определении или свойствах представления в [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] можно с помощью [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] или [!INCLUDE[tsql](../../includes/tsql-md.md)]. Возможность просмотреть определение представления может понадобиться, чтобы понять, как его данные извлекаются из исходных таблиц, или чтобы увидеть данные, определенные представлением.  
  
> [!IMPORTANT]  
>  Если имя объекта, на который ссылается представление, было изменено, необходимо изменить представление так, чтобы в его тексте использовалось новое имя. Следовательно, прежде чем переименовывать объект, следует отобразить зависимости объекта, чтобы определить, повлияет ли предполагаемое изменение на какие-либо представления.  
  
 **В этом разделе**  
  
-   **Перед началом работы выполните следующие действия.**  
  
     [Безопасность](#Security)  
  
-   **Получение сведений о представлении с помощью следующих средств:**  
  
     [Среда SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Перед началом  
  
###  <a name="Security"></a> Безопасность  
  
####  <a name="Permissions"></a> Разрешения  
 Для использования `sp_helptext` для получения определения представления требуется членство в роли **public** . Для использования `sys.sql_expression_dependencies` для поиска всех зависимостей в представлении требуется разрешение VIEW DEFINITION в базе данных и разрешение SELECT в `sys.sql_expression_dependencies` для базы данных. Такие определения системных объектов, как полученные в SELECT OBJECT_DEFINITION, видимы для всех.  
  
##  <a name="SSMSProcedure"></a> Использование среды SQL Server Management Studio  
  
#### <a name="get-view-properties-by-using-object-explorer"></a>Получение свойств представления с помощью обозревателя объектов  
  
1.  В **обозревателе объектов**щелкните знак «плюс» рядом с базой данных, содержащей представление, свойства которого необходимо просмотреть, а затем щелкните знак «плюс», чтобы развернуть папку **Представления** .  
  
2.  Щелкните правой кнопкой представление, свойства которого необходимо просмотреть, и выберите пункт **Свойства**.  
  
     В диалоговом окне **Свойства представления** отображаются следующие свойства:  
  
     **База данных**  
     Имя базы данных, содержащей это представление.  
  
     **Server**  
     Имя текущего экземпляра сервера.  
  
     **Пользователь**  
     Имя пользователя этого соединения.  
  
     **Дата создания**  
     Отображает дату создания представления.  
  
     **Название**  
     Имя текущего представления.  
  
     **Схема**  
     Схема, которой принадлежит представление.  
  
     **Системный объект**  
     Указывает, является ли представление системным объектом. Возможные значения: True и False.  
  
     **Значения NULL по стандарту ANSI**  
     Указывает, был ли объект создан с параметром ANSI NULL.  
  
     **Зашифрована**  
     Указывает, зашифровано ли представление. Возможные значения: True и False.  
  
     **Заключенный в кавычки идентификатор**  
     Показывает, был ли объект создан с параметром «заключенный в кавычки идентификатор».  
  
     **Привязка к схеме**  
     Указывает, является ли представление привязанным к схеме. Возможные значения: True и False. Сведения о представлениях, привязанных к схеме, см. в подразделе SCHEMABINDING раздела [CREATE VIEW (Transact-SQL)](../../t-sql/statements/create-view-transact-sql.md).  
  
#### <a name="getting-view-properties-by-using-the-view-designer-tool"></a>Получение свойств представления с помощью конструктора представлений  
  
1.  В **обозревателе объектов**разверните базу данных, содержащую представление, свойства которого необходимо просмотреть, а затем разверните папку **Представления** .  
  
2.  Щелкните правой кнопкой мыши представление, свойства которого необходимо просмотреть, и выберите пункт **Конструктор**.  
  
3.  Щелкните правой кнопкой мыши пустое пространство на панели диаграммы и выберите пункт **Свойства**.  
  
     На панели **Свойства** отображаются следующие свойства.  
  
     **(Имя)**  
     Имя текущего представления.  
  
     **Имя базы данных**  
     Имя базы данных, содержащей это представление.  
  
     **Описание**  
     Краткое описание текущего представления.  
  
     **Схема**  
     Схема, которой принадлежит представление.  
  
     **Имя сервера**  
     Имя текущего экземпляра сервера.  
  
     **Привязка к схеме**  
     Предотвращает такие изменения пользователями базовых объектов, задействованных в представлении, в результате которых определение представления становится недействительным.  
  
     **Детерминированное**  
     Указывает, может ли тип данных для выбранного столбца быть точно определен  
  
     **Различные значения**  
     Указывает, что запрос будет отфильтровывать повторения в представлении. Этот параметр полезен при использовании только некоторых столбцов из таблицы, притом что эти столбцы могут содержать повторяющиеся значения, или если обработка соединения двух или более таблиц приводит к появлению повторяющихся строк в результирующем наборе. Выбор этого параметра эквивалентен вставке ключевого слова DISTINCT в инструкцию на панели SQL.  
  
     **Расширение GROUP BY**  
     Указывает, что для представлений доступны дополнительные параметры, основанные на агрегатных запросах.  
  
     **Выводить все столбцы**  
     Указывает, возвращаются ли в выбранном представлении все столбцы. Этот параметр задается во время создания представления.  
  
     **Комментарий SQL**  
     Показывает описание инструкций SQL. Чтобы просмотреть или отредактировать описание целиком, щелкните его и затем нажмите кнопку с многоточием **(...)** справа от свойства. Комментарии могут содержать, например, сведения о том, кто использует это представление и когда оно используется.  
  
     **Спецификация TOP**  
     Разворачивается для отображения свойств **Первые**, **Выражение**, **Процент**и **Со связями** .  
  
     **(Верх)**  
     Указывает, что представление будет иметь предложение TOP, возвращающее только первые n строк или первые n процентов строк из результирующего набора. По умолчанию представление возвращает первые 10 строк из результирующего набора. Это поле позволяет изменить число возвращаемых строк или указать другой процент.  
  
     **Выражение**  
     Указывает, какой процент (если для параметра **Процент** выбрано значение **Да**) или какое количество записей (если для параметра **Процент** выбрано значение **Нет**) возвращает представление.  
  
     **Процент**  
     Указывает, что запрос будет включать предложение **TOP** , возвращающее только первые n процентов строк из результирующего набора.  
  
     **Со связями**  
     Указывает, что представление включает предложение **WITH TIES** . **WITH TIES** полезно, если представление включает предложения **ORDER BY** и **TOP** , основанные на процентах. Если этот параметр установлен и пороговое значение процента приходится на середину набора строк с одинаковыми значениями в предложении **ORDER BY** , то данное представление будет расширено и будет включать все такие строки.  
  
     **Спецификация Update**  
     Разворачивается для отображения свойств **Правила обновления через представление** и **Параметр проверки** .  
  
     **(Обновление с использованием правил представления.)**  
     Указывает, что все обновления и вставки в представлении будут преобразованы с помощью Microsoft Data Access Components (MDAC) в инструкции SQL, которые ссылаются на представление, а не в инструкции SQL, которые ссылаются непосредственно на базовые таблицы представления.  
  
     В некоторых случаях компоненты MDAC представляют операции обновления и вставки представления в виде операций обновления и вставки в базовых таблицах представления. Выбор **Обновление с использованием правил представления**позволяет гарантировать создание MDAC операций обновления и вставки для самого представления.  
  
     **Параметр проверки**  
     Указывает, что при открытии этого представления и изменении панели **Результаты** источник данных проверяет соответствие добавленных или измененных данных предложению **WHERE** определения представления. Если изменения не соответствуют предложению **WHERE** , будет отображено сообщение об ошибке с более подробными сведениями.  
  
#### <a name="to-get-dependencies-on-the-view"></a>Получение зависимостей представления  
  
1.  В **обозревателе объектов**разверните базу данных, содержащую представление, свойства которого необходимо просмотреть, а затем разверните папку **Представления** .  
  
2.  Щелкните правой кнопкой мыши представление, свойства которого необходимо просмотреть, и выберите пункт **Просмотреть зависимости**.  
  
3.  Выберите **Объекты, зависящие от [имя_представления]** для отображения объектов, которые ссылаются на представление.  
  
4.  Для отображения объектов, на которые ссылается представление, выберите **Объекты, от которых зависит [имя_представления]** .  
  
##  <a name="TsqlProcedure"></a> Использование Transact-SQL  
  
#### <a name="to-get-the-definition-and-properties-of-a-view"></a>Получение определения и свойств представления  
  
1.  В **обозревателе объектов**подключитесь к экземпляру компонента [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  На стандартной панели выберите пункт **Создать запрос**.  
  
3.  Скопируйте и вставьте один из следующих примеров в окно запроса и нажмите кнопку **Выполнить**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT definition, uses_ansi_nulls, uses_quoted_identifier, is_schema_bound  
    FROM sys.sql_modules  
    WHERE object_id = OBJECT_ID('HumanResources.vEmployee');   
    GO  
    ```  
  
    ```  
    USE AdventureWorks2012;   
    GO  
    SELECT OBJECT_DEFINITION (OBJECT_ID('HumanResources.vEmployee')) AS ObjectDefinition;   
    GO  
    ```  
  
    ```  
    EXEC sp_helptext 'HumanResources.vEmployee';  
    ```  
  
 Дополнительные сведения см. в разделах [sys.sql_modules (Transact-SQL)](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md), [OBJECT_DEFINITION (Transact-SQL)](../../t-sql/functions/object-definition-transact-sql.md) и [sp_helptext (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md).  
  
#### <a name="to-get-the-dependencies-of-a-view"></a>Получение зависимостей представления  
  
1.  В **обозревателе объектов**подключитесь к экземпляру компонента [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  На стандартной панели выберите пункт **Создать запрос**.  
  
3.  Скопируйте следующий пример в окно запроса и нажмите кнопку **Выполнить**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT OBJECT_NAME(referencing_id) AS referencing_entity_name,   
        o.type_desc AS referencing_desciption,   
        COALESCE(COL_NAME(referencing_id, referencing_minor_id), '(n/a)') AS referencing_minor_id,   
        referencing_class_desc, referenced_class_desc,  
        referenced_server_name, referenced_database_name, referenced_schema_name,  
        referenced_entity_name,   
        COALESCE(COL_NAME(referenced_id, referenced_minor_id), '(n/a)') AS referenced_column_name,  
        is_caller_dependent, is_ambiguous  
    FROM sys.sql_expression_dependencies AS sed  
    INNER JOIN sys.objects AS o ON sed.referencing_id = o.object_id  
    WHERE referencing_id = OBJECT_ID(N'Production.vProductAndDescription');  
    GO  
    ```  
  
 Дополнительные сведения см. в разделах [sys.sql_expression_dependencies (Transact-SQL)](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md) и [sys.objects (Transact-SQL)](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md).  
  
  