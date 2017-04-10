---
title: "Поиск документов с помощью списков результатов | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "поиск [среда SQL Server Management Studio], списки результатов"
  - "поиск по спискам результатов [среда SQL Server Management Studio]"
  - "поиск [среда SQL Server Management Studio], несколько файлов"
  - "редактор запросов [среда SQL Server Management Studio], поиск нескольких файлов"
ms.assetid: 275e1b6c-fbd0-4408-af77-35903f90657c
caps.latest.revision: 22
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 22
---
# Поиск документов с помощью списков результатов
  С помощью диалогового окна **Найти и заменить** можно выполнять поиск и замену текста во всех файлах проекта или решения, или в папке файловой системы, даже если они не открыты в среде [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Результаты поиска, выполненного в диалоговом окне **Найти и заменить** , появляются в окнах «Результаты поиска 1» и «Результаты поиска 2», что позволяет просмотреть точный текст строки, содержащей совпадение.  
  
### Выполнение поиска в группе файлов  
  
1.  В меню **Правка** укажите **Найти и заменить** и далее **Найти в файлах**.  
  
2.  В текстовом поле **Найти** введите текст, который необходимо найти.  
  
3.  В списке **Искать в** выберите один из пунктов — **Все открытые документы**, **Текущий проект**, **Все решение**— или введите путь каталога.  
  
4.  В списке **Типы файлов** выберите один из указанных наборов расширений файлов или введите расширения, соответствующие типам файлов, в которых будет выполняться поиск, разделив их точками с запятой. Используйте \*.\* для поиска по всем файлам каталога, выбранного в раскрывающемся списке **Искать в**.  
  
5.  Установите остальные параметры поиска, чтобы повысить его точность.  
  
6.  Чтобы начать поиск, нажмите кнопку **Найти** .  
  
 Совпадения при поиске отображаются по умолчанию в окне «Результаты поиска 1». Совпадения можно просмотреть двойным щелчком на каждой записи в окне «Результаты поиска 1». Чтобы просмотреть результаты поиска в новом окне, выберите **Показывать в результатах 2**.  
  
#### Выполнение замены в нескольких файлах или папках  
  
1.  В меню **Правка** укажите **Найти и заменить** и выберите пункт **Заменить в файлах**.  
  
2.  В текстовом поле **Найти** введите текст, который необходимо найти.  
  
3.  В поле **Заменить на** введите текст, на который следует заменить найденный текст.  
  
4.  В списке **Искать в** выберите один из пунктов — **Все открытые документы**, **Текущий проект**, **Все решение**— или введите путь каталога.  
  
5.  Нажмите кнопку **Заменить** , чтобы заменить текущее совпадение на текст, указанный в поле **Заменить на** . Отдельные совпадения можно пропустить, нажав кнопку **Найти следующее** . Чтобы пропустить целый файл, нажмите кнопку **Пропустить файл**.  
  
     \- или -  
  
     Нажмите кнопку **Заменить все** , чтобы заменить все совпадения на текст, указанный в поле **Заменить на** . Чтобы позже можно было отменить некоторые из замен, выберите **Оставить измененные файлы открытыми после замены** .  
  
    > [!NOTE]  
    > Команда **Заменить все** заменяет все совпадения при поиске, включая совпадения в файлах, пропущенных с помощью кнопок **Пропустить файл** или **Найти далее**. С помощью кнопки **Отменить** можно отменить замены только для тех файлов, которые остались открытыми после операции замены.  
  
 Сведения о заменах появляются по умолчанию в окне «Результаты поиска 1». Замены можно просмотреть двойным щелчком на каждой записи в окне «Результаты поиска 1».  
  
## См. также:  
 [Поиск и замена](../../relational-databases/scripting/search-and-replace.md)   
 [осуществлять поиск в документах в интерактивном режиме](../../relational-databases/scripting/search-documents-interactively.md)   
 [Поиск текста с символами-шаблонами](../../relational-databases/scripting/search-text-with-wildcards.md)   
 [Поиск текста с помощью регулярных выражений](../../relational-databases/scripting/search-text-with-regular-expressions.md)  
  
  