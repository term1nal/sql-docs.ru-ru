---
title: "Создание базы данных служб Master Data Services | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "setup-install"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8373bb35-f0f9-4c3c-a53c-dfaa2ce567ac
caps.latest.revision: 9
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 9
---
# Создание базы данных служб Master Data Services
  Создайте базу данных [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] , если для поддержки веб-приложения [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] и веб-службы [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] требуется новая база данных.  
  
## Предварительные требования  
  
-   Дополнительные сведения о требованиях, предъявляемых к компьютеру, на котором размещается база данных, см. в разделе [Требования баз данных (службы Master Data Services)](../../master-data-services/install-windows/database-requirements-master-data-services.md).  
  
### Создание базы данных служб Master Data Services  
  
1.  Откройте среду [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)].  
  
2.  На панели слева щелкните **Конфигурация базы данных**.  
  
3.  На странице **Конфигурация базы данных** выберите **Создать базу данных**.  
  
4.  Чтобы создать и настроить базу данных, выполните инструкции мастера **создания базы данных** . Дополнительные сведения о параметрах пользовательского интерфейса в мастере см. в разделе [Создание мастера баз данных (диспетчер конфигураций Master Data Services)](../../master-data-services/create-database-wizard-master-data-services-configuration-manager.md).  
  
## Следующие шаги  
  
-   Настройте системные параметры базы данных и веб-приложения. Дополнительные сведения см. в разделе [Системные параметры (службы Master Data Services)](../../master-data-services/system-settings-master-data-services.md).  
  
-   Создайте веб-приложение [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] , которое будет связано с этой базой данных. Дополнительные сведения см. в статье [Создание веб-приложения мастера основных данных (службы Master Data Services)](../../master-data-services/install-windows/create-a-master-data-manager-web-application-master-data-services.md).  
  
-   Настройте план обслуживания для резервного копирования базы данных и журналов транзакций. Дополнительные сведения см. в разделе [Требования к базе данных (службы Master Data Services)](../../master-data-services/install-windows/database-requirements-master-data-services.md).  
  
## См. также:  
 [Установка служб Master Data Services](../../master-data-services/install-windows/install-master-data-services.md)  
  
  