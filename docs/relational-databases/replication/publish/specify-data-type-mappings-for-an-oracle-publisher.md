---
title: "Указание сопоставления типов данных для издателя Oracle | Документация Майкрософт"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Oracle publishing [SQL Server replication], data type mapping
- data types [SQL Server replication], Oracle publishing
- mapping data types [SQL Server replication]
ms.assetid: f172d631-3b8c-4912-bd0f-568366cd9870
caps.latest.revision: 37
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e9ce8ce849533cb29249790d00371fe738d21db6
ms.contentlocale: ru-ru
ms.lasthandoff: 06/22/2017

---
# <a name="specify-data-type-mappings-for-an-oracle-publisher"></a>Указание сопоставления типов данных для издателя Oracle
  В данном разделе описывается указание сопоставления типов данных для издателя Oracle в [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] с помощью среды [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] или [!INCLUDE[tsql](../../../includes/tsql-md.md)]. Хотя в списке для издателей Oracle имеется набор сопоставлений типов данных, для отдельных публикаций может потребоваться создание дополнительных сопоставлений.  
  
 **В этом разделе**  
  
-   **Для указания сопоставления типов данных для издателя Oracle используется:**  
  
     [Среда SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="SSMSProcedure"></a> Использование среды SQL Server Management Studio  
 Укажите сопоставления типов данных на вкладке **Сопоставление данных** диалогового окна **Свойства статьи — \<статья>**. Она доступно на странице **Статьи** мастера создания публикаций и в диалоговом окне **Свойства публикации — \<публикация>**. Дополнительные сведения об использовании мастера и доступе к этому диалоговому окну см. в статьях [Создание публикации из базы данных Oracle](../../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md) и [Просмотр и изменение свойств публикации](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
#### <a name="to-specify-a-data-type-mapping"></a>Указание сопоставления типов данных  
  
1.  На странице **Статьи** мастера создания публикаций или в диалоговом окне **Свойства публикации — \<Публикация>** выберите таблицу и щелкните **Свойства статьи**.  
  
2.  Щелкните **Указать свойства выделенной статьи таблицы**.  
  
3.  На вкладке **Сопоставление данных** диалогового окна **Свойства статьи — \<статья>** выберите сопоставления из столбца **Тип данных подписчика**:  
  
    -   Для некоторых типов данных существует только одно возможное сопоставление, при этом столбец в сетке свойств доступен только для чтения.  
  
    -   Для некоторых типов данных можно осуществить выбор из нескольких типов. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] рекомендует использовать сопоставление по умолчанию, если приложению не требуется другого сопоставления. Дополнительные сведения см. в статье [Data Type Mapping for Oracle Publishers](../../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md).  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Использование Transact-SQL  
 Пользовательские сопоставления типов данных могут быть заданы программно с помощью хранимых процедур репликации. Можно также задать сопоставления по умолчанию, используемые при сопоставлении типов данных между [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] и системой управления базами данных, отличной от[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Дополнительные сведения см. в статье [Data Type Mapping for Oracle Publishers](../../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md).  
  
#### <a name="to-define-custom-data-type-mappings-when-creating-an-article-belonging-to-an-oracle-publication"></a>Определение пользовательского сопоставления данных при создании статьи, принадлежащей публикации Oracle  
  
1.  Если публикация Oracle не существует, ее необходимо создать.  
  
2.  На распространителе выполните хранимую процедуру [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md). В параметре **@use_default_datatypes** укажите значение **@use_default_datatypes**. Дополнительные сведения см. в статье [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
3.  Чтобы просмотреть существующие сопоставления для столбца в опубликованной статье, выполните хранимую процедуру [sp_helparticlecolumns](../../../relational-databases/system-stored-procedures/sp-helparticlecolumns-transact-sql.md) .  
  
4.  На распространителе выполните хранимую процедуру [sp_changearticlecolumndatatype](../../../relational-databases/system-stored-procedures/sp-changearticlecolumndatatype-transact-sql.md). Чтобы определить опубликованный столбец, укажите имя издателя Oracle в параметре **@publisher**и задайте значения параметров **@publication**, **@article**и **@column** . Укажите имя типа данных [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , сопоставляемого с типом **@type**и задайте значения параметров **@length**, **@precision**и **@scale**.  
  
5.  На распространителе выполните хранимую процедуру [sp_articleview](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md). Она создаст представление, используемое для создания моментального снимка из публикации Oracle.  
  
#### <a name="to-specify-a-mapping-as-the-default-mapping-for-a-data-type"></a>Назначение для типа данных сопоставления по умолчанию  
  
1.  (Необязательно) На распространителе в любой базе данных выполните хранимую процедуру [sp_getdefaultdatatypemapping](../../../relational-databases/system-stored-procedures/sp-getdefaultdatatypemapping-transact-sql.md). Укажите значения параметров **@source_dbms**, **@source_type**, **@destination_dbms**, **@destination_version**и других параметров, необходимых для идентификации базы данных-источника. Сведения о текущем сопоставлении типа данных в целевой базе данных возвращаются в выходных параметрах.  
  
2.  На распространителе в любой базе данных выполните хранимую процедуру [sp_helpdatatypemap](../../../relational-databases/system-stored-procedures/sp-helpdatatypemap-transact-sql.md)(необязательно). Укажите значения параметров **@source_dbms** и других параметров, необходимых для фильтрации результирующего набора. В результирующем наборе просмотрите значение параметра **mapping_id** для текущего сопоставления.  
  
3.  На распространителе в любой базе данных выполните хранимую процедуру [sp_setdefaultdatatypemapping](../../../relational-databases/system-stored-procedures/sp-setdefaultdatatypemapping-transact-sql.md)(необязательно).  
  
    -   Если известно необходимое значение параметра **mapping_id** , полученное на шаге 2, укажите его в параметре **@mapping_id**.  
  
    -   Если значение **mapping_id**неизвестно, то необходимо указать значения параметров **@source_dbms**, **@source_type**, **@destination_dbms**, **@destination_type**и других параметров, необходимых для идентификации существующего сопоставления.  
  
#### <a name="to-find-valid-data-types-for-a-given-oracle-data-type"></a>Определение допустимых типов данных, соответствующих типу данных Oracle  
  
1.  На распространителе в любой базе данных выполните хранимую процедуру [sp_helpdatatypemap](../../../relational-databases/system-stored-procedures/sp-helpdatatypemap-transact-sql.md). В параметре **ORACLE** укажите значение **@source_dbms** и других параметров, необходимых для фильтрации результирующего набора.  
  
###  <a name="TsqlExample"></a> Примеры (Transact-SQL)  
 Следующий пример производит сопоставление столбца данных Oracle типа NUMBER с типом данных [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **numeric**(38,38), изменяя стандартное сопоставление с типом **float**.  
  
 [!code-sql[HowTo#sp_changecolumndatatype](../../../relational-databases/replication/codesnippet/tsql/specify-data-type-mappin_1.sql)]  
  
 Следующий пример запроса возвращает два сопоставления для типа данных Oracle 9 **CHAR**: определенное по умолчанию и альтернативное.  
  
 [!code-sql[HowTo#sp_helpcolumndatatype_char](../../../relational-databases/replication/codesnippet/tsql/specify-data-type-mappin_2.sql)]  
  
 Следующий пример запроса возвращает сопоставления по умолчанию для типа данных Oracle 9 **NUMBER** , когда он указан без масштаба и точности.  
  
 [!code-sql[HowTo#sp_helpcolumndatatype_number](../../../relational-databases/replication/codesnippet/tsql/specify-data-type-mappin_3.sql)]  
  
## <a name="see-also"></a>См. также:  
 [Data Type Mapping for Oracle Publishers](../../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md)   
 [Разнородная репликация базы данных](../../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Replication System Stored Procedures Concepts](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [Настройка издателя Oracle](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)  
  
  