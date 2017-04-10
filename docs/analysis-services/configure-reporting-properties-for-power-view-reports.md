---
title: "Настройка свойств отчетов для отчетов Power View | Microsoft Docs"
ms.custom: ""
ms.date: "02/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: 0ffc5f44-17d3-42d4-bc2c-baf3b4485e2d
caps.latest.revision: 16
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Настройка свойств отчетов для отчетов Power View
На этом дополнительном занятии мы рассмотрим задание свойств отчетов для проекта модели интернет-продаж Adventure Works. Свойства отчетов упрощают пользователям выбор и отображение данных модели в Power View. Можно также задать свойства, позволяющие скрывать некоторые столбцы и таблицы, а также создавать новые данные для использования в диаграммах.  
  
По окончании этого занятия и повторного развертывания модели на экземпляре служб [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] в режиме интеграции с SharePoint и служб [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] вы сможете создать источник данных, задать информацию о подключении к данным, запустить Power View и после этого создавать отчеты по модели.  
  
На этом занятии не рассматривается создание и использование отчетов Power View. Его целью является предоставление авторам табличной модели обзора свойств и параметров, оказывающих влияние на внешний вид отчета в Power View. Дополнительные сведения о создании отчетов Power View см. в документе [Учебник. Создание образца отчета в Power View](http://go.microsoft.com/fwlink/?LinkId=221204).  
  
Предполагаемое время выполнения данного занятия: **30 минут**  
  
## Предварительные требования  
Это дополнительное занятие является частью учебника по табличному моделированию, который необходимо изучать по порядку. Прежде чем выполнять задания в этом дополнительном занятии, необходимо завершить все предыдущие занятия.  
  
Для выполнения этого дополнительного занятия необходимо иметь следующее.  
  
-   Модель интернет-продаж Adventure Works (выполняемая в этом учебнике) готова к развертыванию или уже развернута на экземпляре служб Analysis Services, работающем в табличном режиме.  
  
-   Сайт SharePoint интегрирован со службами [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)] в табличном режиме и службами [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)], настроенными для поддержки отчетов Power View.  
  
-   Необходимо иметь достаточные разрешения для создания подключения к данным на сайте SharePoint, который указывает на модель интернет-продаж Adventure Works.  
  
## Свойства модели, влияющие на отчеты  
При создании табличной модели имеются некоторые свойства, которые можно задать для отдельных столбцов и таблиц для улучшения работы пользователей с отчетами в Power View. Кроме того, можно создать дополнительные данные отчета для поддержки представления и других функций, специфичных для клиента построения отчетов. В образце модели интернет-продаж Adventure Works имеются некоторые изменения, которые нужно внести.  
  
-   **Добавление новых данных** — это вычисляемый столбец с формулой DAX, которая создает информацию о дате в формате, который проще отображать в диаграммах.  
  
-   **Скрытие столбцов и таблиц, ненужных пользователю**. Столбец **Скрытый** управляет отображением столбцов и таблиц в клиенте отчетов. Скрытые элементы будут по-прежнему частью модели и доступны для запросов и вычислений.  
  
-   **Включение таблиц одним щелчком**. По умолчанию никакие действия не выполняются, если пользователь щелкает таблицу в списке полей. Для изменения этого поведения, чтобы щелчок таблицы добавлял эту таблицу в отчет, необходимо задать набор полей по умолчанию для каждого столбца, который требуется включить в таблицу. Это свойство имеет значение для столбцов таблицы, которые пользователи, скорее всего, будут использовать.  
  
-   **Задание группирования по мере необходимости**. Свойство **Сохраните уникальные строки** определяет, нужно ли группировать значения в столбце по другому полю, например по идентификатору. Для столбцов, содержащих повторяющиеся значения, такие как имена клиентов (например, нескольких клиентов зовут Александр Иванов), важно выполнить группирование (по уникальным строкам) по полю **Идентификатор строки**, чтобы представить пользователю правильный результат.  
  
-   **Задание типов и форматов данных**. По умолчанию Power View применяет правила исходя из типа данных столбца, чтобы определить, может ли поле использоваться в качестве меры. Так как каждая визуализация данных в Power View также может иметь правила, касающиеся того, где могут быть помещены меры и данные, отличные от мер, важно задать тип данных в модели либо переопределить значение по умолчанию, чтобы добиться результата, необходимого пользователю.  
  
