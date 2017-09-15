---
title: "Извлечение приложения уровня данных из базы данных | Документация Майкрософт"
ms.custom: 
ms.date: 07/18/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-data-tier-apps
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.extractdacwizard.validationandsummary.f1
- sql13.swb.extractdacwizard.introduction.f1
- sql13.swb.extractdacwizard.selectdatapage.f1
- sql13.swb.extractdacwizard.setdacproperties.f1
- sql13.swb.extractdacwizard.buildandsave.f1
helpviewer_keywords:
- extract DAC
- How to [DAC], extract
- data-tier application [SQL Server], extract
- wizard [DAC], extract
ms.assetid: ae52a723-91c4-43fd-bcc7-f8de1d1f90e5
caps.latest.revision: 21
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: faeab1963609f5563f31e13b2ee965fdac8a43b8
ms.contentlocale: ru-ru
ms.lasthandoff: 06/22/2017

---
# <a name="extract-a-dac-from-a-database"></a>Извлечение приложения уровня данных из базы данных
  Извлечение пакета приложения уровня данных из существующей базы данных SQL Server можно с помощью **мастера извлечения приложения уровня данных** или скрипта Windows PowerShell. В результате извлечения будет создан файл пакета DAC, содержащий определения объектов базы данных и связанные элементы уровня экземпляра. Например, файл пакета DAC содержит все таблицы базы данных, хранимые процедуры, представления, пользователей и имена входа, сопоставленные с пользователями базы данных.  
  
 
## <a name="before-you-begin"></a>Перед началом  
 Предусмотрена возможность извлечения приложения уровня данных из баз данных, находящихся на экземплярах [!INCLUDE[ssSDS](../../includes/sssds-md.md)]или [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] с пакетом обновления 4 (SP4) или более поздних версий. Если процесс извлечения запущен для базы данных, которая была развернута из приложения уровня данных, то происходит извлечение только определений объектов в базе данных. Этот процесс не ссылается на приложение уровня данных, зарегистрированное в **msdb** (**master** в [!INCLUDE[ssSDS](../../includes/sssds-md.md)]). Процесс извлечения не регистрирует определение приложения уровня данных в текущем экземпляре компонента Database Engine. Дополнительные сведения о регистрации приложения уровня данных см. в разделе [Register a Database As a DAC](../../relational-databases/data-tier-applications/register-a-database-as-a-dac.md).  
  
##  <a name="LimitationsRestrictions"></a> Ограничения  
 Приложение уровня данных может быть извлечено только из базы данных в [!INCLUDE[ssSDS](../../includes/sssds-md.md)], либо в [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] с пакетом обновления 4 (SP4) и более поздних версиях. Извлечь приложение уровня данных нельзя, если в базе данных имеются объекты, не поддерживаемые в приложении уровня данных, или содержащиеся пользователи. Дополнительные сведения о типах объектов, поддерживаемых в DAC, см. в разделе [DAC Support For SQL Server Objects and Versions](../../relational-databases/data-tier-applications/dac-support-for-sql-server-objects-and-versions.md).  
  
##  <a name="Permissions"></a> Разрешения  
 Чтобы извлечь DAC, необходимы по крайней мере разрешение ALTER ANY LOGIN и разрешение VIEW DEFINITION на уровне базы данных, а также разрешения SELECT для представления каталога **sys.sql_expression_dependencies**. Извлечение DAC может выполняться членами предопределенной роли сервера securityadmin, которые также обладают правами предопределенной роли базы данных database_owner в базе данных, из которой извлекается DAC. Приложения уровня данных могут также извлекать члены предопределенной роли сервера sysadmin или встроенной учетной записи системного администратора SQL Server с именем **sa** .  
  
##  <a name="UsingDACExtractWizard"></a> Использование мастера извлечения приложения уровня данных  
 **Извлечение приложения уровня данных с помощью мастера**  
  
1.  В **обозревателе объектов**разверните узел, относящийся к экземпляру, содержащему базу данных, из которой должно быть извлечено приложение уровня данных.  
  
2.  Разверните узел **Базы данных** .  
  
3.  Щелкните правой кнопкой мыши узел, относящийся к базе данных, из которой должно быть извлечено приложение уровня данных, укажите пункт **Задачи**, а затем выберите **Извлечение приложения уровня данных…**  
  
