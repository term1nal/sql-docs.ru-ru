---
title: "Настройка контрольных точек для повторного запуска пакета, завершившегося с ошибкой | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "контрольные точки [службы Integration Services]"
  - "перезапуск пакетов"
  - "запуск пакетов"
ms.assetid: 9afffa5a-d803-4653-8afc-386453fc163f
caps.latest.revision: 25
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 25
---
# Настройка контрольных точек для повторного запуска пакета, завершившегося с ошибкой
  Устанавливая свойства, влияющие на контрольные точки, можно настроить пакеты служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] таким образом, чтобы они перезапускались с точки сбоя вместо выполнения всего пакета с начала.  
  
### Настройка пакета для перезапуска  
  
1.  В среде [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]откройте проект служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , содержащий пакет, который нужно настроить.  
  
2.  Чтобы открыть пакет, дважды щелкните его в **обозревателе решений**.  
  
3.  Перейдите на вкладку **Поток управления** .  
  
4.  Щелкните правой кнопкой мыши в области конструктора потока управления и выберите **Свойства**.  
  
5.  Присвойте свойству SaveCheckpoints значение **True**.  
  
6.  Введите имя файла контрольных точек в поле свойства CheckpointFileName.  
  
7.  Установите значение свойства CheckpointUsage в одно из двух значений:  
  
    -   Установите **Always** , чтобы всегда перезапускать пакет с контрольной точки.  
  
        > [!IMPORTANT]  
        >  Если файл контрольных точек недоступен, то возникнет ошибка.  
  
    -   Выберете свойство **IfExists** , чтобы перезапускать пакет, только если доступен файл контрольных точек.  
  
8.  Настройте задачи и контейнеры, из которых пакет может быть перезапущен.  
  
    -   Правой кнопкой мыши щелкните задание или контейнер и выберите пункт **Свойства**.  
  
    -   Установите свойство FailPackageOnFailure в значение **True** для каждой выбранной задачи и каждого выбранного контейнера.  
  
## См. также  
 [Перезапуск пакетов с помощью контрольных точек](../../integration-services/packages/restart-packages-by-using-checkpoints.md)  
  
  