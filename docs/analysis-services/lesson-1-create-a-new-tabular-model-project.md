---
title: "Урок 1: Создание нового проекта табличной модели | Документы Microsoft"
ms.custom: 
ms.date: 03/27/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 0d2eb34d-78c8-41ff-b92d-49b62c16b2ac
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: fe2cd5dff362f5db219f5e61071bde8093b45ce5
ms.contentlocale: ru-ru
ms.lasthandoff: 09/01/2017

---
# <a name="lesson-1-create-a-new-tabular-model-project"></a>Занятие 1. Создание нового проекта табличной модели
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

На этом занятии будет создан новый пустой проект табличной модели в среде [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. После создания нового проекта можно начать добавлять данные с помощью мастера импорта таблиц. На этом занятии также предоставляет краткий обзор среды в SSDT для создания табличных моделей.  
  
Предполагаемое время выполнения данного занятия: **10 минут.**  
  
## <a name="prerequisites"></a>Предварительные требования  
Этот раздел — первое занятие учебника по созданию табличных моделей. Для выполнения этого занятия необходимо иметь установленный на экземпляре SQL Server образца базы данных AdventureWorksDW. Дополнительные сведения см. в разделе [табличных моделей &#40; Учебник по Adventure Works &#41; ](../analysis-services/tabular-modeling-adventure-works-tutorial.md).  
  
## <a name="create-a-new-tabular-model-project"></a>Создание нового проекта табличной модели  
  
#### <a name="to-create-a-new-tabular-model-project"></a>Создание нового проекта табличной модели  
  
1.  В SSDT на **файл** меню, нажмите кнопку **New** > **проекта**.  
  
2.  В **новый проект** диалогового окна разверните **установленные** > **бизнес-аналитики** > **служб Analysis Services**, а затем нажмите кнопку **табличный проект служб Analysis Services**.  
  
3.  В **имя**, тип **Интернет-продаж AW**, а затем укажите расположение для файлов проекта.  
  
    По умолчанию **Имя решения** будет таким же, что и имя проекта, однако можно ввести другое имя решения.  
  
4.  Нажмите кнопку **ОК**.  
  
5.  В **конструктор табличных моделей** выберите **встроенной рабочей**.  
  
    Рабочей области будет размещаться база табличной модели с тем же именем, что и проект во время создания модели. Встроенная рабочей области означает, что SSDT будет использовать встроенный экземпляр, что исключает необходимость установить отдельный экземпляр сервера служб Analysis Services для создания модели. Дополнительные сведения см. в разделе [база данных рабочей области](../analysis-services/tabular-models/workspace-database-ssas-tabular.md).
      
6.  Убедитесь в том, что в поле **Уровень совместимости**выбрано значение **SQL Server 2016 (1200)** , и нажмите кнопку **ОК**.   
 
    ![как табличных-занятия 1 tmd](../analysis-services/media/as-tabular-lesson1-tmd.png)
      
    Если вы не видите SQL Server 2016 RTM (1200) в поле со списком уровня совместимости, вы не используете последнюю версию SQL Server Data Tools. Инструкции по получению последней версии см. в разделе [Установка SQL Server Data Tools](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt).  

    Если вы используете последнюю версию SSDT, можно также выбрать 2017 г. SQL Server (1400). Однако для завершения занятия 13: развертывание, необходимо для развертывания на сервере 2017 г. SQL Server или Azure.
      
    При выборе более раннюю совместимости рекомендуется только если планируется развертывание завершенных табличной модели в другой экземпляр служб Analysis Services, под управлением более ранней версии SQL Server. Встроенная рабочая область не поддерживается для предыдущих уровней совместимости. Дополнительные сведения см. в разделе [Уровень совместимости](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md).   
  
## <a name="understanding-the-ssdt-tabular-model-authoring-environment"></a>Основные сведения о среде создания табличных моделей SSDT  
После создания нового проекта табличной модели давайте Познакомьтесь среды в SSDT для создания табличных моделей.  
  
После создания проекта, он открывается в SSDT. С правой стороны в **обозреватель табличной модели**, вы увидите дерево объектов в модели. Поскольку данные еще не импортированы, папки будет пустым. Щелкнуть правой кнопкой мыши папку объекта для выполнения операций, аналогично строки меню. При пошаговом выполнении этого учебника используется обозреватель табличной модели для перехода различных объектов в проекте модели.

![как табличных-занятия 1 времени](../analysis-services/media/as-tabular-lesson1-tme.png)

Нажмите кнопку **обозревателе решений** вкладки. Здесь вы увидите вашей **Model.bim** файла. Если вы не видите окно конструктора влево (пустое окно с вкладкой Model.bim) в **обозревателе решений**в разделе **AW Internet Sales проекта**, дважды щелкните **Model.bim** файла. Файл Model.bim содержит все метаданные для проекта модели. 

![как табличных-занятия 1 se](../analysis-services/media/as-tabular-lesson1-se.png)
  
Давайте взглянем на свойства модели. Нажмите кнопку **обозревателя решений**. В **свойства** окно, вы увидите [свойств модели](../analysis-services/tabular-models/model-properties-ssas-tabular.md), наиболее важное из которых — **режим DirectQuery** свойство. Это свойство определяет, развертывается модель в режиме In-Memory (Выкл.) или в режиме DirectQuery (Вкл.). В этом учебнике модель создается и развертывается в режиме In-Memory.

![как табличных-занятия 1 properties](../analysis-services/media/as-tabular-lesson1-properties.png)
  
При создании новой модели некоторые свойства модели задаются автоматически в соответствии с параметрами моделирования данных, которые могут быть указаны в **средства** > **параметры** диалоговое окно. Свойства «Резервное копирование данных», «Сохранение рабочей области» и «Сервер рабочей области» указывают, как и где база данных рабочей области (база данных для создания модели) резервно копируется, сохраняется в памяти и создается. При необходимости эти параметры можно изменить в дальнейшем, однако на данном этапе следует оставить их как есть.  

В **обозревателе решений**, щелкните правой кнопкой мыши **Интернет-продаж AW** (проект), а затем нажмите кнопку **свойства**. **Страницы свойств Интернет-продаж AW** откроется диалоговое окно. Они являются расширенными [свойства проекта](../analysis-services/tabular-models/project-properties-ssas-tabular.md). Некоторые из этих свойств будет необходимо задать позже перед развертыванием модели.  
  
При установке SSDT, добавлены несколько новых пунктов меню среды Visual Studio. Давайте взглянем на тех, для создания табличных моделей. Откройте меню **Модель** . Здесь вы можно запустить мастер импорта таблиц, просмотреть и изменить существующие подключения, обновить данные рабочей области, просмотреть модель в Excel с помощью функции анализа в Excel, Создание перспектив и ролей, выберите представление модели и задать параметры вычислений.  
  
Откройте меню **Таблица** . С помощью этого меню можно создавать и управлять связями между таблицами, создавать, управлять и указывать параметры таблиц с данными, создавать секции и изменять свойства таблиц.  
  
Откройте меню **Столбец** . С помощью этого меню можно добавлять и удалять столбцы в таблице, закреплять столбцы и указывать порядок сортировки. Также для создания стандартной статистической меры для выбранного столбца можно использовать функцию автосуммирования. Другие кнопки панели инструментов обеспечивают быстрый доступ к часто используемым функциям и командам.  
  
Просмотрите диалоговые окна и расположение различных функциональных возможностей, используемых для создания табличных моделей. Несмотря на то что некоторые элементы не будут активны, можно получить хорошее представление о среде для создания табличных моделей.  


## <a name="additional-resources"></a>Дополнительные ресурсы
Дополнительные сведения о различных типах проектов табличных моделей см. в разделе [Проекты табличной модели (табличные службы SSAS)](../analysis-services/tabular-models/tabular-model-projects-ssas-tabular.md). Дополнительные сведения о среде создания табличных моделей см. в разделе [Конструктор табличных моделей (службы SSAS)](../analysis-services/tabular-models/tabular-model-designer-ssas.md).  
  

## <a name="whats-next"></a>Дальнейшие действия
Перейдите к следующему занятию: [Lesson 2: Добавление данных](../analysis-services/lesson-2-add-data.md).

  
  
  
