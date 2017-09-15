---
title: "Добавление развернуть или свернуть действия к элементу (построитель отчетов и службы SSRS) | Документы Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 49f07ad6-242b-4861-8fc1-91ca78c36d6c
caps.latest.revision: 12
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: dcd1af4aee2c0267f1443d87d80be1e3cc2ad8b3
ms.contentlocale: ru-ru
ms.lasthandoff: 08/09/2017

---
# <a name="add-an-expand-or-collapse-action-to-an-item-report-builder-and-ssrs"></a>Добавление действия "Развернуть" или "Свернуть" к элементу (построитель отчетов и службы SSRS)
  Вы можете позволить пользователю в интерактивном режиме раскрывать или свертывать элементы отчета, а также разворачивать и сворачивать строки и столбцы, связанные с группой для таблицы или матрицы. Чтобы разрешить пользователям разворачивать и сворачивать элемент, необходимо задать свойства видимости для этого элемента. Настройка видимости работает в средстве просмотра отчетов HTML и иногда называется *углубленной детализацией* .  
  
 В представлении конструктора отчетов указывается имя текстового поля, в котором необходимо отобразить значки переключения развертывания и сворачивания. В отчете, готовом для просмотра, помимо самого содержимого, в текстовом поле отображается знак «плюс» (+) или «минус» (-). Когда пользователь щелкает переключатель, отображение отчета обновляется, при этом элемент отчета показывается или скрывается в зависимости от текущих параметров видимости для элементов в отчете.  
  
 Обычно действия развертывания и свертывания используются для отображения только сводных данных, при этом пользователь, нажав знак «плюс», может открыть и подробные данные. Например, изначально можно скрыть таблицу, отображающую значения диаграммы, или скрыть дочерние группы таблицы с группами вложенных строк или столбцов, как в отчете с углубленной детализацией.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-expand-and-collapse-action-to-a-group"></a>Добавление действия развертывания и свертывания к группе  
  
1.  В конструкторе отчетов щелкните таблицу или матрицу, чтобы выбрать ее. На панели группирования будут отображены группы столбцов и строк.  
  
     ![Панель группировки](../../reporting-services/report-design/media/groupingpane.png "область группирования")  
  
     Если панель группирования не появляется, выберите пункт меню **Вид** и нажмите **Группирование**.  
  
2.  Щелкните правой кнопкой в любом месте строки заголовка панели "Группирование" и выберите **Дополнительно**. Режим панели «Группирование» включается для показа базовой структуры отображения строк и столбцов в области конструктора.  
  
     ![Панель группировки с меню в расширенном режиме](../../reporting-services/report-design/media/groupingpane-advancedmode.png "расширенный режим меню в панели группирования")  
  
3.  В соответствующей панели группы щелкните имя группы строк или группы столбцов, для которой необходимо скрыть связанные строки или столбцы. Выбирается группа, и на панели «Свойства» отображаются свойства **Элемент табликса** .  
  
    > [!NOTE]  
    >  Если вы не видите панель "Свойства", нажмите ленту **Вид** и затем **Свойства**.  
  
4.  В пункте **Скрытый**выберите один из следующих параметров для установки видимости данного элемента отчета при первом запуске отчета.  
  
    -   Для отображения элемента отчета выберите **False** .  
  
    -   Для скрытия элемента отчета выберите **True** .  
  
    -   Выберите  **\<выражение >** Открытие **выражение** диалоговое окно «», чтобы создать выражение, которое вычисляется во время выполнения для определения видимости.  
  
5.  В раскрывающемся списке **ToggleItem**выберите имя текстового поля, к которому добавляется изображение переключателя.  
  
     На следующем рисунке настройка группы строк "Цвет" позволяет пользователям разворачивать и сворачивать связанные строки.  
  
     ![Настройка группы строк должны быть увеличены](../../reporting-services/report-design/media/expandcollapse-confighiddentoggleitemwithnumbers.png "Настройка развертываемой группы строки")  
  
    > [!NOTE]  
    >  Текстовое поле с изображением переключателя не может быть группой строк или столбцов, для которой необходимо скрыть связанные строки или столбцы. Текстовое поле должно находиться либо в той же группе, что и скрываемый элемент, либо в родительской группе. Например, чтобы включить видимость строк, связанных с дочерней группой, выберите текстовое поле в строке, связанной с родительской группой.  
  
6.  Для проверки переключателя запустите отчет и щелкните текстовое поле с изображением переключателя. Экран отчета обновляется для отображения групп строк и столбцов с включенной видимостью.  
  
     ![Запуск отчета с развертываемой группой строк](../../reporting-services/report-design/media/expandcollapse-runreport-rowgroup.png "запуск отчета с развертываемой группой строк")  
  
### <a name="to-add-expand-and-collapse-action-to-a-report-item"></a>Добавление действия развертывания и свертывания к элементу отчета  
  
1.  В представлении конструктора отчетов, щелкните правой кнопкой мыши элемент отчета, чтобы показать или скрыть и нажмите кнопку  *\<элемент отчета >* **свойства**.  *\<Элемент отчета >* **свойства** откроется диалоговое окно для элемента отчета.  
  
2.  Щелкните **Видимость**.  
  
3.  В пункте **При первоначальном запуске отчета**выберите один из следующих параметров для установки видимости данного элемента отчета при первом запуске отчета:  
  
    -   Для отображения элемента отчета выберите **Показать** .  
  
    -   Для скрытия элемента отчета выберите **Скрыть** .  
  
    -   Для использования выражения, вычисляемого во время выполнения для определения видимости, выберите **Отображать или скрывать в зависимости от выражения** . Щелкните**fx**, чтобы открыть диалоговое окно **Выражение** .  
  
        > [!NOTE]  
        >  При задании выражения для видимости настраивается свойство Hidden элемента отчета. Выражение вычисляет значение **Boolean** (при значении **True** элемент скрыт, а при значении **False** отображается).  
  
4.  Из раскрывающегося списка **Отображение может переключаться этим элементом отчета**выберите имя текстового поля в отчете, в котором будет отображаться изображение переключателя, например Textbox1, или введите его вручную.  
  
     На следующем рисунке таблица настроена таким образом, чтобы пользователи могли разворачивать и сворачивать ее. Отображение таблицы переключается с помощью текстового поля таблицы продуктов.  
  
     ![Настройте таблицу отчета должны быть увеличены](../../reporting-services/report-design/media/expandcollapse-reporttable.png "Настройте таблицу отчета должны быть увеличены")  
  
    > [!NOTE]  
    >  Выбранное текстовое поле должно находиться в текущей области или в области, которая находится в текущей области, для этого элемента отчета (вплоть до самого текста отчета). Например, чтобы переключить видимость диаграммы, выберите текстовое поле в той же области, где находится эта диаграмма, например в тексте отчета или в прямоугольнике. Текстовое поле должно находиться в той же иерархии контейнеров или выше.  
  
5.  Для проверки переключателя запустите отчет и щелкните текстовое поле с изображением переключателя. Экран отчета обновляется для отображения элементов отчета со включенной видимостью.  
  
     ![Запуск отчета с развертываемой таблицей](../../reporting-services/report-design/media/expandcollapse-runreport-reporttable.png "запуск отчета с развертываемой таблицей")  
  
## <a name="see-also"></a>См. также:  
 [Действие детализации (построитель отчетов и службы SSRS)](../../reporting-services/report-design/drilldown-action-report-builder-and-ssrs.md)   
 [Скрыть элемент &#40; Построитель отчетов и службы SSRS &#41;](../../reporting-services/report-builder/hide-an-item-report-builder-and-ssrs.md)  
  
  