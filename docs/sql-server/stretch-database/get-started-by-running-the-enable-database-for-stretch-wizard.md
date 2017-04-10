---
title: "Запуск мастера включения растяжения для базы данных | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "08/05/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.service: "sql-server-stretch-database"
ms.suite: ""
ms.technology: 
  - "dbe-stretch"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
f1_keywords: 
  - "sql13.swb.stretchwizard.f1"
  - "sql13.swb.stretchwizard.createdatabasecredentials.f1"
  - "sql13.swb.stretchwizard.selectdatabasetables.f1"
  - "sql13.swb.stretchwizard.validatesqlserver.f1"
  - "sql13.swb.stretchwizard.selectazuredeployment.f1"
  - "sql13.swb.stretchwizard.configureazuredeployment.f1"
  - "sql13.swb.stretchwizard.Summary.f1"
  - "sql13.swb.stretchwizard.Results.f1"
  - "sql13.swb.stretchwizard.introduction.f1"
helpviewer_keywords: 
  - "База данных Stretch, мастер"
  - "Мастер включения растяжения для базы данных"
ms.assetid: 855dd9fc-f80c-4dbc-bf46-55a9736bfe15
caps.latest.revision: 39
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 38
---
# Запуск мастера включения растяжения для базы данных
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

 Чтобы настроить в базе данных возможность растяжения, запустите мастер включения растяжения для базы данных.  Эта статья содержит сведения о параметрах, используемых в этом мастере.  
  
 Дополнительные сведения о базе данных Stretch см. в статье [Stretch Database](../../sql-server/stretch-database/stretch-database.md). 
 
 >   [!NOTE] Если позднее вы решите отключить Базу данных Stretch, помните, что ее отключение для таблицы или базы данных не ведет к удалению удаленного объекта. Если вы хотите удалить удаленную таблицу или базу данных, это нужно сделать с помощью портала управления Azure. Пока удаленные объекты не будут удалены вручную, их хранение будет сопровождаться затратами в Azure. 
  
## Запуск мастера  
  
1.  В SQL Server Management Studio в обозревателе объектов выберите базу данных, для которой нужно включить растяжение.  
  
2.  Щелкните правой кнопкой мыши и выберите **Задачи**, затем **Растяжение** и щелкните **Включить** для запуска мастера.  
  
##  <a name="Intro"></a> Введение  
 Ознакомьтесь с предназначением мастера и предварительными требованиями.  
 
 Важные предварительные требования перечислены ниже.
 -   Для внесения изменений в базу данных необходимо быть администратором.
 -   Требуется подписка на Microsoft Azure.
 -   SQL Server должен иметь возможность подключения к удаленному серверу Azure.
  
 ![Introduction page of Stretch Database wizard](../../sql-server/stretch-database/media/stretch-wizard-1.png "Introduction page of Stretch Database wizard")  
  
##  <a name="Tables"></a> Выбор таблиц  
 Выберите таблицы, для которых следует применить растяжение.  
 
Таблицы с большим количеством строк отображаются в начале отсортированного списка. Прежде чем вывести список таблиц, мастер анализирует их на предмет типов данных, не поддерживаемых базой данных Stretch. 
  
 ![Select tables page of Stretch Database wizard](../../sql-server/stretch-database/media/stretch-wizard-2.png "Select tables page of Stretch Database wizard")  
  
|Столбец|Описание|  
|------------|-----------------|  
|(нет имени)|Установите флажок в этом столбце, чтобы применить растяжение для выбранной таблицы.|  
|**Название**|Указывает имя таблицы в базе данных.|  
|(нет имени)|Символ в этом столбце может означать предупреждение, не позволяющее включить поддержку Stretch для выбранной таблицы. Кроме того, он может указывать на проблему блокировки, не позволяющую включить выбранную таблицу для Stretch, например связанную с тем, что в таблице используется неподдерживаемый тип данных. Наведите указатель на символ, чтобы увидеть всплывающую подсказку с дополнительной информацией. Дополнительные сведения см. в статье [Ограничения для базы данных Stretch](../../sql-server/stretch-database/limitations-for-stretch-database.md).|  
|**Растянута**|Указывает, что в таблице уже включена поддержка Stretch.|  
|**анализа**|Можно перенести всю таблицу (**Вся таблица**) или указать фильтр для одного из столбцов в этой таблице. Если вы хотите отобрать строки для переноса, использую другую функцию фильтра, после выхода из мастера выполните инструкцию ALTER TABLE, чтобы указать функцию фильтра. Дополнительные сведения о функции фильтров см. в статье [Выбор строк для миграции с использованием функции фильтров](../../sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md). Дополнительные сведения о способах применения функции см. в статье [Настройка базы данных Stretch для таблицы](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md) или [ALTER TABLE (Transact-SQL)](../../t-sql/statements/alter-table-transact-sql.md).|  
|**Строки**|Указывает количество строк в таблице.|  
|**Размер (КБ)**|Указывает размер элемента в килобайтах.|  
  