-   Свойство**Задать сортировку по столбцу** — это свойство **Сортировать по столбцу** , определяющее значения в столбце, которые необходимо сортировать по значениям в другом поле. Например, столбец Month Calendar, содержащий название месяца, должен сортироваться по столбцу Month Number.  
  
## Скрыть таблицы от клиентских средств  
Поскольку в таблице Product уже есть вычисляемый столбец Product Category и Product Subcategory, не нужно делать таблицы Product Category и Product Subcategory видимыми для клиентских приложений.  
  
#### Скрытие таблиц Product Category и Product Subcategory  
  
1.  В конструкторе моделей щелкните таблицу (вкладку) **Product Category** правой кнопкой мыши и выберите пункт **Скрыть из набора клиентских средств**.  
  
2.  Щелкните таблицу (вкладку) **Product Subcategory** правой кнопкой мыши и выберите пункт **Скрыть из набора клиентских средств**.  
  
## Создание новых данных для диаграмм  
Иногда бывает необходимо создавать в модели новые данные с помощью формул DAX. В данной задаче будет добавлено два новых вычисляемых столбца в таблице Date. Эти новые столбцы представляют поля даты в формате, удобном для использования в диаграммах.  
  
#### Создание новых данных для диаграмм  
  
1.  В таблице **Date** выполните прокрутку до правого края и щелкните **Добавить столбец**.  
  
2.  Добавляется 2 новых вычисляемых столбца со следующими формулами в строке формул.  
  
    |Имя столбца|Формула|  
    |---------------|-----------|  
    |Квартал года|=[Calendar Year] & " Q" & [Calendar Quarter]|  
    |Year Month|=[Calendar Year] & FORMAT([Month],"#00")|  
  
## Набор полей по умолчанию  
Набор полей по умолчанию представляет собой стандартный список столбцов и мер для таблицы, которые автоматически добавляются на лист отчета Power View при выборе таблицы из списка полей отчета. В сущности можно задать столбцы по умолчанию, меры и упорядочение полей, которые пользователи увидят, когда эта таблица будет визуализирована в отчетах Power View.  Для модели интернет-продаж нужно определить набор полей по умолчанию и порядок для таблиц Customer, Geography и Product. Включаются только наиболее распространенные столбцы, которые нужны пользователям во время анализа интернет-продаж Adventure Works в отчетах Power View.  
  
Дополнительные сведения о наборе полей по умолчанию см. в разделе [Настройка набора полей по умолчанию для отчетов Power View (табличные службы SSAS)](../analysis-services/tabular-models/configure-default-field-set-for-power-view-reports-ssas-tabular.md) электронной документации по SQL Server.  
  
#### Задание набора полей по умолчанию для таблиц  
  
1.  В конструкторе моделей щелкните таблицу (вкладку) **Заказчик**.  
  
2.  В окне **Свойства** в разделе **Свойства отчетов**для свойства **Набор полей по умолчанию** щелкните текст **Щелкните, чтобы изменить** , чтобы открыть диалоговое окно **Набор полей по умолчанию** .  
  
3.  В диалоговом окне в списке **Набор полей по умолчанию** в разделе **Поля в таблице** нажмите клавишу CTRL и выберите следующие поля, а затем нажмите **Добавить**.  
  
    **Birth Date**, **Customer Alternate Id**, **First Name**, **Last Name**.  
  
4.  В окне **Поля по умолчанию по порядку** с помощью кнопок перемещения вверх и вниз разместите элементы в следующем порядке.  
  
    **Customer Alternate Id**  
  
    **First Name**  
  
    **Last Name**  
  
    **Birth Date**.  
  
5.  Нажмите кнопку **ОК** , чтобы закрыть диалоговое окно **Набор полей по умолчанию** для таблицы **Customer** .  
  
6.  Выполните те же шаги для таблицы **Geography** , выбрав следующие поля и разместив их в этом порядке.  
  
    **City**, **State Province Code**, **Country Region Code**.  
  
