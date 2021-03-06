---
title: Определение типа измерения (мастер измерений) | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dimensionwizard.bidimensionproperties.f1
ms.assetid: 3215282a-532d-4ff2-b721-286f088967fc
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 166fae1cb6fb76587b6741b6f47449d2600bf8e8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/02/2018
ms.locfileid: "48155864"
---
# <a name="specify-dimension-type-dimension-wizard"></a>Определение типа измерения (мастер измерений)
  Для определения типа измерения и добавления атрибутов специальных типов, связанных с выбранным типом измерений к измерению, используется страница **Определение типа измерения** .  
  
> [!NOTE]  
>  Эта страница отображается, только если на странице **Выбор типа измерения** выбрано **Стандартное измерение** .  
  
## <a name="options"></a>Параметры  
 **Тип измерения**  
 Выберите тип для измерения. В следующей таблице приведен список доступных типов измерений.  
  
|Значение|Описание|  
|-----------|-----------------|  
|**Измерение счетов**|Измерения счетов содержат данные и метаданные, представляющие список счетов.<br /><br /> Дополнительные сведения об измерениях счетов см. в разделе [Создание учетной записи Finance с измерением типа "родитель-потомок"](multidimensional-models/database-dimensions-finance-account-of-parent-child-type.md).|  
|**Измерение ведомости материалов**|Измерения ведомостей материалов (или ВМ) представляют собой обычные измерения, в которых данные и метаданные представляют собой складскую или производственную информацию, например список деталей для продуктов.<br /><br /> Дополнительные сведения об обычных измерениях см. в разделе [Типы измерений](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md).|  
|**Channel**|Измерения каналов представляют собой обычные измерения, в которых данные и метаданные представляют информацию о каналах.<br /><br /> Дополнительные сведения об обычных измерениях см. в разделе [Типы измерений](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md).|  
|**Измерение валют**|Измерения валют содержат данные и метаданные, представляющие информацию о валютах.<br /><br /> Дополнительные сведения об измерениях валют см. в разделе [Создание измерения типа Currency](multidimensional-models/database-dimensions-create-a-currency-type-dimension.md).|  
|**Заказчики**|Измерения заказчиков представляют собой обычные измерения, в которых данные и метаданные представляют информацию о заказчиках или контактную информацию.<br /><br /> Дополнительные сведения об обычных измерениях см. в разделе [Типы измерений](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md).|  
|**Geography**|Измерения географии представляют собой обычные измерения, в которых данные и метаданные представляют географическую информацию, например города или почтовые индексы.<br /><br /> Дополнительные сведения об обычных измерениях см. в разделе [Типы измерений](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md).|  
|**Организации**|Измерения организаций представляют собой обычные измерения, в которых данные и метаданные представляют организационную информацию, например о сотрудниках или дочерних компаниях.<br /><br /> Дополнительные сведения об обычных измерениях см. в разделе [Типы измерений](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md).|  
|**Продукты**|Измерения продуктов представляют собой обычные измерения, в которых данные и метаданные представляют информацию о продуктах.<br /><br /> Дополнительные сведения об обычных измерениях см. в разделе [Типы измерений](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md).|  
|**Promotion**|Измерения продвижений представляют собой обычные измерения, в которых данные и метаданные представляют информацию о маркетинговом продвижении.<br /><br /> Дополнительные сведения об обычных измерениях см. в разделе [Типы измерений](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md).|  
|**Количественное измерение**|Количественные измерения представляют собой обычные измерения, в которых данные и метаданные представляют количественную информацию.<br /><br /> Дополнительные сведения об обычных измерениях см. в разделе [Типы измерений](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md).|  
|**Тарифы**|Курсовые измерения содержат данные и метаданные, представляющие данные о курсах обмена и конвертации валюты.|  
|**Regular**|Обычные измерения являются наиболее распространенным типом измерений, используемых в службах [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].<br /><br /> Дополнительные сведения об обычных измерениях см. в разделе [Типы измерений](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md).|  
|**Сценарий**|Измерения сценариев представляют собой обычные измерения, в которых данные и метаданные представляют информацию о планах или стратегическом анализе.<br /><br /> Дополнительные сведения об обычных измерениях см. в разделе [Типы измерений](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md).|  
|**Time**|Измерения времени содержат данные и метаданные, ориентированные на время.<br /><br /> Дополнительные сведения об измерениях времени см. в разделе [Создание измерения типа Date](multidimensional-models/database-dimensions-create-a-date-type-dimension.md).|  
|**Служебная программа**|Измерения программ представляют собой обычные измерения, в которых данные и метаданные представляют информацию, которая не совпадает с другими типами измерений.<br /><br /> Дополнительные сведения об обычных измерениях см. в разделе [Типы измерений](multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md).|  
  
## <a name="dimension-attributes-options"></a>Параметры атрибутов измерений  
  
> [!NOTE]  
>  Параметры в данном разделе становятся доступными, только если выбранный **Тип измерения** имеет связанные с ним специальные атрибуты. Не все типы измерений имеют связанные с ними специальные типы атрибутов.  
  
 **включить**  
 Выберите для включения типа атрибутов в измерение.  
  
 **Тип атрибута**  
 Отображает тип атрибута, связанный с типом измерений, который выбран в поле **Тип измерения**. Дополнительные сведения о типах атрибутов см. в разделе [Элемент Type (DimensionAttribute) (ASSL)](scripting/properties/type-element-dimensionattribute-assl.md).  
  
 **Атрибут измерения**  
 Выберите атрибут измерения, которому мастер измерений назначит специальный тип атрибута, отображаемый в поле **Тип атрибута**.  
  
## <a name="see-also"></a>См. также  
 [Справка F1 мастера измерений](dimension-wizard-f1-help.md)   
 [Измерения &#40;службы Analysis Services — многомерные данные&#41;](multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)   
 [Измерения в многомерных моделях](multidimensional-models/dimensions-in-multidimensional-models.md)  
  
  
