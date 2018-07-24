---
title: Контейнер "Цикл по элементам" | Документы Майкрософт
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.forloopcontainerdetails.f1
helpviewer_keywords:
- repeating control flow
- containers [Integration Services], For Loop
- For Loop containers
ms.assetid: 44cf7355-992b-4bbf-a28c-bfb012de06f6
caps.latest.revision: 53
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 15e2239a7285e4d460e4fa5a85add8445f797ede
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2018
ms.locfileid: "37227854"
---
# <a name="for-loop-container"></a>Контейнер «цикл по элементам»
  Контейнер «цикл по элементам» определяет повторяющийся поток управления в пакете. Управление циклом аналогично структуре цикла **For** в языках программирования. В ходе каждого повтора цикла контейнер цикла For, вычисляет выражение и повторяет рабочий процесс, пока выражение не примет значение `False`.  
  
 Контейнер "цикл по элементам" использует следующие элементы для определения цикла:  
  
-   дополнительное выражение инициализации, в котором присваиваются значения счетчикам цикла;  
  
-   выражение вычисления, содержащее выражение, которое используется для проверки необходимости продолжения или остановки цикла;  
  
-   дополнительное выражение итерации, которое увеличивает или уменьшает счетчик цикла.  
  
 На следующей диаграмме показан контейнер «цикл по элементам» с задачей «Отправка почты». Если выражение инициализации равно `@Counter = 0`, выражение вычисления равно `@Counter < 4`, а выражение итерации равно `@Counter = @Counter + 1`, то цикл повторяется четыре раза, после чего отправляет четыре электронных сообщения.  
  
 ![Контейнер "Цикл по элементам" повторяет задачу четыре раза](../media/ssis-forloop.gif "Контейнер \"Цикл по элементам\" повторяет задачу четыре раза")  
  
 Выражения должны являться допустимыми выражениями служб [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 Для создания выражений инициализации и присваивания можно использовать оператор присваивания (=). Этот оператор не поддерживается грамматикой выражений служб Integration Services и может быть использован в контейнере «цикл по элементам» только в выражениях инициализации и присваивания. Любое выражение, использующее оператор присваивания, должно содержать выражение синтаксиса `@Var = <expression>`, где **Var** является переменной выполнения, а \<expression> — это выражение, соответствующее правилам синтаксиса выражения служб [!INCLUDE[ssIS](../../../includes/ssis-md.md)]. Выражение может содержать переменные, литералы и другие операторы и функции, которые поддерживаются грамматикой выражений служб SSIS. Выражение должно возвращать тип данных, который может быть приведен к типу данных переменной.  
  
 Контейнер «цикл по элементам» может содержать только одно выражение вычисления. Это означает, что контейнер «цикл по элементам» выполняет все элементы потока управления одинаковое количество раз. Ввиду того, что контейнер «цикл по элементам» может включать другие контейнеры «цикл по элементам», в пакетах можно создавать вложенные циклы и сложные циклы выполнения.  
  
 Можно устанавливать свойство транзакции для контейнера «цикл по элементам», чтобы определить транзакцию для вложенного набора пакета потока управления. Таким образом, возможно выполнение транзакции на более детальном уровне. Например, если контейнер «цикл по элементам» несколько раз повторяет выполнение потока управления для обновления данных, можно настроить «цикл по элементам» и его поток управления с использованием транзакции, чтобы в случае неполного обновления данных обновление вообще не было произведено. Дополнительные сведения см. в разделе [Транзакции служб Integration Services](../integration-services-transactions.md).  
  
## <a name="configuration-of-the-for-loop-container"></a>Настройка контейнера «цикл по элементам»  
 Значения свойств можно задавать с помощью конструктора [!INCLUDE[ssIS](../../../includes/ssis-md.md)] или программными средствами.  
  
 Дополнительные сведения о свойствах, которые можно задать в конструкторе служб [!INCLUDE[ssIS](../../../includes/ssis-md.md)] , см. в следующих разделах:  
  
-   [Редактор циклов по элементам](../for-loop-editor.md)  
  
-   [Страница "Выражения"](../expressions/expressions-page.md)  
  
 Дополнительные сведения о задании этих свойств программными средствами см. в документации по классу **T:Microsoft.SqlServer.Dts.Runtime.ForLoop** в руководстве для разработчиков.  
  
## <a name="related-tasks"></a>Related Tasks  
 Сведения о настройке контейнера «цикл по элементам» см. в следующих разделах.  
  
-   [Настройка контейнера "цикл по элементам"](for-loop-container.md)  
  
-   [Задание свойств задач или контейнеров](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="see-also"></a>См. также  
 [Поток управления](control-flow.md)   
 [Выражения служб Integration Services (SSIS)](../expressions/integration-services-ssis-expressions.md)  
  
  