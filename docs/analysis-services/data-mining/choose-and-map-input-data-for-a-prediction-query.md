---
title: "Выбор и сопоставление входных данных для прогнозирующего запроса | Microsoft Docs"
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
helpviewer_keywords: 
  - "таблицы [службы Analysis Services], прогнозирующие запросы"
  - "прогнозирование модели интеллектуального анализа данных [службы Analysis Services], входные таблицы"
ms.assetid: 00d330a0-879d-4da0-9f29-53c288116f4d
caps.latest.revision: 16
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 16
---
# Выбор и сопоставление входных данных для прогнозирующего запроса
  Создание прогнозов на основе модели интеллектуального анализа данных обычно производится посредством передачи в модель новых данных. (Исключение составляют модели временных рядов, в которых прогнозы могут создаваться только на основании исторических данных.) Для передачи в модель новых данных убедитесь, что данные доступны в представлении источника данных. Если заранее известно, какие данные будут использоваться для прогноза, их можно включить в представление источника данных, который использовался для создания модели. В противном случае может понадобиться создать новое представление источника данных. Дополнительные сведения см. в разделе [Представления источников данных в многомерных моделях](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md).  
  
 Иногда необходимые данные могут содержаться в более чем одной таблице в соединении «один ко многим». Это происходит при использовании данных для моделей взаимосвязей или моделей кластеризации последовательностей, использующих таблицу вариантов, связанную со вложенной таблицей, которая содержит подробные сведения о продуктах или транзакциях. Если в вашей модели используется структура с таблицей вариантов и вложенной таблицей, то в данных, которые используются для прогнозирования, также должна использоваться структура с таблицей вариантов и вложенной таблицей.  
  
> [!WARNING]  
>  Добавлять новые столбцы или сопоставлять столбцы из другого представления источников данных нельзя. Выбранное представление источника данных должно содержать все столбцы, необходимые для прогнозирующего запроса.  
  
 После того как вы определили список таблиц, содержащих данные для использования в прогнозах, будет необходимо сопоставить столбцы внешних данных со столбцами в модели интеллектуального анализа данных. Например, если ваша модель прогнозирует поведение покупателей на основании демографических данных и ответов, полученных в ходе опросов, то входные данные должны содержать информацию, в целом соответствующую содержимому модели. Сопоставлять данные для каждого из столбцов не требуется, но чем больше столбцов будет сопоставлено, тем выше качество прогноза. При попытке сопоставления столбцов с различными типами данных может возникнуть ошибка. В этом случае вы можете определить именованное вычисление в представлении источника данных, чтобы привести или преобразовать тип данных нового столбца к типу, требуемому в модели. Дополнительные сведения см. в разделе [Определение именованных вычислений в представлении источника данных (службы Analysis Services)](../../analysis-services/multidimensional-models/define-named-calculations-in-a-data-source-view-analysis-services.md).  
  
 При выборе используемых для прогноза данных некоторые столбцы из выбранного источника данных могут автоматически сопоставляться со столбцами модели интеллектуального анализа данных на основе сходства имен и совпадения типов данных. Диалоговое окно **Изменение сопоставления** на вкладке **Прогнозирование моделей интеллектуального анализа данных** можно использовать для изменения существующих сопоставлений столбцов, удаления неверных сопоставлений и создания новых сопоставлений существующих столбцов. Область конструктора **Модель интеллектуального анализа данных** также поддерживает изменение соединений посредством перетаскивания.  
  
-   Чтобы создать новое соединение, просто выберите столбец в таблице **Модель интеллектуального анализа данных** и перетащите его в соответствующий столбец в таблице **Выбор входных таблиц**.  
  
-   Для удаления соединения выделите линию соединения и нажмите клавишу DELETE.  
  
 В следующей процедуре описывается изменение соединений, созданных между таблицей вариантов и вложенной таблицей, используемой в качестве входных данных для прогнозирующего запроса в диалоговом окне **Определение вложенного соединения** .  
  
### Выбор входной таблицы  
  
1.  В таблице **Выбор входных таблиц** на вкладке **Диаграмма точности интеллектуального анализа** конструктора интеллектуального анализа данных в среде [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] нажмите **Выбор таблицы вариантов**.  
  
     Откроется диалоговое окно **Выбор таблицы** , в котором можно указать таблицу, содержащую данные, на которых будут основаны запросы.  
  
2.  В диалоговом окне **Выбор таблицы** выберите источник данных из списка **Источник данных** .  
  
3.  В поле **Имя таблицы/представления** выберите таблицу, содержащую данные, с помощью которых будут проверяться модели.  
  
