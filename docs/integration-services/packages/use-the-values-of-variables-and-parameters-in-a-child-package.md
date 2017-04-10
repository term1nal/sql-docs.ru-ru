---
title: "Использование значений переменных и параметров в дочернем пакете | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "переменные [службы Integration Services], передача между пакетами"
  - "конфигурации [службы Integration Services]"
  - "пакеты [службы Integration Services], конфигурации"
  - "переменные [службы Integration Services], добавление"
ms.assetid: 9b939edb-4e17-48e5-8428-855beb10049c
caps.latest.revision: 19
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 19
---
# Использование значений переменных и параметров в дочернем пакете
  Данная процедура описывает создание конфигурации пакета, которая использует тип конфигурации родительской переменной. Данный тип конфигурации, позволяет дочернему пакету, который запускается из родительского, получить доступ к переменной в родительском элементе.  
  
> [!NOTE]  
>  Чтобы передать значения в дочерний пакет, можно настроить задачу «Выполнение пакета» так, чтобы значения стали доступны для дочернего пакета. Для этого переменные, параметры родительского пакета, либо параметры проекта необходимо сопоставить с параметрами дочернего пакета. Дополнительные сведения см. в статье [Execute Package Task](../../integration-services/control-flow/execute-package-task.md).  
  
 Нет необходимости создавать переменные в родительских пакетах до создания пакета конфигурации в дочернем пакете. Можно добавить переменные в родительский пакет в любое время, но нужно использовать правильное имя родительской переменной в конфигурации пакета. Тем не менее перед созданием конфигурации родительской переменной в дочернем пакете должна быть переменная, изменяемая конфигурацией. Дополнительные сведения о добавлении и настройке переменных см. в разделе [Добавление, удаление и изменение области определяемой пользователем переменной в пакете](../Topic/Add,%20Delete,%20Change%20Scope%20of%20User-Defined%20Variable%20in%20a%20Package.md).  
  
 Область видимости переменной родительского пакета, которая используется в конфигурации родительской переменной, может быть установлена в задаче «Выполнение пакета», в контейнере задачи или в пакете. Если в пакете имеется несколько переменных с одним именем, используется переменная, наиболее близкая к области задачи «Выполнение пакета». Ближайшей областью к задаче «Выполнение пакета» является сама задача.  
  
### Добавление переменной в родительский пакет  
  
1.  В среде [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]откройте проект служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , содержащий пакет, к которому нужно добавить переменную для передачи в дочерний пакет.  
  
2.  Чтобы открыть пакет, дважды щелкните его в обозревателе решений.  
  
3.  Для определения области переменной в конструкторе служб [!INCLUDE[ssIS](../../includes/ssis-md.md)] выполните одно из следующих действий.  
  
    -   Чтобы установить в качестве области область пакета, щелкните в любом месте области конструктора на вкладке **Поток управления** .  
  
    -   Чтобы установить в качестве области родительский контейнер задачи «Выполнение пакета», щелкните этот контейнер.  
  
    -   Для настройки области задачи «Выполнение пакета» щелкните задачу.  
  
4.  Добавьте и настройте переменную.  
  
    > [!NOTE]  
    >  Выберите тип данных, совместимый с данными, которые хранятся в переменной.  
  
5.  Чтобы сохранить обновленный пакет, выберите пункт **Сохранить выбранные элементы** в меню **Файл** .  
  
### Добавление переменной в дочерний пакет  
  
1.  В среде [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]откройте проект служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] с пакетом, в который необходимо вставить конфигурацию родительской переменной.  
  
2.  Чтобы открыть пакет, дважды щелкните его в обозревателе решений.  
  
3.  Чтобы установить в качестве области область пакета, щелкните в любом месте конструктора служб [!INCLUDE[ssIS](../../includes/ssis-md.md)] на вкладке **Поток управления** .  
  
4.  Добавьте и настройте переменную.  
  
    > [!NOTE]  
    >  Выберите тип данных, совместимый с данными, которые хранятся в переменной.  
  
5.  Чтобы сохранить обновленный пакет, выберите пункт **Сохранить выбранные элементы** в меню **Файл** .  
  
### Добавление конфигурации родительского пакета в дочерний пакет  
  
1.  Если дочерний пакет еще не открыт, откройте его в среде [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
2.  Щелкните в любом месте вкладки **Поток управления** области конструктора.  
  
3.  В меню **Службы SSIS** выберите команду **Конфигурации пакетов**.  
  
4.  В диалоговом окне **Организатор конфигурации пакетов** выберите **Включить конфигурации пакетов**и нажмите кнопку **Добавить**.  
  
5.  На странице приветствия мастера настройки пакета нажмите кнопку **Далее**.  
  
6.  На странице «Выбор типа конфигурации» в списке **Тип конфигурации** выберите **Переменная родительского пакета** и выполните следующие действия.  
  
    -   Выберите **Указать параметры конфигурации непосредственно**, затем в поле **Родительская переменная** введите имя переменной родительского пакета для использования в конфигурации.  
  
        > [!IMPORTANT]  
        >  В именах переменных учитывается регистр.  
  
    -   Выберите **Сведения о расположении файла конфигурации хранятся в переменной среды**, затем в узле **Список переменных среды** выберите переменную окружения, содержащую имя переменной.  
  
7.  Нажмите кнопку **Далее**.  
  
8.  В окне «Выбор целевого свойства» разверните узел **Переменная** , разверните узел **Свойства** переменной для настройки и выберите свойство для установки в конфигурации.  
  
9. Нажмите кнопку **Далее**.  
  
10. На странице «Завершение работы мастера» при необходимости измените имя конфигурации и просмотрите сведения о конфигурации.  
  
11. Нажмите **Готово** , чтобы завершить работу мастера и вернуться к диалоговому окну **Организатор конфигураций пакетов** .  
  
12. В диалоговом окне **Организатор конфигураций пакетов** в поле **Конфигурация** перечислены новые конфигурации.  
  
13. Щелкните **Закрыть**.  
  
## См. также  
 [Конфигурации пакета](../../integration-services/packages/package-configurations.md)   
 [Создание конфигурации пакетов](../../integration-services/packages/create-package-configurations.md)   
 [Переменные в службах Integration Services (SSIS)](../../integration-services/integration-services-ssis-variables.md)   
 [Использование переменных в пакетах](../Topic/Use%20Variables%20in%20Packages.md)  
  
  