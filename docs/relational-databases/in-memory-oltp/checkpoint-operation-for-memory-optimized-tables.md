---
title: "Использование контрольной точки для таблиц, оптимизированных для памяти | Документация Майкрософт"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 47975bd5-373f-43cd-946a-da8e8088b610
caps.latest.revision: 10
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 04176fec3cc190cba1a89a11780d84561512431a
ms.contentlocale: ru-ru
ms.lasthandoff: 06/22/2017

---
# <a name="checkpoint-operation-for-memory-optimized-tables"></a>Работа контрольной точки для оптимизированных для памяти таблиц
  Контрольную точку нужно периодически обрабатывать для данных, оптимизированных для памяти, в файлах данных и разностных файлах, чтобы дополнять активную часть журнала транзакций. Контрольная точка позволяет восстанавливать таблицы, оптимизированные для памяти, до последней успешной контрольной точки, после чего применяется активная часть журнала транзакций для обновления таблиц, оптимизированных для памяти, и завершения восстановления. Процессы работы контрольной точки для таблиц на диске и оптимизированных для памяти таблиц отличаются. Ниже описываются различные сценарии и режим работы контрольной точки для таблиц на диске и таблиц, оптимизированных для памяти.  
  
## <a name="manual-checkpoint"></a>Контрольная точка, установленная вручную  
 При создании контрольной точки вручную закрывается контрольная точка для таблиц на диске и таблиц, оптимизированных для памяти. Активный файл данных закрывается, хотя он может быть заполнен только частично.  
  
## <a name="automatic-checkpoint"></a>Автоматически создаваемые контрольные точки  
 Автоматически создаваемая контрольная точка реализуется по разному для таблиц на диске и таблиц, оптимизированных для памяти, из-за различных способов сохранения данных.  
  
 Для таблиц на диске устанавливается автоматическая контрольная точка на основе параметра конфигурации, определяющего интервал восстановления (дополнительные сведения см. в разделе [Изменение целевого времени восстановления базы данных (SQL Server)](../../relational-databases/logs/change-the-target-recovery-time-of-a-database-sql-server.md)).  
  
 Для таблиц, оптимизированных для памяти, автоматическая контрольная точка устанавливается, если размер журнала транзакций превышает 1,5 ГБ с последней контрольной точки. Этот размер включает в себя записи журнала транзакций как для дисковых, так и для оптимизированных для памяти таблиц.  
  
## <a name="see-also"></a>См. также:  
 [Создание и управление хранилищем для оптимизированных для памяти объектов](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)  
  
  