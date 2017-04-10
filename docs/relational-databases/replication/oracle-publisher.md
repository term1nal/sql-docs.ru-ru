---
title: "Издатель Oracle | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.newpubwizard.selectoraclepublisher.f1"
ms.assetid: 019b7c49-dcca-445d-8969-5982a8ccbc1a
caps.latest.revision: 22
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 22
---
# Издатель Oracle
  Начиная с версии [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] позволяет публиковать данные из базы данных Oracle, используя репликацию моментальных снимков и репликацию транзакций. Дополнительные сведения см. в разделе [Обзор публикации Oracle](../../relational-databases/replication/non-sql/oracle-publishing-overview.md).  
  
 Издатель Oracle должен использовать удаленный распространитель [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ; данный мастер должен быть запущен на этом сервере после установки и тестирования необходимого сетевого ПО Oracle. Дополнительные сведения см. в разделе [настроить издатель Oracle](../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md).  
  
> [!IMPORTANT]  
>  Если другой администратор настроил базу данных Oracle в качестве издателя, после нажатия кнопки **Далее** будет выбран запрос на ввод пароля для имени входа репликации, используемого для подключения к этой базе данных Oracle. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] установит соответствие между именем входа и соединением связанного сервера с базой данных Oracle. При следующих соединениях с этой базой данных Oracle вводить пароль не потребуется.  
  
## Параметры  
 **Издатели Oracle**  
 Выберите издатель Oracle из списка. Этот список содержит издателей Oracle, ранее настроенных на использование данного сервера, к которому данный мастер обращается как к их распространителю. Если этот список пуст или нужный издатель Oracle в нем отсутствует, щелкните **Добавить издатель Oracle**.  
  
 **Добавить издатель Oracle**  
 Щелкните для запуска **Свойства распространителя** диалоговое окно. В этом диалоговом окне щелкните **Добавить**, затем — **Добавить издатель Oracle**. В диалоговом окне **Соединение с сервером** укажите имя сервера Oracle, имя входа и пароль для схемы администраторской учетной записи репликации. Дополнительные сведения см. в разделе [подключение к серверу & #40; Oracle & #41; входа](../../relational-databases/replication/connect-to-server-oracle-login.md).  
  
> [!NOTE]  
>  Если сервер, к которому обращается этот мастер, еще не настроен как распространитель, выдается запрос на его настройку.  
  
## См. также:  
 [Создание публикации из базы данных Oracle](../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md)   
 [Справочник по свойствам & #40; Репликация & #41;](../../relational-databases/replication/properties-reference-replication.md)  
  
  