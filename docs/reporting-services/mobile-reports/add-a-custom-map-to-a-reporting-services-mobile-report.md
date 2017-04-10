---
title: "Добавление пользовательской карты в мобильный отчет служб Reporting Services | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: fd259b95-bb58-4eb1-a436-6aa12fc6f5f2
caps.latest.revision: 6
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 6
---
# Добавление пользовательской карты в мобильный отчет служб Reporting Services
Для пользовательской карты требуется два файла:  
* SHP-файл для контуров фигур;  
* DBF-файл для метаданных  
  
Вы можете ознакомиться с дополнительными сведениями о [пользовательских картах в мобильных отчетах служб Reporting Services](../../reporting-services/mobile-reports/custom-maps-in-reporting-services-mobile-reports.md).  
  
Храните эти два файла в одной папке. Их имена должны совпадать (например, canada.shp и canada.dbf). Метаданные (DBF-файл) должны включать в себя поле "NAME" со значением соответствующего имени фигуры (ключа), которое будет использоваться при заполнении карты данными.   
  
## Загрузка пользовательской карты  
  
1. На вкладке **Макет** выберите тип карты (**Gradient Heat Map** (Градиентная тепловая карта), **Range Stop Heat Map** (Относительная тепловая карта) или **Пузырьковая карта**), перетащите ее в область конструктора и придайте карте нужный размер.  
  
   ![Коллекция карт SSMRP](../../reporting-services/mobile-reports/media/ssmrp-mapsgallery.png)  
  
2. В представлении **Макет** на панели **Визуальные свойства** в меню **Карта** выберите **Custom Map From File** (Пользовательская карта из файла).   
  
   ![SSMRP_SelectCustomMap](../../reporting-services/mobile-reports/media/ssmrp-selectcustommap.png)  
  
3. В диалоговом окне **Открытие** перейдите к расположению SHP-файла и DBF-файла и выберите их.   
  
   ![SSMRP_SelectDBFandSHP](../../reporting-services/mobile-reports/media/ssmrp-selectdbfandshp.png)  
  
## Подключение данных к пользовательской карте  
Когда пользовательская карта добавляется в отчет впервые, [!INCLUDE[SS_MobileReptPub_Short](../../includes/ss-mobilereptpub-short.md)] добавляет в нее смоделированные географические данные.  
  
![Данные карт SSMRP](../../reporting-services/mobile-reports/media/ssmrp-mapsdata.png)  
  
Реальные данные в пользовательской карте отображаются так же, как и данные во встроенных картах. Следуйте указаниям в разделе [Карты в мобильных отчетах служб Reporting Services](../../reporting-services/mobile-reports/maps-in-reporting-services-mobile-reports.md), чтобы отобразить данные.  
  
### См. также:  
- [Custom maps in Reporting Services mobile reports](../../reporting-services/mobile-reports/custom-maps-in-reporting-services-mobile-reports.md)  
- [Maps in Reporting Services mobile reports](../../reporting-services/mobile-reports/maps-in-reporting-services-mobile-reports.md)  
- [Создание и публикация мобильных отчетов с помощью издателя мобильных отчетов SQL Server](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)   
  
  
  
  