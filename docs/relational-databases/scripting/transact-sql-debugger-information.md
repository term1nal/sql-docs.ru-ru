---
title: "Сведения отладчика Transact-SQL | Microsoft Docs"
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
  - "отладчик Transact-SQL, окно локальных переменных"
  - "отладчик Transact-SQL, окно контрольных значений"
  - "отладчик Transact-SQL, окно потоков"
  - "отладчик Transact-SQL, окно стека вызовов"
  - "отладчик Transact-SQL, быстрая проверка"
  - "отладчик Transact-SQL, просмотр сведений"
ms.assetid: b99819cc-f388-41a1-b304-36e78ce24147
caps.latest.revision: 15
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 15
---
# Сведения отладчика Transact-SQL
  Каждый раз когда отладчик приостанавливает выполнение на определенной инструкции [!INCLUDE[tsql](../../includes/tsql-md.md)] , с текущим состоянием выполнения можно ознакомиться при помощи различных окон отладчика.  
  
## Окна отладчика  
 В режиме отладки внизу основного окна среды [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] отладчик открывает два окна. Все сведения отладчика отображаются в этих двух окнах. В каждом окне отладчика есть вкладки, определяющие, какой набор сведений отображается в данном окне. В левом окне отладчика есть вкладки **Локальные значения**, **Просмотр значений1**, **Просмотр значений2**, **Просмотр значений3**и **Просмотр значений4** . В правом окне отладчика есть вкладки **Стек вызовов**, **Потоки**, **Точки останова**, **Окно команд**и **Вывод** .  
  
> [!NOTE]  
>  В приведенном описании имеется в виду расположение окон отладчика по умолчанию. Вкладки можно перетаскивать из одного окна в другое, а также можно отменить закрепление вкладки и создать новое окно, которое можно поместить в любое место.  
  
 По умолчанию не все эти вкладки или окна активны. Нужное окно можно открыть одним из следующих способов.  
  
-   В меню **Отладка** выбрать пункт **Окна**, а затем выбрать требуемое окно.  
  
-   На панели инструментов **Отладка** нажать кнопку **Точки останова**, а затем выбрать требуемое окно.  
  
## Выражение языка Transact-SQL  
 Выражения — это предложения [!INCLUDE[tsql](../../includes/tsql-md.md)], значением которых является отдельное скалярное значение, например переменная или параметр. В левом окне отладчика могут отображаться значения данных, назначенные на текущий момент выражениям, в максимум пяти вкладках или окнах: **Локальные переменные, Контрольное значение1**, **Контрольное значение2**, **Контрольное значение3**и **Контрольное значение4**.  
  
 В окне **Локальные значения** отображаются сведения о локальных переменных в текущей области отладчика [!INCLUDE[tsql](../../includes/tsql-md.md)] . Набор выражений, которые показаны в окне **Локальные значения** , изменяется по мере прохождения отладчиком разных частей кода.  
  
 Выражения в окне **Быстрая проверка** и четырех окнах **Контрольные значения** не ограничиваются простым отображением идентификатора переменной. Можно указать выражение [!INCLUDE[tsql](../../includes/tsql-md.md)] , результатом вычисления которого является единственное значение, например добавление числа к переменной или инструкции SELECT, результатом которой будет единственное значение. Примеры включают следующее.  
  
-   Имя переменной, например @IntegerCounter.  
  
-   Арифметическая операция над переменной, например @IntegerCounter + 1.  
  
-   Строковая операция над двумя символьными переменными, например @FirstName + @LastName.  
  
-   Инструкция SELECT, возвращающая единственное значение, например SELECT CharCol FROM MyTable WHERE PrimaryKey = 1.  
  
 В окне **Контрольное значение** можно просмотреть значение выражения [!INCLUDE[tsql](../../includes/tsql-md.md)] , а затем сохранить это выражение в окно **Просмотр значений** . Чтобы выделить выражение в окне **Контрольное значение**, выберите выражение или введите его имя в поле **Выражение** .  
  
 В четырех окнах **Просмотр значений** отображаются сведения о выбранных переменных и выражениях. Набор выражений, которые показаны в окнах **Просмотр значений** , изменяется только в случае, если добавить выражения в список или удалить их из него.  
  
 Чтобы добавить выражение в окно **Просмотр значений** , можно либо нажать кнопку **Добавить контрольное значение** в диалоговом окне **Контрольное значение** , либо ввести имя выражения в столбце **Имя** пустой строки в окне **Просмотр значений** .  
  
 Задать значение данных для переменных в окнах **Локальные значения**, **Просмотр значений** или **Контрольное значение** можно, щелкнув строку правой кнопкой мыши и выбрав команду **Изменить значение**. Столбцы **Значение** в окне **Локальные значения** , окне **Просмотр значений** , а также в диалоговом окне **Контрольное значение** допускают текстовые, XML и HTML визуализаторы данных. Визуализаторы представлены как подсказка по данным в виде лупы с правой стороны столбца **Значения** . Визуализаторы можно использовать для просмотра текстовых, XML или HTML-значений данных в программах, которые соответствуют типу данных, например просматривать XML-файлы в окне браузера.  
  
 Если в режиме отладки указатель мыши навести на идентификатор, отображается всплывающее окно **Краткие сведения** с именем выражения и его текущим значением. Дополнительные сведения см. в разделе [Краткие сведения (IntelliSense)](../../relational-databases/scripting/quick-info-intellisense.md).  
  