## При необходимости укажите фильтр строк  
 Если вы хотите отобрать строки для переноса, используя другую функцию фильтра, выполните указанные ниже действия на странице **Выбор таблиц**.  
  
1.  В списке **Выберите таблицы, которые требуется растянуть** выберите пункт **Вся таблица** в строке соответствующей таблицы. Откроется диалоговое окно **Выбор строк для растяжения**.  
  
     ![Define a date-based filter predicate](../../sql-server/stretch-database/media/stretch-wizard-2a.png "Define a date-based filter predicate")  
  
2.  В диалоговом окне **Выбор строк для растяжения** выберите пункт **Выбрать строки**.  
  
3.  В поле **Имя** укажите имя функции фильтра.  
  
4.  В предложении **Где** выберите столбец из таблицы, укажите оператор и введите значение.  
  
5.  Нажмите кнопку **Проверить**, чтобы протестировать функцию. Если функция возвращает результаты из таблицы (т. е. имеются соответствующие условию строки для переноса), проверка завершается с результатом **Успешно**.  

    >   [!NOTE] Текстовое поле, в котором отображается запрос фильтра, доступно только для чтения. Изменить запрос в текстовом поле нельзя.
  
6.  Нажмите кнопку "Готово", чтобы вернуться на страницу **Выбор таблиц**.  

Функция фильтра создается в SQL Server только после завершения работы мастера. А пока это не произошло, вы можете вернуться на страницу **Выбор таблиц** и изменить или переименовать функцию фильтра.

![Select Tables page after defining a filter predicate](../../sql-server/stretch-database/media/stretch-wizard-2b.png "Select Tables page after defining a filter predicate")

Если требуется использовать другой тип функции фильтров, чтобы выбрать строки для переноса, выполните одно из описанных ниже действий.  
  
-   Закройте мастер и выполните инструкцию ALTER TABLE, чтобы включить растяжение для таблицы и указать функцию фильтров. Дополнительные сведения см. в статье [Настройка базы данных Stretch для таблицы](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md).  
  
