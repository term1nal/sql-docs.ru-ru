---
title: "Задача «Файловая система» | Документы Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.filesystemtask.f1
- sql13.dts.designer.filesystemtask.general.f1
helpviewer_keywords:
- File System task [Integration Services]
ms.assetid: 7dd79a6a-e066-4028-a385-1d40f31056f8
caps.latest.revision: 58
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 8806c102eaec2c2540374bfaddc33b76d8f6e584
ms.openlocfilehash: 63fb21cae5f8df981f243035fc7b34e53fa4d0bd
ms.contentlocale: ru-ru
ms.lasthandoff: 08/11/2017

---
# <a name="file-system-task"></a>Задача "Файловая система"
  Задача «Файловая система» выполняет операции над файлами и каталогами файловой системы. Например, при помощи задачи «Файловая система» пакет может создавать, перемещать или удалять каталоги и файлы. Можно также использовать данную задачу для установки атрибутов файлов и каталогов. Например, задача «Файловая система« может пометить файлы как скрытые или предназначенные только для чтения.  
  
 Все операции задачи «Файловая система» используют источник, который может быть файлом или каталогом. Например, файл, который копирует задача, или каталог, который она удаляет, является источником. Источник можно указать при помощи диспетчера подключения файлов, который указывает каталог или файл, или определив имя переменной, содержащей путь к источнику. Дополнительные сведения см. в разделах [Диспетчер соединения файлов](../../integration-services/connection-manager/file-connection-manager.md) и [Переменные в службах Integration Services (SSIS)](../../integration-services/integration-services-ssis-variables.md).  
  
 Операции, копирующие и перемещающие файл и каталоги, а также переименовывающие файлы, используют целевой объект и источник. Целевой объект указывается при помощи диспетчера подключения файла или переменной. Операции задачи «Файловая система» можно настроить для возможности перезаписывать целевые файлы и каталоги. Операцию, которая создает новый каталог, можно настроить для использования существующего каталога, имеющего указанное имя. Это позволит избежать ошибки, если каталог уже существует.  
  
## <a name="predefined-file-system-operations"></a>Предопределенные операции файловой системы  
 Задача «Файловая система» содержит предопределенный набор операций. Данные операции описываются в следующей таблице.  
  
|Операция|Description|  
|---------------|-----------------|  
|Копировать каталог|Копирует папку из одного места в другое.|  
|Копировать файл|Копирует файл из одного места в другое.|  
|Создать каталог|Создает папку в указанном месте.|  
|Удалить каталог|Удаляет папку в указанном месте.|  
|Удалить содержимое каталога|Удаляет все файлы и вложенные папки в текущей папке.|  
|Удалить файл|Удаляет файл в указанном месте.|  
|Переместить каталог|Перемещает папку из одного места в другое.|  
|Переместить файл|Перемещает файл из одного места в другое.|  
|Переименовать файл|Переименовывает файл в указанном месте.|  
|Задать атрибуты|Устанавливает атрибуты файлов и папок. Атрибуты принимают следующие значения: «архивный», «скрытый», «обычный», «только чтение» и «системный». «Обычный» означает отсутствие атрибутов, и его невозможно объединять с другими атрибутами. Все другие атрибуты можно использовать совместно.|  
  
 Задача «Файловая система» работает с одиночным файлом или каталогом. Поэтому данная задача не позволяет использовать символы-шаблоны для выполнения одной операции над несколькими файлами. Чтобы задача «Файловая система» повторила операцию над несколькими файлами или каталогами, поместите ее в контейнер «цикл по каждому элементу», как описано в следующих разделах:  
  
-   **Настройка параметров контейнера «цикл по каждому элементу»** На странице **Коллекция** редактора циклов по каждому элементу установите **Перечислитель с циклом по каждому файлу** и введите выражение с шаблонами в качестве настройки для поля **Файлы**. На странице **Сопоставления переменной** редактора циклов по каждому элементу укажите переменную, которую нужно использовать, чтобы передавать имена файлов по одному в задачу «Файловая система».  
  
-   **Добавление и настройка задачи «Файловая система»** Добавьте задачу «Файловая система» в контейнер «цикл по каждому элементу». На странице **Общие** редактора задачи «Файловая система» установите свойство **SourceVariable** или **DestinationVariable** для переменной, определенной в контейнере «цикл по каждому элементу».  
  
## <a name="custom-log-entries-available-on-the-file-system-task"></a>Пользовательские записи журнала, доступные в задаче «Файловая система»  
 В следующей таблице перечислены пользовательские записи журнала для задачи «Файловая система». Дополнительные сведения см. в разделе [Ведение журналов в службах Integration Services (SSIS)](../../integration-services/performance/integration-services-ssis-logging.md).  
  
