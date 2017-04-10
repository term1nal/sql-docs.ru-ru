---
title: "Задание метода распространения изменений данных в транзакционные статьи | Microsoft Docs"
ms.custom: ""
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "репликация транзакций, методы распространения"
  - "распространение изменений данных [репликация SQL Server]"
ms.assetid: 0a291582-f034-42da-a1a3-29535b607b74
caps.latest.revision: 39
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 39
---
# Задание метода распространения изменений данных в транзакционные статьи
  В этом разделе описывается задание метода распространения изменений данных в транзакционных статьях в [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] с помощью среды [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] или [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
 По умолчанию репликация транзакций передает изменения подписчикам при помощи набора хранимых процедур для каждой статьи. Эти процедуры можно заменить на пользовательские процедуры. Дополнительные сведения см. в разделе [указания способа распространения изменений для транзакционных статей](../../../relational-databases/replication/transactional/specify-how-changes-are-propagated-for-transactional-articles.md).  
  
 **В этом разделе**  
  
-   **Перед началом работы выполните следующие действия.**  
  
     [Ограничения](#Restrictions)  
  
-   **Для задания метода распространения изменений данных в транзакционных статьях используется:**  
  
     [Среда SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
## Перед началом  
  
###  <a name="Restrictions"></a> Ограничения  
  
-   Необходимо соблюдать осторожность при изменении любого файла моментального снимка, созданного репликацией. Необходимо тестировать и поддерживать пользовательскую логику в пользовательских хранимых процедурах. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] не поддерживает настраиваемую логику.  
  
##  <a name="SSMSProcedure"></a> Использование среды SQL Server Management Studio  
 Определите метод распространения на **Свойства** вкладке **Свойства статьи — \< статья>** диалоговое окно доступно в мастере создания публикаций и **Свойства публикации — \< публикации>** диалоговое окно. Дополнительные сведения об использовании мастера и о доступе к диалоговому окну см. в разделе [Создать публикацию](../../../relational-databases/replication/publish/create-a-publication.md) и [Просмотр и изменение свойств публикации](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
#### Указание метода распространения  
  
1.  На **статьи** страница мастера создания публикаций или **Свойства публикации — \< публикация>** диалоговое окно, выберите таблицу и нажмите кнопку **Свойства статьи**.  
  
2.  Щелкните **Указать свойства выделенной статьи таблицы**.  
  
3.  На **Свойства** вкладке **Свойства статьи — \< статья>** в диалоговом **Доставка инструкций** Укажите метод распространения каждой операции с использованием **Формат доставки инструкций INSERT**, **Формат доставки инструкций UPDATE**, и **Формат доставки инструкций DELETE** меню.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  При работе в **Свойства публикации — \< публикация>** диалоговом нажмите кнопку **ОК** Сохранить и закрыть диалоговое окно.  
  
#### Создание и использование пользовательских хранимых процедур  
  
1.  На **статьи** страница мастера создания публикаций или **Свойства публикации — \< публикация>** диалоговое окно, выберите таблицу и нажмите кнопку **Свойства статьи**.  
  
2.  Щелкните **Указать свойства выделенной статьи таблицы**.  
  
     На **Свойства** Вкладка **Свойства статьи — \< статья>** в диалоговом **Доставка инструкций** выберите из меню Формат доставки соответствующий синтаксис ВЫЗОВА (**Формат доставки инструкций INSERT**, **Формат доставки инструкций UPDATE**, или **Формат доставки инструкций DELETE**) и затем введите имя процедуры, для использования в **хранимая процедура INSERT**, **Удаление хранимой процедуры**, или **Обновление хранимой процедуры**. Дополнительные сведения о синтаксисе инструкции CALL см в разделе «Синтаксис вызова для хранимых процедур» [Укажите способа распространения изменений для транзакционных статей](../../../relational-databases/replication/transactional/specify-how-changes-are-propagated-for-transactional-articles.md).  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
4.  При работе в **Свойства публикации — \< публикация>** диалоговом нажмите кнопку **ОК** Сохранить и закрыть диалоговое окно.  
  
5.  Моментальный снимок, созданный для публикации, включает процедуру, заданную вами на предыдущем шаге. Процедуры будут использовать заданный вами синтаксис инструкции CALL, но при этом будут включать логику по умолчанию, используемую репликацией.  
  
     После создания моментального снимка перейдите в папку моментальных снимков, относящуюся к публикации, которой принадлежит данная статья, затем найдите файл с расширением **.sch** и с таким же именем, что и статья. Откройте этот файл при помощи программы «Блокнот» или другого текстового редактора, найдите команду CREATE PROCEDURE для вставки, обновления или удаления хранимых процедур и измените определение процедуры, чтобы указать пользовательскую логику для распространения изменений данных. Если моментальный снимок восстановлен, создайте заново пользовательскую процедуру.  
  
##  <a name="TsqlProcedure"></a> Использование Transact-SQL  
 Репликация транзакций позволяет управлять процессом распространения изменений от издателя к подписчику. Метод распространения может быть задан программным путем при создании и последующем изменении статей с помощью хранимых процедур репликации.  
  
> [!NOTE]  
>  Разным операциям DML (вставка, обновление или удаление), выполняемым над строками опубликованных данных, могут быть назначены различные методы распространения.  
  
 Дополнительные сведения см. в разделе [указания способа распространения изменений для транзакционных статей](../../../relational-databases/replication/transactional/specify-how-changes-are-propagated-for-transactional-articles.md).  
  
#### Создание статьи, использующей команды Transact-SQL для распространения изменений данных  
  
1.  На издателе в базе данных публикации выполните хранимую процедуру [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md). Укажите имя публикации, к которой принадлежит статья, для **@publication**, имя статьи для **@article**, объект базы данных, публикуемые для **@source_object**, а значение **SQL** хотя бы для одного из следующих параметров:  
  
    -   **@ins_cmd** — управляет репликацией [Вставка](../../../t-sql/statements/insert-transact-sql.md) команды.  
  
    -   **@upd_cmd** — управляет репликацией [обновление](../../../t-sql/queries/update-transact-sql.md) команды.  
  
    -   **@del_cmd** — управляет репликацией [Удаление](../../../t-sql/statements/delete-transact-sql.md) команды.  
  
    > [!NOTE]  
    >  При указании значения **SQL** для любого из перечисленных выше параметров команды этого типа будут реплицированы на подписчик, соответствующими [!INCLUDE[tsql](../../../includes/tsql-md.md)] команды.  
  
     Дополнительные сведения см. в статье [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
#### Создание статьи, не распространяющей изменения данных  
  
1.  На издателе в базе данных публикации выполните хранимую процедуру [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md). Укажите имя публикации, к которой принадлежит статья, для **@publication**, имя статьи, для **@article**, объект базы данных, публикуемые для **@source_object**, а значение **** хотя бы для одного из следующих параметров:  
  
    -   **@ins_cmd** — управляет репликацией [Вставка](../../../t-sql/statements/insert-transact-sql.md) команды.  
  
    -   **@upd_cmd** — управляет репликацией [обновление](../../../t-sql/queries/update-transact-sql.md) команды.  
  
    -   **@del_cmd** — управляет репликацией [Удаление](../../../t-sql/statements/delete-transact-sql.md) команды.  
  
    > [!NOTE]  
    >  При указании значения **NONE** для перечисленных выше параметров, команды этого типа не быть реплицированы на подписчик.  
  
     Дополнительные сведения см. в статье [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
#### Создание статьи с изменяемыми пользовательскими хранимыми процедурами  
  
1.  На издателе в базе данных публикации выполните хранимую процедуру [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md). Укажите имя публикации, к которой принадлежит статья, для **@publication**, имя статьи для **@article**, объект базы данных, публикуемые для **@source_object**, значение для **@schema_option** битовую маску, которая содержит значение **0x02** (включает автоматическое создание пользовательских хранимых процедур) и хотя бы один из следующих параметров:  
  
    -   **@ins_cmd** -Укажите значение **CALL sp_MSins_*имя_статьи***, где ***имя_статьи*** — значение, заданное для **@article**.  
  
    -   **@del_cmd** -Укажите значение **ВЫЗОВ sp_MSdel_*имя_статьи*** или **XCALL sp_MSdel_*имя_статьи***, где ***имя_статьи*** — значение, заданное для **@article**.  
  
    -   **@upd_cmd** -Укажите значение **SCALL sp_MSupd_*имя_статьи***, **ВЫЗОВ sp_MSupd_*имя_статьи***, **XCALL sp_MSupd_*имя_статьи***, или **MCALL sp_MSupd_*имя_статьи***, где ***имя_статьи*** — значение, заданное для **@article**.  
  
    > [!NOTE]  
    >  Для каждой из приведенных выше команд в качестве параметров можно указать собственное имя хранимых процедур, создаваемых репликацией.  
  
    > [!NOTE]  
    >  Дополнительные сведения о синтаксисе ВЫЗОВА, SCALL, XCALL и MCALL см. в разделе [указания способа распространения изменений для транзакционных статей](../../../relational-databases/replication/transactional/specify-how-changes-are-propagated-for-transactional-articles.md).  
  
     Дополнительные сведения см. в статье [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
2.  После создания моментального снимка перейдите в папку моментальных снимков, относящуюся к публикации, которой принадлежит данная статья, затем найдите файл с расширением **.sch** и с таким же именем, что и статья. Откройте этот файл в блокноте, найдите инструкцию CREATE PROCEDURE для хранимой процедуры вставки, обновления или удаления и измените ее определение, задав пользовательскую логику распространения изменений данных. Дополнительные сведения см. в разделе [указания способа распространения изменений для транзакционных статей](../../../relational-databases/replication/transactional/specify-how-changes-are-propagated-for-transactional-articles.md).  
  
#### Создание статьи, использующей пользовательские скрипты в пользовательских хранимых процедурах для распространения изменений данных  
  
1.  На издателе в базе данных публикации выполните хранимую процедуру [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md). Укажите имя публикации, к которой принадлежит статья, для **@publication**, имя статьи для **@article**, объект базы данных, публикуемые для **@source_object**, значение для **@schema_option** битовую маску, которая содержит значение **0x02** (включает автоматическое создание пользовательских хранимых процедур) и хотя бы один из следующих параметров:  
  
    -   **@ins_cmd** -Укажите значение **CALL sp_MSins_*имя_статьи***, где ***имя_статьи*** — значение, заданное для **@article**.  
  
    -   **@del_cmd** -Укажите значение **ВЫЗОВ sp_MSdel_*имя_статьи*** или **XCALL sp_MSdel_*имя_статьи***, где ***имя_статьи*** — значение, заданное для **@article**.  
  
    -   **@upd_cmd** -Укажите значение **SCALL sp_MSupd_*имя_статьи***, **ВЫЗОВ sp_MSupd_*имя_статьи***, **XCALL sp_MSupd_*имя_статьи***, **MCALL sp_MSupd_*имя_статьи***, где ***имя_статьи*** — значение, заданное для **@article**.  
  
    > [!NOTE]  
    >  Для каждой из приведенных выше команд в качестве параметров можно указать собственное имя хранимых процедур, создаваемых репликацией.  
  
    > [!NOTE]  
    >  Дополнительные сведения о синтаксисе ВЫЗОВА, SCALL, XCALL и MCALL см. в разделе [указания способа распространения изменений для транзакционных статей](../../../relational-databases/replication/transactional/specify-how-changes-are-propagated-for-transactional-articles.md).  
  
     Дополнительные сведения см. в статье [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
2.  На издателе в базе данных публикации, используйте [ALTER PROCEDURE](../../../t-sql/statements/alter-procedure-transact-sql.md) инструкцию, чтобы изменить [sp_scriptpublicationcustomprocs](../../../relational-databases/system-stored-procedures/sp-scriptpublicationcustomprocs-transact-sql.md) чтобы он возвращал [CREATE PROCEDURE](../../../t-sql/statements/create-procedure-transact-sql.md) скрипт для вставки, обновления и удаления пользовательских хранимых процедур. Дополнительные сведения см. в разделе [указания способа распространения изменений для транзакционных статей](../../../relational-databases/replication/transactional/specify-how-changes-are-propagated-for-transactional-articles.md).  
  
#### Изменение метода распространения изменений для существующей статьи  
  
1.  На издателе в базе данных публикации выполните хранимую процедуру [sp_changearticle](../../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md). Укажите **@publication**, **@article**, значение **ins_cmd**, **upd_cmd**, или **del_cmd** для **@property**, и метод распространения соответствующие **@value**.  
  
2.  Повторите шаг 1 для каждого изменяемого метода распространения.  
  
## См. также:  
 [Указание способа распространения изменений для статей транзакций](../../../relational-databases/replication/transactional/specify-how-changes-are-propagated-for-transactional-articles.md)   
 [Создание, изменение и удаление публикаций и статей & #40; Репликация & #41;](../../../relational-databases/replication/publish/create-modify-and-delete-publications-and-articles-replication.md)  
  
  