-   Выполните инструкцию ALTER TABLE, чтобы указать функцию фильтров после выхода из мастера. Необходимые пошаговые инструкции см. в статье [Добавление функции фильтров после запуска мастера](../../sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md#addafterwiz).  
  
##  <a name="Configure"></a> Настройка Azure  
  
1.  Войдите в Microsoft Azure с учетной записью Майкрософт.  
  
     ![Sign in to Azure - Stretch Database wizard](../../sql-server/stretch-database/media/stretch-wizard-3.png "Sign in to Azure - Stretch Database wizard")  
  
2.  Выберите существующую подписку Azure, которую будете использовать для базы данных Stretch. 

>   [!NOTE] Чтобы включить растяжение в базе данных, требуются права администратора используемой подписки. Мастер базы данных Stretch отобразит только подписки, в которых пользователь имеет права администратора.
  
3.  Выберите регион Azure, который будете использовать для базы данных Stretch.
    -   Создаваемый сервер будет расположен именно в этом регионе.  
    -   Если в выбранном регионе имеется несколько серверов, мастер выдаст их список при выборе пункта **Существующий сервер**.
  
     Чтобы свести к минимуму задержки, выбирайте тот регион Azure, в котором находится SQL Server. Дополнительные сведения о регионах см. в статье [Регионы Azure](https://azure.microsoft.com/regions/).  
  
4.  Укажите, следует ли использовать существующий сервер Azure или создать новый.  
  
     Если Active Directory на сервере SQL Server состоит в федерации с Azure Active Directory, вы можете выбрать для взаимодействия SQL Server с удаленным сервером Azure федеративную учетную запись службы. Дополнительные сведения о требованиях для этого параметра см. в статье [ALTER DATABASE SET Options (Transact-SQL)](../Topic/ALTER%20DATABASE%20SET%20Options%20\(Transact-SQL\).md).  
  
    -   **Создание сервера**  
  
        1.  Создайте имя для входа и пароль администратора сервера.  
  
        2.  Вы также можете использовать федеративную учетную запись службы для взаимодействия SQL Server с удаленным сервером Azure.  
  
         ![Create new Azure server - Stretch Database wizard](../../relational-databases/tables/media/stretch-wizard-4.png "Create new Azure server - Stretch Database wizard")  
  
    -   **Существующий сервер**  
  
        1.  Выберите существующий сервер Azure.  
  
        2.  Выберите метод проверки подлинности.  
  
            -   Если выбран параметр **Проверка подлинности SQL Server**, введите имя и пароль администратора.  
  
            -   Выберите метод **Встроенная проверка подлинности Active Directory** , чтобы использовать федеративную учетную запись службы для взаимодействия SQL Server с удаленным сервером Azure. Если выбранный сервер не интегрирован с Azure Active Directory, этот параметр не отображается.
  
         ![Select existing Azure server - Stretch Database wizard](../../sql-server/stretch-database/media/stretch-wizard-5.png "Select existing Azure server - Stretch Database wizard")  
  
##  <a name="Credentials"></a> Защищенные учетные данные  
 Главный ключ базы данных является обязательным элементом для защиты учетных данных, которые база данных Stretch использует для подключения к удаленной базе данных.  
  
 Если главный ключ базы данных уже существует, введите соответствующий пароль.  
  
 ![Secure credentials page of the Stretch Database wizard](../../sql-server/stretch-database/media/stretch-wizard-6b.PNG "Secure credentials page of the Stretch Database wizard")  
  
 Если главного ключа для базы данных нет, введите надежный пароль, чтобы создать такой ключ.  
  
 ![Secure credentials page of the Stretch Database wizard](../../relational-databases/tables/media/stretch-wizard-6.png "Secure credentials page of the Stretch Database wizard")  
  
 Дополнительные сведения о главном ключе базы данных см. в разделах [CREATE MASTER KEY (Transact-SQL)](../../t-sql/statements/create-master-key-transact-sql.md) и [Создание главного ключа базы данных](../../relational-databases/security/encryption/create-a-database-master-key.md). Дополнительные сведения о создаваемых мастером учетных данных см. в разделе [CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)](../../t-sql/statements/create-database-scoped-credential-transact-sql.md).  
  
##  <a name="Network"></a> Выбор IP-адреса  
 Используя диапазон IP-адресов подсети (рекомендуется) или общедоступный IP-адрес сервера SQL Server, создайте в Azure правило брандмауэра, которое позволит SQL Server обмениваться данными с удаленным сервером Azure.  
  
 Сервер Azure будет использовать IP-адрес или адреса, которые вы укажете на этой странице, для разрешения пропуска через брандмауэр Azure входящих данных, запросов и операций управления, инициированных SQL Server. Мастер не вносит изменения в параметры брандмауэра на сервере SQL Server.  
  
 ![Select IP address page of the Stretch Database wizard](../../relational-databases/tables/media/stretch-wizard-7.png "Select IP address page of the Stretch Database wizard")  
  
##  <a name="Summary"></a> Сводка  
 Просмотрите значения, которые вы ввели или выбрали в мастере, а также оценку предполагаемых затрат на использование Azure. Нажмите кнопку **Готово** , чтобы включить растягивание.  
  
 ![Summary page of the Stretch Database wizard](../../sql-server/stretch-database/media/stretch-wizard-8.png "Summary page of the Stretch Database wizard")  
  
##  <a name="Results"></a> Результаты  
 Просмотрите результаты операции.  
  
 Инструкции по отслеживанию состояния переноса данных см. в статье [Мониторинг переноса данных и устранение неполадок при этой операции (база данных Stretch)](../../sql-server/stretch-database/monitor-and-troubleshoot-data-migration-stretch-database.md).  
  
 ![Results page of the Stretch Database wizard](../../sql-server/stretch-database/media/stretch-wizard-9.PNG "Results page of the Stretch Database wizard")  
  
##  <a name="KnownIssues"></a> Устранение неполадок в работе мастера  
 **Сбой в работе мастера подготовки базы данных Stretch.**  
 Если на сервере не активировано использование базы данных Stretch и для активации запущен мастер без разрешений системного администратора, мастер завершит работу с ошибкой. Попросите системного администратора активировать использование базы данных Stretch на экземпляре локального сервера, а затем повторно запустите мастер. Дополнительные сведения см. в разделе [Prerequisite: Permission to enable Stretch Database on the server](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md#EnableTSQLServer).  
  
## Следующие шаги  
 Включение дополнительных таблиц для базы данных Stretch. Мониторинг миграции данных и управление базами данных и таблицами с поддержкой Stretch.  
  
-   Перемещение дополнительных таблиц описано в статье[Enable Stretch Database for a table](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md) .  
  
-   Инструкции по отслеживанию статуса переноса данных см. в разделе [Мониторинг и устранение неполадок переноса данных (база данных Stretch)](../../sql-server/stretch-database/monitor-and-troubleshoot-data-migration-stretch-database.md).  
  
-   [Приостановка и возобновление переноса данных (база данных Stretch)](../../sql-server/stretch-database/pause-and-resume-data-migration-stretch-database.md)  
  
-   [Управление базой данных Stretch и устранение связанных с ней неполадок](../../sql-server/stretch-database/manage-and-troubleshoot-stretch-database.md)  
  
-   [Резервное копирование баз данных с поддержкой Stretch](../../sql-server/stretch-database/backup-stretch-enabled-databases-stretch-database.md)  
  
-   [Восстановление баз данных с поддержкой Stretch](../../sql-server/stretch-database/restore-stretch-enabled-databases-stretch-database.md)  
  
## См. также:  
 [Включение базы данных Stretch для базы данных](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md)   
 [Enable Stretch Database for a table](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md)  
  
  