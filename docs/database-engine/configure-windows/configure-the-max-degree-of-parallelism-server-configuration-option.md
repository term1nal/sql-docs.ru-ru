---
title: "Настройка параметра конфигурации сервера max degree of parallelism | Microsoft Docs"
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
  - "параллельные запросы [SQL Server]"
  - "процессоры [SQL Server], параллельные запросы"
  - "количество процессоров для параллельных запросов"
  - "max degree of parallelism, параметр"
ms.assetid: 86b65bf1-a6a1-4670-afc0-cdfad1558032
caps.latest.revision: 33
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 33
---
# Настройка параметра конфигурации сервера max degree of parallelism
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  В этом разделе описываются способы настройки параметра конфигурации сервера **max degree of parallelism (MAXDOP)** в [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] с помощью среды [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] или [!INCLUDE[tsql](../../includes/tsql-md.md)]. Если экземпляр [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] работает на многопроцессорном компьютере, он определяет оптимальную степень параллелизма, то есть количество процессоров, задействованных для выполнения одной инструкции, для каждого из планов параллельного выполнения. Для ограничения количества процессоров в плане параллельного выполнения может быть использован параметр **max degree of parallelism** . [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] учитывает планы параллельного выполнения для запросов, операций DDL с индексами, параллельной вставки, изменения столбца в режиме "в сети", параллельного сбора статистики и заполнения статических курсоров и курсоров, управляемых набором ключей.
 

  
  
##  <a name="BeforeYouBegin"></a> Перед началом  
  
###  <a name="Restrictions"></a> Ограничения  
  
-   Если параметр affinity mask имеет значение, отличное от значения по умолчанию, он может ограничивать число процессоров, доступных для [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] в симметричных многопроцессорных системах (SMP).  
  
###  <a name="Recommendations"></a> Рекомендации  
  
-   Этот параметр является дополнительным и его следует изменять только опытным администраторам баз данных или сертифицированным техническим специалистам [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Чтобы разрешить серверу определять максимальную степень параллелизма, установите 0 в качестве значения данного параметра, то есть значение по умолчанию. Установка значения 0 в качестве максимальной степени параллелизма позволяет [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] использовать все доступные процессоры (до 64 процессоров). Чтобы отключить создание параллельных планов, присвойте параметру **max degree of parallelism** значение 1. Задайте значение для параметра в диапазоне от 1 до 32 767, чтобы указать максимальное количество процессорных ядер, которые могут быть использованы при выполнении одного запроса. Если указано значение, превышающее количество доступных процессоров, используется действительное количество доступных процессоров. Если у компьютера только один процессор, то значение параметра **max degree of parallelism** учитываться не будет.  
  
-   Значение параметра max degree of parallelism можно переопределить, задав в инструкции указание запроса MAXDOP. Дополнительные сведения см. в разделе [Указания запросов (Transact-SQL)](../Topic/Query%20Hints%20\(Transact-SQL\).md).  
  
-   Операции по созданию и перестройке индексов, а также по удалению кластеризованного индекса могут оказаться достаточно ресурсоемкими. Значение параметра max degree of parallelism для операций с индексами можно переопределить, указав в инструкции параметр индекса MAXDOP. Значение MAXDOP применяется к инструкции во время выполнения и в метаданных индекса не хранится. Дополнительные сведения см. в статье [Настройка параллельных операций с индексами](../../relational-databases/indexes/configure-parallel-index-operations.md).  
  
-   Помимо запросов и операций с индексами, этот параметр также управляет степенью параллелизма при выполнении инструкций DBCC CHECKTABLE, DBCC CHECKDB и DBCC CHECKFILEGROUP. Планы параллельного выполнения для этих инструкций можно отключить с помощью флага трассировки 2528. Дополнительные сведения см. в разделе [Флаги трассировки (Transact-SQL)](../Topic/Trace%20Flags%20\(Transact-SQL\).md).  
  
###  <a name="Security"></a> Безопасность  
  
####  <a name="Permissions"></a> Разрешения  
 Разрешения на выполнение хранимой процедуры **sp_configure** без параметров или только с первым параметром по умолчанию предоставляются всем пользователям. Для выполнения процедуры **sp_configure** с обоими параметрами для изменения параметра конфигурации или запуска инструкции RECONFIGURE необходимо иметь разрешение ALTER SETTINGS на уровне сервера. Разрешение ALTER SETTINGS неявным образом предоставлено предопределенным ролям сервера **sysadmin** и **serveradmin** .  
  
##  <a name="SSMSProcedure"></a> Использование среды SQL Server Management Studio  
  
#### Настройка параметра максимальной степени параллелизма  
  
1.  В **обозревателе объектов** щелкните правой кнопкой мыши сервер и выберите пункт **Свойства**.  
  
2.  Щелкните узел **Дополнительно** .  
  
3.  В поле **Максимальная степень параллелизма** укажите максимальное число процессоров, которое может быть использовано в плане параллельного выполнения.  
  
##  <a name="TsqlProcedure"></a> Использование Transact-SQL  
  
#### Настройка параметра максимальной степени параллелизма  
  
1.  Установите соединение с компонентом [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  На панели «Стандартная» нажмите **Создать запрос**.  
  
3.  Скопируйте следующий пример в окно запроса и нажмите кнопку **Выполнить**. В этом примере описывается использование процедуры [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) для задания значения параметра `max degree of parallelism` равным `8`.  
  
```tsql  
USE AdventureWorks2012 ;  
GO   
EXEC sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE WITH OVERRIDE;  
GO  
EXEC sp_configure 'max degree of parallelism', 8;  
GO  
RECONFIGURE WITH OVERRIDE;  
GO  
```  
  
 Дополнительные сведения см. в статье [Параметры конфигурации сервера (SQL Server)](../../database-engine/configure-windows/server-configuration-options-sql-server.md).  
  
##  <a name="FollowUp"></a> Продолжение: после настройки параметра max degree of parallelism  
 Параметр вступает в силу немедленно, без перезапуска сервера.  
  
## См. также:  
 [Параметр конфигурации сервера «affinity mask»](../../database-engine/configure-windows/affinity-mask-server-configuration-option.md)   
 [RECONFIGURE (Transact-SQL)](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Параметры конфигурации сервера (SQL Server)](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [CREATE INDEX (Transact-SQL)](../../t-sql/statements/create-index-transact-sql.md)   
 [ALTER INDEX (Transact-SQL)](../../t-sql/statements/alter-index-transact-sql.md)   
 [ALTER TABLE (Transact-SQL)](../../t-sql/statements/alter-table-transact-sql.md)   
 [DBCC CHECKTABLE (Transact-SQL)](../../t-sql/database-console-commands/dbcc-checktable-transact-sql.md)   
 [DBCC CHECKDB (Transact-SQL)](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)   
 [DBCC CHECKFILEGROUP (Transact-SQL)](../../t-sql/database-console-commands/dbcc-checkfilegroup-transact-sql.md)   
 [Настройка параллельных операций с индексами](../../relational-databases/indexes/configure-parallel-index-operations.md) 
 [Указания запросов &#40; Transact-SQL и #41;](../Topic/Query%20Hints%20\(Transact-SQL\).md)    
 [Установка параметров индекса](../../relational-databases/indexes/set-index-options.md)  
  
  