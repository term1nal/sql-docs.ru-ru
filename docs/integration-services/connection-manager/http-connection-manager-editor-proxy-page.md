---
title: "Редактор диспетчера HTTP-соединений (страница &#171;Прокси-сервер&#187;) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.httpconnection.proxy.f1"
helpviewer_keywords: 
  - "редактор диспетчера HTTP-соединений"
ms.assetid: e831a830-49a3-49c5-8a31-9731fc4fd12e
caps.latest.revision: 27
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 27
---
# Редактор диспетчера HTTP-соединений (страница &#171;Прокси-сервер&#187;)
  Используйте вкладку **Прокси-сервер** диалогового окна **Редактор диспетчера HTTP-соединений** , чтобы настроить диспетчер HTTP-соединений для работы с прокси-сервером. HTTP-соединение позволяет пакету получить доступ к веб-серверу через протокол HTTP, чтобы передавать или принимать файлы.  
  
 Дополнительные сведения о диспетчере HTTP-соединений см. в разделе [HTTP Connection Manager](../../integration-services/connection-manager/http-connection-manager.md). Дополнительные сведения о распространенном сценарии использования диспетчера HTTP-соединений см. в разделе [Web Service Task](../../integration-services/control-flow/web-service-task.md).  
  
## Параметры  
 **Использовать прокси-сервер**  
 Укажите, должен ли диспетчер HTTP-сеансов подключаться через прокси-сервер.  
  
 **URL-адрес прокси-сервера**  
 Введите URL-адрес прокси-сервера.  
  
 **Не использовать прокси-сервер при локальном подключении**  
 Укажите, должен ли диспетчер HTTP-соединений исключать прокси-сервер для локальных адресов.  
  
 **Использовать учетные данные**  
 Укажите, должен ли диспетчер HTTP-соединений использовать учетные данные для прокси-сервера.  
  
 **Имя пользователя**  
 Если диспетчер HTTP-соединений использует учетные данные, необходимо указать имя пользователя, пароль и домен.  
  
 **Пароль**  
 Если диспетчер HTTP-соединений использует учетные данные, необходимо указать имя пользователя, пароль и домен.  
  
 **Домен**  
 Если диспетчер HTTP-соединений использует учетные данные, необходимо указать имя пользователя, пароль и домен.  
  
 **Список адресов, не требующих прокси-сервера**  
 Список адресов, для которых прокси-сервер использоваться не должен.  
  
 **Добавить**  
 Введите адрес, для которого прокси-сервер использоваться не должен.  
  
 **Удалить**  
 Выберите адрес и затем удалите его, нажав кнопку **Удалить**.  
  
## См. также  
 [Справочник по сообщениям об ошибках служб Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Редактор диспетчера HTTP-сеансов (страница "Сервер")](../../integration-services/connection-manager/http-connection-manager-editor-server-page.md)  
  
  