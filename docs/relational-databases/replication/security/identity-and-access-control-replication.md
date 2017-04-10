---
title: "Идентификатор и управление доступом (репликация) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "управление доступом [репликация SQL Server]"
  - "безопасность [репликация SQL Server], управление идентификаторами и доступом"
  - "проверка подлинности [репликация SQL Server]"
  - "идентификатор [репликация]"
ms.assetid: 4da0e793-1ee4-4f69-a80b-45c6732a238d
caps.latest.revision: 8
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 8
---
# Идентификатор и управление доступом (репликация)
  Аутентификация — это процесс, в котором сущности (обычно компьютер в данном контексте) проверяет, что другой сущности, также называемой *участника*, кто или что он выдает является (обычно другого компьютера или пользователя). Авторизация — это процесс, с помощью которого авторизованный участник получает доступ к ресурсам, например к файлу в файловой системе или таблице в базе данных.  
  
 Система безопасности репликации использует проверку подлинности и авторизацию для контроля доступа к реплицируемым объектам базы данных, к компьютерам и агентам, участвующим в процессе репликации. Эти действия выполняются с помощью трех механизмов.  
  
-   Безопасность агентов  
  
     Модель безопасности агентов репликации обеспечивает точный контроль учетных записей, под которыми запускаются и подключаются агенты репликации. Подробные сведения о модели безопасности агентов см. в разделе [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md). Сведения о настройке имен входа и паролей агентов см. в разделе [Управление именами входа и паролями в репликации](../../../relational-databases/replication/security/manage-logins-and-passwords-in-replication.md).  
  
-   Роли администрирования  
  
     Убедитесь, что для настройки, обслуживания и обработки репликации используются правильные роли серверов и баз данных. Дополнительные сведения см. в статье [Security Role Requirements for Replication](../../../relational-databases/replication/security/security-role-requirements-for-replication.md).  
  
-   Список доступа к публикации (PAL)  
  
     Предоставьте доступ к публикациям с помощью списка доступа к публикации. Он работает так же, как и список управления доступом [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows. Когда подписчик подключается к издателю или распространителю и запрашивает доступ к публикации, данные для проверки подлинности, переданные агентом, проверяются согласно списку доступа к публикации. Дополнительные сведения и рекомендации для списка доступа к публикации см. в разделе [организация безопасности издателя](../../../relational-databases/replication/security/secure-the-publisher.md).  
  
## Фильтрование опубликованных данных  
 В дополнение к использованию проверки подлинности и авторизации для контроля доступа к реплицируемым данным и объектам репликация имеет два параметра для управления доступными данными на подписчике: фильтрация по столбцам и строкам. Дополнительные сведения о фильтрации см. в разделе [Фильтрация опубликованных данных](../../../relational-databases/replication/publish/filter-published-data.md).  
  
 При определении статьи можно опубликовать только те столбцы, которые необходимы для публикации, и пропустить несущественные столбцы или столбцы, которые содержат конфиденциальные данные. Например, при публикации таблицы **Заказчик** из базы данных Adventure Works для продавцов на выезде можно пропустить столбец **AnnualSales** , который может быть важен лишь для администрации компании.  
  
 Фильтрация опубликованных данных позволяет ограничить доступ к данным и указать данные, доступные на подписчике. Например, можно отфильтровать таблицу **Заказчик** так, чтобы партнеры компании получали сведения только о тех заказчиках, для которых в столбце **ShareInfo** имеется значение «да». При репликации слиянием может возникать проблема безопасности, если используется параметризованный фильтр, содержащий HOST_NAME(). Для получения дополнительных сведений, см. раздел «Фильтрация с помощью HOST_NAME()» в [параметризованные фильтры строк](../../../relational-databases/replication/merge/parameterized-row-filters.md).  
  
## См. также:  
 [Безопасность и защита и #40; Репликация & #41;](../../../relational-databases/replication/security/security-and-protection-replication.md)   
 [Общие сведения о безопасности и #40; Репликация & #41;](../../../relational-databases/replication/security/security-overview-replication.md)   
 [& Угроз и уязвимостей #40; Репликация & #41;](../../../relational-databases/replication/security/threat-and-vulnerability-mitigation-replication.md)  
  
  