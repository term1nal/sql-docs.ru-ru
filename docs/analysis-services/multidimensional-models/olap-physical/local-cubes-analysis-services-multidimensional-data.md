---
title: "Локальные кубы (службы Analysis Services — многомерные данные) | Документы Microsoft"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- cubes [Analysis Services], local
ms.assetid: e52e1515-35a7-4dc3-9bbf-736d176ba0c7
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 849f17d47b443e992bd314d6ce2d2a04ec080cd6
ms.contentlocale: ru-ru
ms.lasthandoff: 09/01/2017

---
# <a name="local-cubes-analysis-services---multidimensional-data"></a>Локальные кубы (службы Analysis Services — многомерные данные)
  Для создания, обновления или удаления локальных кубов разработайте и выполните скрипт ASSL или программу AMO.  
  
 Локальные кубы и локальные модели интеллектуального анализа данных позволяют выполнять анализ на клиентской рабочей станции даже когда она не подключена к сети. Например, клиентское приложение может вызывать поставщик OLE DB для OLAP 9.0 (MSOLAP.3), который загружает локальный механизм куба и выполняет запросы к локальным кубам, как показано на приведенной ниже иллюстрации:  
  
 ![Архитектура клиента для локальных кубов и моделей](../../../analysis-services/multidimensional-models/olap-physical/media/as-localcubearch9.gif "архитектура клиента для локальных кубов и моделей")  
  
 ADMOD.NET и объекты AMO также загружают механизм куба при взаимодействии с локальными кубами. К локальному файлу куба может обращаться только один процесс, поскольку локальный механизм куба устанавливает на локальный файл куба монопольную блокировку, когда тот устанавливает соединение с локальным кубом. Разрешено не более пяти одновременных соединений для одного процесса.  
  
 Файл с расширением CUB может содержать несколько кубов или моделей интеллектуального анализа данных. Запросы к локальным кубам и моделям интеллектуального анализа данных обрабатываются локальным механизмом куба и не требуют соединения с экземпляром служб [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
> [!NOTE]  
>  Управление локальными кубами с помощью среды [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] и [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] не поддерживается.  
  
## <a name="local-cubes"></a>Локальные кубы  
 Локальный куб можно создать и заполнить на основе существующего куба в [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] экземпляра или из реляционного источника данных.  
  
|Источник данных для локального куба|Метод создания|  
|------------------------------------|---------------------|  
|Серверный куб|Можно использовать инструкцию CREATE GLOBAL CUBE или [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] скрипт языка сценариев (ASSL) для создания и наполнения куба из серверного куба. Дополнительные сведения см. в разделе [инструкция CREATE глобального КУБА &#40; Многомерные Выражения &#41; ](../../../mdx/mdx-data-definition-create-global-cube.md) или [служб Analysis Services, язык сценариев &#40; ASSL для XMLA &#41; ](../../../analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla.md).|  
|Реляционный источник данных|Для создания и наполнения куба из реляционной базы данных OLE DB используется скрипт ASSL. Для создания локального куба с помощью скрипта ASSL можно просто соединиться с локальным файлом куба (*.CUB) и выполнить скрипт ASSL, аналогичный сценарию ASSL, выполняемому на экземпляре служб [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] для создания серверного куба. Дополнительные сведения см. в разделе [Справочник по языку ASSL](../../../analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla.md).|  
  
 С помощью инструкции REFRESH CUBE можно перестроить локальный куб и обновить его данные. Дополнительные сведения см. в разделе [инструкцию обновления КУБА &#40; Многомерные Выражения &#41; ](../../../mdx/mdx-data-definition-refresh-cube.md).  
  
### <a name="local-cubes-created-from-server-based-cubes"></a>Локальные кубы, созданные на основе серверных кубов  
 При создании локальных кубов на основе серверных кубов необходимо учитывать следующие замечания:  
  
-   Меры числа различных объектов не поддерживаются.  
  
-   При добавлении меры необходимо также задать хотя бы одно измерение, связанное с добавляемой мерой. Дополнительные сведения о связях измерений с группами мер см. в разделе [связей измерений](../../../analysis-services/multidimensional-models-olap-logical-cube-objects/dimension-relationships.md).  
  
-   При добавлении иерархии типа «родители-потомки» уровни и фильтры в этой иерархии не обрабатываются, и иерархия включается целиком.  
  
-   Свойства членов не создаются.  
  
-   При включении полуаддитивных мер срезы запрещены как в измерении «Счет», так и в измерении «Время».  
  
-   Ссылочные измерения всегда материализуются.  
  
-   При добавлении измерения «многие ко многим» применяются следующие правила.  
  
    -   Нельзя делать срез измерения «многие ко многим».  
  
    -   Необходимо добавлять меры из промежуточной группы мер.  
  
    -   Нельзя делать срез любых измерений, которые являются общими для двух групп мер, входящих в связь «многие ко многим».  
  
-   В локальном кубе оказываются только те вычисляемые элементы, именованные наборы и назначения, которые основаны на мерах и измерениях, добавленных в локальный куб. Недопустимые вычисляемые элементы, именованные наборы и назначения будут автоматически исключаться.  
  
### <a name="security"></a>безопасность  
 Порядок пользователь может создать локальный куб из серверного куба пользователю должны быть предоставлены **детализация и локальный куб** разрешения на серверном кубе. Дополнительные сведения см. в разделе [предоставить куба или модели разрешения &#40; Службы Analysis Services &#41; ](../../../analysis-services/multidimensional-models/grant-cube-or-model-permissions-analysis-services.md).  
  
 Локальные кубы не защищены с помощью ролей, как серверные. Выполнять запросы к ним может любой пользователь, обладающий доступом уровня файла к локальному файлу куба. Можно использовать **пароль шифрования** свойство соединения на файл локального куба, чтобы установить пароль на файл локального куба. При использовании пароля в локальном файле куба для запросов к этому файлу в будущем этот пароль нужно будет вводить для всех соединений с локальным файлом куба.  
  
## <a name="see-also"></a>См. также:  
 [СОЗДАТЬ инструкцию глобального КУБА &#40; Многомерные Выражения &#41;](../../../mdx/mdx-data-definition-create-global-cube.md)   
 [Разработка с использованием служб Analysis Services Scripting Language &#40; ASSL &#41;](../../../analysis-services/multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)   
 [Инструкцию обновления КУБА &#40; Многомерные Выражения &#41;](../../../mdx/mdx-data-definition-refresh-cube.md)  
  
  