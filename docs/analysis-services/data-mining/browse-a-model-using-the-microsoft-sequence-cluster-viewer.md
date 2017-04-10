---
title: "Просмотр модели с помощью средства просмотра кластеризации последовательностей (Майкрософт) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "средство просмотра кластеризации последовательностей"
  - "кластеры [службы Analysis Services]"
  - "интеллектуальный анализ данных [службы Analysis Services], последовательности"
  - "сравнение [службы Analysis Services]"
  - "содержимое модели интеллектуального анализа данных, просмотр"
  - "модели интеллектуального анализа данных [службы Analysis Services], последовательности"
  - "средство просмотра кластеризации последовательностей (Microsoft)"
  - "последовательность [службы Analysis Services]"
  - "переходы [службы Analysis Services]"
ms.assetid: 3ada00aa-da9e-488a-9f53-c3e188f81f84
caps.latest.revision: 38
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 38
---
# Просмотр модели с помощью средства просмотра кластеризации последовательностей (Майкрософт)
  В средстве просмотра кластеризации последовательностей [!INCLUDE[msCoName](../../includes/msconame-md.md)] в службах [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] отображаются модели интеллектуального анализа, построенные с использованием алгоритма кластеризации последовательностей [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Этот алгоритм [!INCLUDE[msCoName](../../includes/msconame-md.md)] является алгоритмом анализа последовательностей для исследования данных, содержащих события, которые могут быть связаны с помощью следования путям или *последовательностям*. Дополнительные сведения об этом алгоритме см. в статье [Алгоритм кластеризации последовательностей (Майкрософт)](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm.md).  
  
> [!NOTE]  
>  Чтобы просмотреть подробные сведения об использованных в модели уравнениях и обнаруженных закономерностях, используйте средство просмотра деревьев содержимого общего вида [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Дополнительные сведения см. в разделах [Просмотр модели в средстве просмотра деревьев содержимого общего вида (Майкрософт)](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md) и [Средство просмотра деревьев содержимого общего вида (Майкрософт) (интеллектуальный анализ данных)](../Topic/Microsoft%20Generic%20Content%20Tree%20Viewer%20\(Data%20Mining\).md).  
  
> [!NOTE]  
>  Это средство просмотра кластеризации последовательностей [!INCLUDE[msCoName](../../includes/msconame-md.md)] предоставляет функции и параметры, подобные средству просмотра кластеризации [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Дополнительные сведения см. в разделе [Просмотр модели с помощью средства просмотра кластеров (Майкрософт)](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-cluster-viewer.md).  
  
##  <a name="BKMK_ViewerTabs"></a> Вкладки средства просмотра  
 При просмотре модели интеллектуального анализа данных в службах [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]модель отображается на вкладке **Средство просмотра моделей интеллектуального анализа данных** конструктора интеллектуального анализа данных с использованием соответствующего средства просмотра для данной модели. Средство просмотра кластеризации последовательностей [!INCLUDE[msCoName](../../includes/msconame-md.md)] содержит следующие вкладки для использования при исследовании моделей интеллектуального анализа с кластеризацией последовательностей:  
  
-   [Диаграмма кластеров](#BKMK_Diagram)  
  
-   [Профили кластеров](#BKMK_Profile)  
  
-   [Характеристики кластеров](#BKMK_Characteristics)  
  
-   [Сравнения кластеров](#BKMK_Discrimination)  
  
-   [Переходы кластеров](#BKMK_Transitions)  
  
###  <a name="BKMK_Diagram"></a> Диаграмма кластеров  
 На вкладке **Диаграмма кластеров** средства просмотра кластеризации последовательностей [!INCLUDE[msCoName](../../includes/msconame-md.md)] отображаются все кластеры, присутствующие в модели интеллектуального анализа. Заливка линии, соединяющей кластеры, показывает степень их сходства. Светлая заливка или отсутствие заливки означает, что кластеры не очень схожи. Чем темнее становится линия, тем сильнее становится сходство связей. Количество линий, отображаемых в окне просмотра, можно настроить, перемещая ползунок справа от кластеров. При движении ползунка вниз отображаются только самые прочные связи.  
  
 По умолчанию тень обозначает заполнение кластера. Используя параметры **Переменная****заливки** и **Состояние**, можно выбрать, какую пару атрибута и состояния представляет заливка. Чем темнее заливка, тем сильнее распределение атрибута для конкретного состояния. Распределение уменьшается по мере того, как заливка становится светлее.  
  
 Чтобы переименовать кластер, щелкните правой кнопкой мыши его узел и выберите команду **Переименовать кластер**. Новое имя сохранится на сервере.  
  
 Чтобы скопировать видимую область диаграммы в буфер обмена, выберите пункт **Копировать представление схемы**. Чтобы скопировать диаграмму полностью, выберите пункт **Копировать всю схему**. Кроме того, можно масштабировать диаграмму кнопками **Увеличить** и **Уменьшить**или подогнать схему по ширине экрана кнопкой **Установить масштаб диаграммы по размерам окна**.  
  
 [В начало](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Profile"></a> Профили кластеров  
 Вкладка **Профили кластера** предоставляет общий вид кластеров, создаваемых алгоритмом в модели. Каждый столбец, идущий за столбцом **Заполнение** в сетке, представляет кластер, обнаруженный моделью. Строка \<атрибут>.samples представляет различные последовательности данных, имеющиеся в кластере, а в строке \<атрибут> содержится описание всех объектов, содержащихся в кластере, и их общего распределения.  
  
 Параметр **Столбцы гистограммы** управляет количеством видимых столбцов на гистограмме. Если доступно больше столбцов, чем выбрано для отображения, то наиболее важные столбцы сохраняются, а оставшиеся группируются в сегмент серого цвета.  
  
 Стандартные имена кластеров можно изменять, сделав их более описательными. Чтобы переименовать кластер, щелкните заголовок его столбца правой кнопкой мыши и выберите команду **Переименовать кластер**. Кластеры можно скрыть, выбрав **Скрыть столбец**, а также столбцы можно перетаскивать для изменения их порядка в средстве просмотра.  
  
 Чтобы открыть окно, содержащее более полное и подробное представление кластеров, дважды щелкните либо ячейку в столбце **Состояния**, либо гистограмму в средстве просмотра.  
  
 [В начало](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Characteristics"></a> Характеристики кластеров  
 Перед началом работы с вкладкой **Характеристики кластера** выберите кластер в списке **Кластер** . После выбора кластера можно просмотреть характеристики, из которых он состоит. Атрибуты, которые содержит кластер, перечислены в столбцах **Переменные** , а их состояние — в столбце **Значения** . Состояния атрибутов отсортированы в списке по важности, основанной на вероятности их появления в кластере. Вероятность отображается в столбце **Вероятность** .  
  
 [В начало](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Discrimination"></a> Сравнения кластеров  
 Вкладку **Сравнения кластеров** можно использовать, чтобы сравнить атрибуты между кластерами для определения порядка предпочтения кластеров для элементов в последовательности. Используйте списки **Кластер 1** и **Кластер 2** , чтобы выбрать кластеры для сравнения. Средство просмотра определяет наиболее важные отличия между кластерами и отображает состояния атрибутов, связанных с этими отличиями, в порядке важности. Полоса справа от атрибута показывает, какой кластер предпочтительнее, а размер полосы показывает степень предпочтения кластера.  
  
 [В начало](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Transitions"></a> Переходы кластеров  
 Выбрав вкладку **Переходы кластеров** , можно просмотреть переходы между состояниями последовательностей в выбранном кластере. Каждый узел в средстве просмотра представляет состояние столбца последовательности. Стрелка представляет переход между двумя состояниями и вероятность, связанную с этим переходом. Если переход возвращается к исходному узлу, то стрелка может указывать обратно на этот исходный узел.  
  
 Стрелка, выходящая из точки, представляет вероятность того, что узел является началом последовательности. Кончик стрелки, ведущий в пустоту, представляет вероятность того, что узел является концом последовательности.  
  
 Границу узлов можно фильтровать, используя ползунок в левой части вкладки.  
  
 [В начало](#BKMK_ViewerTabs)  
  
## См. также  
 [Задачи и инструкции средства просмотра моделей интеллектуального анализа данных](../../analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)   
 [Задачи и инструкции средства просмотра моделей интеллектуального анализа данных](../../analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)   
 [Алгоритм кластеризации последовательностей (Майкрософт)](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm.md)   
 [Средства интеллектуального анализа данных](../../analysis-services/data-mining/data-mining-tools.md)   
 [Средства просмотра моделей интеллектуального анализа данных](../../analysis-services/data-mining/data-mining-model-viewers.md)   
 [Просмотр модели с помощью средства просмотра кластеров (Майкрософт)](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-cluster-viewer.md)  
  
  