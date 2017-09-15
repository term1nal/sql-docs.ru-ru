---
title: "Запуск клиентского приложения DQS | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "data-quality-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dqs.browseforservers.f1"
  - "sql13.dqs.connecttoserver.f1"
ms.assetid: 0b2aa202-7ab2-4c9d-b0f1-802588053a1e
caps.latest.revision: 13
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 13
---
# Запуск клиентского приложения DQS
  Запустите [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]и выполните вход на [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)].  
  
##  <a name="BeforeYouBegin"></a> Перед началом  
  
###  <a name="Prerequisites"></a> Предварительные требования  
 Необходимо, чтобы установка сервера [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] , запускаемая с помощью файла DQSInstaller.exe, была завершена. Дополнительные сведения см. в разделе [Запуск DQSInstaller.exe для завершения установки сервера DQS](../data-quality-services/install-windows/run-dqsinstaller-exe-to-complete-data-quality-server-installation.md).  
  
###  <a name="Security"></a> Безопасность  
  
####  <a name="Permissions"></a> Разрешения  
 Для входа на сервер [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] необходимо иметь одну из трех ролей DQS (dqs_adminstrator, dqs_kb_editor или dqs_kb_operator) в базе данных DQS_MAIN.  
  
##  <a name="Run"></a> Запуск клиента DQS  
 Чтобы запустить [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] на компьютере, где он установлен, выполните следующие действия:  
  
1.  Нажмите кнопку **Пуск**, выберите **Все программы**, затем **[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]**, затем **Службы Data Quality Services**, затем **Data Quality Client**.  
  
2.  В диалоговом окне **Соединение с сервером** выполните следующие действия:  
  
    1.  Укажите сервер, к которому требуется подключить приложение [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] . Выберите **(LOCAL)** для подключения к [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] на локальном компьютере. Можно также щелкните стрелку вниз и выберите **\< Обзор дополнительные серверы в сети>** для подключения к другому серверу (или для подключения к локальному серверу по имени). Открывается диалоговое окно **Обзор серверов** . Вы можете выбрать сервер на вкладках **Локальные серверы** или **Сетевые серверы** .  
  
    2.  Чтобы зашифровать передачу данных между сервером [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] и клиентом [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)], щелкните **Параметры**, а затем установите флажок **Шифровать соединение** .  
  
3.  Нажмите кнопку **Соединить**.  
  
 Открывается на главном экране клиента [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] . Дополнительные сведения см. в разделе [данных качества клиента начального экрана](../data-quality-services/data-quality-client-home-screen.md).  
  
  