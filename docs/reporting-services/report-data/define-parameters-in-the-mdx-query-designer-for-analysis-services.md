---
title: "Определение параметров в конструкторе запросов многомерных Выражений для служб Analysis Services | Документы Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- parameters [Reporting Services], MDX
- Multidimensional Expressions [Reporting Services]
- Data Mining Prediction [Reporting Services]
- MDX [Reporting Services], defining parameters
- DMX [Reporting Services]
ms.assetid: 4ad1e5bc-f510-4752-b4f6-589e55317a90
caps.latest.revision: 37
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: f989ec80fe80d85381673cb12a90b8e3cea82da4
ms.contentlocale: ru-ru
ms.lasthandoff: 08/09/2017

---
# <a name="define-parameters-in-the-mdx-query-designer-for-analysis-services"></a>Определение параметров в конструкторе запросов многомерных выражений для служб Analysis Services
  Чтобы параметризовать запрос многомерных выражений для источника данных служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , необходимо добавить параметр запроса к этому запросу. В конструкторе запросов многомерных выражений параметр запроса можно добавить как в режиме конструктора, так и в режиме запроса, настроив фильтр. После определения запроса с параметром запроса, службы Reporting Services автоматически создают параметр отчета и набор данных, чтобы предоставить список допустимых значений. Это позволяет пользователю указать значение, которое передается непосредственно запросу.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-define-a-query-parameter-in-mdx-in-design-mode"></a>Определение параметра запроса в многомерном выражении в режиме конструктора  
  
1.  В области данных отчета щелкните правой кнопкой мыши набор данных, созданный из типа источника данных служб [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , и выберите пункт **Запрос**. Конструктор запросов многомерных выражений открывается в режиме конструктора.  
  
2.  Перетащите измерение в область фильтра в первую ячейку в столбце **Измерение** .  
  
3.  В столбце **Иерархия** выберите значение в раскрывающемся списке.  
  
4.  В столбце **Оператор** выберите оператор в раскрывающемся списке.  
  
5.  В столбце **Критерий фильтра** выберите отдельные значения из раскрывающегося списка или щелкните **Все** , чтобы выбрать все значения.  
  
6.  В столбце **Параметры** установите флажок, чтобы создать параметр отчета.  
  
7.  Нажмите кнопку **Запустить**.  
  
     После запуска запроса нажмите кнопку **Конструктор** на панели инструментов, чтобы переключиться в режим запроса для просмотра созданного запроса многомерных выражений. Чтобы продолжить работу в режиме конструктора для создания запроса, не изменяйте текст запроса в режиме запроса. Нажмите кнопку **Конструктор** , чтобы снова переключиться в режим конструктора.  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     В области данных отчета разверните узел «Параметры», чтобы отобразить параметр отчета, который был автоматически создан для фильтра.  
  
     Чтобы просмотреть набор данных, который включает доступные значения для параметра отчета, щелкните правой кнопкой мыши в любом пустом месте на панели данных отчета и выберите пункт **Показывать скрытые наборы данных**. В области данных отчета отображаются все наборы данных отчета.  
  
### <a name="to-define-a-query-parameter-in-mdx-in-query-mode"></a>Определение параметра запроса в многомерном выражении в режиме запроса  
  
1.  В области данных отчета щелкните правой кнопкой мыши набор данных, созданный из типа источника данных служб [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , и выберите пункт **Запрос**. Конструктор запросов многомерных выражений открывается в режиме конструктора.  
  
2.  На панели инструментов нажмите кнопку **Конструктор** , чтобы переключиться в режим запроса.  
  
3.  На панели многомерных Выражений инструментов конструктора запросов, нажмите кнопку **параметров запроса** (![значок диалоговое окно «Параметры запроса»](../../reporting-services/report-data/media/iconqueryparameter.gif "значок диалоговое окно «Параметры запроса»")). Откроется диалоговое окно «Параметры запроса».  
  
4.  В **параметр** столбец, нажмите кнопку  **\<введите параметр >**, а затем введите имя параметра.  
  
5.  В столбце **Измерение** выберите значение в раскрывающемся списке.  
  
6.  В столбце **Иерархия** выберите значение в раскрывающемся списке.  
  
7.  В столбце **Несколько значений** установите флажок, чтобы создать многозначный параметр.  
  
8.  В столбце **По умолчанию** выберите в раскрывающемся списке одно или несколько значений (в зависимости от выбора, сделанного на шаге 5).  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
10. На панели инструментов конструктора запросов нажмите кнопку **Выполнить**.  
  
11. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     В области данных отчета разверните узел «Параметры», чтобы отобразить параметр отчета, который был автоматически создан для фильтра.  
  
     Чтобы просмотреть набор данных, который включает доступные значения для параметра отчета, щелкните правой кнопкой мыши в любом пустом месте на панели данных отчета и выберите пункт **Показывать скрытые наборы данных**. В области данных отчета отображаются все наборы данных отчета.  
  
## <a name="see-also"></a>См. также:  
 [Тип соединения служб Analysis Services для многомерных Выражений &#40; Службы SSRS &#41;](../../reporting-services/report-data/analysis-services-connection-type-for-mdx-ssrs.md)   
 [Analysis Services MDX пользовательский интерфейс конструктора запросов](../../reporting-services/report-data/analysis-services-mdx-query-designer-user-interface.md)  
  
  