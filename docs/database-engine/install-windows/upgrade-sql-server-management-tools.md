---
title: "Обновление средств управления SQL Server | Документы Майкрософт"
ms.custom: 
ms.date: 07/24/2017
ms.prod:
- sql-server-2016
- sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- setup-install
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- management tools, upgrading
ms.assetid: 1dab50b9-d16c-49a1-9ecc-af72adb6c378
caps.latest.revision: 19
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 3174cb5f1f865fb73dbb792066bbaf7ab2dc4894
ms.contentlocale: ru-ru
ms.lasthandoff: 08/02/2017

---
# <a name="upgrade-sql-server-management-tools"></a>Обновление средств управления SQL Server
[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] поддерживает обновление с версии [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] или более поздней. В этом разделе описаны средства поддержки и процесс обновления средств управления [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , агента [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , компонента Database Mail, планов обслуживания, XPStar, XPWeb и других компонентов управления.  
  
> [!IMPORTANT]  
>  Для локальных установок программу установки [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] нужно запускать с правами администратора. При установке [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] из удаленной общей папки необходимо пользоваться учетной записью домена, имеющей разрешения на чтение и выполнение для удаленной общей папки.  
  
## <a name="known-upgrade-issues"></a>Известные проблемы при обновлении  
Прежде чем приступать к обновлению до [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], необходимо учесть следующие моменты.  
  
### <a name="for-all-upgrade-scenarios"></a>Для всех сценариев обновления  
  
- Перед обновлением главного сервера должны быть обновлены все целевые серверы. Дополнительные сведения о главных и целевых серверах [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]см. в статье [Автоматизация администрирования в масштабах предприятия](http://msdn.microsoft.com/library/44d8365b-42bd-4955-b5b2-74a8a9f4a75f).  
  
-   Все компоненты экземпляра [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] должны быть обновлены одновременно. Компонент [!INCLUDE[ssDE](../../includes/ssde-md.md)], а также службы [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]и [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] должны иметь один и тот же номер версии для одного экземпляра [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
-   При обновлении до [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] к существующей установке [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]могут быть добавлены новые компоненты. Дополнительные сведения см. в статье [Обновление SQL Server 2016 с помощью мастера установки (программа установки)](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md).  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , такие как [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], помощник по настройке компонента [!INCLUDE[ssDE](../../includes/ssde-md.md)] , sqlcmd и osql, до версии [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Клиентские средства запускаются параллельно с компонентами предыдущих версий [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] поддерживает импорт параметров из предыдущих версий клиентских средств [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Проверка подлинности из агента [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] будет переключена из режима [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] в режим Windows, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] в [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
-   После обновления до [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]данные заданий и предупреждений сохранятся.  
  
-   Если в обновляемом экземпляре используется программа SQLMail, то связанные с ней расширенные хранимые процедуры после обновления будут сохранены и включены. В противном случае они будут отключены.  
  
-   При обновлении [!INCLUDE[ssDE](../../includes/ssde-md.md)] компонент Database Mail (также называемый SQLiMail) обновляется одновременно с компонентом [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. По умолчанию после обновления компонент Database Mail отключается. Все изменения схемы после этого должны быть согласованы со скриптом обновления.  
  
## <a name="see-also"></a>См. также:  
 [Поддерживаемые обновления версий и выпусков](../../database-engine/install-windows/supported-version-and-edition-upgrades.md)   
 [Обратная совместимость_удалено](http://msdn.microsoft.com/library/15d9117e-e2fa-4985-99ea-66a117c1e9fd)   
 [Обновление SQL Server с помощью мастера установки (программа установки)](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)  
  
  