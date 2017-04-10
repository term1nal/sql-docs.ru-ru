---
title: "Шаг 4. Добавление конфигурации пакета | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: e04a5321-63d5-4ec5-85b9-cb4eaf6c87f6
caps.latest.revision: 28
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
---
# Шаг 4. Добавление конфигурации пакета
В этой задаче необходимо добавить конфигурацию каждому пакету. Конфигурации позволяют обновлять значения свойств и объектов пакетов во время выполнения.  
  
[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] предоставляют различные типы конфигурации. Конфигурации можно сохранять в переменных среды, в записях реестра, пользовательских переменных, таблицах [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] и XML-файлах. Чтобы обеспечить дополнительную гибкость, службы [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] поддерживают косвенную конфигурацию. Это подразумевает использование переменной среды для указания расположения конфигурации, которая, в свою очередь, указывает фактические значения. Для пакетов проекта из учебника по развертыванию используется сочетание XML-файлов конфигурации и косвенная конфигурация. В XML-файле конфигурации могут содержаться параметры конфигурации для различных свойств, а когда возможно, и для различных пакетов. В данном учебнике для каждого пакета используется отдельный файл конфигурации.  
  
В файлах конфигурации часто содержатся конфиденциальные данные, такие как строки соединения. Поэтому необходимо использовать список управления доступом (ACL), чтобы ограничить доступ к месту или папке, где хранятся эти файлы, и предоставить доступ только пользователям или учетным записям, обладающим разрешением на выполнение пакетов. Дополнительные сведения см. в разделе [Доступ к файлам, используемым пакетами](../integration-services/security/access-to-files-used-by-packages.md).  
  
Для успешного выполнения после разворачивания на целевом сервере пакетам (DataTransfer и LoadXMLData), добавленным в проект из учебника по развертыванию в предыдущей задаче, необходимы конфигурации. Для выполнения настройки сначала необходимо создать косвенную конфигурацию для XML-файлов конфигурации и затем создать XML-файлы конфигурации.  
  
Будут созданы два файла конфигурации, DataTransferConfig.dtsConfig и LoadXMLData.dtsConfig. Эти файлы содержат пары «имя-значение», обновляющие в пакетах свойства, которые указывают расположение используемых пакетом файлов данных и журналов. Позже, на одном из этапов процесса развертывания, потребуется обновить значения в файлах конфигурации, чтобы отразить новое место хранения файлов на целевом компьютере.  
  
[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] распознают, что файлы DataTransferConfig.dtsConfig и LoadXMLData.dtsConfig представляют собой зависимости пакетов DataTransfer и LoadXMLData, и на следующем занятии при создании комплекта развертывания в них автоматически будут содержаться эти файлы конфигурации.  
  
### Создание косвенной конфигурации для пакета DataTransfer  
  
1.  В обозревателе решений дважды щелкните DataTransfer.dtsx.  
  
2.  В конструкторе служб [!INCLUDE[ssIS](../includes/ssis-md.md)] щелкните в области конструктора потока управления.  
  
3.  В меню **Службы SSIS** выберите команду **Конфигурации пакетов**.  
  
4.  В диалоговом окне **Организатор конфигурации пакетов**установите флажок **Включить конфигурации пакетов** , если эта функция еще не активирована, и нажмите кнопку **Добавить**.  
  
5.  На странице приветствия мастера настройки пакета нажмите кнопку **Далее**.  
  
6.  На странице выбора типа конфигурации в списке **Тип конфигурации** выберите **XML-файл конфигурации** , затем выберите параметр **Сведения о расположении файла конфигурации хранятся в переменной среды** и введите **DataTransfer** или выберите переменную среды **DataTransfer** из списка.  
  
    > [!NOTE]  
    > Чтобы переменная среды была доступна в списке, после добавления переменной может потребоваться перезагрузка компьютера. Если перезагрузка компьютера нежелательна, можно просто ввести имя переменной.  
  
7.  Нажмите кнопку **Далее**.  
  
8.  На странице «Завершение работы мастера» в окне **Имя конфигурации** введите **DataTransfer EV Configuration** , проверьте содержимое конфигурации на панели **Предварительный просмотр** и нажмите кнопку **Готово**.  
  
9. Закройте диалоговое окно **Организатор конфигурации пакетов**.  
  
### Создание XML-конфигурации для пакета DataTransfer  
  
1.  В обозревателе решений дважды щелкните DataTransfer.dtsx.  
  
2.  В конструкторе служб [!INCLUDE[ssIS](../includes/ssis-md.md)] щелкните в области конструктора потока управления.  
  
3.  В меню **Службы SSIS** выберите команду **Конфигурации пакетов**.  
  
4.  В диалоговом окне "Организатор конфигурации пакетов" установите флажок **Включить конфигурации пакетов** и нажмите кнопку **Добавить**.  
  
5.  На странице приветствия мастера настройки пакета нажмите кнопку **Далее**.  
  