4.  Выполните шаги в диалоговых окнах мастера.  
  
    1.  [Вводная страница](#Introduction)  
  
    2.  [Страница выбора данных](#SelectData)  
  
    3.  [Страница «Задание свойств»](#SetProperties)  
  
    4.  [Страница «Проверка и сводка»](#ValidateSummary)  
  
    5.  [Страница построения пакета](#BuildPackage)  
  
###  <a name="Introduction"></a> Страница общих сведений мастера  
 На этой странице описаны шаги извлечения приложения уровня данных.  
  
 **Больше не показывать эту страницу.** — щелкните этот флажок, чтобы предотвратить отображение этой страницы в будущем.  
  
 **Далее >** — переход к странице **Выбор метода**.  
  
 **Отмена** — завершает работу мастера без извлечения приложения уровня данных из базы данных.  
  
 [&#91;Извлеките мастер&#93;](#UsingDACExtractWizard)  
  
###  <a name="SelectData"></a> Select data page  
Выберите эталонные данные, которые нужно включить в файл пакета приложения уровня данных (пакет DAC). Включать данные в пакет DAC не обязательно. Пакет DAC уже включает схему всех поддерживаемых объектов базы данных и объекты экземпляров, связанные с базой данных.  
  
 В файл пакета DAC можно включать до 10 МБ эталонных данных. Однако таблицы, включаемые в пакет DAC, не должны содержать типы данных больших двоичных объектов (BLOB), такие как **image** или **varchar(max)**. Чтобы извлечь данные большего объема для передачи в другую базу данных, используйте службы SQL Server Integration Services, программу массового копирования или один из многих других методов переноса данных.  
  
 **Таблица базы данных** — установите флажок рядом для тех таблиц в базе данных, где находятся данные, которые необходимо включить в пакет приложения уровня данных. Можно выбрать до десяти таблиц, число строк в которых не превышает 10 000.  
  
 [&#91;Извлеките мастер&#93;](#UsingDACExtractWizard)  
  
###  <a name="SetProperties"></a> Set properties page  
 Эта страница мастера содержит описание приложения уровня данных (DAC). Данные свойства используются для определения DAC и помогают отличать его от других приложений.  
  
 **Имя** — имя приложения уровня данных. Оно может отличаться от имени файла пакета DAC и должно описывать приложение. Например, если база данных используется для финансового приложения, то можно назвать ее «Финансы DAC».  
  
 **Версия (в формате xx.xx.xx.xx, где x — цифра)** — числовое значение, которое указывает версию приложения уровня данных. Версия DAC используется в среде Visual Studio для определения версии DAC, над которой работают разработчики. При развертывании DAC версия сохраняется в базе данных **msdb** и впоследствии доступна в узле **Приложения уровня данных** в среде [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 **Описание:** — необязательно. Описывает DAC. При развертывании DAC описание сохраняется в базе данных **msdb** и впоследствии доступно в узле **Приложения уровня данных** в среде [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
 **Сохранить в файл пакета выделенного административного соединения (укажите имя файла с расширением .dacpac)** — сохраняет приложение уровня данных в файле пакета приложения уровня данных с расширением DACPAC. Нажмите кнопку **Обзор** , чтобы задать имя и выбрать местоположение файла.  
  
 **Перезапись существующего файла** — выберите этот флажок, чтобы заменить файл пакета приложения уровня данных с тем же именем, если он уже существует.  
  
###  <a name="ValidateSummary"></a> Validation and summary page  
 На этой странице мастер проверяет, все ли объекты базы данных поддерживаются приложением уровня данных. На ней также проверяются зависимости между объектами базы данных, чтобы определить набор объектов, которые могут быть успешно включены в DAC. После этого отображается отчет о проверке, содержащий сводку параметров, выбранных в этом мастере. Чтобы изменить параметр, нажмите кнопку **Назад**. Чтобы начать извлечение DAC, нажмите кнопку **Далее**.  
  
> **Примечание.**Если один или несколько объектов не поддерживаются DAC, то кнопка **Далее** будет недоступна и процесс извлечения не может быть продолжен. В таком случае рекомендуется удалить неподдерживаемые объекты и вновь запустить данный мастер.  
  
 **Сводка** — сводка выбранных параметров перечисляется в разделе **Свойства приложения уровня данных**. Результаты проверки отображаются в разделе **Объекты DAC**. Существует три типа результатов проверки:  
  
-   **Объекты, успешно включенные в DAC**: эти объекты и их зависимости поддерживаются и могут быть включены в DAC.  
  
-   **Объекты, включенные в DAC с предупреждениями**: эти объекты поддерживаются, но зависят от других объектов, которые не поддерживаются DAC.  
  
-   **Объекты, не включенные в DAC**: эти объекты не поддерживаются, и перед извлечением DAC их необходимо удалить из базы данных.  
  
 Процесс проверки выполняется на нескольких уровнях зависимости. Например, если хранимая процедура зависит от таблицы, использующей неподдерживаемый тип данных CLR, то хранимая процедура будет отображена в разделе **Объекты, включенные в DAC с предупреждениями**.  
  
 Если один или несколько объектов не поддерживаются DAC, то кнопка **Далее** отключена и процесс извлечения не может быть продолжен. В таком случае рекомендуется удалить неподдерживаемые объекты и вновь запустить данный мастер.  
  
 **Сохранение отчета** — позволяет сохранить HTML-файл, в котором перечислены все объекты, находящиеся под узлом **Объекты приложения уровня данных** , в виде сводки. Этот отчет особенно полезен в тех случаях, когда некоторые из объектов базы данных не поддерживаются DAC. Отчет поможет изменить или удалить неподдерживаемые объекты, прежде чем предпринять новую попытку извлечения DAC.  
  
 ###  <a name="BuildPackage"></a> Build package page  
 Эта страница позволяет наблюдать за ходом выполнения мастером извлечения приложения уровня данных.  
  
 **Действие** — во время выполнения действия **Создать и сохранить файл пакета приложения уровня данных** мастер извлекает приложение уровня данных из базы данных SQL Server. Затем пакет DAC создается в памяти и сохраняется в заданном местоположении. Перейдите по ссылке в столбце **Результат** , чтобы просмотреть результат выполнения соответствующего шага.  
  
 **Сохранить отчет** — щелкните, чтобы сохранить результаты работы мастера в файле.  
  
 **Готово** — закрыть мастер после завершения обработки или возникновения ошибки.  
   
##  <a name="ExtractDACPowerShell"></a> Извлечение пакета DAC с помощью PowerShell  
 **Извлечение приложения уровня данных из базы данных с помощью метода Extract() в скрипте PowerShell**  
  
1.  Создайте объект SMO для сервера и присвойте ему экземпляр, где находится база данных, из которой должно быть извлечено приложение уровня данных.  
  
2.  Добавьте переменную, указывающую имя базы данных.  
  
3.  Укажите метаданные для приложения уровня данных, такие как имя, версия и описание приложения уровня данных.  
  
4.  Укажите путь и имя файла извлеченного пакета DAC.  
  
5.  Запустите метод Extract, передав ему вышеперечисленные данные.  
  
### <a name="example-powershell"></a>Пример (PowerShell)  
 В следующем примере показано, как извлечь приложение уровня данных MyApplication из базы данных MyDB.  
  
```  
## Set a SMO Server object to the default instance on the local computer.  
CD SQLSERVER:\SQL\localhost\DEFAULT  
$srv = get-item .  
  
## Specify the database to extract to a DAC.  
$dbname = "MyDB"  
  
## Specify the DAC metadata.  
$applicationname = "MyApplication"  
$version = "1.0.0.0"  
$description = "This DAC defines the database used by my application."  
  
## Specify the location and name for the extracted DAC package.  
$dacpacPath = "C:\MyDACs\MyApplication.dacpac"  
  
## Extract the DAC.  
$extractionunit = New-Object Microsoft.SqlServer.Management.Dac.DacExtractionUnit($srv, $dbname, $applicationname, $version)  
$extractionunit.Description = $description  
$extractionunit.Extract($dacpacPath)  
```  
  
## <a name="see-also"></a>См. также:  
 [Приложения уровня данных](../../relational-databases/data-tier-applications/data-tier-applications.md)  
  
  
