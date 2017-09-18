---
title: "Тестирование взаимодействия приложений | Документы Microsoft"
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
- interoperability [ODBC], testing interoperable applications
- testing interoperable applications [ODBC]
ms.assetid: 489083cb-8430-40be-9ef2-d75b9a2eea88
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d36c443cb6bc4a189006a3d63e90deead3f11e66
ms.contentlocale: ru-ru
ms.lasthandoff: 09/09/2017

---
# <a name="testing-interoperable-applications"></a>Тестирование приложений с возможностью взаимодействия
Тестирование приложений с возможностью взаимодействия в самом лучшем много бизнес- и в худшем случае невозможно, так как постоянно появляются новые драйверы на рынке. Тем не менее возможна разумного степень тестирования. Приложений с помощью ограниченного или очень маленькими взаимодействия требуется проверены только в те драйверы, которые они гарантированно поддерживают. Тем не менее они должны быть полностью проверены в эти драйверы.  
  
 Возможность взаимодействия приложений не удается проверить практически для всех драйверов. Что делать, большинство разработчиков приложений — проверить их полностью для небольшое количество драйверов и cursorily еще несколько. Протестированные драйверы должны содержать наиболее популярных драйверы для наиболее распространенных СУБД на рынке приложения; Если рынке охватывает все СУБД, необходимо протестировать драйверы для настольных компьютеров и серверов СУБД.  
  
 Одна из проблем при тестировании приложения ODBC — количество компоненты, участвующие: само приложение, диспетчер драйверов, драйвер, СУБД и возможно сетевое программное обеспечение или шлюзы. Приложения можно упростить его для отслеживания ошибок, выдавая сообщения об ошибках, возвращаемых функциями ODBC через **SQLGetDiagField** и **SQLGetDiagRec**. Эти сообщения определить изготовителя и компонентов, в которых возникают ошибки. Дополнительные сведения см. в разделе [диагностики](../../../odbc/reference/develop-app/diagnostics.md).