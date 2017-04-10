---
title: "Создание администратора сущностей (службы Master Data Services) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 717be1e8-488e-4219-8d1e-ca9084b864cd
caps.latest.revision: 5
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 5
---
# Создание администратора сущностей (службы Master Data Services)
  В [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] администратор сущностей создается, когда нужно предоставить группе или пользователю все разрешения на доступ ко всем объектам в одной или нескольких сущностях либо разрешение на утверждение ожидающих наборов изменений.  
  
> [!TIP]  
>  Чтобы упростить администрирование, создайте локальную группу или группу Windows и настройте ее в качестве администратора сущностей. Впоследствии добавлять пользователей в группу и удалять их из нее можно без обращения к [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)].  
  
## Предварительные требования  
 Чтобы выполнить эту процедуру:  
  
-   необходимо разрешение на доступ к функциональной области **Разрешения пользователей и групп** ;  
  
-   необходимо быть администратором модели. Дополнительные сведения см. в статье [Администраторы (службы Master Data Services)](../master-data-services/administrators-master-data-services.md).  
  
## Создание администратора сущностей  
  
1.  В среде [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]щелкните **Разрешения пользователей и групп**.  
  
2.  Выберите строку пользователя или группы, которую необходимо изменить, а затем нажмите **Изменить выбранного пользователя**.  
  
3.  Перейдите на вкладку **Модели**, при необходимости выберите модель из списка **Модели**, после чего нажмите кнопку **Изменить**.  
  
4.  Выберите сущность, для которой необходимо предоставить разрешения, и щелкните пункт **Администратор** в меню.  
  
5.  Выполните шаг 4 для каждой сущности, для которой необходимо назначить администратором пользователя или группу.  
  
6.  Нажмите кнопку **Сохранить**.  
  
## См. также:  
 [Администраторы (службы Master Data Services)](../master-data-services/administrators-master-data-services.md)   
 [Назначение разрешения для объекта модели (службы Master Data Services)](../master-data-services/assign-model-object-permissions-master-data-services.md)   
 [Назначение разрешений для элемента иерархии (службы Master Data Services)](../master-data-services/assign-hierarchy-member-permissions-master-data-services.md)   
 [Разрешения объекта модели (службы Master Data Services)](../master-data-services/model-object-permissions-master-data-services.md)   
 [Разрешения на элементы иерархии (службы Master Data Services)](../master-data-services/hierarchy-member-permissions-master-data-services.md)  
  
  