---
title: "Настройка параметра конфигурации сервера remote query timeout | Microsoft Docs"
ms.custom: ""
ms.date: "03/08/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "ограничение на время выполнения удаленных запросов [SQL Server]"
  - "remote query timeout, параметр"
ms.assetid: 888c8448-933b-41e3-8aa1-c206bc0cdb78
caps.latest.revision: 26
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 25
---
# Настройка параметра конфигурации сервера remote query timeout
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  В этом разделе описываются способы настройки параметра конфигурации сервера **remote query timeout** в [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] с помощью среды [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] или [!INCLUDE[tsql](../../includes/tsql-md.md)]. Параметр **remote query timeout** позволяет задать время ожидания [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (в секундах), в течение которого может выполняться удаленная операция. Значение по умолчанию для этого параметра составляет 600, и это означает ожидание в течение 10 минут. Это значение применяется для исходящих подключений, инициированных компонентом [!INCLUDE[ssDE](../../includes/ssde-md.md)] как удаленный запрос. Это значение не влияет на запросы, получаемые ядром СУБД [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Чтобы отключить время ожидания, установите значение 0. Запрос будет ожидать до момента его отмены.  
  
 Для разнородных запросов параметр **remote query timeout** задает время ожидания удаленным поставщикам в секундах (инициализированное в объекте команд с помощью свойства набора строк DBPROP_COMMANDTIMEOUT) результирующих наборов. Это значение также используется, чтобы задать DBPROP_GENERALTIMEOUT, если это поддерживается удаленным поставщиком. Это приведет к тому, что время ожидания других операций станет равно указанному числу секунд.  
  
 Для удаленных хранимых процедур параметр **remote query timeout** задает число секунд, которое должно пройти после отправки удаленной инструкции `EXEC` перед тем, как истечет время ожидания удаленной хранимой процедуры.  
  
 **В этом разделе**  
  
-   **Перед началом работы выполните следующие действия.**  
  
     [Предварительные требования](#Prerequisites)  
  
     [Безопасность](#Security)  
  
-   **Настройка параметра времени ожидания удаленного запроса с помощью следующих средств:**  
  
     [Среда SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Дальнейшие действия.** [После настройки параметра remote query timeout](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Перед началом  
  
###  <a name="Prerequisites"></a> Предварительные требования  
  
-   Это значение можно установить только при разрешенных соединениях с удаленными серверами.  
  
###  <a name="Security"></a> Безопасность  
  
####  <a name="Permissions"></a> Разрешения  
 Разрешения на выполнение хранимой процедуры **sp_configure** без параметров или только с первым параметром по умолчанию предоставляются всем пользователям. Для выполнения процедуры **sp_configure** с обоими параметрами для изменения параметра конфигурации или запуска инструкции RECONFIGURE необходимо иметь разрешение ALTER SETTINGS на уровне сервера. Разрешение ALTER SETTINGS неявным образом предоставлено предопределенным ролям сервера **sysadmin** и **serveradmin** .  
  
##  <a name="SSMSProcedure"></a> Использование среды SQL Server Management Studio  
  
#### Настройка параметра время ожидания удаленного запроса  
  
1.  В обозревателе объектов щелкните правой кнопкой мыши сервер и выберите пункт **Свойства**.  
  
2.  Выберите узел **Соединения** .  
  
3.  В поле **Подключения удаленного сервера**в области **Время ожидания удаленного запроса** введите или выберите значение от 0 до 2 147 483 647, соответствующее максимальному времени ожидания [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (в секундах).  
  
##  <a name="TsqlProcedure"></a> Использование Transact-SQL  
  
#### Настройка параметра время ожидания удаленного запроса  
  
1.  Установите соединение с компонентом [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  На панели «Стандартная» нажмите **Создать запрос**.  
  
3.  Скопируйте следующий пример в окно запроса и нажмите кнопку **Выполнить**. В этом примере описывается использование хранимой процедуры [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) для задания значения параметра `remote query timeout` равным `0` сек., чтобы отключить время ожидания.  
  
```tsql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'remote query timeout', 0 ;  
GO  
RECONFIGURE ;  
GO  
  
```  
  
 Дополнительные сведения см. в статье [Параметры конфигурации сервера (SQL Server)](../../database-engine/configure-windows/server-configuration-options-sql-server.md).  
  
##  <a name="FollowUp"></a> Дальнейшие действия. После настройки параметра remote query timeout  
 Параметр вступает в силу немедленно, без перезапуска сервера.  
  
## См. также:  
 [RECONFIGURE (Transact-SQL)](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Свойства и поведение наборов строк](../../relational-databases/native-client-ole-db-rowsets/rowset-properties-and-behaviors.md)   
 [Параметры конфигурации сервера (SQL Server)](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  