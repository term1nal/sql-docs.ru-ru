---
title: "Задача &#171;Очистка журнала&#187; (план обслуживания) | Microsoft Docs"
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
  - "sql13.swb.maint.historycleanup.f1"
helpviewer_keywords: 
  - "диалоговое окно «Задача "Очистка журнала"»"
ms.assetid: 66bb6c39-958c-4053-a27f-b1118d2567f5
caps.latest.revision: 21
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 21
---
# Задача &#171;Очистка журнала&#187; (план обслуживания)
  Используйте диалоговое окно **Задача «Очистка журнала»** , чтобы исключить устаревшие данные предыстории из таблиц в базе данных msdb. Эта задача поддерживает удаление и восстановление журнала резервного копирования, журнала заданий агента [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], а также журнала плана обслуживания.  
  
 Эта инструкция применяет инструкции **sp_purge_jobhistory** и **sp_delete_backuphistory**.  
  
## Список элементов пользовательского интерфейса  
 **Соединение**  
 Выберите соединение с сервером, которое будет использоваться для выполнения этой задачи.  
  
 **Создать**  
 Создать новое соединение с сервером для его использования при выполнении этой задачи. Диалоговое окно **Создать соединение** описано ниже в этом разделе.  
  
 **Журнал резервного копирования и восстановления**  
 Хранение записей о том, когда были созданы последние резервные копии, может помочь [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] в создании плана восстановления, когда потребуется восстановить базу данных. Срок хранения должен быть не меньше периода создания полных резервных копий базы данных.  
  
 **Журнал заданий агента SQL Server**  
 Этот журнал может помочь устранить ошибки, возникшие при выполнении заданий, или определить, почему были выполнены операции с базой данных.  
  
 **Журнал плана обслуживания**  
 Этот журнал может помочь устранить ошибки, возникшие при выполнении заданий плана обслуживания, или определить, почему были выполнены операции с базой данных.  
  
 **Удалить из журнала записи старше**  
 Укажите возраст элементов, которые следует удалить.  
  
 **Просмотр T-SQL**  
 Просмотрите инструкции [!INCLUDE[tsql](../../includes/tsql-md.md)], выполняемые для данной задачи по отношению к серверу, на основе выбранных параметров.  
  
> [!NOTE]  
>  Если количество затронутых объектов велико, построение этого отображения может занять значительное время.  
  
## Диалоговое окно «Создание соединения»  
 **Имя соединения**  
 Введите имя нового соединения.  
  
 **Выберите или введите имя сервера**  
 Выберите сервер для подключения при выполнении этой задачи.  
  
 **Обновить**  
 Обновите список доступных серверов.  
  
 **Введите данные для входа на сервер**  
 Укажите способ проверки подлинности на сервере.  
  
 **Использовать встроенную безопасность Windows**  
 Подключитесь к экземпляру компонента SQL Server [!INCLUDE[ssDE](../../includes/ssde-md.md)] с помощью проверки подлинности Microsoft Windows.  
  
 **Использовать указанные имя пользователя и пароль**  
 Подключитесь к экземпляру компонента SQL Server [!INCLUDE[ssDE](../../includes/ssde-md.md)] с помощью проверки подлинности SQL Server. Этот параметр недоступен.  
  
 **Имя пользователя**  
 Укажите имя входа, используемое при проверке подлинности [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Этот параметр недоступен.  
  
 **Пароль**  
 Укажите используемый при проверке подлинности пароль. Этот параметр недоступен.  
  
## См. также:  
 [sp_purge_jobhistory (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-purge-jobhistory-transact-sql.md)   
 [sp_delete_backuphistory (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql.md)  
  
  