|Запись журнала|Description|  
|---------------|-----------------|  
|**FileSystemOperation**|Сообщает об операции, выполняемой задачей. Эта запись журнала формируется, когда операция файловой системы начинается и включает сведения об источнике и назначении.|  
  
## <a name="configuring-the-file-system-task"></a>Настройка задачи «Файловая система»  
 Значения свойств можно задавать с помощью конструктора [!INCLUDE[ssIS](../../includes/ssis-md.md)] или программными средствами.  
  
 Дополнительные сведения о свойствах, которые можно задать в конструкторе служб [!INCLUDE[ssIS](../../includes/ssis-md.md)] , см. в следующих разделах:  
  
-   [Редактор задачи "Файловая система" (страница "Общие")](../../integration-services/control-flow/file-system-task-editor-general-page.md)  
  
-   [Страница «Выражения»](../../integration-services/expressions/expressions-page.md)  
  
 Дополнительные сведения об установке этих свойств в конструкторе служб [!INCLUDE[ssIS](../../includes/ssis-md.md)] см. в следующем разделе:  
  
-   [Задание свойств задач или контейнеров](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
 Дополнительные сведения об установке этих свойств программными средствами см. в следующем разделе:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.FileSystemTask.FileSystemTask>  
  
## <a name="related-tasks"></a>Связанные задачи  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] содержат задачу, которая загружает и отправляет файлы данных и управляет каталогами на серверах. Дополнительные сведения см. в статье [FTP Task](../../integration-services/control-flow/ftp-task.md).  
  
## <a name="file-system-task-editor-general-page"></a>Редактор задачи «Файловая система» (страница «Общие»)
  Используйте страницу **Общие** диалогового окна **Редактор задачи «Файловая система»** для настройки операции файловой системы, выполняемой задачей.  
  
 Необходимо указать диспетчер подключений к источнику и назначению, установив свойства SourceConnection и DestinationConnection. Можно задать либо имена диспетчеров подключения файлов, которые указывают на файлы, используемые задачей в качестве источника или назначения, либо, если пути к файлам хранятся в переменных, имена этих переменных. Чтобы использовать переменные для хранения путей к файлам, вначале необходимо задать значение **True**для параметра соединения с источником IsSourcePathVariable и параметра соединения с назначением IsDestinationPatheVariable. После этого можно выбрать существующие системные или определенные пользователем переменные либо можно создать новые переменные. В диалоговом окне **Добавить переменную** можно настроить переменные и указать область их действия. Областью действия должна быть задача «Файловая система» или родительский контейнер. Дополнительные сведения см. в разделах [Переменные в службах Integration Services (SSIS)](../../integration-services/integration-services-ssis-variables.md) и [Использование переменных в пакетах](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787).  
  
> [!NOTE]  
>  Чтобы переопределить переменные, выбранные для свойств **SourceConnection** и **DestinationConnection** , введите выражения для свойств **Source** и **Destination** . Эти выражения вводятся на странице **Выражения** редактора задачи **Файловая система**. Например, чтобы задать путь к файлам, которые задача будет использовать в качестве назначения, может потребоваться в одном случае использовать переменную A, а в другом — переменную B.  
  
> [!NOTE]  
>  Задача «Файловая система» работает с одиночным файлом или каталогом. Поэтому данная задача не поддерживает использование символов-шаблонов для выполнения одинаковых операций на множестве файлов или каталогов. Чтобы заставить задачу «Файловая система» повторить операцию для множества файлов или каталогов, поместите ее в контейнер «цикл по каждому элементу». Дополнительные сведения см. в статье [File System Task](../../integration-services/control-flow/file-system-task.md).  
  
 Можно использовать выражения для использования других переменных для  
  
### <a name="options"></a>Параметры  
 **IsDestinationPathVariable**  
 Укажите, хранится ли целевой путь в переменной. Это свойство имеет параметры, указанные в следующей таблице.  
  
|Значение|Description|  
|-----------|-----------------|  
|**True**|Целевой путь хранится в переменной. При выборе этого значения отображается динамический параметр **DestinationVariable**.|  
|**False**|Целевой путь задается в диспетчере подключения файлов. При выборе этого значения отображается динамический параметр **DestinationConnection**.|  
  
 **OverwriteDestination**  
 Укажите, может ли операция перезаписывать файлы в каталоге назначения.  
  
 **Название**  
 Введите уникальное имя для задачи «Файловая система». Это имя используется в качестве метки для значка задачи.  
  
> [!NOTE]  
>  Имена задач в пределах пакета должны быть уникальными.  
  
 **Description**  
 Введите описание задачи «Файловая система».  
  
 **Операция**  
 Выберите операцию файловой системы для выполнения. Это свойство имеет параметры, указанные в следующей таблице.  
  
|Значение|Description|  
|-----------|-----------------|  
|**Копировать каталог**|Скопируйте каталог. При выборе этого значения отображаются динамические параметры для источника и места назначения.|  
|**Копировать файл**|Скопируйте файл. При выборе этого значения отображаются динамические параметры для источника и места назначения.|  
|**Создать каталог**|Создайте каталог. При выборе этого значения отображаются динамические параметры для исходного и целевого каталога.|  
|**Удалить каталог**|Удалите каталог. При выборе этого значения отображаются динамические параметры для источника.|  
|**Удалить содержимое каталога**|Удалите содержимое каталога. При выборе этого значения отображаются динамические параметры для источника.|  
|**Удалить файл**|Удалите файл. При выборе этого значения отображаются динамические параметры для источника.|  
|**Переместить каталог**|Переместите каталог. При выборе этого значения отображаются динамические параметры для источника и места назначения.|  
|**Переместить файл**|Переместите файл. При выборе этого значения отображаются динамические параметры для источника и места назначения. При перемещении файла не включайте его имя в путь назначения.|  
|**Переименовать файл**|Переименуйте файл. При выборе этого значения отображаются динамические параметры для источника и места назначения. При переименовании файла, включите новое имя файла в путь назначения.|  
|**Задать атрибуты**|Задайте атрибуты файла или каталога. При выборе этого значения отображаются динамические параметры для источника и операции.|  
  
 **IsSourcePathVariable**  
 Укажите, хранится ли целевой путь в переменной. Это свойство имеет параметры, указанные в следующей таблице.  
  
|Значение||  
|-----------|-|  
|**True**|Целевой путь хранится в переменной. При выборе этого значения отображается динамический параметр **SourceVariable**.|  
|**False**|Целевой путь задается в диспетчере подключения файлов. При выборе этого значения отображается динамический параметр **DestinationVariable**.|  
  
### <a name="isdestinationpathvariable-dynamic-options"></a>Динамические параметры IsDestinationPathVariable  
  
#### <a name="isdestinationpathvariable--true"></a>IsDestinationPathVariable = True  
 **DestinationVariable**  
 Выберите имя переменной из списка или нажмите кнопку \< **создать переменную...** > для создания новой переменной.  
  
 **См. также:** [Переменные в службах Integration Services (SSIS)](../../integration-services/integration-services-ssis-variables.md), [Добавление переменной](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
#### <a name="isdestinationpathvariable--false"></a>IsDestinationPathVariable = False  
 **DestinationConnection**  
 Выберите из списка диспетчер подключения файлов или нажмите кнопку \< **новое подключение...** > для создания нового соединения диспетчера.  
  
 **См. также:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
### <a name="issourcepathvariable-dynamic-options"></a>Динамические параметры IsSourcePathVariable  
  
#### <a name="issourcepathvariable--true"></a>IsSourcePathVariable = True  
 **SourceVariable**  
 Выберите имя переменной из списка или нажмите кнопку \< **создать переменную...** > для создания новой переменной.  
  
 **См. также:** [Переменные в службах Integration Services (SSIS)](../../integration-services/integration-services-ssis-variables.md), [Добавление переменной](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
#### <a name="issourcepathvariable--false"></a>IsSourcePathVariable = False  
 **SourceConnection**  
 Выберите из списка диспетчер подключения файлов или нажмите кнопку \< **новое подключение...** > для создания нового соединения диспетчера.  
  
 **См. также:** [Диспетчер соединения файлов](../../integration-services/connection-manager/file-connection-manager.md)  
  
### <a name="operation-dynamic-options"></a>Динамические параметры операции  
  
#### <a name="operation--set-attributes"></a>Операция = Задать атрибуты  
 **Скрыта**  
 Укажите, виден ли файл или каталог.  
  
 **ReadOnly**  
 Укажите, доступен ли файл только для чтения.  
  
 **Архив**  
 Укажите, готов ли файл или каталог для архивирования.  
  
 **System**  
 Укажите, является ли файл файлом операционной системы.  
  
#### <a name="operation--create-directory"></a>Операция = Создать каталог  
 **UseDirectoryIfExists**  
 Указывает, использует ли операция **Создать каталог** существующий каталог с указанным именем вместо создания нового каталога.  
  
## <a name="see-also"></a>См. также:  
 [Задачи служб Integration Services](../../integration-services/control-flow/integration-services-tasks.md)   
 [Поток управления](../../integration-services/control-flow/control-flow.md)  
  
  