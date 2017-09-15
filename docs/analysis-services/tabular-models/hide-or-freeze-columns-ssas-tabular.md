---
title: "Скрытие или закрепление столбцов (табличные службы SSAS) | Документы Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.asvs.bidtoolset.hideunhidecolumnsdb.f1
ms.assetid: 5407aee5-6a07-4559-a2ba-2ca00a242f02
caps.latest.revision: 10
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 875994a4c5b2f8a78d21c049236a4c95d8c38f76
ms.contentlocale: ru-ru
ms.lasthandoff: 09/01/2017

---
# <a name="hide-or-freeze-columns-ssas-tabular"></a>Скрытие или закрепление столбцов (табличные службы SSAS)
  Если в конструкторе моделей некоторые столбцы не нужно отображать в таблице, то их можно временно скрыть. Скрытый столбец освобождает пространство на экране, позволяя добавлять новые столбцы или работать только с необходимыми столбцами данных. Скрыть или отобразить столбцы можно через меню **Столбец** в конструкторе моделей или через меню заголовка столбца, которое вызывается нажатием правой кнопкой мыши. Чтобы область модели оставалась видимой при переходе в другую область при прокрутке, можно закрепить определенные столбцы в одной области.  
  
> [!IMPORTANT]  
>  Возможность скрытия столбцов предусмотрена не для защиты данных, а только для упрощения и уменьшения списка столбцов, видимых в конструкторе моделей или отчетах. Для защиты данных можно задать роли безопасности. Роли дают возможность сделать метаданные и данные видимыми только для тех объектов, которые определены в роли. Дополнительные сведения см. в разделе [Роли (табличные службы SSAS)](../../analysis-services/tabular-models/roles-ssas-tabular.md).  
  
 Можно выбрать скрытие столбца во время работы в конструкторе моделей или в отчетах. Если скрыть все столбцы, то вся таблица в конструкторе моделей будет выглядеть пустой.  
  
> [!NOTE]  
>  Если необходимо скрыть много столбцов, то вместо этого можно создать перспективу. Перспектива — это пользовательское представление данных, упрощающее работу с подмножествами взаимосвязанных данных. Дополнительные сведения см. в разделе [Создание перспектив и управление ими (табличные службы SSAS)](../../analysis-services/tabular-models/create-and-manage-perspectives-ssas-tabular.md).  
  
### <a name="to-hide-an-individual-column"></a>Скрытие отдельного столбца  
  
1.  В конструкторе моделей выберите таблицу со столбцом, который необходимо скрыть.  
  
2.  Щелкните столбец правой кнопкой мыши, выберите команду **Скрыть столбцы**, а затем выберите **Из конструктора и отчетов**, **Из отчетов**или **Из конструктора**.  
  
### <a name="to-hide-multiple-columns"></a>Скрытие нескольких столбцов  
  
1.  В конструкторе моделей выберите таблицу со столбцом, который необходимо скрыть.  
  
2.  В меню **Столбец** выберите пункт **Скрыть и показать**.  
  
3.  В диалоговом окне **Скрытие и отображение столбцов** найдите столбцы, которые нужно скрыть, и снимите для них флажки **В конструкторе** , **В отчетах**либо оба флажка.  
  
4.  Нажмите кнопку **ОК**.  
  
### <a name="to-freeze-columns"></a>Закрепление столбцов  
  
1.  В конструкторе моделей выберите таблицу со столбцом, который нужно закрепить.  
  
2.  Выберите один или несколько столбцов для закрепления.  
  
3.  В меню **Столбцы** выберите пункт **Закрепить**.  
  
    > [!NOTE]  
    >  При закреплении столбцов они перемещаются влево или в начало таблицы в конструкторе. При освобождении столбца он не возвращается в исходное местоположение.  
  
## <a name="see-also"></a>См. также  
 [Таблицы и столбцы (табличные службы SSAS)](../../analysis-services/tabular-models/tables-and-columns-ssas-tabular.md)   
 [Перспективы (табличные службы SSAS)](../../analysis-services/tabular-models/perspectives-ssas-tabular.md)   
 [Роли (табличные службы SSAS)](../../analysis-services/tabular-models/roles-ssas-tabular.md)  
  
  