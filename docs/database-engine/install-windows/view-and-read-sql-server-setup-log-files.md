---
title: "Просмотр и чтение файлов журналов программы установки SQL Server | Документы Майкрософт"
ms.custom: 
ms.date: 03/09/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- setup-install
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- viewing logs
- displaying log files
- Setup [SQL Server], logs
- installation log files [SQL Server]
- installing SQL Server, logs
- errors [SQL Server], Setup
- logs [SQL Server], Setup
ms.assetid: 9d77af64-9084-4375-908a-d90f99535062
caps.latest.revision: 54
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 21f0cfd102a6fcc44dfc9151750f1b3c936aa053
ms.openlocfilehash: 3f87dec24a195cabd75fb653fcb5bcaf51e29db9
ms.contentlocale: ru-ru
ms.lasthandoff: 08/28/2017

---
# <a name="view-and-read-sql-server-setup-log-files"></a>Просмотр и чтение файлов журналов программы установки SQL Server
  При каждом выполнении программы установки создаются файлы журналов в новой папке журналов с меткой времени в %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\130\Setup Bootstrap\Log\\. Формат папки журналов с меткой времени — ГГГГММДД_ччммсс. При запуске программы установке в автоматическом режиме журналы создаются в % temp%\sqlsetup*.log. Все файлы в папке журналов архивируются в файле Log\*.cab в соответствующей папке журналов.  
  
 В процессе выполнения запрос программы установки проходит через три фазы:  
  
1.  Текстовое содержание глобальных правил  
  
2.  Обновление компонента  
  
3.  Действие, указанное пользователем  
  
 На каждом этапе программа становки создает подробный и сводный журналы; при этом, если необходимо, создаются дополнительные журналы. Программа установки вызывается по меньшей мере трижды при выполнении каждого указанного пользователем действия по установке.  
  
 В файлах хранилища данных содержится моментальный снимок состояния всех объектов конфигурации, отслеживаемых процессом установки; эти файлы могут пригодиться при диагностике ошибок конфигурации. Дампы XML-файлов создаются для объектов хранилища данных в каждой фазе выполнения. Они сохраняются в собственной подпапке журналов в папке журналов с меткой времени следующим образом:  
  
-   Datastore_GlobalRules  
  
-   Datastore_ComponentUpdated  
  
