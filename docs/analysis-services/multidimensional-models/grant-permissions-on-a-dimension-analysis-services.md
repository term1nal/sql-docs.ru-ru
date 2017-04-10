---
title: "Предоставление разрешений измерению (службы Analysis Services | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.asvs.roledesignerdialog.dimensions.f1"
helpviewer_keywords: 
  - "измерения [службы Analysis Services], безопасность"
  - "разрешения на чтение и запись"
  - "права доступа пользователя [службы Analysis Services], измерения"
  - "разрешения [службы Analysis Services], измерения"
ms.assetid: be5b2746-0336-4b12-827e-131462bdf605
caps.latest.revision: 39
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 39
---
# Предоставление разрешений измерению (службы Analysis Services
  Настройка безопасности измерения используется для установки разрешений на объект измерения, а не на его данные. Обычно, при предоставлении или ограничении доступа к операциям обработки является основной целью при установке разрешений на измерение.  
  
 Однако, возможно, вашей целью является не управление операциями обработки, а доступ данных к измерению, или к атрибутам и иерархиям, которые оно содержит. Например, компания с региональным отделом продаж возможно желает подготовить информацию по превышению объемов продаж тем, кто находится за пределами отдела. Для того, чтобы разрешить или ограничить доступ к фрагментам данных измерения для различных клиентов, вы можете установить разрешения на атрибуты измерения и элементы измерения. Обратите внимание на то, то вы не можете запретить доступ к самому индивидуальному объекту измерения, только к его данным. Если ваша ближайшая цель — предоставление или ограничение доступа к элементам в измерении, включая права доступа к индивидуальным иерархиям атрибута, обратитесь к разделу [Предоставление настраиваемого доступа к данным измерений (Analysis Services)](../../analysis-services/multidimensional-models/grant-custom-access-to-dimension-data-analysis-services.md) за дополнительной информацией.  
  
 Оставшаяся информация данной темы касается разрешений, которые вы можете установить на самом объекте измерения, включая:  
  
-   Разрешения на Чтение или Чтение/Запись (вы можете выбирать только среди Чтение или Чтение/Запись; "никакой" не является параметром). Как отмечается, если вашей целью является ограничение доступа к данным измерения, обратитесь к разделу [Предоставление настраиваемого доступа к данным измерений (Analysis Services)](../../analysis-services/multidimensional-models/grant-custom-access-to-dimension-data-analysis-services.md) за дополнительной информацией.  
  
-   Разрешения на обработку (выполняйте, когда сценариям необходима стратегия обработки, которая предусматривает пользовательские разрешения на индивидуальных объектах)  
  
-   Разрешения на чтение описания (обычно вы будете выполнять это действие для поддержки интерактивной обработки в средстве, или для обеспечения видимости в модели.   Чтение описания позволяет вам видеть структуру измерения, без разрешения на его данные или способности изменять его описание).    
  
 При определении ролей для измерения, доступные разрешения различаются в зависимости от того, является ли объект отдельным измерением базы данных -внутренним для базы данных, но наружным для куба- или измерением куба.  
  
> [!NOTE]  
>  По умолчанию, разрешения на измерении базы данных достаются измерению куба. Например, если вы активируете **Чтение/Запись** на измерении базы данных Клиента, измерение куба Клиента получит **Чтение/Запись** в контексте текущей роли. Мы можете очистить полученные разрешения, если вы хотите переопределить настройки разрешений.  
  
## Установка разрешений на измерение базы данных  
 Измерения базы данных являются отдельными объектами в рамках базы данных, которые позволяют повторное использование измерений в рамках одной и той же модели. Рассмотрим измерение базы данных ДАТА, которое много раз используется в модели в качестве измерений куба Дата Заказа, Дата Отгрузки и Дата Выполнения. Так как измерения кубов и базы данных являются одноранговыми объектами в базе данных, вы можете установить разрешения на обработку независимо на каждый объект.  
  
1.  В среде [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] соединитесь с экземпляром служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], разверните узел **Роли** для соответствующей базы данных в обозревателе объектов, а затем щелкните роль базы данных (или создайте новую).  
  
2.  На вкладке **Измерения** настройка измерения должна быть установлена на **Все измерения базы данных**.  
  
     По умолчанию разрешения установлены на **Чтение**.  
  
     Хотя разрешение **Чтение/Запись** доступно, мы не рекомендуем его применять. Разрешение **Чтение и запись** используется для сценариев обратной записи измерений, которые считаются устаревшими. См. раздел [Нерекомендуемые функции служб Analysis Services в SQL Server 2016](../../analysis-services/deprecated-analysis-services-features-in-sql-server-2016.md).  
  
     При необходимости вы можете установить разрешения **Чтение Описания** и **Обработка** на индивидуальные объекты измерения, при условии, что эти разрешения еще не установлены на уровне базы данных. Дополнительные сведения см. в разделах [Предоставление разрешений на обработку (службы Analysis Services)](../../analysis-services/multidimensional-models/grant-process-permissions-analysis-services.md) и [Предоставление разрешений на чтение описания метаданным объекта (службы Analysis Services)](../../analysis-services/multidimensional-models/grant-read-definition-permissions-on-object-metadata-analysis-services.md).  
  
## Установка разрешений на измерение базы куба  
 Разрешения куба являются разрешениями базы данных, которые были добавлены кубу. По этой причине структурно они зависят от связанных групп мер. Хотя вы можете обрабатывать эти объекты в автоматическом режиме, в рамках авторизации, имеет смысл рассматривать куб и измерения куба в качестве единой сущности.  
  
1.  В среде [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] соединитесь с экземпляром служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], разверните узел **Роли** для соответствующей базы данных в обозревателе объектов, а затем щелкните роль базы данных (или создайте новую).  
  
2.  На вкладке **Измерения** измените настройку измерения на **измерения куба** \<имя_куба>.  
  
     По умолчанию разрешения наследуются от соответствующего измерения базы данных. Снимите флажок **Наследование** для изменения разрешений с **Чтение** на **Чтение/Запись**. Перед использованием разрешения **Чтение/Запись** убедитесь, что вы прочли примечание в предыдущем разделе.  
  
> [!IMPORTANT]  
>  При выполнении настройки разрешений роли базы данных с помощью объектов AMO любая ссылка на измерение куба в атрибуте DimensionPermission куба отменяет наследование разрешений из атрибута DimensionPermission базы данных. Дополнительные сведения об AMO см. в разделе [Разработка объектов управления аналитикой (объекты AMO)](../../analysis-services/multidimensional-models/analysis-management-objects/developing-with-analysis-management-objects-amo.md).  
  
## См. также  
 [Роли и разрешения (службы Analysis Services)](../../analysis-services/multidimensional-models/roles-and-permissions-analysis-services.md)   
 [Предоставление разрешений кубу или модели (службы Analysis Services)](../../analysis-services/multidimensional-models/grant-cube-or-model-permissions-analysis-services.md)   
 [Предоставление разрешений структурам интеллектуального анализа данных и моделям интеллектуального анализа данных (службы Analysis Services)](../../analysis-services/multidimensional-models/grant-permissions-on-data-mining-structures-and-models-analysis-services.md)   
 [Предоставление настраиваемого доступа к данным измерений (службы Analysis Services)](../../analysis-services/multidimensional-models/grant-custom-access-to-dimension-data-analysis-services.md)   
 [Предоставление настраиваемого доступа к данным ячейки (службы Analysis Services)](../../analysis-services/multidimensional-models/grant-custom-access-to-cell-data-analysis-services.md)  
  
  