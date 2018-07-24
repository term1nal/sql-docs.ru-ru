---
title: Выбор устройства резервного копирования | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: backup-restore
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.selectbackupdevice.f1
ms.assetid: 7887c9fd-15ce-4cc8-b069-845c1d09088c
caps.latest.revision: 26
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: aeecd5db3b5c8666eb7e585dbacc522da26f0c44
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2018
ms.locfileid: "37290940"
---
# <a name="select-backup-device"></a>Выбор устройства резервного копирования
  Используйте диалоговое окно **Выбор устройства резервного копирования** , чтобы выбрать логическое устройство резервного копирования для операции восстановления.  
  
 Логическим устройством резервного копирования является определяемое пользователем логическое устройство, которое относится к физическим устройствам, или ленточный накопитель, или дисковый накопитель, предоставляемый операционной системой.  
  
> [!NOTE]  
>  Если несколько устройств резервного копирования используется для выполнения операции резервного копирования, все они должны соответствовать одному типу устройства.  
  
 **Использование среды SQL Server Management Studio для просмотра содержимого устройства резервного копирования**  
  
-   [Просмотр содержимого ленты или файла резервной копии (SQL Server)](view-the-contents-of-a-backup-tape-or-file-sql-server.md)  
  
-   [Просмотр свойств и содержимого логического устройства резервного копирования (SQL Server)](view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
## <a name="options"></a>Параметры  
 **устройство резервного копирования;**  
 В окне списка выберите имя устройства резервного копирования, с которого необходимо произвести восстановление.  
  
 Сведения о просмотре содержимого устройства резервного копирования см. в разделе [Просмотр свойств и содержимого логического устройства резервного копирования (SQL Server)](view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md).  
  
## <a name="remarks"></a>Примечания  
 Если не отображается логическое устройство резервного копирования, содержащее необходимую резервную копию, резервная копия может быть записана прямо на один или более дисковых накопителей или ленточных накопителей. В таком случае закройте диалоговое окно **Выбор устройства резервного копирования** и в диалоговом окне **Указание резервной копии** выберите **Файл** или **Лента** в окне списка **Носитель резервной копии** .  
  
## <a name="see-also"></a>См. также  
 [Устройства резервного копирования (SQL Server)](backup-devices-sql-server.md)  
  
  