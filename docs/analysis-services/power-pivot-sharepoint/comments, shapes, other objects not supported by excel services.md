---
title: "Следующие объекты не поддерживаются службой Excel Services и могут не отображаться совсем или отображаться лишь частично: комментарии, фигуры или другие объекты. | Microsoft Docs"
ms.custom: ""
ms.date: "03/23/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: ade92e15-dfbf-496b-9378-a00bd83ba750
caps.latest.revision: 6
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Следующие объекты не поддерживаются службой Excel Services и могут не отображаться совсем или отображаться лишь частично: комментарии, фигуры или другие объекты.
  Эта ошибка происходит, когда вы добавляете срезы в книгу [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] из списка полей [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)].  
  
## Сведения  
  
|||  
|-|-|  
|Область применения|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] для SharePoint|  
|Номер версии продукта|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|Причина|Excel Web Access не может обработать объект "Фигура", который используется для управления расположением и форматированием срезов, добавленных в книгу из списка полей [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)].|  
|Текст сообщения|Следующие объекты не поддерживаются службой Excel Services и могут не отображаться совсем или отображаться лишь частично:<br /><br /> комментарии, фигуры или другие объекты.<br /><br /> Некоторые функции, например запросы внешних данных, отображают данные из кэша, которые можно обновить только в Microsoft Excel.|  
  
## Объяснение  
 Excel Web Access отображает эту ошибку при открытии книги [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] в браузере и нажатии кнопки **Сведения** для сообщения **Неподдерживаемые функции. Эта книга может отображаться ненадлежащим образом**.  
  
 Эта ошибка возникает потому, что книга [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] содержит срезы, параметры которых управляются скрытым объектом "Фигура" в Excel. Объект «Фигура» отвечает за форматирование и расположение срезов по горизонтали и вертикали.  
  
 Служба Excel Services не может обработать объект «Фигура» для отображения, но, поскольку объект является скрытым, тот факт, что он не отображается, не является проблемой.  
  
## Действие пользователя  
 Эту ошибку можно пропускать. Нажмите кнопку **ОК**, чтобы закрыть сообщение об ошибке и продолжить использовать книгу и срезы без проблем.  
  
  