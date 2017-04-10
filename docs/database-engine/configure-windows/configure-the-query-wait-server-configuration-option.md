---
title: "Настройка параметра конфигурации сервера query wait | Microsoft Docs"
ms.custom: ""
ms.date: "03/02/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "запросы [SQL Server], время ожидания"
  - "время [SQL Server], время ожидания запроса"
  - "query wait, параметр [SQL Server]"
ms.assetid: 0fc4aa01-65a3-4a33-9ef4-caca41add238
caps.latest.revision: 26
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 26
---
# Настройка параметра конфигурации сервера query wait
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  В этом разделе описано, как настроить параметр конфигурации сервера **query wait** в [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] с помощью среды [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] или [!INCLUDE[tsql](../../includes/tsql-md.md)]. Запросы, требующие много памяти (например, включающие сортировку и хеширование), помещаются в очередь, если для выполнения запроса не хватает памяти. Параметр **query wait** указывает время в секундах (от 0 до 2147483647), в течение которого запрос будет ожидать необходимые ресурсы. Значение по умолчанию для этого параметра равно -1. Это означает, что время ожидания вычисляется как время на запрос, умноженное на 25 раз.  
  
> [!IMPORTANT]  
>  Транзакция, содержащая ожидающий запрос, может блокироваться, пока запрос ожидает памяти. В редких ситуациях возможна неопределяемая взаимоблокировка. Уменьшение времени ожидания запроса снижает вероятность такой взаимоблокировки. Со временем ожидающий запрос будет отменен, и блокировка транзакции снимется. Однако увеличение максимального времени ожидания может увеличить время, необходимое для отмены запроса. Этот параметр не рекомендуется менять.  
  
 **В этом разделе**  
  
-   **Перед началом работы выполните следующие действия.**  
  
     [Рекомендации](#Recommendations)  
  
     [Безопасность](#Security)  
  
-   **Настройка параметра query wait**  
  
     [Среда SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Дальнейшие действия.**  [После настройки параметра query wait](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Перед началом  
  
###  <a name="Recommendations"></a> Рекомендации  
  
-   Этот параметр является дополнительным и его следует изменять только опытным администраторам баз данных или сертифицированным техническим специалистам [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
###  <a name="Security"></a> Безопасность  
  
####  <a name="Permissions"></a> Разрешения  
 Разрешения на выполнение хранимой процедуры **sp_configure** без параметров или только с первым параметром по умолчанию предоставляются всем пользователям. Для выполнения процедуры **sp_configure** с обоими параметрами для изменения параметра конфигурации или запуска инструкции RECONFIGURE необходимо иметь разрешение ALTER SETTINGS на уровне сервера. Разрешение ALTER SETTINGS неявным образом предоставлено предопределенным ролям сервера **sysadmin** и **serveradmin** .  
  
##  <a name="SSMSProcedure"></a> Использование среды SQL Server Management Studio  
  
#### Настройка параметра query wait  
  
1.  В обозревателе объектов щелкните правой кнопкой мыши сервер и выберите пункт **Свойства**.  
  
2.  Щелкните узел **Дополнительно** .  
  
3.  В разделе **Параллелизм**введите необходимое значение параметра **query wait** .  
  
##  <a name="TsqlProcedure"></a> Использование Transact-SQL  
  
#### Настройка параметра query wait  
  
1.  Установите соединение с компонентом [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  На панели «Стандартная» нажмите **Создать запрос**.  
  
3.  Скопируйте следующий пример в окно запроса и нажмите кнопку **Выполнить**. В этом примере описывается использование процедуры [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) для задания значения параметра `query wait` равным `7500` секундам.  
  
```tsql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE ;  
GO  
EXEC sp_configure 'query wait', 7500 ;  
GO  
RECONFIGURE;  
GO  
  
```  
  
 Дополнительные сведения см. в статье [Параметры конфигурации сервера (SQL Server)](../../database-engine/configure-windows/server-configuration-options-sql-server.md).  
  
##  <a name="FollowUp"></a> Дальнейшие действия. После настройки параметра query wait  
 Параметр вступает в силу немедленно, без перезапуска сервера.  
  
## См. также:  
 [RECONFIGURE (Transact-SQL)](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Параметры конфигурации сервера (SQL Server)](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  