## Точки останова  
 Окно **Точки останова** можно использовать для просмотра установленных точек останова и управления ими. Дополнительные сведения см. в разделе [Пошаговая отладка кода Transact-SQL](../../relational-databases/scripting/step-through-transact-sql-code.md).  
  
## Стеки вызовов  
 В окне **Стек вызовов** отображается текущее место выполнения, а также сведения о том, как выполнение прошло от исходного окна редактора через все модели [!INCLUDE[tsql](../../includes/tsql-md.md)] (функции, хранимые процедуры и триггеры) до текущего положения выполнения. Каждая строка в окне **Стек вызовов** называется кадром стека и представляет один из следующих элементов:  
  
-   текущее положение выполнения;  
  
-   вызов от одного модуля к другому;  
  
-   вызов от окна редактора к модулю [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
 Порядок модулей в стеке является обратным порядку, в котором модули вызывались. Текущее положение выполнения находится вверху стека, а начальный вызов — внизу. Желтая стрелка на левом краю кадра стека обозначает кадр, на котором отладчик приостанавливает выполнение.  
  
 В столбце **Имя** записываются следующие сведения.  
  
-   Исходный модуль, содержащий строку кода, которая произвела вызов следующего уровня.  
  
-   Строка кода, которая вызвала следующий модуль в стеке.  
  
-   Если была вызвана хранимая процедура или функция, которая приняла параметры, то также отображаются имена, типы данных и значения всех параметров.  
  
 Выражения в окнах **Локальные переменные**, **Контрольные значения**и **Быстрая проверка** вычисляются для текущего кадра стека. По умолчанию текущий кадр стека является верхним кадром в стеке, на котором отладчик приостановил выполнение. При указании другого кадра стека в качестве текущего выражения в окнах **Локальные переменные**, **Контрольные значения**и **Быстрая проверка** вычисляются для нового кадра стека Чтобы изменить текущий кадр стека, нужно либо дважды щелкнуть кадр, либо щелкнуть кадр и выбрать **Переключиться на фрагмент**. После этого выражения в окнах **Локальные переменные**, **Контрольные значения**и **Быстрая проверка** будут вычислены для нового кадра. Зеленая стрелка на левом краю кадра стека обозначает текущий кадр, когда он не является верхним в стеке.  
  
 Если щелкнуть кадр стека правой кнопкой мыши и выбрать пункт **К исходному коду**, код для этого кадра появится в окне редактора запросов. Однако этот кадр не становится текущим, а содержимое окон **Локальные переменные**, **Контрольные значения**и **Быстрая проверка** не изменяется.  
  
## Системные сведения и результаты Transact-SQL  
 Отладчик отображает свое состояние и сообщения о событиях в окне **Вывод** . Сюда входят такие сведения, как время прикрепления отладчика к другим процессам или время завершения потока отладчика.  
  
 Когда редактор запросов находится в режиме отладки, вкладки **Результаты** и **Сообщения** остаются активными. На вкладке **Результаты** продолжают отображаться результирующие наборы от инструкций [!INCLUDE[tsql](../../includes/tsql-md.md)] , которые выполняются во время сеанса отладки. На вкладке **Сообщения** продолжают отображаться такие сообщения, как *xx* строк затронуто, а также вывод инструкций PRINT и RAISERROR.  
  
## См. также:  
 [окно локальных переменных](../../relational-databases/scripting/locals-window.md)   
 [окно просмотра значений](../../relational-databases/scripting/watch-window.md)   
 [Диалоговое окно «Быстрая проверка»](../../relational-databases/scripting/quickwatch-dialog-box.md)   
 [Окно точек останова](../../relational-databases/scripting/breakpoints-window.md)   
 [Окно стека вызовов](../../relational-databases/scripting/call-stack-window.md)   
 [Окно потоков](../../relational-databases/scripting/threads-window.md)   
 [Окно вывода](../../relational-databases/scripting/output-window.md)   
 [Отладчик Transact-SQL](../../relational-databases/scripting/transact-sql-debugger.md)  
  
  