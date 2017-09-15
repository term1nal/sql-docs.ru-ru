---
title: "Изменение многоугольников, линий и отображение точек с помощью правил и аналитических данных | Документы Microsoft"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- "10538"
- "10537"
- sql13.rtp.rptdesigner.mapembeddedpolygonlayerproperties.general.f1
- MICROSOFT.REPORTDESIGNER.MAPMARKER.MARKERSTYLE
- sql13.rtp.rptdesigner.mapembeddedlinelayerproperties.general.f1
- sql13.rtp.rptdesigner.mapembeddedpointlayerproperties.general.f1
- "10531"
- "10536"
- sql13.rtp.rptdesigner.maplinelayerproperties.widthrules.f1
ms.assetid: 7f1f5584-37b4-4fa2-ae44-8988c5f0c744
caps.latest.revision: 12
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 00778c0861d701aee22b366e202c25f8be60871e
ms.contentlocale: ru-ru
ms.lasthandoff: 08/09/2017

---
# <a name="vary-polygon-line-and-point-display-by-rules-and-analytical-data"></a>Изменение параметров отображения многоугольников, линий и точек с помощью правил и аналитических данных
  Параметры отображения многоугольников, линий и точек слоя карты управляются настройками слоя, правилами для элементов слоя карты или переопределенными параметрами отдельных внедренных элементов слоя карты.  
  
 Параметры отображения применяются с определенными приоритетами, перечисленными далее от низшего к высшему.  
  
1.  Параметры, заданные для слоя многоугольников, линий или точек, применяются ко всем элементам этого слоя карты вне зависимости от того, внедрены ли они в определение отчета.  
  
2.  Параметры, заданные для правил, применяются ко всем элементам слоя карты. Все параметры визуализации данных применяются только к элементам карты, связанным с пространственными данными. Параметры визуализации данных требуют задания поля данных, на котором основаны изменения параметров отображения. Перед применением правил визуализации данных необходимо задать поля соответствия аналитических и пространственных данных. Дополнительные сведения см. в разделе [Карты (построитель отчетов и службы SSRS)](../../reporting-services/report-design/maps-report-builder-and-ssrs.md).  
  
