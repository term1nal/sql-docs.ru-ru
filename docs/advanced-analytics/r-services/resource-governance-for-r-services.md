---
title: "Управление ресурсами для служб R | Microsoft Docs"
ms.custom: ""
ms.date: "05/31/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 18c9978a-aa55-42bd-9ab3-8097030888c9
caps.latest.revision: 11
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 11
---
# Управление ресурсами для служб R
  Один головной боли с R, что анализ больших объемов данных в рабочей среде необходимо дополнительное оборудование и данных часто перемещается за пределы базы данных на компьютерах, не контролируются ИТ.  Для выполнения аналитических операций, клиентам нужно использовать ресурсы сервера базы данных и защиты данных, они требуют, что таких операций корпоративного уровня соответствия требованиям, например, безопасности и производительности.  
  
 Этот раздел предоставляет сведения об управлении ресурсов, используемых средой выполнения R и R задания с помощью [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] экземпляр как контекст вычисления.  
  
## Что такое управление ресурсами  
 Управление ресурсами предназначен для выявления и предотвращения проблем, которые используются в среде сервера базы данных, где часто существует несколько зависимых приложений и нескольких служб для поддержки и распределения. Для [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], управление ресурсами включает в себя следующие задачи:  
  
-   Определение сценариев, использующих слишком много ресурсов сервера.  
  
     Администратор должен иметь возможность завершить или регулирования заданий, которые потребляют слишком много ресурсов.  
  
-   Сдерживание непрогнозируемых рабочих нагрузок.  
  
     Например если параллельное выполнение нескольких заданий R на сервере и задания не изолированы друг от друга с помощью пулов ресурсов, полученный о конфликтах ресурсов может привести к непредсказуемым производительности или угрожать завершения рабочей нагрузки.  
  
-   Расстановка приоритетов рабочих нагрузок.  
  
     Администратор или разработчик должен иметь возможность указать рабочих нагрузок, которые должны приоритет или гарантирует некоторых рабочих нагрузок для выполнения при наличии конфликта ресурсов.  
  
 В [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], можно использовать [регулятора ресурсов](../../relational-databases/resource-governor/resource-governor.md) для управления ресурсами, используемых средой выполнения R и удаленного задания R.  
  
## Способы использования регулятора ресурсов для задания управление R  
 В общем, управлять ресурсы, выделенные для задания R, создав *внешних ресурсов пулы* и назначение пула или пулов рабочих нагрузок. Пул внешних ресурсов — это новый тип пула ресурсов, представленные в [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], чтобы упростить управление, среда выполнения R и других процессов, внешних к компоненту database engine.  
  
 В [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], теперь существует три типа пулов ресурсов по умолчанию.  
  
-    *Внутренний пул* представляет ресурсов используется SQL Server и не удается нельзя изменять или ограничен.  
  
-    *По умолчанию пула* — стандартный пользовательский пул, можно использовать для изменения использования ресурсов на сервере в целом. Можно также определить группы пользователей, входящих в этот пул для управления доступом к ресурсам.  
  
-    *По умолчанию пула внешних* — стандартный пользовательский пул для внешних ресурсов. Кроме того можно создать новые пулы внешних ресурсов и определения групп пользователей, должен принадлежать к этому пулу.  
  
 Кроме того, можно создать *пулы ресурсов, определяемых пользователем* для распределения ресурсов в ядре базы данных или других приложений и создания *внешних ресурсов, определяемых пользователем пулов* Управление R и других внешних процессов.  
  
 Хорошим введением терминологию и основные принципы, в разделе [пула ресурсов регулятора ресурсов](../../relational-databases/resource-governor/resource-governor-resource-pool.md).  
  
> [!NOTE]  
>  В настоящее время новые свойства регулятора ресурсов доступны только через DDL-инструкций или сценариев; группы внешних ресурсов не может создаваться с помощью пользовательского интерфейса в [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
## Управление ресурсами с помощью регулятора ресурсов 

   Если вы новичок в регулятора ресурсов, см. в этом разделе Краткое описание того, как изменение ресурсов экземпляра по умолчанию и создать новый пул внешних ресурсов:  [How To: Создание пула ресурсов для R](../../advanced-analytics/r-services/how-to-create-a-resource-pool-for-r.md)   
  
 Можно использовать *пула внешних ресурсов* механизм управления ресурсами, используемые следующие R исполняемые файлы:  
  
-   Rterm.exe и вспомогательные процессы  
  
-   BxlServer.exe и вспомогательные процессы  
  
-   Вспомогательные процессы, запущенные с панели запуска  
  
 Однако прямого управления запуска службы с помощью регулятора ресурсов не поддерживается. Это потому, что [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] является доверенной службы, можно намеренно размещения только средства запуска, предоставляемые корпорацией Майкрософт. Во избежание интенсивно использует ресурсы настраиваются доверенные средства запуска.  
  
 Рекомендуется управлять вспомогательные процессы с помощью регулятора ресурсов и настроить их в соответствии с потребностями для отдельной базы данных конфигурации и рабочих нагрузок.  Например любой процесс отдельных вспомогательных может быть создан или уничтожен по запросу во время выполнения.  
  
## Отключить выполнение внешнего скрипта  
 Поддержка внешних скриптов является необязательным в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] установки. Даже после установки [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)], возможность выполнения внешних сценариев, по умолчанию отключена, и необходимо вручную изменить свойство и перезапустить экземпляр, чтобы обеспечить выполнение сценариев.  
  
 Таким образом, если ресурс проблему, которая должна немедленно устранить или проблема с безопасностью, администраторы могут немедленно отключить любой выполнении внешних скриптов с помощью [sp_configure & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) и установите свойство `external scripts enabled` значение FALSE или 0.  
  
## См. также:  
 [Мониторинг решений R и управление ими](../../advanced-analytics/r-services/managing-and-monitoring-r-solutions.md)  
 [Практическое руководство: Создание пула ресурсов для R](../../advanced-analytics/r-services/how-to-create-a-resource-pool-for-r.md)  
 [Пул ресурсов регулятора ресурсов](../../relational-databases/resource-governor/resource-governor-resource-pool.md)
  