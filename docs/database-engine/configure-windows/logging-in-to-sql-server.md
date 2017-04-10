---
title: "Вход в систему SQL Server | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "SQL Server, вход в систему"
  - "службы [SQL Server], вход в систему"
  - "Строка подключения TCP"
  - "соединение с компонентом Database Engine"
  - "имена входа [SQL Server], о входе в систему"
  - "Строка подключения именованного канала"
  - "имена входа [SQL Server]"
  - "строка подключения общей памяти"
  - "вход в систему [SQL Server]"
  - "имена входа [SQL Server]"
ms.assetid: 77158a9a-d638-4818-90a1-cb2eb57df514
caps.latest.revision: 34
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 34
---
# Вход в систему SQL Server
  Войти в систему на экземпляре [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] можно с использованием любого графического средства администрирования или из командной строки.  
  
 При входе на экземпляр [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] с помощью графического средства администрирования, такого как среда [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], пользователю предлагается ввести имя сервера, имя входа [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] и, при необходимости, пароль. Если вход на [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] осуществляется с проверкой подлинности Windows, то каждый раз при обращении к экземпляру [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]вводить имя входа SQL Server не нужно. Вместо этого в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] используется учетная запись [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows для автоматического входа в систему. Если [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] работает в смешанном режиме (проверка подлинности [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] и Windows) и пользователь входит в систему с проверкой подлинности [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], то необходимо указать имя входа [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] и пароль. По возможности используйте аутентификацию Windows.  
  
> [!NOTE]  
>  Если при установке [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] были выбраны параметры сортировки с учетом регистра, то для имени входа [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] регистр также учитывается.  
  
## Формат для указания имени сервера SQL Server  
 При соединении с экземпляром компонента [!INCLUDE[ssDE](../../includes/ssde-md.md)] необходимо указать имя экземпляра [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Если экземпляр [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] является экземпляром по умолчанию (неименованным экземпляром), то укажите имя компьютера, на котором установлен [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], или IP-адрес этого компьютера. Если экземпляр [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] является именованным (например, SQLEXPRESS), то укажите имя компьютера, на котором установлен [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], или IP-адрес этого компьютера и добавьте косую черту и имя экземпляра.  
  
 В следующем примере выполняется подключение к экземпляру [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], работающему на компьютере с именем APPHOST. При задании именованного экземпляра в примерах используется имя экземпляра SQLEXPRESS.  
  
 **Примеры:**  
  
|Тип экземпляра|Элемент для имени сервера|  
|----------------------|-------------------------------|  
|Соединение с экземпляром по умолчанию с помощью протокола по умолчанию. (Это рекомендуемый элемент для экземпляра по умолчанию).|APPHOST|  
|Соединение с именованным экземпляром с помощью протокола по умолчанию. (Это рекомендуемый элемент для именованного экземпляра).|APPHOST\SQLEXPRESS|  
|Соединение с экземпляром по умолчанию на том же компьютере при помощи точки для указания, что экземпляр выполняется на локальном компьютере.|.|  
|Соединение с именованным экземпляром на том же компьютере с помощью точки для указания, что экземпляр выполняется на локальном компьютере.|.\SQLEXPRESS|  
|Соединение с экземпляром по умолчанию на том же компьютере при помощи localhost для указания, что экземпляр выполняется на локальном компьютере.|localhost|  
|Соединение с именованным экземпляром на том же компьютере с помощью localhost, указывающее, что экземпляр выполняется на локальном компьютере.|localhost\SQLEXPRESS|  
|Соединение с экземпляром по умолчанию на том же компьютере с помощью (local), указывающее, что экземпляр выполняется на локальном компьютере.|(local)|  
|Соединение с именованным экземпляром на том же компьютере с помощью (local), указывающее, что экземпляр выполняется на локальном компьютере.|(local)\SQLEXPRESS|  
|Соединение с экземпляром по умолчанию на том же компьютере с принудительным подключением к общей памяти.|lpc:APPHOST|  
|Соединение с именованным экземпляром на том же компьютере с принудительным подключением к общей памяти.|lpc:APPHOST\SQLEXPRESS|  
|Соединение с экземпляром по умолчанию, с прослушиванием TCP-адреса 192.168.17.28 с помощью IP-адреса.|192.168.17.28|  
|Соединение с именованным экземпляром, с прослушиванием TCP-адреса 192.168.17.28 с помощью IP-адреса.|192.168.17.28\SQLEXPRESS|  
|Соединение с экземпляром по умолчанию, который не прослушивает TCP-порт по умолчанию, с указанием используемого порта, в данном случае 2828. (Это не является обязательным, если компонент [!INCLUDE[ssDE](../../includes/ssde-md.md)] прослушивает порт по умолчанию 1433.)|APPHOST, 2828|  
|Соединение с именованным экземпляром на назначенный TCP порт, в данном случае 2828. (Это часто необходимо, если служба [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] браузера не выполняется на главном компьютере.)|APPHOST, 2828|  
|Соединение с экземпляром по умолчанию, который не прослушивает TCP-порт по умолчанию, с указанием IP-адреса и TCP-порта, в данном случае 2828.|192.168.17.28,2828|  
|Соединение с именованным экземпляром, с указанием IP-адреса и TCP-порта, в данном случае 2828.|192.168.17.28,2828|  
|Соединение с экземпляром по умолчанию по имени при форсировании соединения TCP.|tcp:APPHOST|  
|Соединение с именованным экземпляром по имени, с принудительным TCP-соединением.|tcp:APPHOST\SQLEXPRESS|  
|Соединение с экземпляром по умолчанию, с указанием имени именованного канала.|\\\APPHOST\pipe\unit\app|  
|Соединение с именованным экземпляром, с указанием имени именованного канала.|\\\APPHOST\pipe\MSSQL$SQLEXPRESS\SQL\query|  
|Соединение с экземпляром по умолчанию по имени, с принудительным подключением к именованным каналам.|np:APPHOST|  
|Соединение с именованным экземпляром по имени, с принудительным подключением к именованным каналам.|np:APPHOST\SQLEXPRESS|  
  
## Проверка протокола соединения  
 При соединении с компонентом [!INCLUDE[ssDE](../../includes/ssde-md.md)] следующий запрос возвратит протокол, используемый для текущего соединения, вместе с методом проверки подлинности (NTLM или Kerberos) и укажет состояние шифрования соединения.  
  
```tsql  
SELECT net_transport, auth_scheme, encrypt_option   
FROM sys.dm_exec_connections   
WHERE session_id = @@SPID;  
```  
  
## Связанные задачи  
 [Вход в экземпляр SQL Server (командная строка)](../../database-engine/configure-windows/log-in-to-an-instance-of-sql-server-command-prompt.md)  
  
 Следующие ресурсы могут помочь устранить проблему с соединением.  
  
-   [Поиск и устранение неполадок соединений с SQL Server Database Engine](http://social.technet.microsoft.com/wiki/contents/articles/how-to-troubleshoot-connecting-to-the-sql-server-database-engine.aspx)  
  
-   [Шаги для устранения неполадок с подключением SQL](http://blogs.msdn.com/b/sql_protocols/archive/2008/04/30/steps-to-troubleshoot-connectivity-issues.aspx)  
  
## См. также  
 [Выбор режима проверки подлинности](../../relational-databases/security/choose-an-authentication-mode.md)  
  
 [Использование программы sqlcmd](../../relational-databases/scripting/use-the-sqlcmd-utility.md)  
  
 [Создание имени входа](../../t-sql/creating-a-login.md)  
  
  