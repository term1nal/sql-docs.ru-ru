---
title: "Пошаговое руководство. Публикация пакета служб SSIS в представлении SQL | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.ssis.packagepublishwizard.f1"
ms.assetid: d32d9761-93fb-4020-bf82-231439c6f3ac
caps.latest.revision: 12
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 12
---
# Пошаговое руководство. Публикация пакета служб SSIS в представлении SQL
  В этом пошаговом руководстве приводятся подробные инструкции для публикации пакета служб SSIS в качестве представления SQL в базе данных [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## Предварительные требования  
 Для выполнения данного пошагового руководства на компьютере должно быть установлено следующее программное обеспечение.  
  
1.  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] или более поздняя версия с [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
2.  [SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx).  
  
## Шаг 1. Построение и развертывание проекта служб SSIS в каталоге служб SSIS  
 На этом шаге создается пакет служб SSIS, который извлекает данные из поддерживаемого источника данных SSIS (в данном примере будет использоваться база данных [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]) и выводит данные с помощью компонента назначения потоковой передачи данных. Затем будет выполнено построение и развертывание проекта служб SSIS в каталоге служб SSIS.  
  
1.  Запустите **SQL Server Data Tools**. В меню **Пуск** последовательно укажите пункты **Все программы**, **Microsoft SQL Server**и выберите **SQL Server Data Tools**.  
  
2.  Создайте новый проект [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
    1.  В строке меню щелкните **Файл** , выберите **Создать**, а затем нажмите **Проект**.  
  
    2.  Разверните узел **Business Intelligence** на левой панели и нажмите **Службы Integration Services** в древовидной структуре.  
  
    3.  Выберите **Проект служб Integration Services** , если это еще не сделано.  
  
    4.  Укажите **SSISPackagePublishing** в поле **Имя проекта**.  
  
    5.  Укажите расположение для проекта.  
  
    6.  Нажмите кнопку **ОК** , чтобы закрыть диалоговое окно **Новый проект** .  
  
3.  Перетащите компонент **Поток данных** из **области элементов служб SSIS** в конструктор на вкладке **Поток управления** .  
  
4.  Дважды щелкните компонент **Поток данных** в **потоке управления**, чтобы открыть **Конструктор потоков данных**.  
  
5.  Перетащите **исходный компонент** из области элементов в **Конструктор потоков данных** и настройте его на извлечение данных из источника данных.  
  
    1.  Для пошагового руководства создайте тестовую базу данных **TestDB** с таблицей **Сотрудник**. Создайте таблицу с тремя столбцами: **Идентификатор**, **FirstName** и **LastName**.  
  
    2.  Задайте **Идентификатор** в качестве первичного ключа.  
  
    3.  Вставьте две записи со следующими данными.  
  
        |Идентификатор|FirstName|LastName|  
        |--------|---------------|--------------|  
        |1|Джон|Doe|  
        |2|Джейн|Doe|  
  
    4.  Перетащите компонент **Источник OLE DB** из **области элементов служб SSIS** в **Конструктор потоков данных**.  
  
    5.  Настройте компонент на извлечение данных из таблицы **Сотрудник** в базе данных **TestDB** . Выберите **(local).TestDB** для параметра **Диспетчер соединений OLE DB**, **Таблица или представление** для параметра **Режим доступа к данным** и **[dbo].[Сотрудник]** для параметра **Имя таблицы или представления**.  
  
         ![Data Streaming Destination - OLE DB Connection](../../integration-services/data-flow/media/dsd-oledbconnectionmanager.jpg "Data Streaming Destination - OLE DB Connection")  
  
6.  Теперь перетащите **Назначение потоковой передачи данных** из области элементов в поток данных. Этот компонент необходимо найти в разделе "Общие" области элементов.  
  
7.  Соедините компонент **Источник OLE DB** в потоке данных с компонентом **Назначение потоковой передачи данных** .  
  
8.  Построение и развертывание проекта служб SSIS в каталоге служб SSIS  
  
    1.  В строке меню щелкните **Проект** и нажмите кнопку **Развернуть**.  
  
    2.  В соответствии с инструкциями мастера разверните проект в каталоге служб SSIS на локальном сервере базы данных. В следующем примере используется **Power BI** в качестве имени папки и **SSISPackagePublishing** в качестве имени проекта в каталоге служб SSIS.  
  
## Шаг 2. Использование мастера публикации веб-канала данных служб SSIS для публикации пакета служб SSIS в виде представления SQL  
 На этом шаге используется мастер публикации веб-канала данных служб SQL Server Integration Services (SSIS) для публикации пакета служб SSIS в виде представления в базе данных SQL Server. Выходные данные пакета могут быть востребованы посредством запроса этого представления.  
  
 Мастер публикации веб-канала данных служб SSIS создает связанный сервер с помощью поставщика OLE DB для служб SSIS (SSISOLEDB), а затем создает представление SQL, состоящее из запроса на связанном сервере. Этот запрос содержит имя папки, имя проекта и имя пакета в каталоге служб SSIS.  
  
 Во время выполнения представление отправляет запрос поставщику OLE DB относительно служб SSIS через созданный связанный сервер. Поставщик OLE DB для служб SSIS выполняет пакет, указанный в запросе, и возвращает табличный результирующий набор в ответ на запрос.  
  
1.  Откройте **Мастер публикации веб-канала данных служб SSIS**, запустив файл ISDataFeedPublishingWizard.exe из папки C:\Program Files\Microsoft SQL Server\130\DTS\Binn или щелкнув Microsoft SQL Server 2016\SQL Server 2016 Data Feed Publishing Wizard в меню "Пуск\Все программы".  
  
2.  На странице **Вводная** щелкните **Далее** .  
  
     ![Data Feed Publishing Wizard - Introduction Page](../../integration-services/data-flow/media/dsd-feedpublishingwizard-introductionpage.jpg "Data Feed Publishing Wizard - Introduction Page")  
  
3.  На странице **Настройки пакета** выполните следующие задачи.  
  
    1.  Введите **имя** экземпляра SQL Server, содержащее каталог служб SSIS, или щелкните **Обзор** , чтобы выбрать сервер.  
  
         ![Data Feed Publishing Wizard - Package Settings Pag](../../integration-services/data-flow/media/dsd-feedpublishingwizard-packagesettingspage.jpg "Data Feed Publishing Wizard - Package Settings Pag")  
  
    2.  Щелкните **Обзор** рядом с полем "Путь", перейдите в каталог служб SSIS, выберите пакет служб SSIS, который требуется опубликовать (например, **SSISDB**->**SSISPackagePublishing**->**Package.dtsx**), и нажмите кнопку **ОК**.  
  
         ![Data Feed Publishing Wizard - Browse for Package](../../integration-services/data-flow/media/dsd-feedpublishingwizard-browseforpackage.jpg "Data Feed Publishing Wizard - Browse for Package")  
  
    3.  На вкладках "Параметры пакета", "Параметры проекта" и "Диспетчеры соединений" в нижней части страницы введите значения для соответствующих параметров. Кроме того, можно указать ссылку на среду, которую следует использовать для выполнения пакета, и привязать параметры проекта и пакета к переменным среды.  
  
         К переменным среды рекомендуется привязывать конфиденциальные параметры. В данном случае значение конфиденциального параметра гарантированно не будет храниться в обычном текстовом формате в представлении SQL, которое было создано мастером.  
  
    4.  Щелкните **Далее** , чтобы перейти на страницу **Параметры публикации** .  
  
4.  На странице **Параметры публикации** выполните следующие задачи.  
  
    1.  Выберите **базу данных** для создаваемого представления.  
  
         ![Data Feed Publishing Wizard - Publish Settings Pag](../../integration-services/data-flow/media/dsd-feedpublishingwizard-publishsettingspage.jpg "Data Feed Publishing Wizard - Publish Settings Pag")  
  
    2.  Введите **имя** для **представления**. Кроме того, можно выбрать существующее представление в раскрывающемся списке.  
  
    3.  В списке **Параметры** укажите **имя** **связанного сервера** , который следует связать с представлением. Если связанный сервер еще не существует, мастер его создаст перед созданием представления. Кроме того, здесь можно задать значения для **User32BitRuntime** и **времени ожидания** .  
  
    4.  Нажмите кнопку **Дополнительно** . Должно появиться диалоговое окно **Дополнительные параметры** .  
  
    5.  В диалоговом окне **Дополнительные параметры** выполните следующие действия.  
  
        1.  Укажите схему базы данных, в которой нужно создать представление (поле "Схема").  
  
        2.  Укажите, необходимо ли шифрование данных перед их отправкой по сети (поле "Шифрование"). Дополнительные сведения о данном параметре и параметре TrustServerCertificate см. в разделе [Использование шифрования без проверки](http://msdn.microsoft.com/library/ms131691.aspx) .  
  
        3.  Укажите, может ли использоваться самозаверяющий сертификат сервера, если включен параметр шифрования (поле **TrustServerCertificate**).  
  
        4.  Нажмите кнопку **ОК** , чтобы закрыть диалоговое окно **Дополнительные параметры** .  
  
    6.  Нажмите кнопку **Далее** , чтобы перейти к странице **Проверка** .  
  
5.  На странице **Проверка** просмотрите результаты проверки значений для всех параметров. В следующем примере отображается **предупреждение** о наличии связанного сервера, так как такого сервера не существует на выбранном экземпляре SQL Server. Если вы увидите **ошибку** в качестве **результата**, наведите указатель мыши на **ошибку** , чтобы получить сведения о ней. Например, если параметр "Допускать в ходе процесса" для поставщика SSISOLEDB не включен, при выполнении действия "Настройка связанного сервера" появится сообщение об ошибке.  
  
     ![Data Feed Publishing Wizard - Validation Page](../../integration-services/data-flow/media/dsd-feedpublishingwizard-validationpage.jpg "Data Feed Publishing Wizard - Validation Page")  
  
6.  Нажмите кнопку "Сохранить отчет", чтобы сохранить отчет в виде XML-файла.  
  
7.  Нажмите кнопку **Далее** на странице **Проверка** , чтобы перейти на страницу **Сводка** .  
  
8.  Просмотрите выбранные параметры на странице **Сводка** и нажмите кнопку **Публикация** , чтобы начать процесс публикации, который создаст связанный сервер, если он еще не существует на сервере, а затем представления с помощью связанного сервера.  
  
     ![Data Feed Publishing Wizard - Summary Page](../../integration-services/data-flow/media/dsd-feedpublishingwizard-summarypage.jpg "Data Feed Publishing Wizard - Summary Page")  
  
     Теперь выходные данные пакета можно запрашивать путем выполнения следующей инструкции SQL для базы данных SELECT * FROM [SSISPackageView].  
  
9. Нажмите кнопку **Сохранить отчет**, чтобы сохранить этот отчет в виде XML-файла.  
  
10. Просмотрите результаты процесса публикации и нажмите кнопку **Готово** для завершения работы мастера.  
  
    > [!NOTE]  
    >  Не поддерживаются следующие типы данных: text, ntext, image, nvarchar(max), varchar(max) и varbinary(max).  
  
## Шаг 3. Тестирование представления SQL  
 На этом шаге выполняется запуск представления SQL, которое было создано мастером публикации веб-канала данных служб SSIS.  
  
1.  Запустите среду SQL Server Management Studio.  
  
2.  Разверните \<**имя компьютера**>, **Базы данных**, \<**база данных, выбранная в мастере**> и **Представления**.  
  
3.  Щелкните правой кнопкой мыши \<**представление, созданное мастером**> и нажмите кнопку **Выбрать первые 1000 строк**.  
  
4.  Убедитесь, что это результаты из пакета служб SSIS.  
  
## Шаг 4. Проверка выполнение пакета служб SSIS  
 На этом шаге проверяется выполнение пакета служб SSIS.  
  
1.  В SQL Server Management Studio разверните **Каталоги служб Integration Services**, **SSISDB**, далее разверните **папку** , в которой находится проект служб SSIS, разверните **Проекты**, узел проекта, а затем **Пакеты**.  
  
2.  Щелкните правой кнопкой мыши пакет служб SSIS, выберите пункты **Отчеты**, **Стандартные отчеты** и нажмите кнопку **Все выполнения**.  
  
3.  В отчете должно быть отражено выполнение пакета служб SSIS.  
  
    > [!NOTE]  
    >  На компьютере с ОС Windows Vista с пакетом обновления 2 (SP2) в отчете будут отражены два сеанса выполнения пакета служб SSIS (один выполнен успешно, а второй с ошибкой). Не обращайте внимания на сбой, так как он вызван известной проблемой в этой версии.  
  
## Дополнительные сведения  
 Мастер публикации веб-канала данных выполняет следующие важные операции.  
  
1.  Создает связанный сервер и настраивает его на использование поставщика OLE DB для служб SSIS.  
  
2.  Создает представление SQL в указанной базе данных, которое запрашивает выбранный пакет на связанном сервере, где содержатся данные о каталоге.  
  
 В этом разделе описываются процедуры создания связанного сервера и представления SQL без использования мастера публикации веб-канала данных. Кроме того, в нем содержатся дополнительные сведения об использовании функции OPENQUERY с поставщиком OLE DB для служб SSIS.  
  
### Создание связанного сервера с помощью поставщика OLE DB для служб SSIS  
 Создайте связанный сервер с помощью поставщика OLE DB для служб SSIS (SSISOLEDB), выполнив следующий запрос в SQL Server Management Studio.  
  
```  
  
USE [master]  
GO  
  
EXEC sp_addlinkedserver  
@server = N'SSISFeedServer',  
@srvproduct = N'Microsoft',  
@provider = N'SSISOLEDB',  
@datasrc = N'.'  
GO  
  
```  
  
### Создание представления с помощью связанного сервера и данных о каталоге служб SSIS  
 На этом шаге будет создано представление SQL, которое выполняет запрос на связанном сервере, созданном в предыдущем разделе. Этот запрос будет содержать имя папки, имя проекта и имя пакета в каталоге служб SSIS.  
  
 В ходе работы при выполнении представления запрос к связанному серверу, определенный в представлении, запускает пакет служб SSIS, указанный в запросе, и получает выходные данные пакета в виде табличного результирующего набора.  
  
1.  Перед созданием представления введите и выполните следующий запрос в новом окне запроса. OPENQUERY является функцией, возвращающей набор строк, которая поддерживается сервером SQL Server. Она выполняет указанный запрос к заданному связанному серверу с помощью поставщика OLE DB, связанного со связанным сервером. Из предложения FROM запроса можно ссылаться на функцию OPENQUERY как на имя таблицы. Дополнительные сведения см. в разделе [Документация по OPENQUERY в библиотеке MSDN](http://msdn.microsoft.com/library/ms188427.aspx) .  
  
    ```  
    SELECT * FROM OPENQUERY(SSISFeedServer,N'Folder=Eldorado;Project=SSISPackagePublishing;Package=Package.dtsx')   
    GO  
    ```  
  
    > [!IMPORTANT]  
    >  При необходимости обновите имя папки, имя проекта и имя пакета. При сбое функции OPENQUERY в **SQL Server Management Studio**разверните **Объекты сервера**, **Связанные сервера**, **Поставщики**, дважды щелкните поставщика **SSISOLEDB** и убедитесь, что установлен флажок **Допускать в ходе процесса** .  
  
2.  Создайте представление в базе данных **TestDB** в данном пошаговом руководстве, выполнив следующий запрос:  
  
    ```  
  
    USE [TestDB]   
    GO   
  
    CREATE VIEW SSISPackageView AS   
    SELECT * FROM OPENQUERY(SSISFeedServer, 'Folder=Eldorado;Project=SSISPackagePublishing;Package=Package.dtsx')   
    GO  
  
    ```  
  
3.  Протестируйте представление, выполнив следующий запрос.  
  
    ```  
    SELECT * FROM SSISPackageView  
    ```  
  
### Функция OPENQUERY  
 Для функции OPENQUERY используется следующий синтаксис:  
  
```  
SELECT * FROM OPENQUERY(<LinkedServer Name>, N’Folder=<Folder Name from SSIS Catalog>; Project=<SSIS Project Name>; Package=<SSIS Package Name>; Use32BitRuntime=[True | False];Parameters=”<parameter_name_1>=<value1>; parameter_name_2=<value2>”;Timeout=<Number of Seconds>;’)  
```  
  
 Параметры папки, проекта и пакета являются обязательными. Use32BitRuntime, время ожидания и Параметры являются необязательными.  
  
 Use32BitRuntime может иметь только значение 0, 1, True или False. Данный параметр указывает, следует ли пакету использовать 32-разрядную среду выполнения (1 или true), если платформа SQL Server является 64-разрядной.  
  
 Время ожидания указывает число секунд, в течение которых поставщик OLE DB для служб SSIS может ожидать поступления новых данных из пакета служб SSIS. По умолчанию это время составляет 60 секунд. Для времени ожидания можно указать целочисленное значение в диапазоне от 20 до 32 000.  
  
 Параметры содержат значения параметров пакета и параметров проекта. Правила для параметров идентичны параметрам в [DTExec](http://msdn.microsoft.com/library/hh231187.aspx).  
  
 В следующем списке указаны допустимые специальные символы в предложении запроса.  
  
-   Одинарная кавычка (') — этот символ поддерживается стандартной функцией OPENQUERY. Если в предложении запроса нужно использовать одинарную кавычку, используйте две одинарные кавычки (‘’).  
  
-   Двойная кавычка (‘’) — в двойные кавычки заключается часть параметров запроса. Если двойные кавычки содержатся в самом значении параметра, используйте escape-символ. Например: \”.  
  
-   Левая и правая квадратные скобки ([ и ]) — эти символы используются для указания начальных и конечных пробелов. Например, "[ несколько пробелов ]" представляет собой строку " несколько пробелов " с одним начальным и одним конечным пробелами. Если сами эти символы используются в предложении запроса, их необходимо экранировать. Например, \\[ и \\].  
  
-   Косая черта (\\) — каждый символ \, применяемый в запросе предложения, должен использовать escape-символ. Например, \\\ воспринимается как символ \ в предложении запроса.  
  
 Косая черта (\\) — каждый символ \, применяемый в запросе предложения, должен использовать escape-символ. Например, \\\ воспринимается как символ \ в предложении запроса.  
  
## См. также  
 [Назначение потоковой передачи данных](../../integration-services/data-flow/data-streaming-destination.md)   
 [Настройка назначения потоковой передачи данных](../../integration-services/data-flow/configure-data-streaming-destination.md)  
  
  