4.  Нажмите кнопку **ОК**.  
  
     Столбцы в структуре интеллектуального анализа данных автоматически сопоставляются со столбцами, имеющими то же имя во входной таблице.  
  
### Изменение способа сопоставления входных данных с моделью  
  
1.  В конструкторе интеллектуального анализа данных в среде [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]перейдите на вкладку **Прогнозирование моделей интеллектуального анализа данных** .  
  
2.  В меню **Модель интеллектуального анализа данных** выберите пункт **Изменить подключения**.  
  
     Откроется диалоговое окно **Изменение сопоставления** . Столбец в этом диалоговом окне, **Столбец модели интеллектуального анализа данных** , содержит список столбцов выбранной структуры интеллектуального анализа данных. В столбце **Столбец таблицы** перечисляются столбцы внешнего источника данных, выбранные в диалоговом окне **Выбор входных таблиц**. Столбцы внешнего источника данных сопоставляются столбцам модели интеллектуального анализа данных.  
  
3.  В списке **Столбцы таблицы**выберите строку, соответствующую столбцу модели интеллектуального анализа данных, сопоставление с которым нужно задать.  
  
4.  Выберите столбец из списка доступных столбцов внешнего источника данных. Выберите пустой элемент в списке, чтобы удалить сопоставление столбца.  
  
5.  Нажмите кнопку **ОК**.  
  
     Новые сопоставления столбцов отображаются в конструкторе.  
  
### Удаление связи между входными таблицами  
  
1.  В таблице **Выбор входных таблиц** на вкладке **Прогнозирование моделей интеллектуального анализа данных** в конструкторе интеллектуального анализа данных в среде [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] нажмите кнопку **Изменить соединение**.  
  
     Откроется диалоговое окно **Указание вложенного соединения** .  
  
2.  Выберите связь.  
  
3.  Нажмите кнопку **Удалить связь**.  
  
4.  Нажмите кнопку **ОК**.  
  
     Связь между таблицей вариантов и вложенной таблицей удалится.  
  
### Создание новой связи между входными таблицами  
  
1.  В таблице **Выбор входных таблиц** на вкладке **Модель интеллектуального анализа данных** в конструкторе интеллектуального анализа данных нажмите кнопку **Изменить соединение**.  
  
     Откроется диалоговое окно **Указание вложенного соединения** .  
  
2.  Нажмите кнопку **Создать связь**.  
  
     Открывается диалоговое окно **Создание связи** .  
  
3.  Выберите ключ вложенной таблицы в списке **Исходные столбцы**.  
  
4.  Выберите ключ таблицы вариантов в списке **Целевые столбцы**.  
  
5.  Нажмите кнопку **ОК** в диалоговом окне **Создание связи** .  
  
6.  Нажмите кнопку **ОК** в диалоговом окне **Указание вложенного соединения** .  
  
     Между таблицей вариантов и вложенной таблицей создастся новая связь.  
  
### Добавление вложенной таблицы во входные таблицы прогнозирующего запроса  
  
1.  На вкладке **Прогноз модели интеллектуального анализа данных** конструктора интеллектуального анализа данных нажмите кнопку **Выбрать таблицу вариантов** , чтобы открыть диалоговое окно **Выбор таблицы** .  
  
    > [!NOTE]  
    >  Вложенную таблицу невозможно добавить ко входам, пока не задана таблица вариантов. При использовании вложенной таблицы в модели интеллектуального анализа данных также обязательно должна использоваться вложенная таблица.  
  
2.  В диалоговом окне **Выбор таблицы** выберите источник данных из списка **Источник данных** и в представлении источника данных выберите таблицу, в которой содержатся данные варианта. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
3.  Нажмите кнопку **Выбрать вложенную таблицу** , чтобы открыть диалоговое окно **Выбор таблицы** .  
  
4.  В диалоговом окне **Выбор таблицы** выберите источник данных из списка **Источник данных** и в представлении источника данных выберите таблицу, в которой содержатся вложенные данные. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     Если связь уже имеется, то столбцы в модели интеллектуального анализа данных автоматически сопоставляются со столбцами, имеющими то же имя во входной таблице. Связь между вложенной таблицей и таблицей вариантов можно изменить, нажав кнопку **Изменить соединение**, после чего откроется диалоговое окно **Создание связи** .  
  
## См. также раздел  
 [Прогнозирующие запросы (интеллектуальный анализ данных)](../../analysis-services/data-mining/prediction-queries-data-mining.md)  
  
  