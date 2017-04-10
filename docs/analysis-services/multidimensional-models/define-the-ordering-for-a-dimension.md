---
title: "Определение упорядочивания для измерения | Microsoft Docs"
ms.custom: ""
ms.date: "03/23/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "OrderBy, свойство"
  - "измерения [службы Analysis Services], упорядочивание"
  - "расширения бизнес-аналитики [службы Analysis Services],упорядочивание"
  - "измерения [службы Analysis Services], расширения бизнес-аналитики"
  - "упорядочивание измерений [службы Analysis Services]"
  - "OrderByAttributeID, свойство"
ms.assetid: c42fbd58-244d-4e0a-b715-6f919cbc3ad9
caps.latest.revision: 31
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Определение упорядочивания для измерения
  Добавьте расширение упорядочивания атрибутов к кубу или измерению, чтобы указать, как упорядочиваются элементы атрибута. Элементы можно упорядочивать по имени или ключу атрибута, либо по имени или ключу другого атрибута (основанному на связи атрибута). По умолчанию элементы упорядочиваются по имени. Это расширение изменяет настройки свойств **OrderBy** и **OrderByAttributeID** для атрибутов в измерении.  
  
 Чтобы добавить упорядочивание атрибутов, используйте мастер бизнес-аналитики и выберите параметр **Задать сортировку атрибута** на странице **Выбор расширения** . После этого мастер отобразит шаги, позволяющие выбрать измерение, к которому необходимо применить упорядочивание атрибутов, и указать способ упорядочивания атрибутов для выбранного измерения.  
  
## Выбор измерения  
 На первой странице **Определение порядка атрибутов** мастера указывается измерение, к которому необходимо применить упорядочивание атрибутов. Добавление расширения упорядочивания атрибутов к этому выбранному измерению приведет к изменению измерения. Эти изменения будут наследоваться всеми кубами, включающими выбранное измерение.  
  
## Указание упорядочивания  
 На второй странице **Определение порядка атрибутов** мастера указывается, как будут упорядочиваться все атрибуты в измерении.  
  
 В столбце **Атрибут сортировки** можно изменить атрибут, используемый для выполнения упорядочивания. Если атрибут, который необходимо использовать для упорядочивания элементов, отсутствует в списке, то прокрутите список вниз, а затем выберите пункт **\<Создать атрибут...>**, чтобы открыть диалоговое окно **Выбор столбца**, где можно выбрать столбец в таблице измерения. При выборе столбца с использованием диалогового окна **Выбор столбца** создается дополнительный атрибут, с помощью которого необходимо упорядочивать элементы атрибута.  
  
 В столбце **Критерии** после этого можно выбрать, необходимо ли упорядочивать элементы атрибута по **Key** или **Name**.  
  
  