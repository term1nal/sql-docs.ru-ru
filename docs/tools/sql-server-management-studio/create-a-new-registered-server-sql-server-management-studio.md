---
title: "Создание нового зарегистрированного сервера (среда SQL Server Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.swb.registerserver.general.sqlce.f1"
  - "sql13.swb.registerserver.general.sqlserver.f1"
helpviewer_keywords: 
  - "зарегистрированные серверы [SQL Server], создание зарегистрированных серверов"
ms.assetid: 716ea070-a3b5-4514-9de2-82ce8a96514b
caps.latest.revision: 31
author: "stevestein"
ms.author: "sstein"
manager: "jhubbard"
caps.handback.revision: 31
---
# Создание нового зарегистрированного сервера (среда SQL Server Management Studio)
  В этом разделе описывается, как сохранить сведения о соединении для серверов, к которым часто выполняется обращение, путем регистрации сервера в компоненте «Зарегистрированные серверы» среды [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] в [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Сервер может быть зарегистрирован в обозревателе объектов до или во время подключения. Для регистрации экземпляра сервера на локальном компьютере существует специальный пункт меню.  
  
 Существует два вида зарегистрированных серверов.  
  
-   Группы локальных серверов  
  
     Группы локальных серверов можно использовать для простого подключения к серверам, которыми пользователь часто управляет. И локальные, и нелокальные серверы регистрируются в группах локальных серверов. Группы локальных серверов уникальны для каждого пользователя. Сведения о том, как обмениваться сведениями о зарегистрированном сервере, см. в разделах [Экспорт сведений компонента "Зарегистрированные серверы" (среда SQL Server Management Studio)](../../tools/sql-server-management-studio/export-registered-server-information-sql-server-management-studio.md) и [Импорт сведений компонента "Зарегистрированные серверы" (среда SQL Server Management Studio)](../../tools/sql-server-management-studio/import-registered-server-information-sql-server-management-studio.md).  
  
    > [!NOTE]  
    >  Рекомендуется использовать проверку подлинности Windows.  
  
-   Центральные серверы управления  
  
     Центральные серверы управления сохраняют регистрации серверов на центральном сервере управления, а не в файловой системе. Центральные серверы управления и подчиненные зарегистрированные серверы могут быть зарегистрированы только с помощью проверки подлинности Windows. После регистрации центральных серверов управления связанные с ним зарегистрированные серверы будут отображены автоматически. Дополнительные сведения о центральных серверах управления в разделе [Администрирование нескольких серверов с помощью центральных серверов управления](../../relational-databases/administer-multiple-servers-using-central-management-servers.md). Версии [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ранее [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] нельзя назначить в качестве сервера централизованного управления.  
  
##  <a name="SSMSProcedure"></a> Использование среды SQL Server Management Studio  
  
#### Автоматическая регистрация экземпляров локального сервера  
  
-   В компоненте "Зарегистрированные серверы" щелкните правой кнопкой мыши любой узел в дереве "Зарегистрированные серверы", затем выберите **Обновить регистрацию локального сервера**.  
  
#### Создание нового зарегистрированного сервера  
  
1.  Если компонент «Зарегистрированные серверы» не виден в среде [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], в меню **Вид** выберите **Зарегистрированные серверы**.  
  
     **Тип сервера**  
     При регистрации сервера из окна "Зарегистрированные серверы" поле **Тип сервера** доступно только для чтения и соответствует типу сервера, который выводится на панели "Зарегистрированные серверы". Для регистрации сервера другого типа выберите **ядро СУБД**, **службу Analysis Server**, **службы Reporting Services**или **службы Integration Services** на панели инструментов **Зарегистрированные серверы** перед регистрацией нового сервера.  
  
     **Имя сервера**  
     Выберите экземпляр сервера для регистрации в формате: *\<имя_сервера>\>*[\\*\<имя_экземпляра>*].  
  
     **Проверка подлинности**  
     При соединении с экземпляром [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] доступны два режима проверки подлинности.  
  
     **Проверка подлинности Windows.**  
     Режим проверки подлинности Windows позволяет пользователям подключаться с помощью учетных записей [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows.  
  
     **Проверка подлинности SQL Server**  
     При подключении пользователя с указанным именем входа и паролем из ненадежных соединений [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] выполняет проверку подлинности посредством проверки наличия учетной записи входа [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] и проверки совпадения пароля с записанным ранее. Если в службе [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] не задана учетная запись входа, проверка подлинности завершается ошибкой, о которой пользователь получит сообщение.  
  
    > [!IMPORTANT]  
    >  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)] Дополнительные сведения см. в разделе [Выбор режима проверки подлинности](../../relational-databases/security/choose-an-authentication-mode.md).  
  
     **Имя пользователя**  
     Показывает текущее имя пользователя, с которым устанавливается соединение. Этот параметр только для чтения доступен лишь при соединении с использованием метода проверки подлинности Windows. Чтобы изменить **Имена пользователей**, войдите в систему под другим именем.  
  
     **Имя входа**  
     Введите имя входа для подключения. Этот параметр доступен только в том случае, если выбрано соединение с использованием проверки подлинности [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     **Пароль**  
     Введите пароль для этого имени входа. Этот параметр доступен для изменения только при соединении с использованием метода проверки подлинности [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     **Запомнить пароль**  
     Выберите для шифрования и сохранения введенного пароля в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Этот параметр отображается только в том случае, если выбрано подключение с проверкой подлинности [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
    > [!NOTE]  
    >  Чтобы пароль больше не запоминался, снимите этот флажок и нажмите кнопку **Сохранить**.  
  
     **Имя зарегистрированного сервера**  
     Имя, которое будет отображаться на панели «Зарегистрированные серверы». Это имя не должно совпадать с именем, указанным в поле **Имя сервера** .  
  
     **Описание зарегистрированного сервера**  
     Введите необязательное описание сервера.  
  
     **Тест**  
     Нажмите для проверки соединения с сервером, заданным в поле **Имя сервера**.  
  
     **Сохранять**  
     Нажмите эту кнопку, чтобы сохранить настройки зарегистрированного сервера.  
  
## Многосерверные запросы  
 С помощью окна «Редактор запросов» в среде [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] можно одновременно подключиться и выполнять запросы к нескольким экземплярам [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Возвращаемые запросом результаты можно объединить в единую панель результатов либо они могут возвращаться как отдельные области результатов. Дополнительно редактор запросов может включить столбцы, в которых приводятся имена серверов, предоставивших каждую строку, и имена входа, используемые для подключения к серверам, предоставившим строки. Дополнительные сведения о выполнении многосерверных запросов см. в разделе [Выполнение инструкций на нескольких серверах одновременно (среда SQL Server Management Studio)](../../tools/sql-server-management-studio/execute statements against multiple servers simultaneously.md).  
  
 Чтобы выполнить запрос ко всем серверам в группе локальных серверов, щелкните правой кнопкой мыши группу серверов, укажите пункт **Соединить** и выберите команду **Создать запрос**. В новом окне редактора запросов запросы выполняются по отношению ко всем все серверам в группе с использованием хранимых сведений о соединении, включая контекст проверки подлинности пользователя. Если серверы были зарегистрированы с помощью проверки подлинности [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], но пароль не был сохранен, то установить соединение не удастся.  
  
 Для выполнения запросов применительно ко всем серверам, зарегистрированным на центральном сервере управления, разверните центральный сервер управления, щелкните правой кнопкой мыши группу серверов, укажите пункт **Соединить** и выберите команду **Создать запрос**. Если запросы выполняются в окне «Редактор запросов», то они будут выполнены для всех серверов в группе серверов с использованием хранимых сведений о соединении и контекста проверки подлинности Windows пользователя.  
  
## См. также:  
 [Скрытие системных объектов в обозревателе объектов](../../ssms/object/hide-system-objects-in-object-explorer.md)   
 [Экспорт сведений компонента "Зарегистрированные серверы" (среда SQL Server Management Studio)](../../tools/sql-server-management-studio/export-registered-server-information-sql-server-management-studio.md)   
 [Импорт сведений компонента "Зарегистрированные серверы" (среда SQL Server Management Studio)](../../tools/sql-server-management-studio/import-registered-server-information-sql-server-management-studio.md)  
  
  