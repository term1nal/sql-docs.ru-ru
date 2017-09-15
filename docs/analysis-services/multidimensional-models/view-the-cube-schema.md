---
title: "Просмотр схемы куба | Документы Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 82fc715c-e08e-447d-8fc8-9c9005f145f0
caps.latest.revision: 8
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 7a46b1e284d2f75a22f7ac21b0353872db7108a1
ms.contentlocale: ru-ru
ms.lasthandoff: 09/01/2017

---
# <a name="view-the-cube-schema"></a>Просмотр схемы куба
  Панель **Представление источника данных** вкладки **Структура куба** в **Конструкторе кубов** отображает схему куба. Схема представляет собой набор таблиц, на основе которых созданы меры и измерения для куба. Каждая схема куба состоит из одной или более таблиц фактов и одной или более таблиц измерений, на которых основаны меры и измерения в кубе.  
  
 Панель **Представление источника данных** вкладки **Структура куба** отображает диаграмму представления источников данных, на которой основан куб. Эта диаграмма представляет собой подмножество главной диаграммы представления источников данных. Можно скрыть и показать таблицы на панели **Представление источника данных** и просмотреть любые существующие диаграммы. Однако нельзя изменить базовую схему (например, добавить новые связи или именованные запросы). Для изменения схемы используйте конструктор представления источников данных.  
  
 При создании куба диаграмма, отображенная на панели **Представление источников данных** вкладки **Структура куба** , изначально совпадает с диаграммой **Показать все таблицы** в представлении источников данных проекта или базы данных. Можно заменить эту диаграмму на существующую в представлении источника данных и внести изменения на панели **Представление источника данных** .  
  
 Пока осуществляется работа с диаграммой в **Конструкторе кубов**, команды для работы с вкладкой или любыми выделенными объектами на вкладке будут доступны в меню **Представление источника данных** . Команды для работы с вкладкой или любыми выделенными объектами доступны также через контекстное меню, появляющееся при щелчке правой кнопкой мыши. Возможные действия:  
  
-   Переключаться между форматами диаграммы и дерева.  
  
-   Упорядочивать, осуществлять поиск, отображать и скрывать таблицы.  
  
-   Показывать понятные имена.  
  
-   Переключать макеты.  
  
-   Изменять масштаб.  
  
-   Просматривать свойства.  
  
 Кроме того, можно выполнять действия, перечисленные в следующей таблице.  
  
|Чтобы|выполните следующее:|  
|--------|-------------|  
|Использовать диаграмму из представления источников данных куба|В меню **Представление источника данных** выберите пункт **Копировать диаграмму из**и щелкните диаграмму представления источников данных, которую необходимо использовать.<br /><br /> — или —<br /><br /> Щелкните правой кнопкой мыши панель **Представление источника данных** , выберите пункт **Копировать диаграмму из**и щелкните диаграмму представления источников данных, которую необходимо использовать. В результате будет создана независимая копия диаграммы, в которой можно производить любые изменения на вкладке **Построитель кубов** , не отображающиеся в первоначальной диаграмме.|  
|Показать только таблицы, используемые в кубе|В меню **Представление источника данных** выберите пункт **Показать только используемые таблицы**.<br /><br /> — или —<br /><br /> Щелкните правой кнопкой мыши панель **Представление источника данных** и выберите команду **Показать только используемые таблицы**.|  
|Изменить схему представления источников данных|В меню **Представление источника данных** выберите пункт **Изменить представление источника данных**.<br /><br /> — или —<br /><br /> Щелкните правой кнопкой мыши панель **Представление источника данных** и выберите команду **Изменить представление источника данных**.|  
  
  