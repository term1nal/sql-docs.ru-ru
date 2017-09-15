---
title: "Получение и интерпретация измененных данных | Документы Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- incremental load [Integration Services],retrieving data
ms.assetid: af366697-6942-42bb-aea5-18fdef018965
caps.latest.revision: 30
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: caf66f974e832fcd1b27caf650d187942b3f19fe
ms.contentlocale: ru-ru
ms.lasthandoff: 08/03/2017

---
# <a name="retrieve-and-understand-the-change-data"></a>Получение и интерпретация измененных данных
  В потоке данных пакета служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , выполняющего добавочную загрузку измененных данных, первая задача — выполнение запроса, который получает информацию об изменениях. Этот запрос выполняется внутри исходного компонента задачи потока данных. Затем можно использовать нисходящие преобразования и назначения, чтобы применить данные об изменениях к назначению.  
  
> [!NOTE]  
>  Создание запроса, содержащего возвращающую табличное значение функцию, является третьим шагом в процессе создания пакета, который осуществляет добавочную загрузку измененных данных. Дополнительные сведения об этом запросе см. в разделе [Создание функции для получения информации об изменениях](../../integration-services/change-data-capture/create-the-function-to-retrieve-the-change-data.md). Описание общего процесса создания пакета, выполняющего добавочную загрузку информации об изменениях, см. в разделе [Система отслеживания измененных данных (SSIS)](../../integration-services/change-data-capture/change-data-capture-ssis.md).  
  
## <a name="adding-the-data-flow-task"></a>Добавление задачи потока данных  
 В потоке данных пакета получаются измененные данные, отдельные строки на основе типа произошедших изменений, а затем изменения применяются к назначению.  
  
#### <a name="to-add-a-data-flow-task-to-the-package"></a>Добавление задачи потока данных к пакету  
  
1.  В среде [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]на вкладке **Поток управления** добавьте задачу потока данных.  
  
2.  Соедините предыдущую задачу, подготовившую строку запроса, с задачей потока данных.  
  
## <a name="configuring-the-source-component-to-query-for-changes"></a>Настройка исходного компонента для выполнения запроса об изменениях  
 С помощью подготовленной и сохраненной в переменной строки запроса исходный компонент вызывает возвращающую табличное значение функцию, которая получает измененные данные.  
  
> [!NOTE]  
>  Дополнительные сведения о подготовленной и сохраненной в переменной строке запроса см. в разделе [Подготовка к запросу информации об изменениях](../../integration-services/change-data-capture/prepare-to-query-for-the-change-data.md). Дополнительные сведения о возвращающей табличное значение функции, которая получает данные об изменениях, см. в разделе [Создание функции для получения информации об изменениях](../../integration-services/change-data-capture/create-the-function-to-retrieve-the-change-data.md).  
  
#### <a name="to-configure-an-ole-db-source-to-retrieve-the-change-data"></a>Настройка источника OLE DB для получения измененных данных.  
  
1.  На вкладке [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]Поток данных **среды** добавьте источник OLE DB.  
  
2.  На странице **Диспетчер соединений**в области **Редактор источника OLE DB** установите следующие параметры.  
  
    1.  Настройте допустимое соединение с базой данных-источником.  
  
    2.  В списке **Режим доступа к данным**выберите **Команда SQL из переменной**.  
  
    3.  В поле **Имя переменной**выберите **User::SqlDataQuery**.  
  
3.  В области **Редактор источника OLE DB**на странице **Столбцы** убедитесь, чтобы все необходимые столбцы были сопоставлены с выходными столбцами.  
  
## <a name="next-step"></a>Следующий шаг  
 После настройки источника OLE DB для получения измененных данных начинается проектирование потока данных в пакете.  
  
 **Следующий раздел:** [Обработка операций вставки, обновления и удаления](../../integration-services/change-data-capture/process-inserts-updates-and-deletes.md)  
  
  