7.  Наконец, выполните те же действия для таблицы **Product** , выбрав следующие поля и разместив их в том же порядке.  
  
    **Product Alternate Id**, **Product Name**.  
  
## Поведение таблиц  
Свойства поведения таблиц позволяют изменить поведение по умолчанию для различных типов представления и группирования таблиц, используемых в отчетах Power View. Это повышает эффективность размещения и идентификации — имена, изображения, заголовки в мозаике, макеты карт и диаграмм.  
  
Подробные сведения о свойствах поведения таблиц см. в разделе [Настройка свойств работы таблицы для отчетов Power View (табличные службы SSAS)](../analysis-services/tabular-models/configure-table-behavior-properties-for-power-view-reports-ssas-tabular.md).  
  
#### Задание поведения таблиц  
  
1.  В конструкторе моделей щелкните таблицу (вкладку) **Заказчик**.  
  
2.  В окне **Свойства** для свойства **Поведение таблицы** щелкните текст **Щелкните, чтобы изменить**, чтобы открыть диалоговое окно **Поведение таблицы** .  
  
3.  В диалоговом окне **Поведение таблиц** в раскрывающемся списке **Идентификатор строки** выберите столбец **Customer Id** .  
  
4.  В списке **Сохранять уникальные строки** выберите **First Name** и **Last Name**.  
  
    Этот параметр указывает, есть ли у этого столбца значения, которые должны рассматриваться как уникальные, даже если они содержат повторяющиеся значения, например если несколько сотрудников имеют одно и то же имя.  
  
5.  В раскрывающемся списке **Метка по умолчанию** выберите столбец **Last Name** .  
  
    Этот параметр указывает, что столбец содержит отображаемое имя для представления данных в строке.  
  
6.  Повторите эти шаги для таблицы **Geography** , выбрав столбец **Geography Id** в качестве идентификатора строки, а столбец **City** в списке **Сохранить уникальные строки** . Нет необходимости задавать метку по умолчанию для этой таблицы.  
  
7.  Повторите эти шаги для таблицы **Product** , выбрав столбец **Product Id** в качестве идентификатора строки, а столбец **Product Name** в списке **Сохранить уникальные строки** . В поле **Метка по умолчанию**выберите **Product Alternate Id**.  
  
## Свойства отчетов для столбцов  
Можно задать несколько основных свойств столбца и отдельные свойства отчетов по столбцам для улучшения моделей отчетов. Например, пользователю может потребоваться возможность видеть все столбцы во всех таблицах. Таким же образом, как и ранее с таблицами Product Category и Product Subcategory, с помощью свойства «Скрытый» можно скрыть отдельные столбцы в таблице, если они отображаются. Другие свойства, например «Формат данных» и «Сортировать по столбцу», также влияют на отображение данных в отчетах. Зададим некоторые из этих столбцов. Другие столбцы не требуют никаких действий и не отображаются ниже.  
  
Здесь необходимо задать только несколько отличающихся свойств, но существует еще и множество других. Дополнительные сведения о свойствах столбцов отчетов см. в разделе [Свойства столбца (табличные службы SSAS)](../analysis-services/tabular-models/column-properties-ssas-tabular.md) электронной документации по SQL Server.  
  
#### Задание свойств столбцов  
  
1.  В конструкторе моделей щелкните таблицу (вкладку) **Заказчик**.  
  
2.  Щелкните столбец **Customer Id** , чтобы свойства столбца отобразились в окне **Свойства** .  
  
3.  В окне **Свойства** установите свойство **Скрытый** равным True. Столбец **Customer Id** становится выделенным серым цветом в конструкторе моделей.  
  
