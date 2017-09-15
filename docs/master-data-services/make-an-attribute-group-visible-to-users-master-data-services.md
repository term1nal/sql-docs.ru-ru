---
title: "Превращение группы атрибутов в видимую для пользователей (Master Data Services) | Документы Microsoft"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b2f6cc27-dbc9-4f3f-961e-e81e76375248
caps.latest.revision: 6
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d9b4e9b3fb165d2aa8c445daa5d38c7a8d81ed03
ms.contentlocale: ru-ru
ms.lasthandoff: 08/02/2017

---
# <a name="make-an-attribute-group-visible-to-users-master-data-services"></a>Превращение группы атрибутов в видимую для пользователей (службы Master Data Services)
  В [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]сделайте группу атрибутов видимой для пользователей или групп, если необходимо, чтобы у пользователей присутствовали вкладки над сеткой в функциональной области **Обозреватель** .  
  
 При создании группы атрибутов она автоматически скрыта от всех пользователей, кроме того, кто ее создал.  
  
## <a name="prerequisites"></a>Предварительные требования  
 Чтобы выполнить эту процедуру:  
  
-   необходимо иметь разрешение на доступ к функциональной области **Администрирование системы** ;  
  
-   необходимо быть администратором модели. Дополнительные сведения см. в статье [Администраторы (службы Master Data Services)](../master-data-services/administrators-master-data-services.md).  
  
-   Должна существовать хотя бы одна группа атрибутов. Дополнительные сведения см. в статье [Create an Attribute Group &#40;Master Data Services&#41;](../master-data-services/create-an-attribute-group-master-data-services.md).  
  
### <a name="to-make-an-attribute-group-visible-to-users"></a>Превращение группы атрибутов в видимую для пользователей  
  
1.  В [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]щелкните область **Администрирование системы**.  
  
2.  На странице **Manage Model** (Управление моделью) выберите в сетке модель и щелкните **Сущности**.  
  
3.  На странице **Manage Entity** (Управление сущностью) выберите в сетке строку сущности, для которой необходимо изменить группу атрибутов.  
  
4.  Щелкните **Группы атрибутов**.  
  
5.  На странице **Управление группами атрибутов** выберите тип элемента из раскрывающегося списка **Типы элементов** , чтобы развернуть узел **Конечный**, **Консолидированный** или **Коллекция**в зависимости от типа группы, которую нужно сделать видимой.  
  
6.  Выберите в сетке группу атрибутов, которую необходимо изменить, а затем нажмите **Изменить**.  
  
7.  Выберите пользователя или группу в поле **Доступные** и щелкните стрелку **Добавить** . Чтобы добавить все, щелкните стрелку **Добавить все** .  
  
8.  Нажмите кнопку **Сохранить**.  
  
## <a name="see-also"></a>См. также:  
 [Группы атрибутов &#40; Службы Master Data Services &#41;](../master-data-services/attribute-groups-master-data-services.md)   
 [Создать группу атрибутов &#40; Службы Master Data Services &#41;](../master-data-services/create-an-attribute-group-master-data-services.md)  
  
  