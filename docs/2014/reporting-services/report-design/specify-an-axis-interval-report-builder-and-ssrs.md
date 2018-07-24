---
title: Задание интервала оси (построитель отчетов и службы SSRS) | Документы Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ae46712d-a5bf-44c0-9929-e30ccc1e7e33
caps.latest.revision: 10
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 3c619ec718e3471eb6518f6604a65c97cb367508
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2018
ms.locfileid: "37304994"
---
# <a name="specify-an-axis-interval-report-builder-and-ssrs"></a>Задание интервала оси (построитель отчетов и службы SSRS)
  Интервал оси определяет количество меток и дополняет деления на оси. Интервалы на оси значений обеспечивают согласованное измерение точек данных на диаграмме. Однако на оси категорий эта функция возможность может вызвать отображение некоторых категорий без меток на оси. Можно указать необходимое количество интервалов в свойстве оси Interval. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] вычисляют количество интервалов во время выполнения в зависимости от данных результирующего набора. Дополнительные сведения в вычислениях интервалов оси см. в разделе [Форматирование меток оси на диаграмме (построитель отчетов и службы SSRS)](formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md).  
  
 Этот раздел неприменим для значений данных или времени на оси категорий. По умолчанию `DateTime` значения отображаются как дни. Для определения различных интервалов данных или времени, например интервал месяца или времени, необходимо отформатировать метки оси и установить отображение экземпляров типов `DateTime` вместо типов `String`. Кроме того, необходимо задать свойство Interval. Дополнительные сведения см. в разделе [Форматирование меток оси в виде значений даты или валюты (построитель отчетов и службы SSRS)](format-axis-labels-as-dates-or-currencies-report-builder-and-ssrs.md).  
  
 Это раздел неприменим к круговым, кольцевым, воронкообразным или пирамидальным диаграммам, которые не имеют осей.  
  
> [!NOTE]  
>  Ось категорий обычно является горизонтальной осью (осью X). Однако для линейчатых диаграмм ось категорий является вертикальной (осью Y).  
  
 Пример диаграммы с различными интервалами осей доступен в виде образца отчета. Дополнительные сведения о скачивании этого и других примеров отчетов см. в статье [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][Report Builder and Report Designer sample reports](http://go.microsoft.com/fwlink/?LinkId=198283).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-show-all-category-labels-on-the-x-axis"></a>Отображение всех меток категории на оси X  
  
1.  Щелкните правой кнопкой мыши ось категорий и выберите **Свойства оси**. Откроется диалоговое окно **Свойства оси** .  
  
2.  В **параметры оси**, задайте `Interval` для **1**. Отобразится каждая метка группы категории. Если требуется отобразить каждую метку группы другой категории на оси X, введите значение **2**.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
    > [!NOTE]  
    >  После установки интервала оси автоматическое присваивание меток отключается. При указании значения для интервала оси может возникнуть непредсказуемое поведение при присваивании меток в зависимости от количества категорий на оси категорий.  
  
### <a name="to-enable-a-variable-interval-calculation-on-an-axis"></a>Включение вычисления переменного интервала на оси  
  
1.  Щелкните правой кнопкой мыши по оси диаграммы, которую необходимо изменить, и выберите пункт **Свойства оси**. Откроется диалоговое окно **Свойства оси** .  
  
2.  В **параметры оси**, задайте `Interval` для **автоматически**. В диаграмме отобразится оптимальное количество меток категории, умещающееся на оси.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>См. также  
 [Форматирование диаграммы (построитель отчетов и службы SSRS)](formatting-a-chart-report-builder-and-ssrs.md)   
 [Форматирование точек данных на диаграмме &#40;построитель отчетов и службы SSRS&#41;](formatting-data-points-on-a-chart-report-builder-and-ssrs.md)   
 [Сортировка данных в области данных (построитель отчетов и службы SSRS)](sort-data-in-a-data-region-report-builder-and-ssrs.md)   
 [Диалоговое окно "Свойства оси" — "Параметры оси" (построитель отчетов и службы SSRS)](../axis-properties-dialog-box-axis-options-report-builder-and-ssrs.md)   
 [Задание логарифмической шкалы (построитель отчетов и службы SSRS)](specify-a-logarithmic-scale-report-builder-and-ssrs.md)   
 [Построение данных на вспомогательной оси (построитель отчетов и службы SSRS)](plot-data-on-a-secondary-axis-report-builder-and-ssrs.md)  
  
  