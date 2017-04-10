---
title: "Скрытие элемента (построитель отчетов и службы SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rtp.rptdesigner.shared.visibility.f1"
  - "10503"
ms.assetid: 9d78f8de-959b-456f-8947-687fa6e2ba91
caps.latest.revision: 7
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 7
---
# Скрытие элемента (построитель отчетов и службы SSRS)
  Если необходимо скрывать элемент в зависимости от параметра отчета или другого указанного выражения, то можно настроить видимость для этого элемента отчета.  
  
 Отчет можно разработать таким образом, чтобы позволить пользователям переключать видимость элементов отчета, щелкая текстовые поля, например, для вывода отчета с углубленной детализацией. Дополнительные сведения см. в разделе [Добавление действия "Развернуть" или "Свернуть" к элементу (построитель отчетов и службы SSRS)](../../reporting-services/report-design/add-an-expand-or-collapse-action-to-an-item-report-builder-and-ssrs.md).  
  
 В следующих процедурах показывается, как можно скрыть или отобразить элемент отчета, готового для просмотра, на основе значения константы или выражения.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### Скрытие элемента отчета  
  
1.  В представлении конструктора отчетов щелкните правой кнопкой мыши элемент отчета и откройте страницу **Свойства**.  
  
    > [!NOTE]  
    >  Для выбора целой таблицы или матричной области данных щелкните в области данных, чтобы выбрать ее, затем щелкните правой кнопкой мыши маркер строки или столбца либо угловой маркер и выберите пункт **Свойства табликса**.  
  
2.  Нажмите кнопку **Видимость**.  
  
3.  В поле **При первом запуске отчета**укажите, следует ли скрыть элемент при первом просмотре отчета.  
  
    -   Чтобы отобразить элемент, щелкните **Показать**.  
  
    -   Чтобы скрыть его, щелкните **Скрыть**.  
  
    -   Чтобы указать выражение, которое будет вычисляться во время выполнения, щелкните **Отображать или скрывать в зависимости от выражения**. Введите выражение или нажмите кнопку (**fx**), чтобы создать выражение в диалоговом окне **Выражение**.  
  
        > [!NOTE]  
        >  Когда вы определяете выражения для видимости, вы настраиваете свойство Hidden элемента отчета, как показано на следующем изображении. Данное вычисляемое выражение отображает элемент отчета, если значение равно False и скрывает его, если значение равно True.   
        > ![Свойства_Диалоговое окно видимости и скрытые свойства](../../reporting-services/report-builder/media/hiddenproperty-propertiesvisibility.png "Свойства_Диалоговое окно видимости и скрытые свойства")  
  
4.  Дважды нажмите кнопку **ОК** .  
  
### Скрытие статических строк в таблице, матрице или списке  
  
1.  В представлении конструктора отчетов щелкните таблицу, матрицу или список, чтобы показать маркеры строк и столбцов.  
  
2.  Щелкните правой кнопкой мыши маркер строки и выберите пункт **Видимость строки**. Откроется диалоговое окно **Видимость строки** .  
  
3.  Чтобы настроить видимость, выполните шаги 3 и 4 первой процедуры.  
  
### Скрытие статических столбцов в таблице, матрице или списке  
  
1.  В режиме конструктора выберите таблицу, матрицу или список, чтобы показать маркеры строк и столбцов.  
  
2.  Щелкните правой кнопкой мыши маркер столбца и выберите пункт **Видимость столбца**.  
  
3.  В диалоговом окне **Видимость столбца** повторите шаги 3 и 4 первой процедуры.  
  
## См. также  
 [Действие детализации (построитель отчетов и службы SSRS)](../../reporting-services/report-design/drilldown-action-report-builder-and-ssrs.md)   
 [Добавление действия "Развернуть" или "Свернуть" к элементу (построитель отчетов и службы SSRS)](../../reporting-services/report-design/add-an-expand-or-collapse-action-to-an-item-report-builder-and-ssrs.md)   
 [Примеры выражений (построитель отчетов и службы SSRS)](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)  
  
  