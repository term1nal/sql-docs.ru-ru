---
title: "Задача &#171;Передача заданий&#187; | Microsoft Docs"
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
  - "sql13.dts.designer.transferjobstask.f1"
helpviewer_keywords: 
  - "задача «Передача заданий» [службы Integration Services]"
ms.assetid: 1bf33885-9c5b-47e4-a549-f5920b66a1de
caps.latest.revision: 28
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 28
---
# Задача &#171;Передача заданий&#187;
  Задача «Передача заданий» служит для передачи одного или нескольких заданий агента [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] между экземплярами [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Задачу «Передача заданий» можно настроить на передачу всех или только определенных заданий. Можно также указать, будут ли переданные задания доступны в месте назначения.  
  
 Задания, подлежащие передаче, могут уже существовать в месте назначения. Задачу «Передача заданий» можно настроить на обработку существующих задач одним из следующих способов:  
  
-   Перезаписать существующие задания.  
  
-   Аварийно завершить задачу при наличии дубликатов заданий.  
  
-   Пропустить дубликаты заданий.  
  
 Во время выполнения задача «Передача заданий» подключается к исходному и целевому серверу, используя один или два диспетчера соединений SMO. Диспетчер соединений SMO настраивается независимо от задачи «Передача заданий», но задача будет на него ссылаться. Диспетчер соединений SMO определяет сервер и режим проверки подлинности, используемый для доступа к серверу. Дополнительные сведения см. в статье [SMO Connection Manager](../../integration-services/connection-manager/smo-connection-manager.md).  
  
## Передача заданий между экземплярами SQL Server  
 Задача «Передача заданий» поддерживает исходные серверы и серверы назначения [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Ограничений в отношении использования определенных версий источника или целевого объекта не существует.  
  
## События  
 Задача «Передача заданий» инициирует уведомляющее событие, сообщающее число переданных заданий, а также событие-предупреждение в случае, когда задание перезаписывается. Задача не сообщает о ходе передачи задания; она сообщает лишь о выполнении 0% и 100%.  
  
## Значение выполнения  
 Значение выполнения, определяемое свойством **ExecutionValue** задачи, возвращает число переданных заданий. Назначив пользовательскую переменную значению свойства **ExecValueVariable** задачи "Передача заданий", можно сделать сведения о передаче заданий доступными для других объектов пакета. Дополнительные сведения см. в разделах [Переменные в службах Integration Services (SSIS)](../../integration-services/integration-services-ssis-variables.md) и [Использование переменных в пакетах](../Topic/Use%20Variables%20in%20Packages.md).  
  
## Записи журнала  
 Задача «Передача заданий» позволяет настраивать запись в журнал следующих событий:  
  
-   TransferJobsTaskStarTransferringObjects   Эта запись журнала сообщает о начале передачи. В записях журнала указывается время запуска.  
  
-   TransferJobsTaskStarTransferringObjects   Эта запись журнала сообщает об окончании передачи. В записях журнала указывается время завершения.  
  
 Кроме того, запись журнала о событии **OnInformation** сообщает число переданных заданий, а запись журнала о событии **OnWarning** производится при перезаписи каждого задания, находящегося на сервере назначения.  
  
## Безопасность и разрешения  
 Чтобы передавать задания, пользователь должен быть членом предопределенной роли сервера sysadmin или членом одной из предопределенных ролей базы данных агента [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] для базы данных msdb как в экземпляре-источнике, так и в экземпляре назначения [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## Настройка задачи «Передача заданий»  
 Значения свойств можно задавать с помощью конструктора [!INCLUDE[ssIS](../../includes/ssis-md.md)] или программными средствами.  
  
 Дополнительные сведения о свойствах, которые можно задать в конструкторе служб [!INCLUDE[ssIS](../../includes/ssis-md.md)] , см. в следующих разделах.  
  
-   [Редактор задачи "Передача заданий" (страница "Общие")](../../integration-services/control-flow/transfer-jobs-task-editor-general-page.md)  
  
-   [Редактор задачи "Передача заданий" (страница "Задания")](../../integration-services/control-flow/transfer-jobs-task-editor-jobs-page.md)  
  
-   [Страница «Выражения»](../../integration-services/expressions/expressions-page.md)  
  
 Дополнительные сведения об установке этих свойств программным путем см. в следующих разделах:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferJobsTask.TransferJobsTask>  
  
## Связанные задачи  
 Дополнительные сведения об установке этих свойств в конструкторе служб [!INCLUDE[ssIS](../../includes/ssis-md.md)] см. в следующем разделе:  
  
-   [Задание свойств задач или контейнеров](../Topic/Set%20the%20Properties%20of%20a%20Task%20or%20Container.md)  
  
## См. также  
 [Задачи служб Integration Services](../../integration-services/control-flow/integration-services-tasks.md)   
 [Поток управления](../../integration-services/control-flow/control-flow.md)  
  
  