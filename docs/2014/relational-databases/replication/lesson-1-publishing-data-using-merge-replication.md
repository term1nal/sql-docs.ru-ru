---
title: Урок 1. Публикация данных с помощью репликации слиянием | Документация Майкрософт
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: c3c6e0b6-54cd-4b7d-8efb-2cefe14fcd7f
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 65debc2ad15045984f43e05d0afcf3011c50f2b8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/02/2018
ms.locfileid: "48112914"
---
# <a name="lesson-1-publishing-data-using-merge-replication"></a>Урок 1. Публикация данных с помощью репликации слиянием
  На этом занятии с помощью среды [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] создается публикация слиянием с целью публикации подмножества таблиц **Employee**, **SalesOrderHeader**и **SalesOrderDetail** в образце базы данных [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] . Эти таблицы фильтруются с помощью параметризованных фильтров строк, так что каждая подписка содержит уникальную секцию данных. Также в список доступа к публикации добавляется имя входа [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , используемое агентом слияния. Для работы с этим учебником требуется завершить работу с предыдущим учебником, [Подготовка сервера для репликации](tutorial-preparing-the-server-for-replication.md).  
  
### <a name="to-create-a-publication-and-define-articles"></a>Создание публикации и определение статей  
  
1.  Подключитесь к издателю в среде [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], а затем раскройте узел сервера.  
  
2.  Разверните папку **Репликация** , щелкните правой кнопкой мыши элемент **Локальные публикации**и выберите пункт **Создать публикацию**.  
  
     Будет запущен мастер настройки публикации.  
  
3.  На странице «База данных публикации» выберите [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]и нажмите кнопку **Далее**.  
  
4.  На странице «Тип публикации» выберите **Публикация слиянием**и нажмите кнопку **Далее**.  
  
5.  На странице «Типы подписчиков» убедитесь, что выбрана только [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] или более поздняя версия, и нажмите кнопку **Далее**.  
  
6.  На странице «Статьи» разверните узел **Таблицы** , выберите **SalesOrderHeader** и **SalesOrderDetail**, затем разверните узел **Employee**, выберите **EmployeeID** или **LoginID**и нажмите кнопку **Далее**.  
  
    > [!TIP]  
    >  Дополнительные требуемые столбцы выделяются автоматически. Выберите один из автоматически выбранных столбцов и просмотрите примечание под списком **Объекты для публикации** , объясняющее причину обязательного наличия столбца.  
  
7.  На странице «Фильтрация строк таблицы» нажмите кнопку **Добавить** , а затем щелкните **Добавить фильтр**.  
  
8.  В диалоговом окне **Добавление фильтра** выберите **Сотрудник (HumanResources)** в поле **Выберите таблицу для фильтрации**, щелкните столбец **LoginID** , нажмите кнопку со стрелкой вправо, чтобы добавить столбец в предложение WHERE фильтра запроса, и измените предложение WHERE следующим образом:  
  
    ```  
    WHERE [LoginID] = HOST_NAME()  
    ```  
  
9. Щелкните элемент **Строка из этой таблицы будет отправлена только одной подписке**и нажмите кнопку **ОК**.  
  
10. На странице **Фильтрация строк таблицы** выберите **Сотрудник (кадры)**, нажмите **Добавить** , а затем **Добавить соединение для расширения выбранного фильтра**.  
  
11. В диалоговом окне **Добавление соединения** выберите **Sales.SalesOrderHeader** в **Соединяемая таблица**, щелкните **Создать инструкцию соединения вручную**и завершите инструкцию соединения следующим образом:  
  
    ```  
    ON Employee.EmployeeID = SalesOrderHeader.SalesPersonID  
    ```  
  
12. В поле **Укажите параметры соединения**выберите **Уникальный ключ**, а затем нажмите кнопку **ОК**.  
  
13. На странице «Фильтрация строк таблицы» щелкните **SalesOrderHeader**, нажмите кнопку **Добавить**, а затем щелкните **Добавить соединение для расширения выбранного фильтра**.  
  
14. В диалоговом окне **Добавление соединения** выберите **Sales.SalesOrderDetail** в поле **Соединяемая таблица**.  
  
15. Нажмите **Создать инструкцию соединения вручную**.  
  
16. В поле **Столбцы отфильтрованной таблицы**выберите **BusinessEntityID**, затем нажмите кнопку со стрелкой, чтобы скопировать имя столбца в инструкцию соединения.  
  
17. В поле **Инструкция соединения** завершите инструкцию соединения следующим образом:  
  
    ```  
    ON Employee.BusinessEntityID = SalesOrderHeader.SalesPersonID  
    ```  
  
18. В поле **Укажите параметры соединения**выберите **Уникальный ключ**, а затем нажмите кнопку **ОК**.  
  
19. На странице **Фильтрация строк таблицы** выберите **SalesOrderHeader (Sales)**, нажмите **Добавить**, а затем **Добавить соединение для расширения выбранного фильтра**.  
  
20. В диалоговом окне **Добавление соединения** выберите **Sales.SalesOrderDetail** в поле **Соединяемая таблица**, нажмите кнопку **ОК**, а затем кнопку **Далее**.  
  
21. Установите флажок **Создать моментальный снимок немедленно**, снимите флажок **Запланировать запуск агента моментальных снимков в следующее время**и нажмите кнопку **Далее**.  
  
22. На странице "Безопасность агента" щелкните **Настройки безопасности**, введите \<*имя_компьютера>***\repl_snapshot** в поле **Учетная запись процесса**, укажите пароль для учетной записи и нажмите кнопку **ОК**. Нажмите кнопку **Готово**.  
  
23. На странице «Завершение работы мастера» введите **AdvWorksSalesOrdersMerge** в поле **Имя публикации** и нажмите кнопку **Готово**.  
  
24. По завершении создания публикации нажмите кнопку **Закрыть**.  
  
### <a name="to-view-the-status-of-snapshot-generation"></a>Просмотр состояния создания моментального снимка  
  
1.  Подключитесь к издателю в среде [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], а затем раскройте узел сервера и папку **Репликация** .  
  
2.  В папке "Локальные публикации" щелкните правой кнопкой мыши публикацию **AdvWorksSalesOrdersMerge**и выберите пункт **Просмотр состояния агента моментальных снимков**.  
  
3.  Отобразится текущее состояние задания агента моментальных снимков для публикации. Перед тем как перейти к следующему занятию, убедитесь, что задание моментального снимка выполнено успешно.  
  
### <a name="to-add-the-merge-agent-login-to-the-pal"></a>Добавление имени входа агента слияния в список доступа к публикации  
  
1.  Подключитесь к издателю в среде [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], а затем раскройте узел сервера и папку **Репликация** .  
  
2.  В папке "Локальные публикации" щелкните правой кнопкой мыши публикацию **AdvWorksSalesOrdersMerge**и выберите пункт **Свойства**.  
  
     Откроется диалоговое окно **Свойства публикации** .  
  
3.  Выберите страницу **Список доступа к публикации** и нажмите кнопку **Добавить**.  
  
4.  В диалоговом окне "Добавление доступа к публикации" выберите *<имя_компьютера>***\repl_merge** и нажмите кнопку **ОК**. Нажмите кнопку **ОК**.  
  
## <a name="next-steps"></a>Следующие шаги  
 Публикация слиянием успешно создана. Далее будет создана подписка на эту публикацию. См. [Занятие 2. Создание подписки на публикацию слиянием](lesson-2-creating-a-subscription-to-the-merge-publication.md).  
  
## <a name="see-also"></a>См. также  
 [Фильтрация опубликованных данных](publish/filter-published-data.md)   
 [Parameterized Row Filters](merge/parameterized-filters-parameterized-row-filters.md)   
 [Определение статьи](publish/define-an-article.md)  
  
  
