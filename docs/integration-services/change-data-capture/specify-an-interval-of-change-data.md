---
title: "Задание интервала для информации об изменениях данных | Microsoft Docs"
ms.custom: ""
ms.date: "03/13/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "добавочная загрузка [службы Integration Services], указание интервала"
ms.assetid: 17899078-8ba3-4f40-8769-e9837dc3ec60
caps.latest.revision: 30
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 30
---
# Задание интервала для информации об изменениях данных
  Первой задачей в потоке управления пакета служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , который выполняет добавочную загрузку информации об измененных данных, является вычисление конечных точек интервала изменений. Эти конечные точки имеют значения **datetime** и сохраняются в переменных пакета для дальнейшего использования в пакете.  
  
> [!NOTE]  
>  Описание общего процесса по проектированию потока управления см. в разделе [Система отслеживания измененных данных (SSIS)](../../integration-services/change-data-capture/change-data-capture-ssis.md).  
  
## Настройка переменных пакета для конечных точек  
 Прежде чем настраивать задачи «Выполнение SQL» для вычисления конечных точек, необходимо определить переменные пакета, в которых будут храниться конечные точки.  
  
#### Настройка переменных пакета  
  
1.  В среде [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]откройте новый проект служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
2.  В окне **Переменные** создайте следующие переменные:  
  
    1.  Создайте переменную с типом данных **datetime** для хранения начальной точки интервала.  
  
         В этом примере используется имя переменной ExtractStartTime.  
  
    2.  Создайте переменную с типом данных **datetime** для хранения конечной точки интервала.  
  
         В этом примере используется имя переменной ExtractEndTime.  
  
 Если конечные точки вычисляются в главном пакете, который управляет несколькими дочерними пакетами, можно использовать конфигурации переменных родительского пакета, чтобы передать значения этих переменных каждому дочернему пакету. Дополнительные сведения см. в разделах [Задача "Выполнение пакета"](../../integration-services/control-flow/execute-package-task.md) и [Использование значений переменных и параметров в дочернем пакете](../../integration-services/packages/use-the-values-of-variables-and-parameters-in-a-child-package.md).  
  
## Вычисление начальной и конечной точек для измененных данных  
 Когда переменные пакета для конечных точек интервала настроены, можно вычислить фактические значения конечных точек и сопоставить эти значения с соответствующими переменными пакета. Поскольку конечные точки имеют значения **datetime** , необходимо использовать функции, поддерживающие вычисление или обработку значений **datetime** . Язык выражений служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] и язык Transact-SQL имеют функции, работающие со значениями **datetime**:  
  
 Функции языка выражений служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], работающие со значениями **datetime**  
 -   [DATEADD (выражение служб SSIS)](../../integration-services/expressions/dateadd-ssis-expression.md)  
  
-   [DATEDIFF (выражение служб SSIS)](../../integration-services/expressions/datediff-ssis-expression.md)  
  
-   [DATEPART (выражение служб SSIS)](../../integration-services/expressions/datepart-ssis-expression.md)  
  
-   [DAY (выражение служб SSIS)](../../integration-services/expressions/day-ssis-expression.md)  
  
-   [GETDATE (выражение служб SSIS)](../../integration-services/expressions/getdate-ssis-expression.md)  
  
-   [GETUTCDATE (выражение служб SSIS)](../../integration-services/expressions/getutcdate-ssis-expression.md)  
  
-   [MONTH (выражение служб SSIS)](../../integration-services/expressions/month-ssis-expression.md)  
  
-   [YEAR (выражение служб SSIS)](../../integration-services/expressions/year-ssis-expression.md)  
  
 Функции языка Transact-SQL, работающие со значениями **datetime**  
 [Типы данных и функции даты и времени (Transact-SQL)](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).  
  
 Прежде чем использовать какую-либо из этих функций **datetime** для вычисления конечных точек, необходимо определить, является ли интервал фиксированным и регулярно повторяющимся. Обычно требуется регулярное применение изменений, произошедших в исходных таблицах, к целевым таблицам. Например, эти изменения могут применяться каждый час, ежедневно или еженедельно.  
  
 Когда характер интервала изменений установлен (фиксированный или случайный), можно вычислять конечные точки.  
  
-   **Вычисление начальной даты и времени**. В качестве текущей начальной даты и времени используется конечная дата и время предыдущей загрузки. Если для добавочных загрузок используется фиксированный интервал, значение можно вычислить с помощью функций **datetime** языка Transact-SQL или языка выражений служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. В других случаях иногда приходится сохранять конечные точки между выполнениями и использовать задачи «Выполнение SQL» или «Скрипт» для загрузки предыдущей конечной точки.  
  
-   **Вычисление конечной даты и времени**. Если для добавочной загрузки используется фиксированный интервал, текущая конечная дата и время вычисляются как смещение относительно начальной даты и времени. Это значение можно также вычислить с помощью функций **datetime** языка Transact-SQL или языка выражений служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 В следующей процедуре используется фиксированный интервал изменений и предполагается, что пакет добавочной загрузки выполняется ежедневно без каких-либо исключений. Иначе информация об измененных данных за пропущенные интервалы будет потеряна. Начальной точкой интервала является полночь позавчерашнего дня, т. е. от 24 до 48 часов назад. Конечной точкой интервала является полночь вчерашнего дня, т. е. прошлая ночь, от 0 до 24 часов назад.  
  
#### Вычисление начальной и конечной точек интервала отслеживания  
  
1.  На вкладке **Поток управления** в конструкторе служб [!INCLUDE[ssIS](../../includes/ssis-md.md)] добавьте в пакет задачу «Выполнение SQL».  
  
2.  Откройте **Редактор задачи «Выполнение SQL»**и на странице **Общие** выберите следующие параметры:  
  
    1.  Для параметра **ResultSet**выберите значение **Одна строка**.  
  
    2.  Настройте допустимое соединение с базой данных-источником.  
  
    3.  Для параметра **SQLSourceType**выберите значение **Прямой ввод**.  
  
    4.  В поле **SQLStatement**введите приведенную ниже инструкцию SQL:  
  
        ```  
        SELECT DATEADD(dd,0, DATEDIFF(dd,0,GETDATE()-1)) AS ExtractStartTime,  
          DATEADD(dd,0, DATEDIFF(dd,0,GETDATE())) AS ExtractEndTime  
  
        ```  
  
3.  На странице **Результирующий набор** **Редактора задачи «Выполнение SQL»**сопоставьте результат ExtractStartTime с переменной ExtractStartTime пакета, а результат ExtractEndTime — с переменной ExtractEndTime пакета.  
  
    > [!NOTE]  
    >  Если для установки значения переменной служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] используется выражение, это выражение вычисляется при каждом обращении к значению переменной.  
  
## Следующий шаг  
 После вычисления начальной и конечной точек диапазона изменений необходимо определить, готовы ли измененные данные.  
  
 **Следующий раздел:** [Определение готовности информации об изменениях данных](../../integration-services/change-data-capture/determine-whether-the-change-data-is-ready.md)  
  
## См. также  
 [Использование переменных в пакетах](../Topic/Use%20Variables%20in%20Packages.md)   
 [Выражения служб Integration Services (SSIS)](../../integration-services/expressions/integration-services-ssis-expressions.md)   
 [Задача «Выполнение SQL»](../../integration-services/control-flow/execute-sql-task.md)   
 [Задача «Скрипт»](../../integration-services/control-flow/script-task.md)  
  
  