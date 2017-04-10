---
title: "Автономный доступ к документации по SQL Server | Microsoft Docs"
ms.custom: ""
ms.date: "08/22/2016"
ms.prod: "sql-non-specified"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "server-general"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 257ed357-8cbb-43bd-b042-254be5fbb977
caps.latest.revision: 6
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 6
---
# Автономный доступ к документации по SQL Server

Просмотр технической документации по SQL Server 2016 в автономном режиме.
  
## Предварительные требования
Для просмотра технической документации по SQL Server 2016 в автономном режиме требуется средство HelpViewer 2.2, которое устанавливается вместе со следующими компонентами: 
- [Visual Studio 2015 (любой выпуск, включая Community)](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) или
- [предварительная версия SQL Server Management Studio (SSMS) за апрель 2016 г. (13.0.12500.29) или более поздняя версия.](https://msdn.microsoft.com/library/mt238290.aspx)

Прежде чем перейти к выполнению указанных ниже действий, установите любой из следующих компонентов.
  
## Установка автономной технической документации по SQL Server 

1. Установите любой выпуск Visual Studio 2015 либо предварительную версию SSMS за апрель 2016 г. или более позднюю версию. 
2. Запустите SSMS или Visual Studio.
3. В меню **Справка** в верхней панели навигации выберите пункт **Добавление и удаление содержимого справки**. 

#### (Будет запущено средство HelpViewer.)

4. В HelpViewer выберите источник установки по умолчанию: **Сеть**. 
5. Нажмите кнопку **Добавить** рядом с разделом документации, который нужно установить.
6. Нажмите кнопку **Обновить** в правой нижней части экрана, чтобы скачать и установить выбранную документацию.
![загрузка автономного содержимого](../sql-server/media/load-offline-content.png) 

 >** ВАЖНО!** После нажатия кнопки "Обновить" средство HelpViewer зависнет. Однако выбранная документация будет скачана и установлена. **Чтобы устранить эту проблему**, снимите задачу HelpViewer в диспетчере задач, а затем перезапустите средство, выполнив шаг 3 выше. При первом зависании HelpViewer выполните и [эти действия](https://msdn.microsoft.com/library/mt654096.aspx). Это нужно сделать только один раз, но, вероятно, вам потребуется закрывать HelpViewer в диспетчере задач при каждом обновлении содержимого.  
6. Перезапустите HelpViewer снова, выбрав в меню "Справка" пункт "Добавление и удаление содержимого". Теперь ваша автономная документация готова к использованию!



   ![Автономная документация, готовая к использованию](../sql-server/media/offline-ready-to-use.png)

