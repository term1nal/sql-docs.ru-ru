---
title: Резервное копирование сервера планирования емкости - Parallel Data Warehouse | Документы Microsoft
description: Этот лист планирования емкости поможет вам определить требования для резервного копирования сервера для выполнения параллельного хранилища данных резервной копии базы данных операций и восстановления. Используется для создания плана для приобретения новых или подготовки существующих резервных серверов.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 500bebab375a0d0b94032a1855af3844bc2e6fa7
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/19/2018
ms.locfileid: "31539144"
---
# <a name="backup-server-capacity-planning-worksheet---parallel-data-warehouse"></a>Резервное копирование сервера емкости лист планирования - Parallel Data Warehouse
Этот лист планирования емкости поможет вам определить требования для резервного копирования сервера для выполнения резервного копирования базы данных SQL Server PDW операций и восстановления. Используется для создания плана для приобретения новых или подготовки существующих резервных серверов.  
  
Этот лист — в дополнение к инструкциям [приобретать и настраивать резервное копирование сервера](acquire-and-configure-backup-server.md).  
  
## <a name="capacity-planning-worksheet-for-backup-servers"></a>Лист производительности планирования для резервного копирования серверов  

### <a name="notes"></a>Примечания  
  
1.  Этот лист относится к серверам, будет выполнять операции резервного копирования и восстановления для баз данных PDW.  
  
2.  Единственный способ резервного копирования и восстановления баз данных PDW — использование команд базы данных АРХИВАЦИИ и восстановления базы данных SQL. Однако после резервного копирования данных на сервере резервного копирования, он существует как набор файлов Windows. Вы можете архивировать файлы резервной копии с сервера в другом хранилище с помощью традиционных Windows на основе файла методы резервного копирования.  
  
### <a name="clipboard-iconmediaclipboard-iconpng-clipboard-icon-capacity-planning-worksheet"></a>![Значок буфера обмена](media/clipboard-icon.png "значок буфера обмена") листа планирования емкости 
  
Печать листа и наполнить требованиями.  
  
|Компонент|Требование|Заполните этот столбец с требованиями|Рекомендации|  
|-------------|---------------|--------------------------------------------------|-------------------|  
|Память|Максимально число байтов, которые планируется хранить на сервере резервного копирования на любой период времени.|![Значок карандаша](media/pencil-icon.png "значок карандаша")|Чтобы определить требования к хранилищу, выясните, какой объем данных будет храниться на сервере резервного копирования на любой период времени.<br /><br />Данные архивации хранятся на сервере резервного копирования в сжатом формате. Степень сжатия данных, зависят от характеристик данных.<br /><br />Например: в качестве приблизительной оценки, мы советуем оценка коэффициент сжатия 7:1 относительно размера несжатых данных. Предполагается, что по крайней мере 80% данных хранятся в кластеризованных индексах columnstore. Например при наличии 700 ГБ несжатых данных в базе данных, и он хранится в кластеризованных индексах columnstore, затем вы может оценить резервной копии базы данных может понадобиться примерно 100 ГБ данных.<br /><br />Если вы планируете создать несколько копий резервных копий базы данных на сервере резервного копирования, необходимо учитывать для них.<br /><br />Например: Если вы планируете создать резервную копию 10 баз данных, каждый из которых содержит 5 ТБ несжатых данных, базы данных имеют общий размер 50 ТБ. Если вы планируете создать резервную копию этих ежедневно 10 баз данных для 5 дней подряд, общий размер несжатого файла — 250 ТБ. Учитывая соотношение сжатия 7:1, вам потребуется 250 / 7 = 35.7 ТБ памяти на сервере резервного копирования. Рекомендуется, чтобы он осторожен и о получении 30% дополнительную емкость для учетной записи для дисперсии и увеличиваться.  В этом примере лучше 46.6 ТБ.|  
|Сеть|Тип сетевого подключения.|![Значок карандаша](media/pencil-icon.png "значок карандаша")|Определите наилучший тип сетевого подключения, способную удовлетворять требованиям скорость загрузки.<br /><br />Например: InfiniBand или 10Gbit Ethernet предоставит оптимальный загрузку ставки. Ethernet 1 Гбит ограничит скорости загрузки 360 ГБ в час или меньше.|  
|Ввод-вывод|Байт в час для операций записи.|![Значок карандаша](media/pencil-icon.png "значок карандаша")|Для записи резервных копий на диск емкостью 4 ТБ в час, скорости записи являются оптимальными.<br /><br />Например: для дисков, которое может записывать 50 МБ в секунду, требуется по крайней мере 24 дисках, а также более для зеркального отображения или контроля четности.<br /><br />Ресурсы ввода-вывода принимая в учетной записи всех операций ввода-вывода, происходящих на сервере загрузки. Если загрузка сервера имеет другой трафик ввода-вывода в дополнение к загрузке данных, как получение файлов данных с сервера ETL, увеличит требования ввода-вывода.|  
|ЦП|Число процессоров.|![Значок карандаша](media/pencil-icon.png "значок карандаша")|Получения и хранения файлов резервной копии не является приложением процессор.  Как минимум рекомендуется использовать двухпроцессорный сервер недавно производства.|  
|ОЗУ|Загружает ГБ памяти, который позволяет Windows для кэширования файлов во время.|![Значок карандаша](media/pencil-icon.png "значок карандаша")|Получения и хранения резервных копий файлов требует очень мало оперативной памяти на сервере загрузки.<br /><br />Чтобы определить требования к ОЗУ, см. установке Windows Server и требования приложения сторонних производителей. Рекомендуется не менее 32 ГБ, если у вас требования из других источников.|  
  
После определения требований к емкости вернуться к [приобретать и настраивать сервер загрузки](acquire-and-configure-loading-server.md) разделе для планирования покупки.  
  
## <a name="see-also"></a>См. также  
[Резервное копирование и загрузка оборудования](backup-and-loading-hardware.md)  
  
