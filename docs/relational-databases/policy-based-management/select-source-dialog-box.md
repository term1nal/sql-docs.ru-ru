---
title: "Диалоговое окно &#171;Выбор источника&#187; | Microsoft Docs"
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
  - "sql13.swb.dmf.selectsource.f1"
ms.assetid: d664c2e5-dd0c-4da8-b27d-aa4ee4fc0ffd
caps.latest.revision: 16
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 16
---
# Диалоговое окно &#171;Выбор источника&#187;
  Это диалоговое окно позволяет выбрать источник политик, которые будут запущены. Чтобы выбрать один или несколько XML-файлов, содержащих политики, выберите **Файлы**. Чтобы запустить политики, найденные в экземпляре [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], выберите **Сервер**.  
  
 Это диалоговое окно можно открыть несколькими способами.  
  
 **Открытие этого окна**  
  
-   В окне "Зарегистрированные серверы" щелкните правой кнопкой мыши элемент **Группы локальных серверов** или любой сервер в области **Группы локальных серверов** или любой сервер в области **Центральные серверы управления** и выберите команду **Оценить политики**. На странице **Выбор политик** диалогового окна **Выполнение политик** нажмите кнопку обзора (**...**).  
  
-   В обозревателе объектов раскройте узлы **Управление** и **Управление политиками**, щелкните правой кнопкой мыши **Политики** и выберите пункт **Импортировать политику**. В диалоговом окне **Импорт** нажмите кнопку "Обзор" (**...**).  
  
-   В обозревателе объектов щелкните правой кнопкой мыши сервер, базу данных или объект базы данных, выберите **Политики** и команду **Вычислить**. На странице **Выбор политик** диалогового окна **Выполнение политик** нажмите кнопку обзора (**...**).  
  
## Параметры  
 **Files**  
 Выберите один или несколько XML-файлов, содержащих политики.  
  
 **Server**  
 Позволяет выбрать сервер, содержащий политики, которые следует запустить.  
  
 **Тип сервера**  
 Политики содержатся только на серверах компонента [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Поле доступно только для чтения.  
  
 **Имя сервера**  
 Выберите экземпляр сервера для подключения. По умолчанию отображается экземпляр сервера, с которым в последний раз устанавливалось соединение.  
  
 **Проверка подлинности**  
 При подключении к экземпляру компонента [!INCLUDE[ssDE](../../includes/ssde-md.md)] доступны два режима проверки подлинности.  
  
 **Режим проверки подлинности Windows (проверка подлинности Windows)**  
 Режим проверки подлинности Windows позволяет подключаться с пользовательской учетной записью Windows.  
  
 **Проверка подлинности SQL Server**  
 При подключении пользователя с указанным именем входа и паролем из ненадежных соединений [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] выполняет проверку подлинности посредством проверки наличия учетной записи входа [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] и проверки совпадения пароля с записанным ранее. Если в службе [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] не задана учетная запись входа, проверка подлинности завершается ошибкой, о которой пользователь получит сообщение.  
  
> [!IMPORTANT]  
>  По возможности используйте аутентификацию Windows.  
  
 **Имя пользователя**  
 Введите имя пользователя для соединения. Этот параметр доступен только при соединении с использованием метода проверки подлинности Windows.  
  
 **Имя входа**  
 Введите имя входа для подключения. Этот параметр доступен только в случае, если выбрано соединение с использованием проверки подлинности [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Пароль**  
 Введите пароль для этого имени входа. Этот параметр можно изменить только в случае, если выбрано соединение с использованием проверки подлинности [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## См. также:  
 [Узел управления политиками (обозреватель объектов)](../../relational-databases/policy-based-management/policy-management-node-object-explorer.md)   
 [Администрирование серверов с помощью управления на основе политик](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  