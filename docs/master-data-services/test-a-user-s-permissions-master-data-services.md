---
title: "Проверка разрешений пользователя (службы Master Data Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 83a03b85-ea7f-4b4a-b19b-f7eca534ffae
caps.latest.revision: 4
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 4
---
# Проверка разрешений пользователя (службы Master Data Services)
  В [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]можно создать тестовую учетную запись и войти в веб-приложение для проверки разрешений. При попытке пользователя получить доступ к URL-адресу [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] выполняется проверка учетных данных пользователя. В Internet Explorer в зависимости от параметров безопасности проверка подлинности будет выполнена автоматически либо пользователю придется ввести имя и пароль. Чтобы изменить эти настройки, выполните следующие действия.  
  
### Проверка безопасности пользователя  
  
1.  В Internet Explorer версии 7 и выше выберите в меню **Сервис**пункт **Свойства обозревателя**и перейдите на вкладку **Безопасность** .  
  
2.  Нажмите **Местная интрасеть** , затем нажмите кнопку **Другой** .  
  
3.  В разделе **Проверка подлинности пользователя** выберите **Запрос имени пользователя и пароля**.  
  
4.  При следующем открытии окна браузера будет предложено указать имя пользователя и пароль.  
  
## См. также:  
 [Безопасность (службы Master Data Services)](../master-data-services/security-master-data-services.md)  
  
  