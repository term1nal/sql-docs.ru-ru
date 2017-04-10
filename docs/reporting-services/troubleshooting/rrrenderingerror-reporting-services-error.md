---
title: "rrRenderingError - Ошибка службы Reporting Services | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "rrRenderingError"
ms.assetid: 0751efc3-b81b-44ee-8aac-8560f86ca322
caps.latest.revision: 26
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 26
---
# rrRenderingError - Ошибка службы Reporting Services
    
## Сведения  
  
|||  
|-|-|  
|Название продукта|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|Идентификатор события|rrRenderingError|  
|Источник события|Microsoft.ReportingServices.Diagnostics.Utilities.ErrorStrings.resources.Strings|  
|Компонент|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|  
|Текст сообщения|Во время подготовки отчета к просмотру произошла ошибка. (rrRenderingError) %1|  
  
## Объяснение  
 Это сообщение возвращается, когда службам [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] не удается подготовить к просмотру или экспортировать отчет.  
  
 Сообщение о неподдерживаемом размере обычно возникает, если указан недопустимый размер страницы на языке определения отчетов. Укажите допустимый в языке определения отчетов размер страницы и повторите попытку.  
  
 Сообщение о неподдерживаемой единице измерения размера в языке определения отчетов обычно возникает, если указан недопустимый тип единиц измерения. Допустимы следующие типы единиц измерения: см, дюйм, мм, пика и пункт. Укажите допустимый тип единиц измерения и повторите попытку.  
  
 Сообщение о том, что отрицательный размер не поддерживается, обычно возникает при вводе отрицательного размера страницы, например -5 см. Укажите положительное число для размера страницы и повторите попытку.  
  
 Сообщение о том, что размер в языке определения отчетов находится вне допустимого диапазона, обычно возникает, если размер страницы находится за пределами допустимого размера полей. Введите размер страницы в пределах допустимых размеров полей.  
  
 Сообщение о том, что цвет не поддерживается, обычно возникает, если на языке определения отчетов указан недопустимый. Выберите цвет, поддерживаемый языком определения отчетов, и повторите попытку.  
  
 Сообщение о том, что метка действия необязательна только при использовании единичного действия (а при добавлении нескольких действий для каждого из них необходима своя метка), обычно возникает, если метка действия указана и недопустима. Укажите допустимую метку для каждого действия.  
  
 Сообщение о том, что аргумент стиля должен иметь определенный тип, обычно возникает, если введено неверное значение стиля для типа данных. Спецификация языка определения отчетов определяет допустимые типы, которые можно использовать в качестве значений стиля различных элементов языка определения отчетов. Например, значение «2pt» является недопустимым для цвета фона, а значение «true» неверно для высоты. Укажите правильное значение и повторите попытку.  
  
 Сообщение о том, что стиль границ не поддерживается, обычно возникает, если указан недопустимый стиль границ. Укажите поддерживаемый стиль границ и повторите попытку.  
  
 Сообщение о том, что тип MIME для рисунка не поддерживается, обычно возникает, если введен недопустимый тип MIME для элемента-изображения отчета. Укажите поддерживаемый тип MIME для элемента отчета и повторите попытку.  
  
 Сообщение о том, что количество строк превышает допустимое максимальное количество строк на страницу, обычно возникает, если превышено количество строк на листе Excel. Программа Excel поддерживает до 65 000 строк.  
  
 Сообщение о том, что количество столбцов превышает допустимое максимальное количество столбцов на страницу, обычно возникает, если превышено количество столбцов на листе Excel.  
  
## Действие пользователя  
  
## Только для внутреннего использования  
  