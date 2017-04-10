---
title: "вставлять фрагменты кода Transact-SQL | Microsoft Docs"
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
  - "IntelliSense [SQL Server], фрагменты кода"
  - "фрагменты кода Transact-SQL, код"
  - "фрагменты кода [Transact-SQL], как вставить"
ms.assetid: d66c96f4-2e84-4d79-9bfd-3635fdd98425
caps.latest.revision: 7
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 7
---
# вставлять фрагменты кода Transact-SQL
  Фрагмент кода [!INCLUDE[tsql](../../includes/tsql-md.md)] можно использовать в качестве шаблона при написании новых инструкций [!INCLUDE[tsql](../../includes/tsql-md.md)] в редакторе запросов компонента [!INCLUDE[ssDE](../../includes/ssde-md.md)] .  
  
## Вставка фрагментов  
 Открыть упорядоченный по категориям перечень доступных для выбора фрагментов можно из меню **Вставить фрагмент** .  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] содержат точки замены: текст с рекомендациями по синтаксису, относящемуся к данной точке. Например, во фрагменте CREATE TABLE находятся точки замены для таких элементов, как имя таблицы, имена столбцов, типы данных в столбцах. После вставки фрагмента кода необходимо заменить текст замены, образовав правильную инструкцию [!INCLUDE[tsql](../../includes/tsql-md.md)]. Дополнительные сведения см. в разделе [Завершение фрагментов кода Transact-SQL](../../relational-databases/scripting/complete-transact-sql-snippets.md).  
  
#### Вставка фрагмента с помощью меню «Вставить фрагмент»  
  
1.  Откройте окно «Редактор запроса компонента [!INCLUDE[ssDE](../../includes/ssde-md.md)] » и переместите курсор в место будущей вставки фрагмента [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
2.  Вызовите подсказку одним из следующих способов.  
  
    -   Нажмите комбинацию клавиш CTRL+K или CTRL+X.  
  
    -   В меню **Правка** укажите пункт **IntelliSense**и выберите **Вставить фрагмент**.  
  
    -   Щелкните правой кнопкой мыши и выберите из контекстного меню команду **Вставить фрагмент**.  
  
3.  Дважды щелкните фрагмент или выберите фрагмент из захваченных и нажмите клавишу TAB или ВВОД.  
  
## См. также:  
 [Вставка фрагментов кода окружения Transact-SQL](../../relational-databases/scripting/insert-surround-with-transact-sql-snippets.md)  
  
  