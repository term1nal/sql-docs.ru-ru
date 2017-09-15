---
title: "Функция var (построитель отчетов и службы SSRS) | Документы Microsoft"
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
ms.assetid: 7b2018ce-c5f9-4f8b-bd44-4201379a584b
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 33107c7bd4fd2b55b2301beb7cb45ce1c81dc667
ms.contentlocale: ru-ru
ms.lasthandoff: 08/09/2017

---
# <a name="report-builder-functions---var-function"></a>Функция Var в функции построителя - отчета
  Возвращает дисперсию всех числовых значений, отличных от NULL, заданных выражением, вычисляемым для данной области.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
Var(expression, scope, recursive)  
```  
  
#### <a name="parameters"></a>Параметры  
 *expression*  
 (**Integer** или **Float**) Выражение, к которому применяется статистическая обработка.  
  
 *область*  
 (**String**) Необязательно. Константа, являющаяся именем набора данных, группирования или области данных, содержащих элементы отчета, к которым применяется агрегатная функция. Если аргумент *scope* не задан, используется текущая область.  
  
 *рекурсивные*  
 (**Перечислимый тип**) Необязательно. **Simple** (по умолчанию) или **RdlRecursive**. Указывает, нужно ли выполнять статистическую обработку рекурсивно.  
  
## <a name="return-type"></a>Тип возвращаемых данных  
 Возвращает значение типа **Decimal** для десятичных выражений и **Double** — для всех остальных выражений.  
  
## <a name="remarks"></a>Замечания  
 Данные в наборе, указанном в выражении, должны иметь один и тот же тип. Чтобы преобразовать данные, имеющие разные числовые типы, к одному и тому же типу, используйте функции преобразования, такие как **CInt**, **CDbl** или **CDec**. Дополнительные сведения см. в разделе [Функции преобразования типов](http://go.microsoft.com/fwlink/?LinkId=96142).  
  
 Значение *scope* должно быть строковой константой и не может быть выражением. Для внешних агрегатов и агрегатов, в которых не задаются другие агрегаты, параметр *scope* должен ссылаться не текущую область или включающую область. Для агрегатов, содержащих агрегаты, во вложенных агрегатах может указываться дочерняя область.  
  
 *Expression* может содержать вызовы вложенных агрегатных функций со следующими условиями и исключениями.  
  
-   Параметр*Scope* для вложенных агрегатов должен совпадать с областью внешнего агрегата или входить в нее. Одна область из всех уникальных областей в выражении должна быть дочерней относительно всех других областей.  
  
-   Параметр*Scope* для вложенных агрегатов не может быть именем набора данных.  
  
-   *Expression* не может содержать функции **First**, **Last**, **Previous**и **RunningValue** .  
  
-   *Expression* не может содержать вложенные агрегаты, в которых указан параметр *recursive*.  
  
 Дополнительные сведения см. в разделах [Справочник по агрегатным функциям (построитель отчетов и службы SSRS)](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md) и [Область выражения для суммирования, агрегатных функций и встроенных коллекций (построитель отчетов и службы SSRS)](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
 Дополнительные сведения о рекурсивных агрегатах см. в разделе [Создание групп рекурсивной иерархии (построитель отчетов и службы SSRS)](../../reporting-services/report-design/creating-recursive-hierarchy-groups-report-builder-and-ssrs.md).  
  
## <a name="example"></a>Пример  
 В следующем примере кода показана дисперсия сумм элементов строк в группировании `Order` или области данных:  
  
```  
=Var(Fields!LineTotal.Value, "Order")  
```  
  
## <a name="see-also"></a>См. также  
 [Использование выражений в отчетах &#40; Построитель отчетов и службы SSRS &#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Примеры выражений &#40; Построитель отчетов и службы SSRS &#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Типы данных в выражениях &#40; Построитель отчетов и службы SSRS &#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [Область выражения для итогов, статистические выражения и встроенных коллекций &#40; Построитель отчетов и службы SSRS &#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  