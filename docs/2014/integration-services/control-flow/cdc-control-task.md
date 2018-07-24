---
title: Задача управления CDC | Документы Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.cdccontroltask.f1
ms.assetid: 6404dc7f-550c-47cc-b901-c072742f430a
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 90d9aa5fbc864b9e5da68fbb80c9b97918bd0d80
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2018
ms.locfileid: "37199644"
---
# <a name="cdc-control-task"></a>Задача управления CDC
  Задача «Управление CDC» используется для управления жизненным циклом пакетов системы отслеживания изменений данных (CDC). Эта задача обеспечивает синхронизацию пакета CDC с пакетом начальной загрузки и управление диапазонами регистрационных номеров транзакций в журнале (номеров LSN), которые обрабатываются в прогоне пакета CDC. Дополнительно задача «Управление CDC» связана со сценариями обработки ошибок и с восстановлением.  
  
 Задача «Управление CDC» поддерживает информацию состояния пакета CDC в переменной пакета служб SSIS и может также сохранить ее в таблице базы данных, что позволяет поддерживать состояние от одной активации пакета к другой, а также между несколькими пакетами, которые вместе выполняют общий процесс CDC (например, одна задача может отвечать за начальную загрузку, а другая — за обновления тонкого канала).  
  
 Задача «Управление CDC» поддерживает две группы операций. Одна группа обеспечивает синхронизацию начальной нагрузки и обработки изменений, а другая группа управляет диапазоном номеров LSN, связанных с обработкой изменений, для прогона пакета CDC, а также следит за тем, какая часть обработки была выполнена успешно.  
  
 Для синхронизации начальной нагрузки и обработки изменений применяются следующие операции.  
  
|Операция|Описание|  
|---------------|-----------------|  
|ResetCdcState|Эта операция используется для сброса хранимого состояния CDC, связанного с текущим контекстом CDC. После выполнения этой операции текущий максимальный номер LSN из таблицы LSN-timestamp `sys.fn_cdc_get_max_lsn` становится началом следующего диапазона обработки. Эта операция требует создания соединения с базой данных-источником.|  
|MarkInitialLoadStart|Операция используется в начале пакета начальной загрузки для записи текущего номера LSN в базу данных-источник перед тем как пакет начальной загрузки начинает читать исходные таблицы. Для этого требуется соединение с базой данных-источником для вызова `sys.fn_cdc_get_max_lsn`.<br /><br /> Если будет выбрано MarkInitialLoadStart при работе с CDC [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] (т. е. отличной от Oracle), то пользователем, указанным в диспетчере соединений, должен быть db_owner или sysadmin.|  
|MarkInitialLoadEnd|Эта операция используется в конце пакета начальной загрузки для записи текущего номера LSN в базу данных-источник после того, как пакет начальной нагрузки завершит чтение исходных таблиц. Номер LSN определяется путем записи текущего времени при осуществлении данной операции и последующего запроса таблицы сопоставления `cdc.lsn_time_`в базе данных CDC для поиска любого изменения, которое произошло в последующее время.<br /><br /> Если будет выбрано MarkInitialLoadEnd при работе с CDC [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] (т. е. отличной от Oracle), то пользователем, указанным в диспетчере соединений, должен быть db_owner или sysadmin.|  
|MarkCdcStart|Эта операция используется, если начальная загрузка выполняется из базы данных моментальных снимков. В таком случае обработка изменений должна начаться с номера, который непосредственно следует за номером LSN моментального снимка. Можно указать имя используемой базы данных моментальных снимков, и задача «Управление CDC» запросит в [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] номер LSN моментального снимка. Предусмотрена также возможность непосредственно указать номер LSN моментального снимка.<br /><br /> Если будет выбрано MarkCdcStart при работе с CDC [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] (т. е. отличной от Oracle), то пользователем, указанным в диспетчере соединений, должен быть db_owner или sysadmin.|  
  
 Для управления диапазоном обработки предназначены следующие операции:  
  
