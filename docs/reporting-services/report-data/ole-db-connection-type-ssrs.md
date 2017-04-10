---
title: "Тип соединения OLE DB (службы SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d00cb13b-e1c2-4300-a195-3da1430a2df1
caps.latest.revision: 8
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 7
---
# Тип соединения OLE DB (службы SSRS)
  Для включения данных из источника данных OLE DB необходим набор данных на основе источника данных отчета типа OLE DB. Этот встроенный тип источника данных основан на модуле обработки данных OLE DB служб [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 OLE DB представляет собой технологию доступа к данным, позволяющую клиентам подключаться к различным поставщикам данных. После выбора источника данных OLE DB необходимо выбрать определенный поставщик данных. Поддержка различных функций, таких как параметры и учетные данные, зависит от выбранного поставщика данных.  
  
 Используйте сведения в этом разделе для создания источника данных. Пошаговые инструкции см. в разделе [Добавление и проверка подключения к данным (построитель отчетов и службы SSRS)](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md).  
  
##  <a name="Connection"></a> Строка подключения  
 Строка соединения для модуля обработки данных OLE DB зависит от требуемого поставщика данных. Обычная строка соединения содержит пары имя-значение, поддерживаемые поставщиком данных. Например, приведенная ниже строка соединения задает поставщика OLE DB для собственного клиента [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] и базы данных AdventureWorks:  
  
```  
Provider=SQLNCLI10.1;Data Source=server; Initial Catalog=AdventureWorks  
```  
  
 Используемая строка подключения зависит от внешнего источника данных, с которым выполняется соединение. Чтобы установить свойства строки соединения для поставщика данных, на странице **Общие** диалогового окна **Свойства источника данных** нажмите кнопку **Построить** , чтобы открыть диалоговое окно **Свойства соединения** . Расширенные свойства источника данных задаются в диалоговом окне **Свойства связи данных** .  
  
 Примеры строк подключения см. в разделе [Подключения к данным, источники данных и строки подключения в построителе отчетов](../Topic/Data%20Connections,%20Data%20Sources,%20and%20Connection%20Strings%20in%20Report%20Builder.md).  
  
 ![Значок стрелки, используемый со ссылкой «В начало»](../../analysis-services/instances/media/uparrow16x16.png "Значок стрелки, используемый со ссылкой «В начало»") [В начало](#BackToTop)  
  
##  <a name="Credentials"></a> Учетные данные  
 Учетные данные необходимы для запуска запросов, локального предварительного просмотра отчетов, а также для предварительного просмотра отчетов на сервере отчетов.  
  
 После публикации отчета может понадобиться изменить учетные данные источника данных, чтобы разрешения, необходимые для получения данных при запуске отчета на сервере отчетов, были допустимыми.  
  
 Дополнительные сведения см. в разделах [Подключения к данным, источники данных и строки подключения (построитель отчетов и службы SSRS)](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md) и [Указание учетных данных в построителе отчетов](../Topic/Specify%20Credentials%20in%20Report%20Builder.md).  
  
###### Специальные символы в пароле  
 Если источник данных OLE DB настроен таким образом, что предлагается ввести пароль, либо пароль включен в строку подключения и пользователь вводит пароль, содержащий специальные символы (например, знаки препинания), драйверы некоторых базовых источников данных не смогут проверить специальные символы. При обработке отчета сообщение «Неверный пароль» может быть признаком этой ошибки.  
  
> [!NOTE]  
>  Не рекомендуется включать в строку соединения такие сведения, относящиеся к имени входа, как пароли. В построителе отчетов в диалоговом окне **Источник данных** предусмотрена отдельная вкладка, где можно ввести учетные данные.  
  
 ![Значок стрелки, используемый со ссылкой «В начало»](../../analysis-services/instances/media/uparrow16x16.png "Значок стрелки, используемый со ссылкой «В начало»") [В начало](#BackToTop)  
  
##  <a name="Parameters"></a> Параметры  
 Некоторые поставщики OLE DB поддерживают неименованные параметры и не поддерживают именованные параметры. Параметры передаются по расположению с помощью заполнителя в запросе. Символ заполнителя определяется синтаксисом, который поддерживается поставщиком данных.  
  
 ![Значок стрелки, используемый со ссылкой «В начало»](../../analysis-services/instances/media/uparrow16x16.png "Значок стрелки, используемый со ссылкой «В начало»") [В начало](#BackToTop)  
  
##  <a name="Remarks"></a> Замечания  
 OLEDB представляет собой собственную технологию создания поставщиков данных для определенных источников данных. Технология OLEDB основана на COM-интерфейсах. Технология OLEDB была разработана после появления технологии ODBC, но раньше поставщиков данных ADO.NET. Поставщики данных OLEDB регистрируются в операционной системе аналогично остальным COM-компонентам. Поставщики данных OLEDB предоставляются корпорацией Майкрософт и сторонними производителями. Корпорация Майкрософт также предоставляет MSDASQL, поставщик данных OLEDB, обеспечивающий мост с драйверами ODBC. Дополнительные сведения см. в разделе [Тип соединения ODBC (службы SSRS)](../../reporting-services/report-data/odbc-connection-type-ssrs.md).  
  
 Для успешного получения требуемых данных необходимо, чтобы синтаксис запроса поддерживался поставщиком данных. Поддержка параметров различается в зависимости от поставщика данных. Дополнительные сведения см. в разделах по выбранным поставщикам данных. Например:  
  
-   [Поставщик OLE DB служб Analysis Services (службы Analysis Services — многомерные данные)](../Topic/Analysis%20Services%20OLE%20DB%20Provider%20\(Analysis%20Services%20-%20Multidimensional%20Data\).md)  
  
-   [Использование поставщика данных платформы .NET Framework для Oracle](http://go.microsoft.com/fwlink/?LinkId=112314)  
  
-   [SQL Server Native Client (OLE DB)](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
 Дополнительные сведения о конкретных поставщиках данных OLE DB см. в разделе [Источники данных, поддерживаемые службами Reporting Services (SSRS)](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md) документации по службам [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] в [электронной документации](http://go.microsoft.com/fwlink/?linkid=121312) по [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Значок стрелки, используемый со ссылкой «В начало»](../../analysis-services/instances/media/uparrow16x16.png "Значок стрелки, используемый со ссылкой «В начало»") [В начало](#BackToTop)  
  
##  <a name="HowTo"></a> Инструкции  
 В этом разделе содержатся пошаговые инструкции по работе с подключениями к данным, источниками данных и наборами данных.  
  
 [Добавление и проверка подключения к данным (построитель отчетов и службы SSRS)](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
 [Создание общего или внедренного набора данных (построитель отчетов и службы SSRS)](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)  
  
 [Добавление фильтра к набору данных (построитель отчетов и службы SSRS)](../../reporting-services/report-data/add-a-filter-to-a-dataset-report-builder-and-ssrs.md)  
  
 ![Значок стрелки, используемый со ссылкой «В начало»](../../analysis-services/instances/media/uparrow16x16.png "Значок стрелки, используемый со ссылкой «В начало»") [В начало](#BackToTop)  
  
##  <a name="Related"></a> См. также  
 В этих разделах документации содержатся подробные сведения о данных отчетов, а также методические сведения об определении, настройке и использовании элементов отчетов, связанных с данными.  
  
 [Наборы данных отчетов (службы SSRS)](../../reporting-services/report-data/report-datasets-ssrs.md)  
 Предоставляет общие сведения о доступе к данным отчета.  
  
 [Подключения к данным, источники данных и строки подключения в построителе отчетов](../Topic/Data%20Connections,%20Data%20Sources,%20and%20Connection%20Strings%20in%20Report%20Builder.md)  
 Предоставляет сведения о подключениях к данным и источникам данных.  
  
 [Внедренные и общие наборы данных отчета (построитель отчетов и службы SSRS)](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
 Предоставляет сведения об общих и внедренных наборах данных.  
  
 [Коллекция полей набора данных (построитель отчетов и службы SSRS)](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)  
 Предоставляет сведения о коллекции полей набора данных, создаваемой запросом.  
  
 [Источники данных, поддерживаемые службами Reporting Services (SSRS)](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md), см. в документации к [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] в [электронной документации](http://go.microsoft.com/fwlink/?linkid=121312) по [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
 Предоставляет подробные сведения о поддержке платформ и версий для каждого модуля обработки данных.  
  
 ![Значок стрелки, используемый со ссылкой «В начало»](../../analysis-services/instances/media/uparrow16x16.png "Значок стрелки, используемый со ссылкой «В начало»") [В начало](#BackToTop)  
  
## См. также  
 [Параметры отчета (построитель отчетов и конструктор отчетов)](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [Фильтрация, группирование и сортировка данных (построитель отчетов и службы SSRS)](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Выражения (построитель отчетов и службы SSRS)](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)  
  
  