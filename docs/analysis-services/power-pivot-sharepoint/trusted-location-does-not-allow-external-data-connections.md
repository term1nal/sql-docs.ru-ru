---
title: "Доверенные расположение не разрешает подключения к внешним данным | Документы Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: dc0cedfd-a7d0-40ef-bdd6-ea508130640a
caps.latest.revision: 7
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0f774f6bc9a4d950d8f7c00e3c3e79aa3211e4cf
ms.contentlocale: ru-ru
ms.lasthandoff: 09/01/2017

---
# <a name="trusted-location-does-not-allow-external-data-connections"></a>Надежное расположение, не разрешает подключения к внешним данным
  Служба Excel Services возвращает эту ошибку для книг Excel, содержащих данные [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , если она не может подключиться к внедренным источникам данных.  
  
## <a name="details"></a>Сведения  
  
|||  
|-|-|  
|Область применения|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] для SharePoint|  
|Номер версии продукта|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|Причина|Служба Excel Services настроена так, чтобы отказывать в доступе к внешним данным.|  
|Текст сообщения|Надежное расположение, в котором находится книга, не разрешает подключения к внешним данным. Следующие соединения не удалось обновить: данные [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .|  
  
## <a name="explanation"></a>Объяснение  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] содержат подключения к внедренным данным. Для поддержки взаимодействия книги через срезы и фильтры в настройках службы Excel Services должен быть разрешен доступ к внешним данным с помощью данных внедренных соединений. Доступ к внешним данным требуется для получения данных [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , которые находятся на серверах [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] в ферме.  
  
## <a name="user-action"></a>Действие пользователя  
 Измените параметры конфигурации, чтобы разрешить внедренные источники данных.  
  
1.  В разделе «Управление приложениями» центра администрирования выберите пункт **Управление приложениями служб**.  
  
2.  Щелкните **Приложение служб Excel**.  
  
3.  Щелкните **Надежные расположения файлов**.  
  
4.  Щелкните **http://** или расположение, которое требуется настроить.  
  
5.  На странице «Внешние данные» для параметра «Разрешить внешние данные» установите значение **Надежные библиотеки подключений к данным и внедренные**.  
  
6.  Нажмите кнопку **ОК**.  
  
 Или можно создать новое надежное местоположение для сайтов, содержащих книги [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , а затем изменить параметры конфигурации только для этого сайта. Дополнительные сведения см. в разделе [Создание надежного расположения для сайтов PowerPivot в центре администрирования](../../analysis-services/power-pivot-sharepoint/create-a-trusted-location-for-power-pivot-sites-in-central-administration.md).  
  
  