-   Datastore  
  
 В следующих разделах описываются файлы журналов установки [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="summary-text"></a>Текстовое содержание сводки  
  
### <a name="overview"></a>Обзор  
 В этом файле отображаются компоненты [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , обнаруженные на этапе установки, среда операционной системы, значения параметров командной строки (если указаны) и общее состояние всех выполненных MSI/MSP.  
  
 Журнал структурирован с использованием следующих разделов:  
  
-   Общая сводка выполнения  
  
-   Свойства и конфигурация компьютера, на котором была запущена программа установки [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , ранее установленного на компьютере  
  
-   Описание версии установки и свойства пакета установки  
  
-   Входные параметры среды выполнения, указанные при установке  
  
-   Местоположение файла конфигурации  
  
-   Данные о результатах выполнения  
  
-   Глобальные правила  
  
-   Правила, связанные с определенным сценарием установки  
  
-   Правила, при выполнении которых произошла ошибка  
  
-   Местоположение файла отчета о выполнении правил  
  
### <a name="location"></a>Местоположение  
 Расположен в папке %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\130\Setup Bootstrap\Log\\.  
  
 Чтобы найти ошибки в текстовом файле сводки, воспользуйтесь поиском с ключевыми словами «error» или «failed».  
  
## <a name="summaryengine-baseyyyymmddhhmmsstxt"></a>Summary_engine-base_YYYYMMDD_HHMMss.txt  
  
### <a name="overview"></a>Обзор  
 Базовый файл summary_engine схож с файлом справки и создается при выполнении основного рабочего процесса.  
  
### <a name="location"></a>Местоположение  
 Расположен в папке %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\130\Setup Bootstrap\Log\\<ГГГГММДД_ЧЧММ>\\.  
  
## <a name="summaryengine-baseyyyymmddhhmmsscomponentupdatetxt"></a>Summary_engine-base_YYYYMMDD_HHMMss_ComponentUpdate.txt  
  
### <a name="overview"></a>Обзор  
 Базовый файл summary_engine схож с файлом справки и создается при выполнении основного рабочего процесса.  
  
### <a name="location"></a>Местоположение  
 Расположен в папке %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\130\Setup Bootstrap\Log\\<ГГГГММДД_ЧЧММ>\\.  
  
## <a name="summaryengine-baseversionnumbermmddhhmmssglobalrulestxt"></a>Summary_engine-base_\<номер-версии>ММДД_ЧЧММссs_GlobalRules.txt  
  
### <a name="overview"></a>Обзор  
 Файл сводного журнала глобальных правил схож с файлом справки и создается при выполнении рабочего процесса глобальных правил.  
  
### <a name="location"></a>Местоположение  
 Расположен в папке %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\130\Setup Bootstrap\Log\\<ГГГГММДД_ЧЧММ>\\.  
  
## <a name="detailtxt"></a>Detail.txt  
  
### <a name="overview"></a>Обзор  
 Detail.txt создается при выполнении рабочего процесса основных процедур, таких как установка или обновление, и обеспечивает сведения о выполнении. Журналы в файле создаются с учетом времени инициации всех действий, связанных с установкой, и указывают на порядок выполнения действий и их зависимости.  
  
### <a name="location"></a>Местоположение  
 Расположен в папке %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\130\Setup.  
  
 Bootstrap\Log\\<ГГГГММДД_ЧЧММ>\Detail.txt.  
  
 При возникновении ошибки во время процесса установки исключение или ошибка регистрируются в конце этого файла. Чтобы найти ошибки в этом файле, сначала проверьте конец файла, а затем воспользуйтесь поиском по файлу с ключевыми словами «ошибка» и «исключение».  
  
## <a name="detailcomponentupdatetxt"></a>Detail_ComponentUpdate.txt  
  
### <a name="overview"></a>Обзор  
 Файл Detail_ComponentUpdate.txt создается для рабочего процесса обновлений компонентов и похож на файл Detail.txt.  
  
### <a name="location"></a>Местоположение  
 Расположен в папке %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\130\Setup Bootstrap\Log\\<ГГГГММДД_ЧЧММ>\\.  
  
## <a name="detailglobalrulestxt"></a>Detail_GlobalRules.txt  
  
### <a name="overview"></a>Обзор  
 Файл Detail_GlobalRules.txt создается при выполнении глобальных правил и похож на файл Detail.txt.  
  
### <a name="location"></a>Местоположение  
 Расположен в папке %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\130\Setup Bootstrap\Log\\<ГГГГММДД_ЧЧММ>\\.  
  
## <a name="msi-log-files"></a>Файлы журнала MSI.  
  
### <a name="overview"></a>Обзор  
 В файлах журнала MSI указаны сведения о установке пакетов. Они создаются MSIEXEC при установке определенных пакетов.  
  
 Типы файлов журналов MSI:  
  
-   \<компонент>_\<архитектура>\_\<взаимодействие>.log  
  
-   \<компонент>_\<архитектура>\_\<язык>\_\<взаимодействие>.log  
  
-   \<компонент>_\<архитектура>\_\<взаимодействие>\_\<рабочий процесс>.log  
  
### <a name="location"></a>Местоположение  
 Файлы журналов MSI расположены в папке %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\130\Setup Bootstrap\Log\\<ГГГГММДД_ЧЧММ>\\<имя\>.log.  
  
 В конце файла приведена сводка выполнения, в которой указываются общее состояние (успешное или ошибка) и свойства. Для поиска ошибок в файле MSI воспользуйтесь поиском по ключевому выражению «value 3». Обычно ошибки можно найти рядом со строкой.  
  
## <a name="configurationfileini"></a>ConfigurationFile.ini  
  
### <a name="overview"></a>Обзор  
 В файле конфигурации содержатся входные параметры, указанные при установке. Их можно использовать для повторной установки, что избавит от необходимости их ввода вручную. Однако пароли учетных записей, PID и некоторые параметры не сохраняются в файле конфигурации. Параметры могут либо быть добавлены к файлу или указаны с помощью командной строки или пользовательского интерфейса программы установки. Дополнительные сведения см. в разделе [Установка SQL Server 2016 с помощью файла конфигурации](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md).  
  
### <a name="location"></a>Местоположение  
 Расположен в папке %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\130\Setup Bootstrap\Log\\<ГГГГММДД_ЧЧММ>\\.  
  
## <a name="systemconfigurationcheckreporthtm"></a>SystemConfigurationCheck_Report.htm  
  
### <a name="overview"></a>Обзор  
 В отчете о проверке конфигурации системы содержится краткое описание всех выполняемых правил и состояния выполнения.  
  
### <a name="location"></a>Местоположение  
 Расположен в папке %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\130\Setup Bootstrap\Log\\<ГГГГММДД_ЧЧММ>\\.  
  
## <a name="see-also"></a>См. также:  
 [Установка SQL Server 2016](../../database-engine/install-windows/install-sql-server.md)  
  
  
