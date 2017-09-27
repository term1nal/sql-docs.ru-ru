---
title: "Шаг 3: Добавление пакетов и других файлов | Документы Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: a7e6ec9c-d31d-4613-9525-8947a7b358f7
caps.latest.revision: 24
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f8cf4eedc8930492e28f41cee67f0c25a382bacd
ms.contentlocale: ru-ru
ms.lasthandoff: 09/26/2017

---
# <a name="lesson-1-3---adding-packages-and-other-files"></a>Занятие 1-3 - Добавление пакетов и других файлов
В этой задаче к проекту, созданному в предыдущей задаче учебника по развертыванию, добавляются существующие пакеты, вспомогательные файлы для поддержки отдельных пакетов, а также файл сведений. Например, будет добавлен файл XML-данных, содержащий данные для пакета, и текстовый файл Readme с данными о всех пакетах проекта.  
  
При развертывании пакетов в тестовой или рабочей среде файлы данных обычно не включаются в развертывание. Вместо этого источники данных настраиваются таким образом, чтобы обновлять соответствующие пути доступа к тестовым или рабочим версиям файлов или баз банных. В данном учебнике файлы данных включены в пакет развертывания для учебных целей.  
  
Пакеты и образцы данных, используемые пакетами, устанавливаются вместе с образцами сервера [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . К проекту из учебника по развертыванию добавляются следующие пакеты.  
  
-   **DataTransfer.** Основной пакет для извлечения данных из неструктурированного файла, оценки значений столбцов в целях хранения строк в наборе данных по условию, а также для загрузки данных в таблицу базы данных AdventureWorks.  
  
-   **LoadXMLData.** Пакет передачи данных, используемый для извлечения данных из XML-файла, оценки и статистической обработки значений столбцов, а также для загрузки данных в таблицу базы данных AdventureWorks.  
  
Для поддержки развертывания этих пакетов проекту из учебника по развертыванию требуются следующие вспомогательные файлы.  
  
|Пакет|Файл|  
|-----------|--------|  
|DataTransfer|NewCustomers.txt|  
|LoadXMLData|orders.xml и orders.xsd|  
  
Кроме этого добавляется текстовый файл Readme с данными о проекте из учебника по развертыванию.  
  
Пути, используемые в последующих процедурах, подразумевают, что образцы сервера [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] были установлены в папку по умолчанию, [!INCLUDE[ssSampPathIS](../includes/sssamppathis-md.md)]. Если образцы были установлены в другое место, в процедурах следует указать его.  
  
В следующей задаче добавляются настройки для пакетов DataTransfer и LoadXMLData. Все настройки хранятся в виде XML-файлов, и для указания их местоположения используются системные переменные среды. После создания файлов конфигурации их можно добавить в проект.  
  
### <a name="to-add-packages-to-the-deployment-tutorial-project"></a>Добавление пакетов в проект из учебника по развертыванию  
  
1.  Если среда [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] еще не открыта, нажмите кнопку **Пуск**, наведите указатель на пункт **Все программы**, затем на пункт **Microsoft SQL Server**и выберите пункт **SQL Server Data Tools**.  
  
2.  В меню **Файл** выберите пункт **Открыть**, щелкните **Проект или решение**, разверните папку **Deployment Tutorial** и нажмите кнопку **Открыть**, а затем дважды щелкните файл **Deployment Tutorial.sln**.  
  
3.  В обозревателе решений правой кнопкой мыши щелкните проект Deployment Tutorial, нажмите кнопку **Добавить**и выберите **Существующий пакет**.  
  
4.  В диалоговом окне **Добавление копии существующего пакета** в разделе **Расположение пакета**выберите пункт **Файловая система**.  
  
5.  Нажмите кнопку обзора **(…)** , перейдите к папке C:\Program Files\Microsoft SQL Server\100\Samples\Integration ServicesTutorial\Deploying Packages\Completed Packages, выберите файл **DataTransfer.dtsx**и нажмите кнопку **Открыть**.  
  
6.  Нажмите кнопку **ОК**.  
  
7.  Повторите шаги 3 — 6, выбрав на этот раз пакет LoadXMLData.dtsx, расположенный в папке «C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services\Tutorial\Deploying Packages\Completed Packages».  
  
### <a name="to-add-ancillary-files-to-the-deployment-tutorial-project"></a>Добавление вспомогательных файлов в проект из учебника по развертыванию  
  
1.  В обозревателе решений правой кнопкой мыши щелкните проект Deployment Tutorial, выберите пункт **Добавить**, а затем пункт **Существующий элемент**.  
  
2.  В диалоговом окне **Добавление существующего элемента — Deployment Tutorial** перейдите к папке C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services\Tutorial\Deployment Packages\Sample Data, выберите файлы orders.xml, orders.xsd и NewCustomers.txt и нажмите кнопку **Добавить**.  
  
3.  В диалоговом окне **Добавление существующего элемента — Deployment Tutorial** перейдите к папке C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services\Tutorial\Deployment Packages\\, выберите файл Readme.txt и нажмите кнопку **Добавить**.  
  
4.  В меню «Файл» выберите команду **Сохранить все**.  
  
## <a name="next-task-in-lesson"></a>Следующая задача занятия  
[Шаг 4. Добавление конфигурации пакета](../integration-services/lesson-1-4-adding-package-configurations.md)  
  
  
  
