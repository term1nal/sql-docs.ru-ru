---
title: Выполнение хранимых процедур | Документация Майкрософт
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- ODBC, stored procedures
- stored procedures [ODBC], running
- SQL Server Native Client ODBC driver, stored procedures
- stored procedures [ODBC], executing
ms.assetid: 866b6dd3-2acd-4dfb-aeca-a0352b2d4c6a
caps.latest.revision: 35
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5275dca79f7519a64b2ace936e5f91a6961819fd
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/03/2018
ms.locfileid: "37426363"
---
# <a name="running-stored-procedures"></a>Выполнение хранимых процедур
  Хранимая процедура представляет собой исполняемый объект, хранящийся в базе данных. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] поддерживает:  
  
-   Хранимые процедуры  
  
     Одна или несколько инструкций SQL предварительно откомпилированы в одну исполняемую процедуру.  
  
-   Расширенные хранимые процедуры  
  
     Библиотеки динамических ссылок (DLL) C или C++, написанные с использованием API-интерфейса служб SQL Server Open Data Services для расширенных хранимых процедур. API-интерфейс служб Open Data Services расширяет возможности хранимых процедур, позволяя им использовать код на C или C++.  
  
 При выполнении инструкций путем вызова хранимой процедуры для источника данных (в противоположность непосредственному выполнению или подготовке инструкций в клиентском приложении) можно получить следующие преимущества.  
  
-   Более высокая производительность  
  
     Инструкции SQL анализируются и компилируются во время формирования процедур. Затем эта дополнительная нагрузка компенсируется при выполнении процедур.  
  
-   Снижение сетевых издержек  
  
     Когда вместо отправки по сети сложных запросов выполняется процедура, это способствует сокращению объема сетевого трафика. Если при выполнении хранимой процедуры приложение ODBC использует синтаксическую конструкцию ODBC {CALL}, драйвер ODBC принимает дополнительные меры по оптимизации, которые снимают необходимость преобразования данных параметров.  
  
-   Повышение уровня согласованности  
  
     Если правила организации реализованы в центральном ресурсе, таком, как хранимая процедура, их можно кодировать, тестировать и отлаживать в один прием. Затем индивидуальные программисты могут использовать эти протестированные хранимые процедуры, не разрабатывая собственных реализаций.  
  
-   Более высокая точность  
  
     Поскольку хранимые процедуры, как правило, создаются опытными программистами, они обычно бывают более эффективными и содержат меньше ошибок, нежели код, создаваемый многократно программистами различных уровней компетентности.  
  
-   Дополнительные функциональные возможности  
  
     В расширенных хранимых процедурах можно использовать средства на языках C и C++, недоступные в инструкциях [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
     Пример вызова хранимой процедуры, см. в разделе [Обработка кодов возврата и выходные параметры &#40;ODBC&#41;](../native-client-odbc-how-to/running-stored-procedures-process-return-codes-and-output-parameters.md).  
  
## <a name="in-this-section"></a>в этом разделе  
  
-   [Вызов хранимой процедуры](calling-a-stored-procedure.md)  
  
-   [Пакетная обработка вызовов хранимых процедур](batching-stored-procedure-calls.md)  
  
-   [Обработка результатов хранимой процедуры](processing-stored-procedure-results.md)  
  
## <a name="see-also"></a>См. также  
 [Собственный клиент SQL Server &#40;ODBC&#41;](../native-client/odbc/sql-server-native-client-odbc.md)   
 [Выполнение разделы руководства, посвященные хранимых процедур &#40;ODBC&#41;](../../database-engine/dev-guide/running-stored-procedures-how-to-topics-odbc.md)  
  
  