3.  Параметры, заданные для отдельных внедренных элементов карты. Обратите внимание, что при переопределении параметров слоя изменения в определении отчета необратимы. Можно как изменять значения полей данных, так и переопределять параметры отображения для настройки внешнего вида отдельных многоугольников, линий и точек слоя.  
  
 Помимо управления отображением элементов слоя карты, можно управлять и прозрачностью слоя, что позволяет слоям, отрисованным раньше, просвечивать сквозь слои, отрисованные позже. Дополнительные сведения об изменении параметров, которые влияют на карты или слоя карты в целом, см. в разделе [Настройка данных и отображения карты или слоя карты (построитель отчетов и службы SSRS)](../../reporting-services/report-design/customize-the-data-and-display-of-a-map-or-map-layer-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="Rules"></a> Основные сведения о правилах  
 Обработчик отчетов поддерживает четыре типа правил, позволяющих автоматически настраивать параметры отображения элементов слоя карты. Правила различаются для элементов карты разных типов: многоугольников, линий и точек.  
  
-   **Многоугольники.** Различные цвета многоугольников.  
  
    -   **Центральные точки многоугольников.** Различные цвета, размеры и типы маркеров, которые отображаются в центральной точке каждого многоугольника.  
  
-   **Линии.** Различные цвета и толщины линий.  
  
-   **Точки.** Различные цвета, размеры и типы маркеров, которые отображаются в каждой точке.  
  
##  <a name="Color"></a> Основные сведения о правилах цветов  
 Правила цвета применяются для заполнения многоугольников, линий и маркеров, представляющих точки или центральные точки многоугольников, определенным цветом.  
  
 Правила цвета поддерживают четыре варианта использования.  
  
-   Применение стиля шаблона. Тема, выбранная в мастере, определяет стиль шаблона слоя. Тема задает стиль шрифта, стиль границы и палитру.  
  
-   Визуализация данных с помощью палитры цветов. Палитра указывается по имени. Обработчик отчетов задает цвет каждого элемента слоя карты, последовательно проходя по цветам палитры, а затем выбирая все более светлые оттенки каждого цвета палитры.  
  
-   Визуализация данных с помощью диапазонов цветов. Указываются начальный, средний и конечный цвета. Затем указываются параметры распределения. Обработчик отчетов использует значения параметров распределения для создания набора цветов, аналогичного используемому в карте температур. Карта температур отображает цвет, соответствующий температуре. Например, на шкале от 0 до 100 малые значения обозначаются синим цветом и представляют холод, а большие значения обозначаются красным цветом и представляют тепло.  
  
-   Визуализация данных с помощью пользовательских цветов. Указывается набор цветов. Обработчик отчетов задает цвет каждого элемента слоя карты, последовательно проходя по заданным значениям.  
  
 Палитра по умолчанию содержит белый цвет. Чтобы избежать резкого контраста между белым цветом и другими цветами палитры, задавайте в качестве начального светлый цвет из палитры.  
  
 Для отображения элементов карты, не связанных с данными, без использования цвета задайте для элементов слоя карты значение по умолчанию **Без цвета** .  
  
### <a name="color-scale"></a>Шкала цветов  
 По умолчанию все значения правила цвета отображаются в шкале цветов, а также в первой легенде. Шкала цветов предназначена для отображения одного диапазона цветов. Выберите для отображения в ней цвета, соответствующие наиболее важным данным.  
  
 Чтобы удалить ненужные значения из шкалы цветов, снимите соответствующий флажок для каждого правила цвета на каждом слое.  
  
##  <a name="Width"></a> Основные сведения о правилах толщины линии  
 Правила толщины применяются к линиям. Правила толщины поддерживают два параметра использования.  
  
-   Использование толщины линий по умолчанию. Толщина линий задается в пунктах.  
  
-   Визуализация данных с использованием толщины линий. Задается минимальная и максимальная толщина линий, поле данных, в зависимости от которого изменяется толщина, а также параметры распределения, которые применяются к данным.  
  
##  <a name="Size"></a> Основные сведения о правилах размера маркера  
 Правила размера применяются к маркерам, представляющим точки или центральные точки многоугольников. Правила размера поддерживают два варианта использования.  
  
-   Использование размера маркера по умолчанию. Размер задается в пунктах.  
  
-   Визуализация данных при помощи размера. Задается минимальный и максимальный размер маркера, поле данных, в зависимости от которого изменяется размер, а также параметры распределения, которые применяются к данным.  
  
##  <a name="Marker"></a> Основные сведения о правилах типа маркера  
 Правила типа маркера применяются к маркерам, представляющим точки или центральные точки многоугольников. Правила типа маркера поддерживают два варианта использования.  
  
-   Использование типа маркера по умолчанию. Указывается один из доступных типов маркеров.  
  
-   Визуализация данных при помощи маркеров. Указывается набор маркеров и порядок их применения. Существуют маркеры следующих типов: **Circle**, **Diamond**, **Pentagon**, **PushPin**, **Rectangle**, **Star**, **Triangle**, **Trapezoid**и **Wedge**.  
  
##  <a name="Distribution"></a> Основные сведения о параметрах распределения  
 Чтобы создать распределение значений, данные разбиваются на диапазоны. Указывается тип распределения, число поддиапазонов, а также минимальные и максимальные значения диапазонов.  
  
 В следующем списке предполагается, что имеется три элемента карты и шесть связанных с ними аналитических значений в диапазоне от 1 до 9 999 со следующими значениями: 1, 10, 200, 2000, 4777, 8999.  
  
-   **Равноинтервальный.** Создаются диапазоны, которые разбивают данные на равные интервалы. Например, три диапазона будут иметь границы 0-2999, 3000-5999, 6000-8999. Поддиапазон 1: 1, 10, 200, 500. Поддиапазон 2: 4777. Поддиапазон 3: 8999. Этот метод не учитывает распределение данных. Очень большие или очень маленькие значения могут исказить результаты распределения.  
  
-   **Равнораспределенный.** Порождаются диапазоны, которые делят данные так, что каждый диапазон содержит равное число элементов. Для данных в приведенном примере три диапазона будут иметь границы 0-10, 11-500, 501-8999. Поддиапазон 1: 1, 10. Поддиапазон 2: 200, 500. Поддиапазон 3: 4777, 8999. Этот метод может исказить распределение за счет порождения очень крупных или очень малых диапазонов.  
  
-   **Оптимальный.** Порождается распределение с автоматически сбалансированными поддиапазонами. Количество поддиапазонов определяется алгоритмом.  
  
-   **Пользовательский.** Укажите собственное количество диапазонов для управления распределением значений. Для приведенных в примере данных можно задать три диапазона: 1–2, 3–8, 9.  
  
 Значения распределения используются правилами для изменения параметров отображения элементов карты.  
  
##  <a name="Legends"></a> Основные сведения об условных обозначениях и элементах условных обозначений  
 Элементы условных обозначений автоматически создаются на основе правил, указанных для каждого слоя. Параметры правил определяют, сколько элементов создается и в каких условных обозначениях они отображаются. По умолчанию все правила добавляются в первые условные обозначения. Чтобы переместить элементы из первых условных обозначений, можно создать необходимое количество дополнительных условных обозначений и указать для каждого правила условные обозначения, которые должны отображать элементы, порождаемые этим правилом. Чтобы скрыть элементы, основанные на правиле, укажите пустое имя условных обозначений.  
  
 Для управления местом отображения условных обозначений используйте диалоговое окно «Свойства условных обозначений», которое позволяет указать положение условных обозначений относительно окна просмотра карты. Дополнительные сведения см. в разделе [Изменение условных обозначений карты, цветовой шкалы и связанных правил (построитель отчетов и службы SSRS)](../../reporting-services/report-design/change-map-legends-color-scale-and-associated-rules-report-builder-and-ssrs.md).  
  
 Условные обозначения автоматически расширяются, чтобы отобразить заголовок или текст условных обозначений. Чтобы форматировать текст элементов условных обозначений, используйте ключевые слова для условных обозначений карты и пользовательские форматы. Дополнительные сведения см. в разделе [To change the format of content in a legend](../../reporting-services/report-design/change-map-legends-color-scale-and-associated-rules-report-builder-and-ssrs.md#ChangeFormatItems).  
  
 В следующей таблице показаны примеры различных доступных форматов.  
  
|Ключевое слово и формат|Description|Пример отображения текста в условных обозначениях|  
|------------------------|-----------------|---------------------------------------------------|  
|`#FROMVALUE {C0}`|Отображает итоговое значение в формате валюты без десятичных разрядов|$400|  
|`#FROMVALUE {C2}`|Отображает итоговое значение в формате валюты с двумя десятичными разрядами.|$400,55|  
|`#TOVALUE`|Отображает действительное числовое значение поля данных.|10000|  
|`#FROMVALUE{N0} - #TOVALUE{N0}`|Отображает текущее числовое значение начала и конца диапазона.|10–790|  
  
## <a name="see-also"></a>См. также  
 [Изменение условных обозначений карты, цветовой шкалы и связанных правил (построитель отчетов и службы SSRS)](../../reporting-services/report-design/change-map-legends-color-scale-and-associated-rules-report-builder-and-ssrs.md)   
 [Maps &#40; Построитель отчетов и службы SSRS &#41;](../../reporting-services/report-design/maps-report-builder-and-ssrs.md)   
 [Мастер карт и мастер слоев карт &#40; Построитель отчетов и службы SSRS &#41;](../../reporting-services/report-design/map-wizard-and-map-layer-wizard-report-builder-and-ssrs.md)  
  
  