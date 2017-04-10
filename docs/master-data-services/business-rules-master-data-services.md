---
title: "Бизнес-правила (службы Master Data Services) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/18/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "бизнес-правила [Master Data Services], о бизнес-правилах"
  - "бизнес-правила [службы Master Data Services]"
ms.assetid: a9f9e41a-2461-4845-b947-58b3a205543f
caps.latest.revision: 16
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 16
---
# Бизнес-правила (службы Master Data Services)
  Бизнес-правило в [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] — это правило, позволяющее обеспечить качество и точность основных данных. Бизнес-правило можно использовать для автоматического обновления данных, отправки электронной почты или запуска бизнес-процесса или рабочего процесса.  
  
 Примеры бизнес-правил см. [Примеры правил Business & #40; Службы Master Data Services & #41;](../master-data-services/business-rule-examples-master-data-services.md).  
  
## Создание и публикация бизнес-правил  
 Бизнес-правила **If-Then-Else** инструкций, созданных в [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]. Если значение атрибута удовлетворяет указанному условию, выполняется определенное действие. В противном случае выполняется действие Else. Возможны такие действия, как задание значения по умолчанию или изменение значения. Эти действия могут сочетаться с отправкой уведомления по электронной почте.  
  
 Бизнес-правила могут основываться на определенных значениях атрибутов (например, предпринимать действие, если Цвет=Синий) или на изменении значения атрибута (например, предпринимать действие, если значение атрибута «Цвет» изменяется). Дополнительные сведения об отслеживании изменений общего характера см. в разделе [отслеживания изменений и #40; Службы Master Data Services & #41;](../master-data-services/change-tracking-master-data-services.md).  
  
 Для использования бизнес-правил сначала необходимо создать и опубликовать правила, а затем применить опубликованные правила к данным. Правила можно применять к подмножествам данных или ко всем данным в версии путем проверки версии. Версию нельзя зафиксировать, пока все атрибуты не пройдут проверку на соответствие бизнес-правилам.  
  
 Если пользователь пытается добавить значение атрибута, которое не проходит проверку на соответствие бизнес-правилам, это значение все равно можно сохранить. Просмотреть ошибки проверки и исправить их можно в [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)].  
  
 При создании пакета развертывания модели в случае необходимости включить бизнес-правила следует включить данные из версии пакета.  
  
 При создании бизнес-правило, которое использует **или** оператор, необходимо создать отдельное правило для каждого условного оператора, которое может обрабатываться независимо друг от друга. При необходимости правила можно исключать, что повышает гибкость и упрощает устранение неполадок.  
  
## Применение бизнес-правил  
 Вы можете установить приоритет, согласно которому следует выполнять правила. Для этого перемещайте бизнес-правила вверх и вниз. Однако перед тем как учесть приоритет, применяются бизнес-правила на основании типа действия, которое предпринимает правило. Порядок выглядит следующим образом.  
  
1.  **Значение по умолчанию**  
  
2.  **Изменение значения**  
  
3.  **Проверка**  
  
4.  **Внешнее действие**  
  
5.  **Пользовательский сценарий действия**  
  
 В рамках этих групп действия применяются в порядке, определенном их приоритетом, — от самого низкого до самого высокого. Например, четыре отдельных правила могут содержать **значение по умолчанию** действия.  **Значение по умолчанию** сначала выполняемое действие зависит от приоритета, определенного в веб-Интерфейсе.  
  
 Другие важные замечания о применении правил.  
  
-   Если бизнес-правило исключено или не опубликовано с состоянием **Active**, правило все еще доступна, но не включен, при применении бизнес-правила.  
  
-   Бизнес-правила применяются к значениям атрибутов для всех конечных элементов или всех консолидированных элементов, но не для тех и других сразу.  
  
-   Бизнес-правила могут применяться к любой версии модели, которая является **Откройте** или **заблокирована**.  
  
-   Изменения данных при применении бизнес-правил не регистрируются как транзакции.  
  
-   Бизнес-правила не может содержать более одного **Запуск рабочего процесса** действие.  
  
## Системные настройки  
 В программе [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] имеется два параметра, которые влияют на бизнес-правила. Эти параметры можно настроить в [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] или непосредственно в таблице системных настроек. Дополнительные сведения см. в разделе [системные параметры & #40; Службы Master Data Services & #41;](../master-data-services/system-settings-master-data-services.md).  
  
## Связанные задачи  
  
|Описание задачи|Раздел|  
|----------------------|-----------|  
|Создание и публикация бизнес-правила.|[Создание и публикация бизнес-правило & #40; Службы Master Data Services & #41;](../master-data-services/create-and-publish-a-business-rule-master-data-services.md)|  
|Добавление нескольких условий к бизнес-правилу.|[Добавление нескольких условий к бизнес-правило & #40; Службы Master Data Services & #41;](../master-data-services/add-multiple-conditions-to-a-business-rule-master-data-services.md)|  
|Создание бизнес-правила, которое требует заполнения атрибутов.|[Требуется атрибут значения & #40; Службы Master Data Services & #41;](../master-data-services/require-attribute-values-master-data-services.md)|  
|Создание бизнес-правила, которое запускает действие при изменении значений атрибутов.|[Запуск действия в зависимости от значения атрибута & #40; Службы Master Data Services & #41;](../master-data-services/initiate-actions-based-on-attribute-value-changes-master-data-services.md)|  
|Создание бизнес-правила для использования пользовательского сценария как условия|[Расширения бизнес-правил и #40; Службы Master Data Services & #41;](../master-data-services/business-rules-extension-master-data-services.md)|  
|Создание бизнес-правила для использования пользовательского сценария как действия|[Расширения бизнес-правил и #40; Службы Master Data Services & #41;](../master-data-services/business-rules-extension-master-data-services.md)|  
|Изменение имени существующего бизнес-правила.|[Изменение имени бизнес-правила и #40; Службы Master Data Services & #41;](../master-data-services/change-a-business-rule-name-master-data-services.md)|  
|Настройка [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] для отправки уведомлений при применении бизнес-правил.|[Настройка бизнес-правил для отправки уведомлений и #40; Службы Master Data Services & #41;](../master-data-services/configure-business-rules-to-send-notifications-master-data-services.md)|  
|Применение бизнес-правил к определенным элементам.|[Проверка отдельных элементов для бизнес-правил и #40; Службы Master Data Services & #41;](../master-data-services/validate-specific-members-against-business-rules-master-data-services.md)|  
|Исключите бизнес-правило, чтобы оно не использовалось.|[Исключить бизнес-правило & #40; Службы Master Data Services & #41;](../master-data-services/exclude-a-business-rule-master-data-services.md)|  
|Удаление существующего бизнес-правила.|[Удаление бизнес-правило & #40; Службы Master Data Services & #41;](../master-data-services/delete-a-business-rule-master-data-services.md)|  
  
## См. также  
  
-   [Обзор служб Master Data Services и #40; MDS & #41;](../master-data-services/master-data-services-overview-mds.md)  
  
-   [Версии & #40; Службы Master Data Services & #41;](../master-data-services/versions-master-data-services.md)  
  
-   [Проверка & #40; Службы Master Data Services & #41;](../master-data-services/validation-master-data-services.md)  
  
-   [Отслеживание изменений и #40; Службы Master Data Services & #41;](../master-data-services/change-tracking-master-data-services.md)  
  
  