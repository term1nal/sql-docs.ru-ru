---
title: "Установка служб Integration Services версии параллельно | Документы Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- interoperability and coexistence [Integration Services]
- Integration Services, interoperability and coexistence
ms.assetid: edfbcd56-012f-462e-a542-95491394fda9
caps.latest.revision: 41
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d642d8d9d732a51c210e5d83cecf2b090ac2f426
ms.contentlocale: ru-ru
ms.lasthandoff: 08/03/2017

---
# <a name="installing-integration-services-versions-side-by-side"></a>Установка нескольких версий служб Integration Services в одной среде
  Можно установить   
      [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]Integration Services (SSIS) side-by-side с более ранними версиями служб SSIS. В этом разделе описываются некоторые ограничения подобной установки.  
  
## <a name="designing-and-maintaining-packages"></a>Проектирование и обслуживание пакетов  
 Для разработки и обслуживания пакетов, нацеленных на SQL Server 2016, SQL Server 2014 или SQL Server 2012, используйте SQL Server Data Tools (SSDT) для Visual Studio 2015. Процедуру получения SSDT см. в разделе [Скачивание последней версии SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx).  
  
 На странице свойств проекта служб Integration Services, на вкладке **Общие** окна **Свойства конфигурации**, выберите свойство **TargetServerVersion** , затем выберите SQL Server 2016, SQL Server 2014 или SQL Server 2012.  
  
|Целевая версия SQL Server|Среда разработки для пакетов служб SSIS|  
|----------------------------------|-----------------------------------------------|  
|2016|SQL Server Data Tools для Visual Studio 2015|  
|2014|SQL Server Data Tools для Visual Studio 2015<br /><br /> либо<br /><br /> SQL Server Data Tools — Business Intelligence для Visual Studio 2013|  
|2012|SQL Server Data Tools для Visual Studio 2015<br /><br /> либо<br /><br /> SQL Server Data Tools — бизнес-аналитика для Visual Studio 2012|  
|2008 г.|Business Intelligence Development Studio из SQL Server 2008|  
  
 При добавлении существующего пакета в существующий проект этот пакет преобразуется в формат, используемый в проекте.  
  
## <a name="running-packages"></a>Запуск пакетов  
 Можно использовать версию служебной программы [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] dtexec **для** или агент [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , чтобы запускать пакеты служб Integration Services, созданные в предыдущих версиях инструментов разработки. Когда эти инструменты [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] загружают пакет, который был разработан в более ранней версии инструментов разработки, они временно преобразуют его в памяти в формат пакета, используемый [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] . Если пакет вызывает проблемы, препятствующие успешному преобразованию, инструмент [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] не сможет запустить пакет, пока проблемы не будут устранены. Дополнительные сведения см. в разделе [Обновление пакетов служб Integration Services](../../integration-services/install-windows/upgrade-integration-services-packages.md).  
  
  