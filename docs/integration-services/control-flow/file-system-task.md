---
title: "Задача &quot;Файловая система&quot; | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.filesystemtask.f1"
helpviewer_keywords: 
  - "задача «Файловая система» [службы Integration Services]"
ms.assetid: 7dd79a6a-e066-4028-a385-1d40f31056f8
caps.latest.revision: 58
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 58
---
# Задача &quot;Файловая система&quot;
  Задача «Файловая система» выполняет операции над файлами и каталогами файловой системы. Например, при помощи задачи «Файловая система» пакет может создавать, перемещать или удалять каталоги и файлы. Можно также использовать данную задачу для установки атрибутов файлов и каталогов. Например, задача «Файловая система« может пометить файлы как скрытые или предназначенные только для чтения.  
  
 Все операции задачи «Файловая система» используют источник, который может быть файлом или каталогом. Например, файл, который копирует задача, или каталог, который она удаляет, является источником. Источник можно указать при помощи диспетчера подключения файлов, который указывает каталог или файл, или определив имя переменной, содержащей путь к источнику. Дополнительные сведения см. в разделах [Диспетчер соединения файлов](../../integration-services/connection-manager/file-connection-manager.md) и [Переменные в службах Integration Services (SSIS)](../../integration-services/integration-services-ssis-variables.md).  
  
 Операции, копирующие и перемещающие файл и каталоги, а также переименовывающие файлы, используют целевой объект и источник. Целевой объект указывается при помощи диспетчера подключения файла или переменной. Операции задачи «Файловая система» можно настроить для возможности перезаписывать целевые файлы и каталоги. Операцию, которая создает новый каталог, можно настроить для использования существующего каталога, имеющего указанное имя. Это позволит избежать ошибки, если каталог уже существует.  
  
## Предопределенные операции файловой системы  
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
  
## Пользовательские записи журнала, доступные в задаче «Файловая система»  
 В следующей таблице перечислены пользовательские записи журнала для задачи «Файловая система». Дополнительные сведения см. в разделах [Ведение журналов в службах Integration Services (SSIS)](../../integration-services/performance/integration-services-ssis-logging.md) и [Пользовательские сообщения для ведения журнала](../../integration-services/performance/custom-messages-for-logging.md).  
  
|Запись журнала|Description|  
|---------------|-----------------|  
|**FileSystemOperation**|Сообщает об операции, выполняемой задачей. Эта запись журнала формируется, когда операция файловой системы начинается и включает сведения об источнике и назначении.|  
  
## Настройка задачи «Файловая система»  
 Значения свойств можно задавать с помощью конструктора [!INCLUDE[ssIS](../../includes/ssis-md.md)] или программными средствами.  
  
 Дополнительные сведения о свойствах, которые можно задать в конструкторе служб [!INCLUDE[ssIS](../../includes/ssis-md.md)] , см. в следующих разделах:  
  
-   [Редактор задачи "Файловая система" (страница "Общие")](../../integration-services/control-flow/file-system-task-editor-general-page.md)  
  
-   [Страница «Выражения»](../../integration-services/expressions/expressions-page.md)  
  
 Дополнительные сведения об установке этих свойств в конструкторе служб [!INCLUDE[ssIS](../../includes/ssis-md.md)] см. в следующем разделе:  
  
-   [Задание свойств задач или контейнеров](../Topic/Set%20the%20Properties%20of%20a%20Task%20or%20Container.md)  
  
 Дополнительные сведения об установке этих свойств программными средствами см. в следующем разделе:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.FileSystemTask.FileSystemTask>  
  
## Связанные задачи  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] содержат задачу, которая загружает и отправляет файлы данных и управляет каталогами на серверах. Дополнительные сведения см. в статье [FTP Task](../../integration-services/control-flow/ftp-task.md).  
  
## См. также  
 [Задачи служб Integration Services](../../integration-services/control-flow/integration-services-tasks.md)   
 [Поток управления](../../integration-services/control-flow/control-flow.md)  
  
  