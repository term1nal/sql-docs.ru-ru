---
title: "Объединение данных (надстройка MDS для Excel) | Документы Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a867dc15-5a0d-457c-8304-ac323bcf9377
caps.latest.revision: 6
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 87457a33b1fd66f42baab7ea59dbaa9c2f2123df
ms.contentlocale: ru-ru
ms.lasthandoff: 08/02/2017

---
# <a name="combine-data-mds-add-in-for-excel"></a>Объединение данных (надстройка MDS для Excel)
  В [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], объедините данные из двух листов, чтобы сравнить их перед публикацией. В этой процедуре данные из двух таблиц объединяются в одну. Затем можно выполнить сравнения и определить, какие данные (если имеются) следует опубликовать в репозитории MDS.  
  
## <a name="prerequisites"></a>Предварительные требования  
  
-   Необходимо иметь лист, содержащий данные, управляемые MDS. Дополнительные сведения см. в разделе [Экспорт данных в Excel из служб Master Data Services](../../master-data-services/microsoft-excel-add-in/export-data-to-excel-from-master-data-services.md).  
  
-   Необходимо иметь лист, содержащий данные, которые нужно объединить с данными, управляемыми MDS. Этот лист должен иметь строку заголовка.  
  
### <a name="to-combine-non-managed-data-into-an-mds-managed-sheet"></a>Объединение неуправляемых данных на листе, управляемом MDS  
  
1.  На листе, содержащем данные, управляемые MDS, в группе **Публикация и проверка** нажмите кнопку **Объединить данные**.  
  
2.  В диалоговом окне **Объединение данных** рядом с текстовым полем **Диапазон для объединения с данными MDS** щелкните значок. Диалоговое окно свернется.  
  
3.  Щелкните лист, содержащий данные, которые нужно объединить.  
  
4.  Выделите все ячейки на листе, которые нужно объединить, включая строку заголовка.  
  
5.  В диалоговом окне **Объединение данных** щелкните значок. Диалоговое окно раскроется.  
  
6.  Для столбца, указанного для сущности MDS, выберите столбец в поле **Соответствующий столбец**. Соответствующие столбцы нужны не для всех столбцов MDS.  
  
7.  Нажмите кнопку **Объединить**. Появится столбец **SOURCE** , указывающий, берутся ли данные из MDS или внешнего источника.  
  
## <a name="next-steps"></a>Следующие шаги  
  
-   Сходство между данными, управляемыми MDS и внешние данные, в разделе [схожие данные соответствия &#40; Надстройка MDS для Excel &#41; ](../../master-data-services/microsoft-excel-add-in/match-similar-data-mds-add-in-for-excel.md).  
  
## <a name="see-also"></a>См. также:  
 [Обзор экспорта данных в Excel (надстройка MDS для Excel)](../../master-data-services/microsoft-excel-add-in/overview-exporting-data-to-excel-mds-add-in-for-excel.md)   
 [Сопоставление качества данных в надстройке MDS для Excel](../../master-data-services/microsoft-excel-add-in/data-quality-matching-in-the-mds-add-in-for-excel.md)  
  
  