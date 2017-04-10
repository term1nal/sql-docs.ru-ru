---
title: "Занятие&#160;11. Создание секций | Microsoft Docs"
ms.custom: ""
ms.date: "02/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: 92eb21a8-5fc4-4999-ad37-1332ce26431d
caps.latest.revision: 28
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Занятие&#160;11. Создание секций
На этом занятии мы создадим секции для разделения таблицы интернет-продаж на более мелкие логические части, которые могут быть обработаны (обновлены) независимо от других секций. По умолчанию каждая таблица, включенная в модель, имеет одну секцию, включающую все столбцы и строки таблицы. Для таблицы интернет-продаж нам необходимо разделить данные по годам — по одной секции на каждые пять лет.  После этого каждую секцию можно обработать независимо. Дополнительные сведения см. в разделе [Секции (табличные службы SSAS)](../analysis-services/tabular-models/partitions-ssas-tabular.md).  
  
Предполагаемое время выполнения этого занятия: **15 минут**  
  
## Предварительные требования  
Этот раздел является частью учебника по табличному моделированию, который необходимо изучать по порядку. Прежде чем выполнять задания в этом занятии, необходимо завершить предыдущее занятие: [Занятие 10. Создание иерархий](../analysis-services/lesson-10-create-hierarchies.md).  
  
## Создание секций  
  
#### Создание секций в таблице интернет-продаж  
  
1.  В конструкторе моделей щелкните таблицу **Интернет-продажи**, а затем откройте меню **Таблица** и выберите пункт **Секции**.  
  
    Откроется диалоговое окно **Диспетчер секций**.  
  
2.  В диалоговом окне **Диспетчер секций** в списке секций щелкните секцию **Интернет-продажи**.  
  
3.  В строке **Имя секции** введите новое имя **Интернет-продажи 2010**.  
  
    > [!TIP]  
    > Прежде чем переходить к следующему шагу, обратите внимание, что имена столбцов в окне «Предварительный просмотр таблицы» отображают столбцы, включенные в таблицу модели (которая отмечена флажком) с именами столбцов из источника. Это происходит, потому что окно «Предварительный просмотр таблицы» отображает столбцы из исходной таблицы, а не из таблицы модели.  
  
4.  Нажмите кнопку **Редактор запросов** чуть выше в правой части окна предварительного просмотра.  
  
    Поскольку необходимо, чтобы секция включала только строки из определенного периода, используйте предложение WHERE. Предложение WHERE можно создать только с помощью инструкции SQL.  
  
5.  В поле **Инструкция SQL** замените существующую инструкцию, вставив следующее:  
  
    ```  
    SELECT   
    [dbo].[FactInternetSales].[ProductKey],  
    [dbo].[FactInternetSales].[CustomerKey],  
    [dbo].[FactInternetSales].[PromotionKey],  
    [dbo].[FactInternetSales].[CurrencyKey],  
    [dbo].[FactInternetSales].[SalesTerritoryKey],  
    [dbo].[FactInternetSales].[SalesOrderNumber],  
    [dbo].[FactInternetSales].[SalesOrderLineNumber],  
    [dbo].[FactInternetSales].[RevisionNumber],  
    [dbo].[FactInternetSales].[OrderQuantity],  
    [dbo].[FactInternetSales].[UnitPrice],  
    [dbo].[FactInternetSales].[ExtendedAmount],  
    [dbo].[FactInternetSales].[UnitPriceDiscountPct],  
    [dbo].[FactInternetSales].[DiscountAmount],  
    [dbo].[FactInternetSales].[ProductStandardCost],  
    [dbo].[FactInternetSales].[TotalProductCost],  
    [dbo].[FactInternetSales].[SalesAmount],  
    [dbo].[FactInternetSales].[TaxAmt],  
    [dbo].[FactInternetSales].[Freight],  
    [dbo].[FactInternetSales].[CarrierTrackingNumber],  
    [dbo].[FactInternetSales].[CustomerPONumber],  
    [dbo].[FactInternetSales].[OrderDate],  
    [dbo].[FactInternetSales].[DueDate],  
    [dbo].[FactInternetSales].[ShipDate]   
    FROM [dbo].[FactInternetSales]  
    WHERE (([OrderDate] >= N'2010-01-01 00:00:00') AND ([OrderDate] < N'2011-01-01 00:00:00'))  
    ```  
  
    Эта инструкция указывает, что секция должна включать все данные из строк, в которых OrderDate относится к 2010 календарному году, согласно предложению WHERE.  
  
