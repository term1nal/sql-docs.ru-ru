---
title: "Настройка набора полей по умолчанию для отчетов Power View (табличные службы SSAS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/23/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "ql12.asvs.bidtoolset.deffieldset.f1"
ms.assetid: 6836b42f-28b8-4a98-a86d-2c3c109f0189
caps.latest.revision: 7
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Настройка набора полей по умолчанию для отчетов Power View (табличные службы SSAS)
  Набор полей по умолчанию представляет собой предустановленный список столбцов и мер, которые автоматически добавляются на лист отчета [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] при выборе таблицы из списка полей отчета. Автор табличной модели может создавать наборы полей по умолчанию, чтобы удалить лишние шаги для создателей отчетов, которые используют модель данных для своих отчетов. Например, если известно, что большинство авторов отчетов, работающих с контактными сведениями клиентов, хотят видеть имя, основной номер телефона, адрес электронной почты и название компании, можно сделать предварительный выбор этих столбцов так, чтобы они всегда добавлялись на лист отчета, если автор щелкает таблицу «Сведения о клиентах».  
  
> [!NOTE]  
>  Набор полей по умолчанию применим только к табличной модели, которая используется в качестве модели данных в [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]. Наборы полей по умолчанию не поддерживаются в сводных отчетах Excel.  
  
## Создание набора полей по умолчанию  
 Пользователь определяет, какие поля должны быть включены по умолчанию при выборе любой таблицы в [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]. Владелец книги также может определять порядок появления полей в списке. Чтобы указать набор полей по умолчанию, необходимо задать свойства отчета в проекте табличной модели.  
  
#### Добавление набора полей по умолчанию  
  
1.  В среде [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] щелкните таблицу (вкладку), для которой настраивается список полей по умолчанию.  
  
2.  В окне **Свойства** щелкните в поле **Набор полей по умолчанию** и выберите команду **Щелкнуть для изменения**.  
  
3.  В диалоговом окне «Набор полей по умолчанию» выберите одно или несколько полей. Можно выбрать любое поле из таблицы, включая меры. Удерживайте клавишу SHIFT, чтобы выбрать диапазон, или клавишу CTRL, чтобы выбрать определенные ячейки.  
  
4.  Нажмите кнопку **Добавить** , чтобы добавить их в набор полей по умолчанию.  
  
5.  С помощью кнопок «Вниз» и «Вверх» задайте порядок полей в списке. Поля будут добавлены в отчет в указанном порядке.  
  
6.  Повторите шаги для других таблиц книги.  
  
## Следующий шаг  
 После создания набора полей по умолчанию можно также указать заголовки по умолчанию, изображения, групповые поведения или указать, должны строки, содержащие одно значение, группироваться вместе в одну строку или отображаться по отдельности. Дополнительные сведения см. в разделе [Настройка свойств работы таблицы для отчетов Power View (табличные службы SSAS)](../../analysis-services/tabular-models/configure-table-behavior-properties-for-power-view-reports-ssas-tabular.md).  
  
  