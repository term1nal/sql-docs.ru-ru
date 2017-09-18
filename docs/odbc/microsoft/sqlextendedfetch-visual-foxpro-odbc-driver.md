---
title: "SQLExtendedFetch (драйвер ODBC для Visual FoxPro) | Документы Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLExtendedFetch function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: b28af112-fb47-4143-b11e-3b743b2ae1b8
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 25a9e0b16551ca27a6818fcfd890e56aeabfb44b
ms.contentlocale: ru-ru
ms.lasthandoff: 09/09/2017

---
# <a name="sqlextendedfetch-visual-foxpro-odbc-driver"></a>SQLExtendedFetch (драйвер ODBC для Visual FoxPro)
> [!NOTE]  
>  Этот раздел содержит сведения по Visual FoxPro ODBC драйвера. Общие сведения об этой функции см. в соответствующем разделе [Справочник по API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Поддержка: полный  
  
 Совместимости API ODBC: Уровень 2  
  
 Аналогично [SQLFetch](../../odbc/microsoft/sqlfetch-visual-foxpro-odbc-driver.md) , но возвращает несколько строк с помощью массива для каждого столбца. Результирующий набор может прокручиваться вперед и могут выполняться обратной прокрутки, если определено как статические, не однопроходный курсор.  
  
 По умолчанию драйвер ODBC для Visual FoxPro не возвращает строк, помечаются как удаленные в таблице FoxPro. Строки помечен для удаления, но еще не удалены из таблицы, не включаются в результирующий набор курсора. Это поведение можно изменить с помощью [SET DELETED](../../odbc/microsoft/set-deleted-command.md) команды.  
  
 Дополнительные сведения см. в разделе [SQLExtendedFetch](../../odbc/reference/syntax/sqlextendedfetch-function.md) в *справочнике программиста ODBC*.