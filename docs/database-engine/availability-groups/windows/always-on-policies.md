---
title: Политики для групп доступности AlwaysOn (SQL Server) | Документы Майкрософт
ms.custom: ag-guide
ms.date: 06/13/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: 26bf8f71-c2b8-45ef-b3a3-372b96c9e6e3
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: d25f54c29937ba4289308e07bb2013a4c671dbbb
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/01/2018
ms.locfileid: "47767892"
---
# <a name="always-on-availability-groups-policies"></a>Политики для групп доступности AlwaysOn
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Системные политики для групп доступности AlwaysOn используются на панели мониторинга AlwaysOn для предоставления пользователю информации о работоспособности групп доступности. Они очень удобны для первоначального устранения неполадок в работе групп доступности. Эти политики можно расширять и использовать для настройки панели мониторинга AlwaysOn, а также оперативно выполнять для получения нужных сведений о работоспособности.  
  
 Существует 14 системных политик для групп доступности. Подробные сведения о каждой политике см. в разделе [Политики AlwaysOn на случай проблем в работе с группами доступности AlwaysOn (SQL Server)](always-on-policies-for-operational-issues-always-on-availability.md).  
  
## <a name="view-or-evaluate-availability-groups-system-policies"></a>Просмотр и оценка системных политик для групп доступности  
 Для просмотра или выполнения системных политик групп доступности в SQL Server Management Studio (SSMS) сделайте следующее:  
  
1.  В **обозревателе объектов** последовательно разверните узлы **Управление**, **Управление политиками**, **Политики** и **Системные политики**.  
  
2.  Щелкните правой кнопкой мыши одну из политик и выберите **Вычислить**. Если вы хотите оценить выбранную политику, больше ничего не требуется. Можно щелкнуть элемент **Просмотреть** в области **Данные целевого объекта**, чтобы просмотреть сведения о результатах оценки.  
  
3.  Чтобы просмотреть все системные политики групп доступности, в области **Выбор страницы** щелкните элемент **Выбор политики**.  
  
## <a name="next-steps"></a>Следующие шаги  
 [Модель работоспособности AlwaysOn, часть 2. Расширение модели работоспособности](http://blogs.msdn.com/b/sqlalwayson/archive/2012/02/13/extending-the-alwayson-health-model.aspx)  
  
  
