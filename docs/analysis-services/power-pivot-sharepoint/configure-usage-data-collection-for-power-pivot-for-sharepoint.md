---
title: "Настройка сбора данных об использовании с PowerPivot для SharePoint | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 955ca6d6-9d5b-47a4-a87c-59bd23f1bf74
caps.latest.revision: 10
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 9
---
# Настройка сбора данных об использовании с PowerPivot для SharePoint
  Сбор данных об использовании — это функция SharePoint на уровне фермы. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] для SharePoint использует и дополняет эту систему для создания отчетов на информационной панели управления [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , которые показывают, как используются данные и службы [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . В зависимости от способа установки SharePoint сбор данных об использовании для фермы может быть отключен. Для создания данных об использовании, которые будут отображаться на информационной панели управления [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , администратор фермы должен включить ведение журнала использования.  
  
 Сведения о работе с данными об использовании на панели мониторинга управления [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] см. в разделе [Информационная панель управления PowerPivot и данные об использовании](../../analysis-services/power-pivot-sharepoint/power-pivot-management-dashboard-and-usage-data.md).  
  
 **В этом разделе:**  
  
 [Включение сбора данных об использовании и выбор событий, запускающих сбор данных](#events)  
  
 [Определение расположения файлов журнала](#configdb)  
  
 [Настройка заданий таймера, используемых при сборе данных об использовании](#jobs)  
  
 [Ограничение срока хранения журнала данных об использовании](#confighist)  
  
 [Определение категорий быстрых, средних и медленных откликов на запросы для подготовки отчетов](#qrh)  
  
 [Указание периодичности предоставления статистики запросов системе сбора данных об использовании](#ttr)  
  
 [Открытие страницы приложения службы PowerPivot для доступа к параметрам конфигурации](#openconfig)  
  
 [Настройки по умолчанию системы сбора данных об использовании PowerPivot](#defaultconfig)  
  
> [!IMPORTANT]  
>  Данные об использовании позволяют увидеть, как пользователи используют данные и ресурсы, однако они не дают гарантии получения надежных и постоянных данных об операциях сервера и доступе пользователей. Например, если происходит перезапуск сервера, данные о событиях использования будут потеряны и их нельзя будет восстановить. Аналогично, если временные файлы журнала достигают максимального размера, новые данные не будут добавляться до тех пор, пока файлы не будут очищены. Если нужна возможность проводить аудит, можно использовать рабочий процесс и тип содержимого, которые обеспечивает SharePoint, чтобы выстроить подсистему аудита для фермы. Дополнительные сведения см. в документации по продукту и сообществу на сайте.  
  
##  <a name="events"></a> Включение сбора данных об использовании и выбор событий, запускающих сбор данных  
 Настройте параметры сбора данных об использовании в центре администрирования SharePoint.  
  
1.  В центре администрирования нажмите **Наблюдение**.  
  
2.  В **разделе «Отчеты»**нажмите **Настроить сбор данных об использовании и исправности.**  
  
3.  Установите флажок **Включить сбор данных об использовании**.  
  
4.  В разделе **События для записи** установите или снимите флажки, чтобы включить или выключить следующие события службы Analysis Services.  
  
    |Событие|Description|  
    |-----------|-----------------|  
    |**[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Соединения**|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] используется для отслеживания соединений с сервером [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , которые выполняются от имени пользователя.|  
    |**[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Использование операций загрузки данных**|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] позволяет отслеживать запросы на загрузку данных [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] в память сервера. Событие загрузки создается для файлов данных [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , загружаемых из базы данных содержимого или из кэша.|  
    |**[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Использование операций выгрузки данных**|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] позволяет отслеживать запросы на выгрузку источника данных [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] после периода отсутствия активности. Кэширование источника данных [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] на диск будет добавлено в отчет как событие выгрузки.|  
    |**[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Использование запросов**|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] позволяет отслеживать время обработки запросов для данных, загружаемых в экземпляр [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] .|  
  
    > [!NOTE]  
    >  Исправность сервера и операции обновления данных также создают данные об использовании, однако нет события, связанного с этими процессами.  
  
5.  Можно также изменить расположение файла журнала. Дополнительные сведения см. в следующем разделе.  
  
6.  Нажмите кнопку **ОК** , чтобы сохранить внесенные изменения.  
  
7.  Можно также указать, следует ли записывать в журнал все события или только события об ошибках. Дополнительные сведения о регулировании сообщений о событиях см. в разделе [Настройка и просмотр файлов журнала SharePoint и ведение журнала диагностики (PowerPivot для SharePoint)](../Topic/Configure%20and%20View%20SharePoint%20Log%20Files%20%20and%20Diagnostic%20Logging%20\(Power%20Pivot%20for%20SharePoint\).md).  
  
##  <a name="configdb"></a> Определение расположения файлов журнала  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] изначально сохраняются в файлах журналов использования на локальном сервере, а затем с заданной периодичностью переносятся в базы данных приложения службы [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Расположение файлов журналов настраивается в центре администрирования. Расположение по умолчанию:  
  
 `C:\Program Files\Common Files\Microsoft Shared\Web Server Extensions\15\logs`  
  
 Для просмотра или изменения этих свойств используйте страницу **Сбор данных об использовании и исправности** .  
  
1.  На домашней странице центра администрирования выберите **Наблюдение**.  
  
2.  В разделе «Мониторинг» нажмите **Настроить сбор данных об использовании и исправности.**  
  
3.  В параметрах сбора данных об использовании можно просмотреть или изменить расположение, имя или максимальный размер файла. Если указать слишком маленький размер файла, размер файла достигнет предела и новые записи не будут добавляться до тех пор, пока его содержимое не будет перемещено в центральную базу данных сбора данных об использовании.  
  
##  <a name="jobs"></a> Настройка заданий таймера, используемых при сборе данных об использовании  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] переносятся в разные расположения в системе сбора данных об использовании с помощью двух заданий таймера.  
  
-   Задание таймера "Импорт данных об использовании Microsoft SharePoint Foundation" перемещает данные об использовании [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] в базу данных приложения службы [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
-   "Задание таймера по обработке панели управления [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]" переносит данные в книгу [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)], которая служит источником данных для встроенных отчетов администратора.  
  
 Если нужно чаще обновлять отчеты администратора, отображаемые на информационной панели управления [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , сделайте следующее.  
  
1.  В центре администрирования нажмите **Наблюдение**.  
  
2.  Нажмите кнопку **Просмотр определений заданий** В **Задания таймера** .  
  
3.  Нажмите кнопку **Импорт данных об использовании Microsoft SharePoint Foundation**.  
  
4.  Нажмите кнопку **Выполнить**. Если кнопка **Выполнить** неактивна, откройте меню **Включить** и выберите команду **Выполнить**.  
  
5.  В списке определений заданий выберите **[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Data Management Dashboard Processing Timer Job**(Задание таймера обработки информационной панели управления данными PowerPivot).  
  
6.  Нажмите кнопку **Выполнить**.  
  
7.  Чтобы просмотреть обновленные данные, щелкните отчеты. Дополнительные сведения см. в разделе [Power Pivot Management Dashboard and Usage Data](../../analysis-services/power-pivot-sharepoint/power-pivot-management-dashboard-and-usage-data.md).  
  
##  <a name="confighist"></a> Ограничение срока хранения журнала данных об использовании  
 Журнал данных об использовании хранится для событий (соединений, загрузки, выгрузки и обработки запросов) и обновления данных (обработки данных по расписанию). Хотя данные по использованию собираются с помощью системы сбора данных SharePoint, данные отчетов перемещаются в базу данных приложения [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] и базу данных отчетов для более длительного хранения. Параметры журнала данных об использовании устанавливают, как долго данные об использовании будут храниться в базах данных приложения [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Такое же ограничение применяется ко всем типам хранимых данных об использовании в той же базе данных приложения службы [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
1.  [Откройте страницу приложения службы PowerPivot](#openconfig).  
  
2.  В разделе **Сбор данных об использовании** в поле **Журнал данных об использовании**введите число дней, в течение которых должны сохраняться записи об операциях обновления данных для каждой книги.  
  
    -   Значение по умолчанию — 365 суток.  
  
    -   0 означает неограниченное хранение, то есть данные об использовании сохраняются на неопределенное время.  
  
    -   Другой способ — указать для максимума значение между 1 и 5000.  
  
     Уменьшение срока хранения до меньшего количества дней удалит все данные, превышающие новое ограничение. Например, изменение значения с 365 до 30 приведет к удалению данных для всех событий журнала, которые произошли более 30 дней назад. Сохранятся только данные за последние 30 дней.  
  
     Фактически данные будут удалены, когда произойдет следующее событие. Ограничение для журнала данных об использовании проверяется только тогда, когда система обрабатывает событие.  
  
3.  Нажмите кнопку **ОК**.  
  
 Дополнительные сведения о сборе и хранении данных об использовании см. в разделе [Сбор данных об использовании PowerPivot](../../analysis-services/power-pivot-sharepoint/power-pivot-usage-data-collection.md).  
  
##  <a name="qrh"></a> Определение категорий быстрых, средних и медленных откликов на запросы для подготовки отчетов  
 Производительность обработки запросов измеряется по стандартным категориям, которые характеризуют цикл «запрос-ответ» по продолжительности завершения цикла. Стандартные категории запросов включают тривиальный, быстрый, ожидаемый, долгий и превышенный. Каждый запрос к серверу [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] попадает в одну из категорий в зависимости от времени его выполнения.  
  
 Информация об ответе на запрос используется в отчетах о функционировании. В таких отчетах каждая категория используется по-разному, чтобы лучше выявлять тенденции изменения производительности системы [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Например, тривиальные запросы полностью исключаются, поскольку их исключение удаляет шум из данных и показывает более значимые тренды по оставшимся категориям. Напротив, статистика по долгим и ожидаемым запросам выделяется в отчете, чтобы администраторы или владельцы книг могли сразу предпринять необходимые действия по исправлению.  
  
 Нельзя добавлять или удалять категории, однако можно задать верхний и нижний пределы, которые определят, где заканчивается одна категория и начинается другая. Если в организации используются соглашения по уровню обслуживания (SLA), то для определения приемлемых уровней доступности и производительности сервера можно настроить категории в соответствии с нормами этих соглашений.  
  
1.  [Откройте страницу приложения службы PowerPivot](#openconfig).  
  
2.  В разделе **Сбор данных об использовании** в поле **Верхняя граница тривиального ответа** введите значение (в миллисекундах), которое будет являться верхней границей для получения тривиального ответа. Запросы, которые соответствуют данной категории, — это, как правило, PING-запросы серверу, инициация сеанса и запрос метаданных. Значение по умолчанию равно 500 миллисекунд (или полсекунды).  
  
3.  В поле «Верхний предел для быстрых запросов» введите значение (в миллисекундах), которое будет являться верхней границей для получения быстрого ответа. Запросы, которые соответствуют данной категории, — это запросы очень маленьких наборов данных или метаданных для больших наборов данных. Значение по умолчанию равно 1000 миллисекунд (или 1 секунде).  
  
4.  В поле **Верхняя граница ожидаемого времени ответа** введите значение (в миллисекундах), которое будет являться верхней границей для получения ответа за ожидаемое или среднее время. Запросы, которые соответствуют данной категории, включают загрузку данных в обозреватель. Значение по умолчанию равно 3000 миллисекунд (3 секундам).  
  
5.  В поле **Верхняя граница долгого ответа** введите значение (в миллисекундах), которое будет являться верхней границей для получения долгого ответа. Такие запросы длятся дольше, чем ожидаемые, но тем не менее попадают в приемлемый диапазон. Значение по умолчанию равно 10000 миллисекунд (10 секундам).  
  
     Запросы, которые превышают данное ограничение, входят в категорию *Превышенный*. Не существует порога для категории *Превышенный*. Порог определяется автоматически исходя из верхней границы, указанной в поле «Верхний предел для долгих запросов». Запросы, попадающие в категорию «Превышенный», длятся дольше, чем разрешено указанным соглашением по уровню обслуживания.  
  
6.  Нажмите кнопку **ОК**.  
  
##  <a name="ttr"></a> Указание периодичности предоставления статистики запросов системе сбора данных об использовании  
 Интервал «время отчета» указывает периодичность предоставления статистики запросов системе сбора данных об использовании. Статистика о запросах собирается в процессе и сообщается как одиночное событие через заданные интервалы времени. Интервал можно изменить для записи большего или меньшего количества событий в файл журнала.  
  
1.  [Откройте страницу приложения службы PowerPivot](#openconfig).  
  
2.  В разделе **Сбор данных об использовании** в поле **Период составления отчетов о запросах** введите количество секунд, по истечении которых сервер отправит отчет по статистике запросов для всех категорий (тривиальный, быстрый, ожидаемый, долгий и превышенный) как об одном событии в систему сбора данных об использовании.  
  
    -   Диапазон включает любые целые положительные числа, начиная с 1.  
  
    -   Значение по умолчанию равно 300 секундам (или 5 минутам). Данное значение рекомендуется для динамических сред фермы, в которых работает большое количество приложений и серверов.  
  
     Если сделать данное значение значительно больше, это может привести к потере статистических данных, прежде чем они попадут в отчет. Например, перезапуск службы приведет к потере статистики запросов. И наоборот, если встроенные отчеты о функционировании включают недостаточное количество данных, можно попробовать уменьшить интервал, чтобы получать чаще события времени отчета.  
  
3.  Нажмите кнопку **ОК**.  
  
##  <a name="openconfig"></a> Открытие страницы приложения службы PowerPivot для доступа к параметрам конфигурации  
 Чтобы изменить параметры приложения службы, необходимы права администратора фермы или службы. Если в ферме определено несколько приложений службы [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , каждое из них необходимо изменить индивидуально.  
  
1.  В центре администрирования SharePoint на вкладке **Управление приложениями**выберите **Управление приложениями служб**.  
  
2.  Найдите приложение службы [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Определить приложение службы можно по его типу. Тип приложения службы [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] — **Приложение службы [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]**.  
  
3.  Щелкните имя приложения службы [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Откроется информационная панель управления [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
4.  В разделе **Действия**выберите пункт **Настройка параметров приложения службы**. Откроется страница параметров приложения службы [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
##  <a name="defaultconfig"></a> Настройки по умолчанию системы сбора данных об использовании PowerPivot  
 Сбор данных об использовании для операций служб [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] можно включить с параметрами по умолчанию, чтобы функция была сразу доступна в приложениях, которые поддерживают возможность интеграции со службами Analysis Services. Параметры по умолчанию включают события, которые запускают сбор данных об использовании, предельное время хранения данных об использовании и пороги для категорий длительности ответов на запросы.  
  
 Следующая таблица показывает значения по умолчанию для настройки сбора данных об использовании.  
  
|Настройка|Значение по умолчанию|Тип|Допустимый диапазон|  
|-------------|-------------------|----------|-----------------|  
|**События использования служб Analysis Services** (соединение, загрузка, выгрузка, запросы)|\<включен>|Логическое значение|Эти значения либо включены, либо выключены.|  
|**Период составления отчетов о запросах**|300 (в секундах)|Целочисленный|От 1 до любого целого положительного числа. Значение по умолчанию равно 5 минутам.|  
|**Журнал данных об использовании**|365 (дни)|Целочисленный|0 означает неограниченное время, однако можно также задать верхнюю границу, по достижении которой данные журнала будут удалены автоматически. Допустимые значения для ограниченного срока хранения — от 1 до 5000 (в днях).|  
|Верхняя граница тривиального ответа|500 (в миллисекундах)|Целочисленный|Задает верхнюю границу, которая определяет время отклика на тривиальный запрос. Запрос, который завершается в течение от 0 до 500 миллисекунд, является тривиальным запросом и не включается в отчет.|  
|Верхняя граница быстрого ответа|1000 (в миллисекундах)|Целочисленный|Задает верхнюю границу, которая определяет время быстрого отклика на запрос.|  
|Верхняя граница ожидаемого времени ответа|3000 (в миллисекундах)|Целочисленный|Задает верхнюю границу, которая определяет ожидаемое время отклика на запрос.|  
|Верхняя граница долгого ответа|10000 (в миллисекундах)|Целочисленный|Задает верхнюю границу, которая определяет время отклика на долгий запрос. Запросы, превышающие данное ограничение, попадают в категорию "Превышенный", у которой нет верхнего предела.|  
  
## См. также  
 [Справочник по параметрам конфигурации (PowerPivot для SharePoint)](../../analysis-services/power-pivot-sharepoint/configuration-setting-reference-power-pivot-for-sharepoint.md)   
 [Сбор данных об использовании Power Pivot](../../analysis-services/power-pivot-sharepoint/power-pivot-usage-data-collection.md)  
  
  