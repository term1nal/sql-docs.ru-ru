---
title: "Использование детализации из средств просмотра моделей | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e5e065ad-c688-4c2c-8c82-7f3038e04915
caps.latest.revision: 6
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 6
---
# Использование детализации из средств просмотра моделей
  В зависимости от типа модели можно использовать детализацию из средств просмотра на вкладке **Средство просмотра модели интеллектуального анализа** в конструкторе интеллектуального анализа данных для изучения вариантов, используемых в модели интеллектуального анализа данных, либо для просмотра дополнительных столбцов в структуре интеллектуального анализа данных. Хотя многие типы моделей не поддерживают детализацию, поскольку шаблоны в этой модели нельзя напрямую связывать с конкретными вариантами, приведенные ниже типы моделей поддерживают детализацию.  
  
 Обратите внимание, что детализация в модели должна быть включена и необходимо наличие соответствующих разрешений. Функция детализации также должна быть отключена, если модель находится в необработанном состоянии независимо от того, обрабатывалась ли она раньше и есть ли в ней содержимое. Для получения данных вариантов модели с помощью детализации, кэш структуры и модели должен быть своевременно обновлен.  
  
### Использование детализация в средстве просмотра деревьев (Майкрософт)  
  
1.  В конструкторе интеллектуального анализа данных выберите модель дерева принятия решений, затем выберите **Просмотреть модель** , чтобы открыть ее в **средстве просмотра деревьев (Майкрософт)**. В среде SQL Server Management Studio щелкните правой кнопкой мыши имя модели и выберите **Обзор**.  
  
2.  Щелкните правой кнопкой мыши любой узел диаграммы дерева и выберите **Детализация**.  
  
3.  Выберите один из следующих вариантов: **Только столбцы модели** или **Столбцы модели и структуры**. Без необходимых разрешений вариант может оказаться недоступным.  
  
4.  Откроется диалоговое окно **Детализация**, в котором отобразятся данные вариантов и (или) данные структуры. В заголовке окна также будет описание, идентифицирующее узел, с которого был выполнен запрос детализации.  
  
5.  Щелкните правой кнопкой мыши в любом месте в результатах и выберите вариант **Копировать все**, чтобы сохранить результаты в буфер обмена.  
  
### Использование детализации в средстве просмотра кластеров (Майкрософт)  
  
1.  В конструкторе интеллектуального анализа данных выберите модель кластеризации, затем выберите **Просмотреть модель** , чтобы открыть ее в **средстве просмотра кластеров (Майкрософт)**. В среде SQL Server Management Studio щелкните правой кнопкой мыши имя модели и выберите **Обзор**.  
  
2.  На вкладке **Кластер** щелкните правой кнопкой мыши любой узел.  
  
3.  Выберите вариант **Детализация**, затем выберите один из следующих вариантов: **Только столбцы модели** или **Столбцы модели и структуры**. Без необходимых разрешений вариант может оказаться недоступным.  
  
4.  Откроется диалоговое окно **Детализация**, в котором отобразятся данные вариантов и (или) данные структуры. В заголовке окна также будет описание, идентифицирующее кластер для вариантов.  
  
5.  Щелкните правой кнопкой мыши в любом месте в результатах и выберите вариант **Копировать все**, чтобы сохранить результаты в буфер обмена.  
  
### Использование детализации в средстве просмотра правил взаимосвязи (Майкрософт)  
  
1.  В конструкторе интеллектуального анализа данных выберите модель связей, затем выберите **Просмотреть модель** , чтобы открыть ее в **средстве просмотра правил взаимосвязи (Майкрософт)**. В среде SQL Server Management Studio щелкните правой кнопкой мыши имя модели и выберите **Обзор**.  
  
2.  На вкладке **Правила** щелкните правой кнопкой мыши любую строку, которая представляет правило. На вкладке **Наборы элементов** щелкните любую строку, содержащую набор элементов.  
  
3.  Выберите вариант **Детализация**, затем выберите один из следующих вариантов: **Только столбцы модели** или **Столбцы модели и структуры**. Без необходимых разрешений вариант может оказаться недоступным.  
  
4.  Откроется диалоговое окно **Детализация**, в котором отобразятся данные вариантов и (или) данные структуры. В заголовке окна также содержится описание, идентифицирующее имя правила.  
  
5.  Щелкните правой кнопкой мыши в любом месте в результатах и выберите вариант **Копировать все**, чтобы сохранить все результаты вариантов в буфере обмена. Можно также выбрать вариант **Копировать** , чтобы скопировать только выбранный вариант. Если модель содержит столбец вложенной таблицы, вставляется только имя столбца вложенной таблицы. Чтобы извлечь значения данных в столбце вложенной таблицы для каждого варианта, необходимо создать запрос к содержимому модели.  
  
### Использование детализация в средстве просмотра кластеризации последовательностей (Майкрософт)  
  
1.  В конструкторе интеллектуального анализа данных выберите модель кластеризации, затем выберите **Просмотреть модель** , чтобы открыть ее в **средстве просмотра кластеров (Майкрософт)**. В среде SQL Server Management Studio щелкните правой кнопкой мыши имя модели и выберите **Обзор**.  
  
2.  На вкладке **Диаграмма кластеров** щелкните правой кнопкой мыши любой узел, представляющий кластер. На вкладке **Профили кластера** щелкните в любом месте профиль кластера либо кластер, представляющий заполнение всей модели.  
  
3.  Выберите вариант **Детализация**, затем выберите один из следующих вариантов: **Только столбцы модели** или **Столбцы модели и структуры**. Без необходимых разрешений вариант может оказаться недоступным.  
  
4.  Откроется диалоговое окно **Детализация**, в котором отобразятся данные вариантов и (или) данные структуры. В заголовке окна также будет описание, идентифицирующее кластер для вариантов.  
  
5.  Щелкните правой кнопкой мыши в любом месте в результатах и выберите вариант **Копировать все**, чтобы сохранить результаты в буфер обмена. Если модель содержит столбец вложенной таблицы, вставляется только имя столбца вложенной таблицы. Чтобы извлечь значения данных в столбце вложенной таблицы для каждого варианта, необходимо создать запрос к содержимому модели.  
  
## См. также  
 [Задачи и инструкции средства просмотра моделей интеллектуального анализа данных](../../analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)   
 [Детализация моделей интеллектуального анализа данных](../../analysis-services/data-mining/drillthrough-on-mining-models.md)   
 [Детализация структур интеллектуального анализа данных](../../analysis-services/data-mining/drillthrough-on-mining-structures.md)  
  
  