---
title: "Мастер преобразования проекта служб Integration Services | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.ssis.migrationwizard.f1"
ms.assetid: a192b094-4d0f-4c21-b911-460ec844a49f
caps.latest.revision: 17
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 17
---
# Мастер преобразования проекта служб Integration Services
  **Мастер преобразования проекта служб Integration Services** преобразует проект в модель развертывания проекта.  
  
> [!NOTE]  
>  Если проект содержит один или более источников данных, то они будут удалены после завершения преобразования проекта. Для создания соединения с источником данных, который может совместно использоваться пакетами в проекте, добавьте диспетчер соединений на уровне проекта. Дополнительные сведения см. в разделе [Add, Delete, or Share a Connection Manager in a Package](../Topic/Add,%20Delete,%20or%20Share%20a%20Connection%20Manager%20in%20a%20Package.md).  
  
 **Выбор действия**  
  
-   [Открытие мастера преобразования проекта служб Integration Services](#open_dialog)  
  
-   [Задание параметров на странице «Поиск пакетов»](#locate)  
  
-   [Задание параметров на странице «Выбор пакетов»](#selectPackages)  
  
-   [Задание параметров на странице «Выбор назначения»](#destination)  
  
-   [Задание параметров на странице «Задание свойств проекта»](#projectProperties)  
  
-   [Задание параметров на странице «Обновление задачи выполнения пакета»](#executePackage)  
  
-   [Задание параметров на странице «Выбор конфигурации»](#configurations)  
  
-   [Задание параметров на странице «Создание параметров»](#createParameters)  
  
-   [Задание параметров на странице «Настройка параметров»](#configureParameters)  
  
-   [Задание параметров на странице «Просмотр»](#review)  
  
-   [Задание параметров на странице «Выполнение преобразования»](#conversion)  
  
##  <a name="open_dialog"></a> Открытие мастера преобразования проекта служб Integration Services  
 Выполните одно из следующих действий, чтобы открыть мастер **преобразования проекта служб Integration Services** .  
  
-   Откройте проект в [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)], а затем в обозревателе решений щелкните его правой кнопкой мыши и выберите команду **Преобразовать в модель развертывания проекта**.  
  
-   В среде [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] в обозревателе объектов щелкните правой кнопкой мыши узел **Проекты** и выберите команду **Импорт пакетов**.  
  
 В зависимости от того, запускается ли **Мастер преобразования проекта служб Integration Services** из [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] или из среды [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], он выполняет разные задачи по преобразованию. Дополнительные сведения см. в разделе [Deploy Projects to Integration Services Server](../../integration-services/packages/deploy-projects-to-integration-services-server.md).  
  
##  <a name="locate"></a> Задание параметров на странице «Поиск пакетов»  
  
> [!NOTE]  
>  Страница **Поиск пакетов** доступна только при запуске мастера из среды [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
 При выборе пункта **Файловая система** в раскрывающемся списке **Источник** на странице отображается следующий параметр. Выберите этот параметр, если пакет размещен в файловой системе.  
  
 **Папка**  
 Введите путь к пакету или перейдите к пакету, нажав кнопку **Обзор**.  
  
 При выборе пункта **Хранилище пакетов служб SSIS** в раскрывающемся списке **Источник** на странице отображаются следующие параметры. Дополнительные сведения о хранилище пакетов см. в разделе [Управление пакетами (службы SSIS)](../../integration-services/service/package-management-ssis-service.md).  
  
 **Server**  
 Введите имя сервера или выберите сервер.  
  
 **Папка**  
 Введите путь к пакету или перейдите к пакету, нажав кнопку **Обзор**.  
  
 При выборе пункта **Microsoft SQL Server** в раскрывающемся списке **Источник** на странице отображаются следующие параметры. Выберите этот параметр, если пакет находится в Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Server**  
 Введите имя сервера или выберите сервер.  
  
 **Использовать проверку подлинности Windows**  
 Режим проверки подлинности Microsoft Windows позволяет подключаться с учетной записью пользователя Windows. При использовании проверки подлинности Windows не требуется ввод имени пользователя или пароля.  
  
 **Использовать проверку подлинности SQL Server**  
 При соединении пользователя с указанным именем и паролем из ненадежных соединений [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] выполняет проверку подлинности подключения посредством проверки настройки учетной записи входа [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] и проверки совпадения указанного пароля с ранее сохраненным. Если в службе [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] не задана учетная запись входа, проверка подлинности завершается ошибкой, о которой пользователь получит сообщение.  
  
 **Имя пользователя**  
 При использовании проверки подлинности SQL Server укажите имя пользователя.  
  
 **Пароль**  
 Укажите пароль, если используется проверка подлинности SQL Server.  
  
 **Папка**  
 Введите путь к пакету или перейдите к пакету, нажав кнопку **Обзор**.  
  
##  <a name="selectPackages"></a> Задание параметров на странице «Выбор пакетов»  
 **Имя пакета**  
 Выводит список файлов пакета.  
  
 **Состояние**  
 Указывает, готов ли пакет к преобразованию в модель развертывания проекта.  
  
 **Сообщение**  
 Отображает сообщение, связанное с пакетом.  
  
 **Пароль**  
 Отображает пароль, связанный с пакетом. Текст пароля скрыт.  
  
 **Применить к выбранным объектам**  
 Нажмите эту кнопку для установки пароля в текстовом поле **Пароль** для выбранного пакета или пакетов.  
  
 **Обновить**  
 Обновляет список пакетов.  
  
##  <a name="destination"></a> Задание параметров на странице «Выбор назначения»  
 На этой странице укажите имя и путь к новому файлу развертывания проекта (ISPAC) или выберите существующий файл.  
  
> [!NOTE]  
>  Страница **Выбор назначения** доступна только при запуске мастера из среды [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
 **Путь вывода**  
 Введите путь к файлу развертывания или перейдите к файлу, нажав кнопку **Обзор**.  
  
 **Имя проекта**  
 Введите имя проекта.  
  
 **Уровень защиты**  
 Выберите уровень защиты. Дополнительные сведения см. в разделе [Access Control for Sensitive Data in Packages](../../integration-services/packages/access-control-for-sensitive-data-in-packages.md).  
  
 **Описание проекта**  
 Введите необязательное описание для проекта.  
  
##  <a name="projectProperties"></a> Задание параметров на странице «Задание свойств проекта»  
  
> [!NOTE]  
>  Страница **Задание свойств проекта** доступна только при запуске мастера из среды [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)].  
  
 **Имя проекта**  
 Выводит список имен проекта.  
  
 **Уровень защиты**  
 Выбор уровня защиты для пакетов, содержащихся в проекте. Дополнительные сведения об уровнях защиты см. в разделе [Access Control for Sensitive Data in Packages](../../integration-services/packages/access-control-for-sensitive-data-in-packages.md).  
  
 **Описание проекта**  
 Введите необязательное описание проекта.  
  
##  <a name="executePackage"></a> Задание параметров на странице «Обновление задачи выполнения пакета»  
 Обновление задачи «Выполнение пакета» содержится в пакетах для использования ссылки на основе проектов. Дополнительные сведения см. в разделе [Execute Package Task Editor](../../integration-services/control-flow/execute-package-task-editor.md).  
  
 **Родительский пакет**  
 Выводит список имен пакета, который выполняет дочерний пакет с помощью задачи «Выполнение пакета».  
  
 **Имя задачи**  
 Выводит список имен задачи «Выполнение пакета».  
  
 **Исходная ссылка**  
 Отображает текущий путь к дочернему пакету.  
  
 **Назначение ссылки**  
 Выбор дочернего пакета, хранящегося в этом проекте.  
  
##  <a name="configurations"></a> Задание параметров на странице «Выбор конфигурации»  
 Выберите конфигурации пакетов, которые требуется заменить параметрами.  
  
 **Пакет**  
 Выводит список файлов пакета.  
  
 **Тип**  
 Выводит список типов конфигурации, например XML-файл конфигурации.  
  
 **Строка конфигурации**  
 Отображает путь к файлу конфигурации.  
  
 **Состояние**  
 Отображает сообщение о состоянии конфигурации. Щелкните это сообщение для просмотра его содержимого.  
  
 **Добавление конфигураций**  
 Добавление конфигурации пакета, содержащейся в других проектах, в список доступных конфигураций, которые необходимо заменить параметрами. Вы можете выбрать конфигурации, которые хранятся в файловой системе или в SQL Server.  
  
 **Обновить**  
 Нажмите эту кнопку для обновления списка конфигураций.  
  
 **Удаление конфигураций из всех пакетов после преобразования**  
 Рекомендуется удалить все конфигурации из проекта, выбрав этот параметр.  
  
 Если не выбрать этот параметр, будут удалены только те конфигурации, которые требуется заменить параметрами.  
  
##  <a name="createParameters"></a> Задание параметров на странице «Создание параметров»  
 Выбор имени параметра и области каждого свойства конфигурации.  
  
 **Пакет**  
 Выводит список файлов пакета.  
  
 **Имя параметра**  
 Выводит список имен параметра.  
  
 **Область действия**  
 Выбор области параметра, пакета или проекта.  
  
##  <a name="configureParameters"></a> Задание параметров на странице «Настройка параметров»  
 **Название**  
 Выводит список имен параметра.  
  
 **Область действия**  
 Отображает область действия параметров.  
  
 **Значение**  
 Выводит список значений параметра.  
  
 Для настройки свойства параметра нажмите кнопку с многоточием рядом с полем значения.  
  
 В диалоговом окне **Задание сведений о параметре** вы можете изменить значение параметра. Вы можете также указать, необходимо ли при запуске пакета указывать значение параметра.  
  
 Изменить значение вы можете на странице **Параметры** диалогового окна **Настройка** в среде [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], нажав кнопку обзора рядом с параметром. Отобразится диалоговое окно **Задание значения параметра** .  
  
 В диалоговом окне **Задание сведений о параметре** перечислены также типы данных значения параметра и его начальное значение.  
  
##  <a name="review"></a> Задание параметров на странице «Просмотр»  
 Подтвердить параметры, которые выбраны для преобразования проекта, можно на странице **Обзор** .  
  
 **Previous**  
 Нажмите эту кнопку для изменения параметра.  
  
 **Преобразовать**  
 Нажмите эту кнопу для преобразования проекта в модель развертывания проекта.  
  
##  <a name="conversion"></a> Задание параметров на странице «Выполнение преобразования»  
 На странице «Выполнение преобразования» отображается состояние преобразования проекта.  
  
 **Действие**  
 Выводит список заданных шагов преобразования.  
  
 **Результат**  
 Отображает состояние каждого шага преобразования. Щелкните сообщение о состоянии для получения дополнительных сведений.  
  
 Преобразование проекта не сохраняется до тех пор, пока проект сохранен в [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)].  
  
 **Сохранить отчет**  
 Нажмите эту кнопку, чтобы сохранить сводку по преобразованию проекта в XML-файл.  
  
## См. также  
 [Развертывание проектов на сервере служб Integration Services](../../integration-services/packages/deploy-projects-to-integration-services-server.md)  
  
  