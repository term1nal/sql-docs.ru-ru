---
title: "окно просмотра значений | Microsoft Docs"
ms.custom: ""
ms.date: "03/23/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vs.debug.watch"
helpviewer_keywords: 
  - "окно просмотра [Transact-SQL]"
ms.assetid: 23f3baa4-14c2-4262-92f7-3f43fcfa0436
caps.latest.revision: 16
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# окно просмотра значений
  В окне **Контрольные значения** отображается информация о выбранных выражениях. Может быть открыто четыре окна контрольных значений: **Контрольные значения 1**, **Контрольные значения 2, Контрольные значения 3**и **Контрольные значения 4**. Выражения вычисляются в области текущего кадра стека вызова, который выбран в окне **Стек вызовов** . Чтобы иметь возможность контролировать значения переменных и выражений, необходимо находиться в режиме отладки.  
  
## Список задач  
 **Доступ к окнам «Контрольные значения»**  
  
-   В меню **Отладка** выберите пункт **Окна**, затем пункт **Контрольные значения**и выберите пункт **Контрольные значения 1**, **Контрольные значения 2, Контрольные значения 3**или **Контрольные значения 4**.  
  
 **Изменение значения выражения**  
  
-   Щелкните правой кнопкой мыши выражение и выберите команду **Изменить значение**.  
  
## Столбцы  
 **Название**  
 Выражения, перечисляемые отладчиком [!INCLUDE[tsql](../../includes/tsql-md.md)]. Поддерживаются следующие выражения:  
  
-   Переменные.  
  
-   Параметры.  
  
-   Системные функции, имена которых начинаются с @@.  
  
-   Выражения, построенные путем применения операторов к одной или нескольким переменным, параметрам или системным функциям, например @IntegerCounter + 1 или FirstName + LastName.  
  
-   Инструкции Transact-SQL, возвращающие единственное значение, например SELECT CharacterCol FROM MyTable WHERE PrimaryKey = 1.  
  
 **Значение**  
 Отображается значение, возвращаемое после оценки отладчиком [!INCLUDE[tsql](../../includes/tsql-md.md)] выражения, указанного в поле **Имя**.  
  
 Если длина выражения больше ширины столбца **Значение** , полное значение отображается в подсказке при перемещении указателя на ячейку **Значение** для этого выражения.  
  
 Значок лупы в ячейке **Значение** указывает, что доступен визуализатор отладчика [!INCLUDE[tsql](../../includes/tsql-md.md)] . В этом списке можно указать **Визуализатор текста**, **Визуализатор XML**или **Визуализатор HTML**. Чтобы выполнить запуск визуализатора отладчика, щелкните значок лупы. В отладчике [!INCLUDE[tsql](../../includes/tsql-md.md)] откроется диалоговое окно, в котором данные будут отображены в формате, соответствующем типу этих данных.  
  
 **Тип**  
 Отображает тип данных выражения.  
  
## См. также:  
 [Отладчик Transact-SQL](../../relational-databases/scripting/transact-sql-debugger.md)   
 [Сведения отладчика Transact-SQL](../../relational-databases/scripting/transact-sql-debugger-information.md)   
 [окно локальных переменных](../../relational-databases/scripting/locals-window.md)   
 [Окно стека вызовов](../../relational-databases/scripting/call-stack-window.md)   
 [Диалоговое окно «Быстрая проверка»](../../relational-databases/scripting/quickwatch-dialog-box.md)   
 [Выражения (Transact-SQL)](../../t-sql/language-elements/expressions-transact-sql.md)  
  
  