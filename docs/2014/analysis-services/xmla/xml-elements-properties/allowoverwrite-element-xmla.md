---
title: Элемент AllowOverwrite (XMLA) | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- AllowOverwrite Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.allowoverwrite
- urn:schemas-microsoft-com:xml-analysis#EndSession
helpviewer_keywords:
- AllowOverwrite element
ms.assetid: e7e92481-5f29-47f2-9efd-4e5e60c002bb
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: eb0d58570349fbbb17b442ddebc0fd3193531149
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/02/2018
ms.locfileid: "48131434"
---
# <a name="allowoverwrite-element-xmla"></a>Элемент AllowOverwrite (XML для аналитики)
  Определяет ли родительский [резервного копирования](../xml-elements-commands/backup-element-xmla.md) или [восстановить](../xml-elements-commands/restore-element-xmla.md) предпринимается попытка перезаписать целевой файл или базу данных.  
  
## <a name="syntax"></a>Синтаксис  
  
```xml  
  
<Backup> <!-- or Restore -->  
   ...  
   <AllowOverwrite>...</AllowOverwrite>  
   ...  
</Backup>  
```  
  
## <a name="element-characteristics"></a>Характеристики элемента  
  
|Характеристика|Описание|  
|--------------------|-----------------|  
|Тип данных и длина|Логическое значение|  
|Значение по умолчанию|False|  
|Количество элементов|0-1: необязательный элемент, который может встречаться только один раз.|  
  
## <a name="element-relationships"></a>Связи элемента  
  
|Связь|Элемент|  
|------------------|-------------|  
|Родительские элементы|[Резервное копирование](../xml-elements-commands/backup-element-xmla.md), [восстановления](../xml-elements-commands/restore-element-xmla.md)|  
|Дочерние элементы|None|  
  
## <a name="remarks"></a>Примечания  
 Для команд `Backup` элемент `AllowOverwrite` определяет, будут ли они перезаписывать файл резервной копии, заданный в элементе `File`.  
  
 Для `Restore` элементов, `AllowOverwrite` элемент определяет, может ли команда перезаписать [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] базы данных, указанной в `DatabaseName` элемент.  
  
## <a name="see-also"></a>См. также  
 [Элемент DatabaseName &#40;XML для Аналитики&#41;](name-element-xmla.md)   
 [Файл элемента &#40;XML для Аналитики&#41;](file-element-xmla.md)   
 [Свойства &#40;XML для Аналитики&#41;](xml-elements-properties.md)  
  
  