6.  Нажмите кнопку **Проверить**.  
  
  
#### Создание секции для 2011 года  
  
1.  В списке секций щелкните только что созданную секцию **Интернет-продажи 2010** и выполните команду **Копировать**.  
  
2.  В поле **Имя секции** введите **Интернет-продажи 2011**.  
  
3.  Для того чтобы секция включала только строки для 2011 года, замените предложение WHERE в инструкции SQL на следующее:  
  
    ```  
    WHERE (([OrderDate] >= N'2011-01-01 00:00:00') AND ([OrderDate] < N'2012-01-01 00:00:00'))  
    ```  
  
#### Создание секции для 2012 года  
  
1.  В диалоговом окне **Диспетчер секций** выберите команду **Копировать**.  
  
2.  В поле **Имя секции** введите **Интернет-продажи 2012**.  
  
3.  Для того чтобы секция включала только строки для 2012 года, замените предложение WHERE в инструкции SQL на следующее:  
  
    ```  
    WHERE (([OrderDate] >= N'2012-01-01 00:00:00') AND ([OrderDate] < N'2013-01-01 00:00:00'))  
    ```  
  
#### Создание секции для 2013 года  
  
1.  В диалоговом окне **Диспетчер секций** выберите команду **Создать**.  
  
2.  В поле **Имя секции** введите **Интернет-продажи 2013**.  
  
3.  Для того чтобы секция включала только строки для 2013 года, замените предложение WHERE в инструкции SQL на следующее:  
  
    ```  
    WHERE (([OrderDate] >= N'2013-01-01 00:00:00') AND ([OrderDate] < N'2014-01-01 00:00:00'))  
    ```  
  
#### Создание секции для 2014 года в таблице "Интернет-продажи"  
  
1.  В диалоговом окне **Диспетчер секций** выберите команду **Создать**.  
  
2.  В поле **Имя секции** введите **Интернет-продажи 2014**.  
  
3.  Для того чтобы секция включала только строки для 2014 года, замените предложение WHERE в инструкции SQL на следующее:  
  
    ```  
    WHERE (([OrderDate] >= N'2014-01-01 00:00:00') AND ([OrderDate] < N'2015-01-01 00:00:00'))  
    ```  
  
## Обработка секций  
В диалоговом окне **Диспетчер секций** обратите внимание на звездочку (**\***) рядом с именем каждой из только что созданных секций. Это означает, что секция не была обработана (обновлена). Во время создания новых секций нужно запустить операцию обработки секций или обработки таблиц для обновления данных в этих секциях.  
  
#### Обработка секций интернет-продаж  
  
1.  Нажмите кнопку **OK**, чтобы закрыть диалоговое окно **Диспетчер секций**.  
  
2.  В конструкторе моделей щелкните таблицу **Интернет-продажи**, откройте меню **Модель**, наведите указатель на пункт **Обработка** (обновление) и выберите команду **Обработать секции**.  
  
3.  Убедитесь в том, что в диалоговом окне **Обработать секции** свойство **Режим** имеет значение **Обработка по умолчанию**.  
  
4.  Установите флажок в столбце **Обработка** для каждой из пяти созданных секций и нажмите кнопку **OK**.  
  
    Если появится окно для ввода учетных данных олицетворения, введите имя пользователя и пароль в системе Windows, которые были указаны в занятии 2, шаге 6.  
  
    Откроется диалоговое окно **Обработка данных** со сведениями обработки для каждой секции. Обратите внимание, что для каждой секции передается различное количество строк. Это происходит, потому что каждая секция включает только строки для года, указанного с помощью предложения WHERE в инструкции SQL. По завершении обработки закройте диалоговое окно "Обработка данных".  
  
  
  
## Следующие шаги  
Чтобы продолжить изучение этого учебника, перейдите к следующему занятию: [Занятие 12. Создание ролей](../analysis-services/lesson-12-create-roles.md).  
  
  
  