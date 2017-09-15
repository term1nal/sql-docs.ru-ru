---
title: "Создание конечного элемента (Master Data Services) | Документы Microsoft"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- leaf members [Master Data Services], creating
- creating leaf members [Master Data Services]
- members [Master Data Services], creating leaf members
ms.assetid: 0499d3b3-d508-4d43-a740-19cf53ade9f1
caps.latest.revision: 14
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3745604313dde3eda55c3d0f5d8f634bf7187440
ms.contentlocale: ru-ru
ms.lasthandoff: 08/02/2017

---
# <a name="create-a-leaf-member-master-data-services"></a>Создание конечного элемента (службы Master Data Services)
  В [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]создайте конечный элемент, если вам нужно добавить в систему основные данные. Если нужно добавить данные в массовом режиме, следует использовать промежуточные таблицы. Дополнительные сведения см. в разделе [Импорт данных из таблиц (службы Master Data Services)](../master-data-services/import-data-from-tables-master-data-services.md).  
  
 Также для импорта данных можно использовать [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)] .  
  
## <a name="prerequisites"></a>Предварительные требования  
 Чтобы выполнить эту процедуру:  
  
-   Необходимо иметь разрешение на доступ к функциональной области **Обозреватель** .  
  
-   Необходимо иметь как минимум разрешение **Создание** или **Обновление** для конечного объекта модели для сущности, в которую нужно добавить элемент. Разрешение "Создание" позволяет создать элемент и изменить только атрибут Code. Разрешение "Обновление" позволяет обновлять другие атрибуты.  
  
     Дополнительные сведения см. в разделе [Безопасность (службы Master Data Services)](../master-data-services/security-master-data-services.md).  
  
### <a name="to-create-a-leaf-member"></a>Создание конечного элемента  
  
1.  На домашней странице [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] выберите модель в списке **Модель** .  
  
2.  Если вы пользователь, выберите открытую версию из списка **Версия** . Если вы являетесь администратором, выберите версию в открытом или блокированном состоянии из списка **Версия** .  
  
3.  Нажмите кнопку **Браузер**.  
  
4.  В строке меню наведите указатель на пункт **Сущности** и щелкните имя сущности, к которой нужно добавить элемент.  
  
5.  Нажмите кнопку **Добавить элемент**.  
  
6.  Заполните поля в области **Сведения** .  
  
     Если фильтр применен к атрибуту, который основан на домене, список значений атрибута будет ограничен родительским атрибутом фильтра.  
  
     Дополнительные сведения о родительских атрибутах фильтров и атрибутах на основе домена см. в разделе [Создание атрибута на основе домена (службы Master Data Services)](../master-data-services/create-a-domain-based-attribute-master-data-services.md).  
  
7.  Необязательно. В поле **Заметки** введите комментарий о том, для чего добавлен элемент. Заметку могут просматривать все пользователи, которые имеют доступ к элементу.  
  
8.  Нажмите кнопку **ОК**.  
  
## <a name="see-also"></a>См. также:  
 [Создание объединенного элемента (службы Master Data Services)](../master-data-services/create-a-consolidated-member-master-data-services.md)   
 [Члены &#40; Службы Master Data Services &#41;](../master-data-services/members-master-data-services.md)  
  
  