4.  Повторите эти действия, задав следующий столбец и свойства для каждой указанной таблицы. Оставьте все остальные свойства в параметрах по умолчанию.  
  
    Примечание. Убедитесь в том, что для всех столбцов даты **Тип данных** — **Дата**.  
  
    **Customer**  
  
    |Column|Свойство|Значение|  
    |----------|------------|---------|  
    |Geography Id|Скрыта|True|  
    |Birth Date|Формат данных|Short Date|  
  
    **Дата**  
  
    > [!NOTE]  
    > Поскольку таблица Date была выбрана в модели в качестве таблицы дат с помощью параметра «Пометить как таблицу дат» на занятии 7, применяется параметр «Пометить как таблицу дат», столбец Date в таблице Date используется как уникальный идентификатор, а свойство «Идентификатор строки» для столбца Date автоматически устанавливается равным True и не может быть изменено. При использовании функций операций со временем в формулах DAX необходимо указание таблицы дат. В этой модели можно создать несколько мер с помощью функции логики операций со временем, подсчитывать продажи за различные периоды, например предыдущий и текущий кварталы, а также использовать ключевые показатели эффективности (KPI). Дополнительные сведения об определении таблицы дат см. в разделе [Указание таблицы дат для использования с логикой операций со временем (табличные службы SSAS)](../analysis-services/tabular-models/specify-mark-as-date-table-for-use-with-time-intelligence-ssas-tabular.md) электронной документации по SQL Server.  
  
    |Столбец|Свойство|Значение|  
    |----------|------------|---------|  
    |Date|Формат данных|Short Date|  
    |Номер дня недели|Скрыта|True|  
    |День недели|Сортировать по столбцу|Номер дня недели|  
    |Day of Week|Скрыта|True|  
    |День месяца|Скрытый|True|  
    |День года|Скрыта|True|  
    |Названия месяца|Сортировать по столбцам|Месяц|  
    |Месяц|Скрыта|True|  
    |Месячный календарь|Скрыта|True|  
    |Финансовый квартал|Скрыта|True|  
    |Финансовый год|Скрыта|True|  
    |Финансовый семестр|Скрыта|True|  
  
    **Измерение географии**  
  
    |Столбец|Свойство|Значение|  
    |----------|------------|---------|  
    |Geography Id|Скрыта|True|  
    |Идентификатор территории продаж|Скрыта|True|  
  
    **Product**  
  
    |Столбец|Свойство|Значение|  
    |----------|------------|---------|  
    |Product Id|Скрыта|True|  
    |Product Alternate Id|Метка по умолчанию|True|  
    |Идентификатор подкатегории продукта|Скрыта|True|  
    |Дата начала жизненного цикла продукта (Дата начала периода расчета стоимости продукта )|Формат данных|Short Date|  
    |Дата окончания жизненного цикла продукта (Дата окончания периода расчета стоимости продукта)|Формат данных|Short Date|  
  
    **Internet Sales**  
  
    |Столбец|Свойство|Значение|  
    |----------|------------|---------|  
    |Product Id|Скрыта|True|  
    |Customer Id|Скрыта|True|  
    |Идентификатор продвижения|Скрыта|True|  
    |Идентификатор валюты|Скрыта|True|  
    |Идентификатор территории продаж|Скрыта|True|  
    |Заказанное количество|Тип данных<br /><br />Формат данных<br /><br />десятичные разряды|Десятичное число<br /><br />Десятичное число<br /><br />0|  
    |Дата заказа|Формат данных|Short Date|  
    |Дата оплаты счета|Формат данных|Short Date|  
    |Дата отгрузки|Формат данных|Short Date|  
  
## Повторное развертывание табличной модели интернет-продаж Adventure Works  
Поскольку модель была изменена, необходимо развернуть ее повторно. Повторите задачи, которые выполнялись в разделе [Занятие 14. Развертывание](../analysis-services/lesson-14-deploy.md).  
  
#### Повторное развертывание табличной модели интернет-продаж Adventure Works  
  
-   В среде [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]выберите в меню **Построение** команду **Развернуть табличную модель интернет-продаж Adventure Works**.  
  
    Появится диалоговое окно **Развертывание** , в котором будет отображено состояние развертывания метаданных, а также показана каждая таблица, включенная в модель.  
  
## Следующие шаги  
После этого можно использовать Power View для визуализации данных модели. Убедитесь, что учетная запись служб Analysis Services и Reporting Services на сайте SharePoint имеет разрешения на экземпляре служб Analysis Services, на котором будет развернута модель.  
  
Инструкции по созданию источника данных отчета служб Reporting Services, который указывает на модель, см. в разделе [Тип соединения табличной модели (служб SSRS)](http://msdn.microsoft.com/library/hh270317%28v=SQL.110%29.aspx).  
  
  
  