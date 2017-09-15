---
title: "Поиск infoObject | Документы Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e7f4c132-a5ec-49d8-a964-45775432731f
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: f25c00406ce375a2a7a380859ca0eaa5031b54d3
ms.contentlocale: ru-ru
ms.lasthandoff: 08/03/2017

---
# <a name="look-up-infoobject"></a>Поиск InfoObject
  Используйте диалоговое окно **Поиск InfoObject** для поиска InfoObject, заданного в системе SAP Netweaver BW. После открытия списка объектов InfoObject выберите нужный объект InfoObject, после чего целевой объект SAP BW заполнит связанные параметры необходимыми значениями.  
  
 Целевой объект SAP BW [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 для SAP BW использует диалоговое окно **Найти InfoObject** . Дополнительные сведения о назначении SAP BW см. в разделе [SAP BW Destination](../../integration-services/data-flow/sap-bw-destination.md).  
  
> [!IMPORTANT]  
>  Документация по Microsoft Connector 1.1 для SAP BW предполагает, что читатель знаком со средой SAP Netweaver BW. Дополнительные сведения о SAP Netweaver BW или сведения о настройке объектов и процессов SAP Netweaver BW см. в документации SAP.  
  
 **Открытие диалогового окна «Поиск InfoObject»**  
  
1.  В [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]откройте пакет [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , содержащий назначение SAP BW.  
  
2.  На вкладке **Поток данных** дважды щелкните назначение SAP BW.  
  
3.  В **Редакторе назначений SAP BW**щелкните **Диспетчер соединений** , чтобы открыть страницу редактора **Диспетчер соединений** .  
  
4.  На странице **Диспетчер соединений** в разделе **Создание объектов SAP BW** выберите один из следующих параметров.  
  
    1.  Выберите **InfoCube**. Затем нажмите кнопку **Создать**. В диалоговом окне **Создание InfoCube для данных транзакции** выберите **Найти** в столбце **IObject** в одной из строк в списке. Каждая строка представляет собой столбец в потоке данных пакета.  
  
    2.  Выберите **InfoSource**. Затем нажмите кнопку **Создать**. В диалоговом окне **Создание InfoSource** выберите **Данные транзакций**. В диалоговом окне **Создание InfoSource для данных транзакции** выберите **Найти** в столбце **IObject** в одной из строк в списке. Каждая строка представляет собой столбец в потоке данных пакета.  
  
    3.  Выберите **InfoSource**. Затем нажмите кнопку **Создать**. В диалоговом окне **Создание InfoSource** выберите **Главные данные**. В диалоговом окне **Создание InfoSource для основных данных** нажмите кнопку **Найти**.  
  
 Также можно открыть диалоговое окно **Найти InfoObject** , щелкнув **Создать** в разделе **Атрибуты** диалогового окна **Создание нового InfoObject** .  
  
## <a name="lookup-options"></a>Параметры поиска  
 В текстовых полях поиска можно фильтровать результаты с помощью символа-шаблона звездочки (*) или с помощью частичной строки в сочетании с символом-шаблоном звездочки. Однако если оставить поле поиска пустым, то процесс поиска будет находить только пустые строки в этом поле.  
  
 **Характеристики**  
 Поиск объектов InfoObject, которые являются выражением характеристик.  
  
 **Единицы измерения**  
 Поиск объектов InfoObject, которые представляют собой единицы.  
  
 **Ключевые цифры**  
 Поиск объектов InfoObject, которые представляют собой ключевые цифры.  
  
 **Характеристики времени**  
 Поиск объектов InfoObject, которые являются выражением характеристик времени.  
  
 **Название**  
 Введите имя InfoObject для поиска или часть имени с символом-шаблоном звездочки (*). Также можно использовать символ-шаблон звездочки для включения всех объектов InfoObject.  
  
 **Description**  
 Введите описание или частичное описание с символом-шаблоном звездочки (*). Также можно использовать символ-шаблон звездочки для включения всех объектов InfoObject независимо от описания.  
  
 **Найти**  
 Выполните поиск соответствующих объектов InfoObject, определенных в системе SAP Netweaver BW.  
  
## <a name="lookup-results"></a>Результаты поиска  
 После нажатия кнопки «Поиск» список объектов InfoObject в системе SAP Netweaver BW отобразится в таблице со следующими заголовками столбцов.  
  
 **InfoObject**  
 Отображается имя объекта InfoObject, определенное в системе SAP Netweaver BW.  
  
 **Текст (краткий)**  
 Отображает краткий текст, связанный с объектом InfoObject.  
  
 После открытия списка объектов InfoObject выберите нужный объект InfoObject, после чего целевой объект заполнит связанные параметры необходимыми значениями.  
  
## <a name="see-also"></a>См. также  
 [Создание InfoCube для данных транзакции](../../integration-services/data-flow/create-infocube-for-transaction-data.md)   
 [Создание InfoSource](../../integration-services/data-flow/create-infosource.md)   
 [Создание InfoSource для данных транзакции](../../integration-services/data-flow/create-infosource-for-transaction-data.md)   
 [Создание InfoSource для основных данных](../../integration-services/data-flow/create-infosource-for-master-data.md)   
 [Создание нового InfoObject](../../integration-services/data-flow/create-new-infoobject.md)   
 [Редактор назначений SAP BW &#40; Страницы диспетчера соединений &#41;](../../integration-services/data-flow/sap-bw-destination-editor-connection-manager-page.md)   
 [Справка F1 по Microsoft Connector для SAP BW](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  