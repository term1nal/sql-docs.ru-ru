---
title: "Назначение &#171;OLE DB&#187; | Microsoft Docs"
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
  - "sql13.dts.designer.oledbdest.f1"
helpviewer_keywords: 
  - "режим доступа к данным с быстрой загрузкой [службы Integration Services]"
  - "назначение «OLE DB» [службы Integration Services]"
  - "параметры быстрой загрузки [службы Integration Services]"
  - "параметры быстрой загрузки [службы Integration Services]"
  - "назначения [службы Integration Services], OLE DB"
  - "режим доступа к данным с быстрой загрузкой [службы Integration Services]"
  - "вставка данных"
ms.assetid: 873a2fa0-2a02-41fc-a80a-ec9767f36a8a
caps.latest.revision: 79
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 79
---
# Назначение &#171;OLE DB&#187;
  Назначение «OLE DB» загружает данные в различные OLE DB-совместимые базы данных при помощи таблицы базы данных или представления, или команды SQL. Например, источник OLE DB может загрузить данные в таблицы [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Access и базы данных [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Для источника данных [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2007 потребуется поставщик данных, отличный от того, который использовался в предыдущих версиях Excel. Дополнительные сведения см. в разделе [Подключение к книге Excel](../../integration-services/connection-manager/connect-to-an-excel-workbook.md).  
  
 Назначение «OLE DB» предусматривает пять различных режимов доступа для загружаемых данных:  
  
-   Таблица или представление. Можно указать существующую таблицу или представление или создать новую таблицу.  
  
-   Таблица или представление с параметрами быстрой загрузки. Можно указать существующую таблицу или создать новую.  
  
-   Таблица или представление, указанные в переменной.  
  
-   Таблица или представление, указанные в переменной с параметрами быстрой загрузки.  
  
-   Результат выполнения инструкции SQL.  
  
> [!NOTE]  
>  Назначение «OLE DB» не поддерживает параметры. Если необходимо выполнить параметризованную инструкцию INSERT, лучше воспользоваться преобразованием «Команда OLE DB». Дополнительные сведения см. в разделе [OLE DB Command Transformation](../../integration-services/data-flow/transformations/ole-db-command-transformation.md).  
  
 Когда назначение «OLE DB» загружает данные, в которых используется двухбайтовая кодировка (DBCS), они могут быть повреждены, если режим доступа к данным не использует возможность быстрой загрузки и если диспетчер соединений OLE DB использует поставщик [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB для [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SQLOLEDB). Чтобы обеспечить целостность данных в двухбайтовой кодировке (DBCS), необходимо настроить диспетчер подключений OLE DB для использования собственного клиента [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] или использовать один из следующих режимов доступа быстрой загрузки: **Быстрая загрузка таблицы или представления ** или **Быстрая загрузка переменной имени представления или имени таблицы**. Оба параметра доступны в диалоговом окне **Редактор назначения "OLE DB"**. Во время программирования объектной модели служб [!INCLUDE[ssIS](../../includes/ssis-md.md)] нужно задать свойству AccessMode значение **OpenRowset Using FastLoad** или **OpenRowset Using FastLoad From Variable**.  
  
> [!NOTE]  
>  При использовании диалогового окна **Редактор назначения "OLE DB"** в конструкторе [!INCLUDE[ssIS](../../includes/ssis-md.md)] для создания целевой таблицы, в которую целевой объект OLE DB вставляет данные, потребуется вручную выбрать вновь созданную таблицу. Необходимость выбора вручную возникает, когда поставщик OLE DB, такой как OLE DB для DB2, автоматически добавляет идентификаторы схемы в имя таблицы.  
  
> [!NOTE]  
>  В зависимости от типа назначения может потребоваться изменить инструкцию CREATE TABLE, которую формирует диалоговое окно **Редактор назначения "OLE DB"**. Например, некоторые целевые объекты не поддерживают типы данных, которые использует инструкция CREATE TABLE.  
  
 Это назначение использует диспетчер соединений OLE DB для подключения к источнику данных, и диспетчер соединений определяет используемый поставщик OLE DB. Дополнительные сведения см. в статье [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md).  
  
 Проект служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] также содержит объект источника данных, из которого можно создать диспетчер соединений OLE DB, чтобы источники данных и представления источников данных стали доступными для целевой OLE DB.  
  
 Целевой объект OLE DB содержит сопоставления между входными столбцами и столбцами в источнике данных назначения. Нет необходимости сопоставлять входные столбцы всем целевым столбцам, но в зависимости от свойств целевых столбцов могут произойти ошибки, если входные столбцы не сопоставлены целевым столбцам. Например, если целевой столбец не допускает значений NULL, входной столбец должен быть ему сопоставлен. Кроме того, типы данных сопоставленных столбцов должны быть совместимыми. Например, нельзя сопоставить входной столбец строкового типа целевому столбцу числового типа данных.  
  
 Целевой объект OLE DB имеет один обычный вход и один выход ошибок.  
  
 Дополнительные сведения о типах данных см. в разделе [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
## Параметры быстрой загрузки  
 Если целевой объект OLE DB использует режим доступа к данным "быстрая загрузка", можно задать следующие параметры быстрой загрузки в интерфейсе пользователя **Редактор назначения "OLE DB"**.  
  
-   Не совмещать значения идентичности с импортированным файлом данных или использовать уникальные значения, назначенные [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Сохранить значение NULL при выполнении операции массовой загрузки.  
  
-   Проверочное ограничение в целевой таблице или представлении при выполнении операции массового импорта.  
  
-   Получить блокировку на уровне таблиц на период операции массовой загрузки.  
  
-   Указать число строк в пакете и зафиксировать размер.  
  
 Некоторые параметры быстрой загрузки хранятся в свойствах, относящихся к конкретному назначению «OLE DB». Например, параметр FastLoadKeepIdentity определяет, нужно ли хранить значения идентификации, параметр FastLoadKeepNulls указывает, будут ли храниться значения NULL, а параметр FastLoadMaxInsertCommitSize задает количество строк, которые следует фиксировать как пакет. Другие параметры быстрой загрузки хранятся в списке с разделителями-запятыми в свойстве FastLoadOptions. Если назначение "OLE DB" использует все параметры быстрой загрузки, хранящиеся в параметре FastLoadOptions и перечисленные в диалоговом окне **Редактор назначения "OLE DB"**, значение свойства устанавливается в **TABLOCK, CHECK_CONSTRAINTS, ROWS_PER_BATCH=1000**. Значение 1000 означает, что назначение настроено на использование пакетов из 1000 строк.  
  
> [!NOTE]  
>  Любое нарушение ограничения в назначении вызывает сбой обработки всего пакета строк, определенного параметром FastLoadMaxInsertCommitSize.  
  
 Помимо параметров быстрой загрузки, отображенных в диалоговом окне **Редактор назначения "OLE DB"**, можно настроить назначение "OLE DB" для использования параметров массовой загрузки. Для этого введите параметры в свойство FastLoadOptions в диалоговом окне **Расширенный редактор**.  
  
|Параметры быстрой загрузки|Description|  
|----------------------|-----------------|  
|KILOBYTES_PER_BATCH|Устанавливает размер в килобайтах для вставки. Параметр имеет форму **KILOBYTES_PER_BATCH** = \<целое положительное число**>**.|  
|FIRE_TRIGGERS|Устанавливает запуск триггеров при вставке таблицы. Параметр имеет форму **FIRE_TRIGGERS**. Наличие параметра означает, что триггер запускается.|  
|ORDER|Устанавливает способ сортировки введенных данных. Параметр ORDER имеет форму \<имя столбца> ASC&#124;DESC. Количество столбцов может быть любым, необязательно включать порядок сортировки. Если порядок сортировки пропущен, операция вставки предполагает, что данные не отсортированы.<br /><br /> Примечание. Производительность можно увеличить, если использовать параметр ORDER для сортировки загружаемых данных согласно кластеризованному индексу таблицы.|  
  
 Ключевые слова [!INCLUDE[tsql](../../includes/tsql-md.md)] традиционно набираются буквами в верхнем регистре, однако учет их регистра не осуществляется.  
  
 Дополнительные сведения о параметрах быстрой загрузки см. в разделе [BULK INSERT (Transact-SQL)](../../t-sql/statements/bulk-insert-transact-sql.md).  
  
## Устранение неполадок, связанных с назначением «OLE DB»  
 В журнал можно записывать вызовы, сделанные назначением «OLE DB» к внешним поставщика данных. Эта возможность ведения журнала может быть использована для устранения неполадок при сохранении данных во внешние источники данных, выполняемом назначением «OLE DB». Чтобы вести журнал вызовов, которые назначение "OLE DB" совершает к внешним поставщикам данных, необходимо включить ведение журнала пакета и выбрать событие **Диагностика** на уровне пакета. Дополнительные сведения см. в разделе [Инструменты устранения неполадок при выполнении пакетов](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md).  
  
## Настройка целевого объекта OLE DB  
 Значения свойств можно задавать с помощью конструктора [!INCLUDE[ssIS](../../includes/ssis-md.md)] или программными средствами.  
  
 Дополнительные сведения о свойствах, которые можно установить в диалоговом окне **Редактор назначения "OLE DB"** см. в следующих разделах:  
  
-   [Редактор назначения OLE DB (страница "Диспетчер соединений")](../../integration-services/data-flow/ole-db-destination-editor-connection-manager-page.md)  
  
-   [Редактор назначения OLE DB (страница "Сопоставления")](../../integration-services/data-flow/ole-db-destination-editor-mappings-page.md)  
  
-   [Редактор назначения "OLE DB" (страница "Вывод ошибок")](../../integration-services/data-flow/ole-db-destination-editor-error-output-page.md)  
  
 Диалоговое окно **Расширенный редактор** содержит свойства, которые можно установить с помощью программных средств. Дополнительные сведения о свойствах, которые вы можете задать в диалоговом окне **Расширенный редактор** или программными средствами, см. в следующих разделах.  
  
-   [Общие свойства](../Topic/Common%20Properties.md)  
  
-   [Пользовательские свойства OLE DB](../../integration-services/data-flow/ole-db-custom-properties.md)  
  
 Дополнительные сведения о настройке свойств см. в следующих разделах.  
  
-   [Загрузка данных с помощью назначения «OLE DB»](../../integration-services/data-flow/load-data-by-using-the-ole-db-destination.md)  
  
-   [Установление свойств компонента потока данных](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## См. также  
 [Источник OLE DB](../../integration-services/data-flow/ole-db-source.md)  
  
 [Переменные в службах Integration Services (SSIS)](../../integration-services/integration-services-ssis-variables.md)  
  
 [Поток данных](../../integration-services/data-flow/data-flow.md)  
  
  