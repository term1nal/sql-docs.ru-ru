---
title: "Сравнение хранилища таблиц на диске с хранилищем таблиц оптимизированным для памяти | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine-imoltp"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: eacf443c-001a-445f-ad1c-5f5a45eca6f4
caps.latest.revision: 5
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 5
---
# Сравнение хранилища таблиц на диске с хранилищем таблиц оптимизированным для памяти
  
  
|Категории|Дисковая таблица|Долговечная, оптимизированная для памяти таблица|  
|----------------|-----------------------|-------------------------------------|  
|DDL|Сведения о метаданных хранятся в системных таблицах в первичной файловой группе базы данных и доступны через представления каталога.|Сведения о метаданных хранятся в системных таблицах в первичной файловой группе базы данных и доступны через представления каталога.|  
|Структура|Строки хранятся в страницах размером 8 КБ. Страница содержит только строки из одной таблицы.|Строки хранятся в виде отдельных строк. Структура страницы не существует. Две последовательные строки в файле данных могут принадлежать к различным, оптимизированным для памяти таблицам.|  
|Индексы|Индексы хранятся в структуре страницы наподобие строк данных.|Сохраняется только определение индекса (не строки индекса). Индексы сохраняются в памяти и создаются повторно, когда оптимизированная для памяти таблица загружается в память при перезапуске базы данных. Так как строки индекса не сохраняются, то для изменений индекса журнал не ведется.|  
|Операция DML|Сначала нужно найти страницу и загрузить ее буферный пул.<br /><br /> Insert<br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] вставляет строки на страницу с учетом порядка страниц для кластеризованного индекса.<br /><br /> Delete<br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] определяет строки, которые нужно удалить, на странице и отмечает их как удаленные.<br /><br /> Update<br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] находит строки на странице. Обновление для неключевых столбцов выполняется на месте. Обновление ключевого столбца выполняется с помощью операции удаления и вставки.<br /><br /> После завершения операции DML измененные страницы записываются на диск при фиксации политики буферного пула, контрольной точки или транзакции для операций с минимальным уровнем ведения журнала. И операции чтения, и операции записи на страницах приводят к ненужным операциям ввода-вывода.|Поскольку данные оптимизированных для памяти таблиц находятся в памяти, операции DML осуществляются непосредственно в памяти. Существует фоновый поток, который считывает записи журнала для оптимизированных для памяти таблиц и сохраняет их в файлы данных и разностные файлы. При обновлении создается новая версия строки. Но обновление записывается в журнал как операция удаления с последующей вставкой.|  
|Фрагментация данных|Фрагменты обработки данных, из-за которых появляются частично заполненные страницы и логически последовательные страницы, которые располагаются на диске непоследовательно. Это уменьшает скорость доступа к данным и может потребовать дефрагментации данных.|Оптимизированные для памяти данные не хранятся в страницах, поэтому фрагментации данных нет. Но при обновлении и удалении строк файлы данных и разностные файлы требуется сжимать. Этим занимается потоковый поток MERGE в соответствии с политикой слияния.|  
  
## См. также:  
 [Создание и управление хранилищем для оптимизированных для памяти объектов](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)  
  
  