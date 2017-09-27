---
title: "Catalog.effective_object_permissions (база данных SSISDB) | Документы Microsoft"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- catalog.effective_object_permissions views [Integration Services]
- effective_object_permissions view [Integration Services]
ms.assetid: e70c4ce9-79f5-44df-ac75-6c29b6e38776
caps.latest.revision: 26
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 3f836aa3e13623a42a3f2e8fe0d3907b45bde850
ms.contentlocale: ru-ru
ms.lasthandoff: 09/26/2017

---
# <a name="catalogeffectiveobjectpermissions-ssisdb-database"></a>catalog.effective_object_permissions (база данных SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Отображает действующие разрешения текущего участника для всех объектов в каталоге служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
|Имя столбца|Тип данных|Description|  
|-----------------|---------------|-----------------|  
|object_type|**smallint**|Тип защищаемого объекта. Типы защищаемых объектов включают папку (`1`), проект (`2`), среду (`3`) и операцию (`4`).|  
|object_id|**bigint**|Уникальный идентификатор (ID) первичного ключа объекта.|  
|permission_type|**smallint**|Тип разрешения.|  
  
## <a name="remarks"></a>Замечания  
 Это представление отображает типы разрешений, перечисленные в следующей таблице.  
  
|Значение permission_type|Имя разрешения|Описание разрешения|Применимые типы объектов|  
|----------------------------|---------------------|----------------------------|-----------------------------|  
|`1`|READ|Разрешает участнику читать сведения, рассматриваемые как часть объекта, например свойства. Тем самым участнику не разрешается перечислять или читать содержимое других объектов, содержащихся в этом объекте.|Папка, проект, среда, операция|  
|`2`|MODIFY|Разрешает участнику изменять сведения, рассматриваемые как часть объекта, например свойства. Тем самым участнику не разрешается изменять другие объекты, содержащиеся в этом объекте.|Папка, проект, среда, операция|  
|`3`|Выполните|Разрешает участнику выполнять все пакеты в проекте.|Проект|  
|`4`|MANAGE_PERMISSIONS|Разрешает участнику назначать разрешения на объекты.|Папка, проект, среда, операция|  
|`100`|CREATE_OBJECTS|Разрешает участнику создавать объекты в папке.|Папка|  
|`101`|READ_OBJECTS|Разрешает участнику читать все объекты в папке.|Папка|  
|`102`|MODIFY_OBJECTS|Разрешает участнику изменять все объекты в папке.|Папка|  
|`103`|EXECUTE_OBJECTS|Разрешает участнику выполнять все пакеты из всех проектов в папке.|Папка|  
|`104`|MANAGE_OBJECT_PERMISSIONS|Разрешает участнику управлять разрешениями на все объекты в папке.|Папка|  
  
 Оцениваются только объекты, на которые у вызывающего имеются разрешения. Разрешения вычисляются на основе следующих факторов.  
  
-   Явные разрешения  
  
-   Наследуемые разрешения  
  
-   Членство участника в ролях  
  
-   Членство участника в группах  
  
## <a name="permissions"></a>Permissions  
 Действующие разрешения у пользователей могут быть только на себя и на те роли, членами которых они являются.  
  
  