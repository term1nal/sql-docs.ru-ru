---
title: "Создание заданий | Документация Майкрософт"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- jobs [SQL Server Agent], creating
- SQL Server Agent jobs, creating
ms.assetid: 465fb7fc-7622-4252-a178-ea51691c935b
caps.latest.revision: 3
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 5997344db6e2ccbbfb0ad5759ac427f8d4de2746
ms.contentlocale: ru-ru
ms.lasthandoff: 06/22/2017

---
# <a name="create-jobs"></a>Создание заданий
Задание — это определенная цепочка действий, последовательно выполняемых агентом [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Задание может выполнять широкий диапазон действий, например запуск скриптов [!INCLUDE[tsql](../../includes/tsql_md.md)] , приложений командной строки, скриптов Microsoft ActiveX, пакетов Integration Services, команд и запросов Analysis Services и задач репликации. Задания могут запускать повторяющиеся или запланированные задачи, они могут автоматически уведомлять пользователей о состоянии задания, формируя предупреждения и тем самым значительно упрощают администрирование [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] .  
  
Чтобы создать задание, пользователь должен быть членом одной из предопределенных ролей базы данных агента [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] или членом предопределенной роли сервера **sysadmin** . Задание может быть изменено его владельцем или членом роли **sysadmin** . Члены роли **sysadmin** могут предоставлять права владения заданием другим пользователям, а также запускать любое задание, независимо от того, кто является его владельцем. Дополнительные сведения о предопределенных ролях базы данных агента [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] см. в разделе [Предопределенные роли базы данных агента SQL Server](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
Задания могут выполняться на локальном экземпляре [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] или быть распределены по нескольким экземплярам, работающим на предприятии. Для запуска заданий на нескольких серверах необходимо установить, по крайней мере, один главный сервер и один или несколько целевых. Дополнительные сведения о главных и целевых серверах см. в статье [Автоматизация администрирования в масштабах предприятия](../../ssms/agent/automated-administration-across-an-enterprise.md)  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Агент записывает сведения о задании и шагах задания в журнал заданий.  
  
## <a name="related-tasks"></a>Связанные задачи  
  
|||  
|-|-|  
|**Description**|**Раздел**|  
|Описывает создание задания агента [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] .|[Создание задания](../../ssms/agent/create-a-job.md)|  
|Описывает переназначение владения заданиями агента [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] другому пользователю.|[Give Others Ownership of a Job](../../ssms/agent/give-others-ownership-of-a-job.md)|  
|Описывает настройку журнала заданий агента [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] .|[Set Up the Job History Log](../../ssms/agent/set-up-the-job-history-log.md)|  
  
## <a name="see-also"></a>См. также:  
[Управление шагами задания](../../ssms/agent/manage-job-steps.md)  
[Автоматизация администрирования в масштабах предприятия](../../ssms/agent/automated-administration-across-an-enterprise.md)  
[Создание и присоединение расписаний к заданиям](../../ssms/agent/create-and-attach-schedules-to-jobs.md)  
[Запуск заданий](../../ssms/agent/run-jobs.md)  
[Просмотр или изменение заданий](../../ssms/agent/view-or-modify-jobs.md)  
  