6.  На странице выбора типа конфигурации в списке **Тип конфигурации** выберите **XML-файл конфигурации** и нажмите кнопку **Обзор**.  
  
7.  В диалоговом окне **Выберите расположение файла конфигурации** укажите путь к папке C:\DeploymentTutorial и в поле **Имя файла** введите **DataTransferConfig**, после чего нажмите кнопку **Сохранить**.  
  
8.  На странице выбора типа конфигурации нажмите кнопку **Далее**.  
  
9. На странице выбора свойств для экспорта раскройте разделы "DataTransfer", "Диспетчеры соединений", "Журнал учебника по развертыванию" и "Свойства", после чего установите флажок **Строка подключения**.  
  
10. В разделе "Диспетчеры соединений" разверните узел "NewCustomers" и установите флажок **Строка подключения**.  
  
11. Нажмите кнопку **Далее**.  
  
12. На странице «Завершение работы мастера» в окне **Имя конфигурации** введите **DataTransfer Configuration** , проверьте содержимое конфигурации и нажмите кнопку **Готово**.  
  
13. В диалоговом окне **Организатор конфигурации пакетов** убедитесь, что конфигурация DataTransfer EV Configuration находится на первом месте в списке, а DataTransfer Configuration на втором, и нажмите кнопку **Закрыть**.  
  
### Создание косвенной конфигурации для пакета LoadXMLData  
  
1.  В обозревателе решений дважды щелкните LoadXMLData.dtsx.  
  
2.  В конструкторе служб [!INCLUDE[ssIS](../includes/ssis-md.md)] щелкните в области конструктора потока управления.  
  
3.  В меню **Службы SSIS** выберите команду **Конфигурации пакетов**.  
  
4.  В диалоговом окне **Организатор конфигурации пакетов**нажмите кнопку **Добавить**.  
  
5.  На странице приветствия мастера настройки пакета нажмите кнопку **Далее**.  
  
6.  На странице выбора типа конфигурации в списке **Тип конфигурации** выберите **XML-файл конфигурации** , выберите параметр **Сведения о расположении файла конфигурации хранятся в переменной среды** и введите **LoadXMLData** или выберите переменную среды **LoadXMLData** из списка.  
  
    > [!NOTE]  
    > Чтобы переменная среды была доступна в списке, после добавления переменной может потребоваться перезагрузка компьютера.  
  
7.  Нажмите кнопку **Далее**.  
  
8.  На странице «Завершение работы мастера» в окне **Имя конфигурации** введите **LoadXMLData EV Configuration** , проверьте содержимое конфигурации и нажмите кнопку **Готово**.  
  
### Создание XML-конфигурации для пакета LoadXMLData  
  
1.  В обозревателе решений дважды щелкните LoadXMLData.dtsx.  
  
2.  В конструкторе служб [!INCLUDE[ssIS](../includes/ssis-md.md)] щелкните в области конструктора потока управления.  
  
3.  В меню **Службы SSIS** выберите команду **Конфигурации пакетов**.  
  
4.  В диалоговом окне "Организатор конфигурации пакетов" установите флажок **Включить конфигурации пакетов** и нажмите кнопку **Добавить**.  
  
5.  На странице приветствия мастера настройки пакета нажмите кнопку **Далее**.  
  
6.  На странице выбора типа конфигурации в списке **Тип конфигурации** выберите **XML-файл конфигурации** и нажмите кнопку **Обзор**.  
  
7.  В диалоговом окне **Выберите расположение файла конфигурации** укажите путь к папке C:\DeploymentTutorial и в поле **Имя файла** введите **LoadXMLDataConfig**, после чего нажмите кнопку **Сохранить**.  
  
8.  На странице выбора типа конфигурации нажмите кнопку **Далее**.  
  
9. На странице выбора свойств для экспорта разверните узлы "LoadXMLData", "Исполняемые объекты", "Загрузка XML-данных" и "Свойства", после чего установите флажки **[XMLSource].[XMLData]** и **[XMLSource].[XMLSchemaDefinition]**.  
  
10. Нажмите кнопку **Далее**.  
  
11. На странице «Завершение работы мастера» в окне **Имя конфигурации** введите **LoadXMLData Configuration** , проверьте содержимое конфигурации и нажмите кнопку **Готово**.  
  
12. В диалоговом окне **Организатор конфигурации пакетов** убедитесь, что конфигурация LoadXMLData EV Configuration находится на первом месте в списке, а LoadXMLData Configuration на втором, и нажмите кнопку **Закрыть**.  
  
## Следующая задача занятия  
[Шаг 5. Тестирование обновленных пакетов](../integration-services/step-5-testing-the-updated-packages.md)  
  
## См. также:  
[Конфигурации пакета](../integration-services/packages/package-configurations.md)  
[Создание конфигурации пакетов](../integration-services/packages/create-package-configurations.md)  
[Доступ к файлам, используемым пакетами](../integration-services/security/access-to-files-used-by-packages.md)  
  
  
  