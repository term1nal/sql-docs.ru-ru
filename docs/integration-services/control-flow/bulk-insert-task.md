---
title: "Задача &#171;Массовая вставка&#187; | Microsoft Docs"
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
  - "sql13.dts.designer.bulkinserttask.f1"
helpviewer_keywords: 
  - "задача «Массовая вставка»"
  - "копирование данных [службы Integration Services]"
ms.assetid: c5166156-6b4c-4369-81ed-27c4ce7040ae
caps.latest.revision: 61
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 61
---
# Задача &#171;Массовая вставка&#187;
  Задача «Массовая вставка» обеспечивает наиболее эффективный способ копирования больших объемов данных в таблицу или представление [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Предположим, что компания хранит список продуктов объемом в миллион строк в головном компьютере, но система электронной коммерции компании использует для заполнения веб-страниц сервер [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Необходимо обновлять таблицу продуктов [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] по ночам в соответствии с главным списком продуктов, хранящимся в головном компьютере. Для обновления таблицы список продуктов сохраняется в формате с символами табуляции в качестве разделителей и используется задача «Массовая вставка» для копирования данных напрямую в таблицу [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Чтобы обеспечить высокую скорость копирования, данные не должны подвергаться преобразованиям при перемещении из исходного файла в таблицу или представление.  
  
## Особенности использования  
 Перед использованием задачи «Массовая вставка» примите во внимание следующее.  
  
-   Задача «Массовая вставка» может передавать данные только из текстового файла в таблицу или представление [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Для использования задачи "Массовая вставка" в целях передачи данных из других систем управления базами данных (СУБД) необходимо будет экспортировать данные из источника в текстовый файл, а затем импортировать их из текстового файла в таблицу или представление [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Назначением должна быть таблица или представление базы данных [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Если целевая таблица или представление уже содержат данные, то при запуске задачи «Массовая вставка» новые данные добавляются к существующим. Если необходимо заменить данные, запустите задачу «Выполнение SQL», которая выполнит инструкцию DELETE или TRUNCATE до запуска задачи «Массовая вставка». Дополнительные сведения см. в разделе [Execute SQL Task](../../integration-services/control-flow/execute-sql-task.md).  
  
-   В объекте задачи «Массовая вставка» можно использовать файл форматирования. Если имеется файл форматирования, созданный программой **bcp** , можно указать путь к нему в задаче «Массовая вставка». Задача «Массовая вставка» поддерживает файлы форматирования как в формате XML, так и в форматах, отличных от XML. Дополнительные сведения об использовании файлов форматирования см. в разделе [Файлы форматирования для импорта или экспорта данных (SQL Server )](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md).  
  
-   Запускать пакеты, содержащие задачу «Массовая вставка», могут только члены предопределенной роли сервера sysadmin.  
  
## Использование задачи «Массовая вставка» вместе с транзакциями  
 Если размер пакета не указан, вся операция массового копирования рассматривается как одна транзакция. Размер пакета **0** указывает, что все данные вставлены в один пакет. Если указан размер пакета, каждый пакет представляет собой транзакцию, которая фиксируется после завершения работы пакета.  
  
 Поведение задачи «Массовая вставка» по отношению к транзакциям зависит от того, присоединяется ли задача к транзакции пакета. Если задача «Массовая вставка» не присоединена к транзакции пакета, каждый пакет без ошибок фиксируется как отдельный модуль перед попыткой передачи следующего пакета. Если задача «Массовая вставка» присоединена к транзакции пакета, пакеты без ошибок остаются в транзакции по завершении задачи. Фиксация или операция отката этих пакетов произойдет вместе со всем пакетом.  
  
 Ошибка задачи «Массовая вставка» не вызывает автоматического отката успешно загруженных пакетов, а успешное завершение задачи не означает, что пакеты автоматически фиксируются. Операции фиксации и отката происходят только в результате настройки свойств пакета и рабочего процесса.  
  
## Источник и назначение  
 При указании расположения исходного текстового файла учитывайте следующее.  
  
-   Сервер должен иметь разрешение на доступ как к файлу, так и к целевой базе данных.  
  
-   Сервер запускает задачу «Массовая вставка». Таким образом, любой файл форматирования, используемый задачей, должен располагаться на этом сервере.  
  
-   Исходный файл, загружаемый задачей «Массовая вставка», может располагаться на том же сервере, что и база данных [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , в которую вставляются данные, либо на удаленном сервере. Если файл расположен на удаленном сервере, необходимо указать имя в формате UNC.  
  
## Оптимизация производительности  
 Чтобы улучшить производительность, учтите следующее.  
  
-   Если текстовый файл расположен на том же компьютере, что и база данных [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , в которую будут вставляться данные, операция копирования производится с большей скоростью, так как данные не перемещаются по сети.  
  
-   Задача «Массовая вставка» не фиксирует в журнале строки, вызвавшие ошибку. Если эти сведения необходимы, воспользуйтесь выходами ошибок компонентов потока данных для обнаружения строк, вызвавших ошибки в файле исключений.  
  
## Пользовательские записи журнала, доступные в задаче «Массовая вставка»  
 В следующей таблице перечислены пользовательские записи в журнале для задачи «Массовая вставка». Дополнительные сведения см. в разделах [Ведение журналов в службах Integration Services (SSIS)](../../integration-services/performance/integration-services-ssis-logging.md) и [Пользовательские сообщения для ведения журнала](../../integration-services/performance/custom-messages-for-logging.md).  
  
|Запись журнала|Description|  
|---------------|-----------------|  
|**BulkInsertTaskBegin**|Указывает, что массовая вставка началась.|  
|**BulkInsertTaskEnd**|Указывает, что массовая вставка завершена.|  
|**BulkInsertTaskInfos**|Выводит описательные сведения об этой задаче.|  
  
## Настройка задачи «Массовая вставка»  
 Чтобы настроить задачу «Массовая вставка», выполните следующее.  
  
-   Укажите диспетчер соединений OLE DB для подключения к целевой базе данных [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] и таблицу или представление, в которые будут вставляться данные. Задача «Массовая вставка» поддерживает только подключения OLE DB к целевой базе данных.  
  
-   Чтобы получить доступ к исходному файлу, укажите диспетчер соединения с плоскими файлами или диспетчер подключения файлов. Задача «Массовая вставка» использует диспетчер соединений только для местоположения исходного файла. Задача пропускает другие параметры, выбранные в редакторе диспетчера соединений.  
  
-   Определите формат, используемый задачей «Массовая вставка», либо при помощи файла форматирования, либо указав разделители столбцов и строк в исходных данных. При использовании файла форматирования укажите для доступа к нему диспетчер подключения файлов.  
  
-   Укажите, какие действия следует произвести над целевой таблицей или представлением при вставке данных. Эти параметры включают в себя проверочное ограничение, разрешение на вставку данных в столбцы удостоверений, сохранение значений NULL, запуск триггеров, блокировку таблицы.  
  
-   Введите сведения о пакете вставляемых данных, такие как размер пакета, первая и последняя вставляемая строка файла, число ошибок вставки, которые могут произойти, прежде чем задача прекратит вставку строк, а также имена столбцов, которые будут отсортированы.  
  
 Если задача «Массовая вставка» использует для доступа к исходному файлу диспетчер соединений с неструктурированными файлами, задача не использует формат, указанный в нем. Вместо этого задача "Массовая вставка" использует либо формат, указанный в файле форматирования, либо значения свойств задачи RowDelimiter и ColumnDelimiter.  
  
 Значения свойств можно задавать с помощью конструктора [!INCLUDE[ssIS](../../includes/ssis-md.md)] или программными средствами.  
  
 Дополнительные сведения о свойствах, которые можно задать в конструкторе служб [!INCLUDE[ssIS](../../includes/ssis-md.md)] , см. в следующих разделах:  
  
-   [Редактор задачи "Массовая вставка" (страница "Общие")](../../integration-services/control-flow/bulk-insert-task-editor-general-page.md)  
  
-   [Редактор задачи "Массовая вставка" (страница "Соединение")](../../integration-services/control-flow/bulk-insert-task-editor-connection-page.md)  
  
-   [Редактор задачи "Массовая вставка" (страница "Параметры")](../../integration-services/control-flow/bulk-insert-task-editor-options-page.md)  
  
-   [Страница «Выражения»](../../integration-services/expressions/expressions-page.md)  
  
 Дополнительные сведения об установке этих свойств в конструкторе служб [!INCLUDE[ssIS](../../includes/ssis-md.md)] см. в следующем разделе:  
  
-   [Задание свойств задач или контейнеров](../Topic/Set%20the%20Properties%20of%20a%20Task%20or%20Container.md)  
  
### Настройка задачи «Массовая вставка» программными средствами  
 Дополнительные сведения об установке этих свойств программными средствами см. в следующем разделе.  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.BulkInsertTask.BulkInsertTask>  
  
## Связанные задачи  
 [Задание свойств задач или контейнеров](../Topic/Set%20the%20Properties%20of%20a%20Task%20or%20Container.md)  
  
## См. также  
  
-   Техническая статья [В системах, поддерживающих контроль учетных записей, может быть получена ошибка «Не удалось подготовить массовую вставку данных служб SSIS»](http://go.microsoft.com/fwlink/?LinkId=233693)на сайте support.microsoft.com.  
  
-   Техническая статья [Руководство по производительности загрузки данных](http://go.microsoft.com/fwlink/?LinkId=233700)на сайте msdn.microsoft.com.  
  
-   Техническая статья [Использование служб SQL Server Integration Services для массовой загрузки данных](http://go.microsoft.com/fwlink/?LinkId=233701) размещена на сайте simple-talk.com.  
  
  