|Операция|Описание|  
|---------------|-----------------|  
|GetProcessingRange|Эта операция используется перед вызовом потока данных, в котором применяется поток исходных данных CDC. Операция устанавливает диапазон номеров LSN, считываемый потоком исходных данных CDC при вызове. Этот диапазон хранится в переменной пакета служб SSIS, которая используется источником CDC во время обработки потока данных.<br /><br /> Дополнительные сведения о сохраненных состояниях см. в разделе [Определение переменной состояния](../data-flow/define-a-state-variable.md).|  
|MarkProcessedRange|Эта операция выполняется после каждого прогона CDC (после успешного завершения потока данных CDC) для записи последнего номера LSN, который был полностью обработан в прогоне CDC. При следующем вызове GetProcessingRange на выполнение эта позиция становится началом диапазона обработки.|  
  
## <a name="handling-cdc-state-persistency"></a>Обработка сохраняемого состояния CDC  
 Задача «Управление CDC» поддерживает сохраняемое состояние от одной активации к другой. Информация, сохраняемая в состоянии CDC, используется в целях определения и сопровождения диапазона обработки для пакета CDC, а также в целях обнаружения условий возникновения ошибок. Информация о сохраняемом состоянии представлена в виде строки. Дополнительные сведения см. в статье [Определение переменной состояния](../data-flow/define-a-state-variable.md).  
  
 Задача «Управление CDC» поддерживает два типа сохранения состояния  
  
-   Сохранение состояния вручную. В этом случае задача управления CDC управляет состоянием, сохраненным в переменной пакета, но разработчик пакета должен считывать переменную из постоянного хранилища перед вызовом запроса управления CDC, а затем снова записывать ее назад в постоянное хранилище после последнего вызова запроса управления CDC и завершения прогона CDC.  
  
-   Автоматическое сохранение состояния. Информация о состоянии CDC хранится в таблице в базе данных. Информация о состоянии хранится под именем, предоставленным в свойстве **StateName** в таблице, указанной в свойстве **Таблица для хранения состояния** , которую можно найти в диспетчере соединений, выбранном для сохранения состояния. По умолчанию применяется диспетчер соединений с источником, но чаще всего используется диспетчер соединений с назначением. Задача «Управление CDC» обновляет значение состояния в таблице состояний, и это значение фиксируется в составе включающей транзакции.  
  
## <a name="error-handling"></a>Обработка ошибок  
 Задача «Управление CDC» может сообщать об ошибках в следующих случаях.  
  
-   В задаче не удается считать хранимое состояние CDC, или обновление сохраняемого состояния оканчивается неудачей.  
  
-   В задаче не удается считать информацию о текущем номере LSN из базы данных-источника.  
  
-   Операция чтения состояния CDC не согласована.  
  
 Во всех этих случаях задача «Управление CDC» сообщает об ошибке, которая может быть обработана стандартным способом, применяемым в службе SSIS для обработки ошибок потока управления.  
  
 Задача «Управление CDC» может также выдать предупреждение, если операция «Получить диапазон обработки» вызывается непосредственно после другой операции «Получить диапазон обработки» без вызова операции «Отметить обработанный диапазон». Такая ситуация указывает на то, что предыдущий прогон окончился неудачей или что, возможно, выполняется еще один пакет CDC, в котором используется то же имя состояния CDC.  
  
## <a name="configuring-the-cdc-control-task"></a>Настройка задачи «Управление CDC»  
 Свойства могут быть заданы с помощью конструктора SSIS или программным путем.  
  
## <a name="in-this-section"></a>в этом разделе  
  
-   [Редактор задачи «Управление CDC»](../cdc-control-task-editor.md)  
  
-   [Пользовательские свойства задачи «Управление CDC»](cdc-control-task-custom-properties.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 [Определение переменной состояния](../data-flow/define-a-state-variable.md)  
  
## <a name="related-content"></a>См. также  
  
-   Техническую статью [Установка системы отслеживания измененных данных Microsoft SQL Server 2012 для Oracle компании Attunity](http://go.microsoft.com/fwlink/?LinkId=252958)см. на сайте social.technet.microsoft.com.  
  
-   Техническую статью [Устранение неполадок в конфигурации системы отслеживания измененных данных Майкрософт для Oracle компании Attunity](http://go.microsoft.com/fwlink/?LinkId=252960)см. на сайте social.technet.microsoft.com.  
  
-   Техническую статью [Устранение неполадок в конфигурации системы отслеживания измененных данных Майкрософт для Oracle компании Attunity](http://go.microsoft.com/fwlink/?LinkId=252961)см. на сайте social.technet.microsoft.com.  
  
  