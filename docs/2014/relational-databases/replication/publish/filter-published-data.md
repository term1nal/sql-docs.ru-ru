---
title: Фильтрация опубликованных данных | Документация Майкрософт
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
helpviewer_keywords:
- filters [SQL Server replication]
- filters [SQL Server replication], about filtering
- filtering [SQL Server replication]
- static row filters
- transactional replication, filtering published data
- replication [SQL Server], filtering published data
- filtering published data [SQL Server replication]
- snapshot replication [SQL Server], filtering published data
- column filters [SQL Server replication]
ms.assetid: 8a914947-72dc-4119-b631-b39c8070c71b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ac56fd795f819fe308dee9980e12883e73b0172d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/02/2018
ms.locfileid: "48222634"
---
# <a name="filter-published-data"></a>Фильтрация опубликованных данных
  Фильтрация статей таблиц позволяет создавать секции публикуемых данных. С помощью фильтрации опубликованных данных можно достичь следующих целей:  
  
-   Минимизировать объем данных, передаваемых по сети.  
  
-   Снизить необходимый подписчику объем для хранения.  
  
-   Настраивать публикации и приложения на основе индивидуальных требований подписчиков.  
  
-   Избежать конфликтов или уменьшить их количество, если подписчики обновляют данные, так как различным подписчикам можно отправить различные секции данных (то есть два подписчика не будут обновлять одни и те же значения данных).  
  
-   Избежать передачи конфиденциальных данных. Фильтры строк и фильтры столбцов могут быть использованы для ограничения доступа подписчика к данным. При репликации слиянием может возникать проблема безопасности, если используется параметризованный фильтр, содержащий HOST_NAME(). Дополнительные сведения см. в подразделе «Фильтрация с использованием HOST_NAME()» раздела [Parameterized Row Filters](../merge/parameterized-filters-parameterized-row-filters.md).  
  
 Репликация предлагает четыре типа фильтров:  
  
-   Статические фильтры строк, которые доступны со всеми типами репликаций.  
  
     Используя статические фильтры строк, можно выбрать для публикации подмножество строк. Все подписчики на фильтрованную публикацию получают одно и то же подмножество строк фильтрованной таблицы. Дополнительные сведения см. в подразделе «Статические фильтры строк» данного раздела.  
  
-   Фильтры столбцов, доступные со всеми типами репликаций.  
  
     Используя фильтры столбцов, можно выбрать для публикации подмножество столбцов. Дополнительные сведения см. в подразделе «Фильтры столбцов» данного раздела.  
  
-   Параметризованные фильтры строк, доступные только с репликацией слиянием.  
  
     Используя параметризованные фильтры строк, можно выбрать для публикации подмножество строк. В отличие от статических фильтров, которые отправляют одно и то же подмножество строк всем подписчикам, параметризованные фильтры строк используют получаемые от подписчиков значения данных для отправки подписчикам разных подмножеств строк. Дополнительные сведения см. в статье [Parameterized Row Filters](../merge/parameterized-filters-parameterized-row-filters.md).  
  
-   Фильтры соединения, доступные только с репликацией слиянием.  
  
     Используя фильтры соединения, можно расширить фильтр строк с одной публикуемой таблицы на другую. Дополнительные сведения см. в статье [Join Filters](../merge/join-filters.md).  
  
## <a name="static-row-filters"></a>статические фильтры строк  
 На следующей иллюстрации показана опубликованная таблица, которая отфильтрована так, что в публикацию включаются только строки 2, 3 и 6.  
  
 ![Фильтрация строк](../media/repl-16.gif "Фильтрация строк")  
  
 Статический строковой фильтр использует предложение WHERE для отбора соответствующих данных для публикации; необходимо указать заключительную часть предложения WHERE. Рассмотрите таблицу **Product** в примере базы данных AdventureWorks, содержащую столбец **ProductLine**. Для публикации только строк с данными о продуктах, относящихся к горным велосипедам, укажите `ProductLine = 'M'`.  
  
 Применение статического фильтра строк приводит к выборке одного набора данных для каждой публикации. В предыдущем примере все подписчики получили бы только строки с данными о продуктах, относящихся к горным велосипедам. Если имеется другой подписчик, которому нужны только строки с данными о продуктах, относящихся к дорожным велосипедам,  
  
-   с помощью репликации моментальных снимков или репликации транзакций можно создать другую публикацию и включить таблицу в обе публикации (в предложении фильтра для статьи в этой публикации укажите `ProductLine = 'R')`.  
  
    > [!NOTE]  
    >  Фильтры строк в публикациях транзакций могут существенно увеличить объем дополнительно выполняемых служебных операций, поскольку предложение фильтра статьи оценивается для каждой строки журнала, записанной для публикуемой таблицы, с целью определения необходимости репликации строки. Необходимо избегать фильтров строк в публикациях транзакций, если каждый узел репликации может поддерживать полную загрузку данных, а общий набор данных достаточно невелик.  
  
-   Вместо создания нескольких публикаций со статическими фильтрами строк используйте с репликацией слиянием параметризованные фильтры строк. Дополнительные сведения см. в статье [Parameterized Row Filters](../merge/parameterized-filters-parameterized-row-filters.md).  
  
 Сведения об определении или изменении статического строкового фильтра см. в разделе [Define and Modify a Static Row Filter](define-and-modify-a-static-row-filter.md).  
  
## <a name="column-filters"></a>Фильтры столбцов  
 На следующей иллюстрации показана публикация, которая отфильтровывает столбец «C».  
  
 ![Фильтрация столбцов](../media/repl-17.gif "Фильтрация столбцов")  
  
 Как показано здесь, можно также применять фильтр строк и фильтр столбцов совместно.  
  
 ![Фильтрация строк и столбцов](../media/repl-18.gif "Фильтрация строк и столбцов")  
  
 После создания публикации можно использовать фильтр столбцов, чтобы удалить столбец из существующей публикации, но сохранить его в таблице у издателя, а также, чтобы включить существующий столбец в публикацию. Для внесения других изменений, например, для добавления нового столбца в таблицу с последующим добавлением этой таблицы в опубликованную статью, используйте репликацию изменения схемы. Дополнительные сведения см. в подразделах "Добавление столбцов" и "Удаление столбцов" раздела [Внесение изменений схем в базы данных публикации](make-schema-changes-on-publication-databases.md).  
  
 Типы столбцов, перечисленных в следующей таблице, не могут быть отфильтрованы из определенных типов публикаций.  
  
|Тип столбца|Тип публикации и параметры|  
|-----------------|-------------------------------------|  
|Первичный ключевой столбец|Первичные ключевые столбцы требуются во всех таблицах публикации транзакций. Первичные ключи не требуются для таблиц в публикациях слиянием, но если первичный ключевой столбец имеется, то к нему не может быть применен фильтр.|  
|Внешний ключевой столбец|Все публикации создаются с использованием мастера создания публикаций. Внешние ключевые столбцы могут фильтроваться с помощью хранимых процедур Transact-SQL. Дополнительные сведения см. в разделе [Define and Modify a Column Filter](define-and-modify-a-column-filter.md).|  
|Столбец **rowguid**|Для публикаций слиянием<sup>1</sup>|  
|Столбец **msrepl_tran_version**|Публикации моментальных снимков или публикации транзакций, разрешающие использование обновляемых подписок|  
|Столбцы, не допускающие значения NULL и не имеющие значений по умолчанию или набора свойств IDENTITY.|Публикации моментальных снимков или публикации транзакций, разрешающие использование обновляемых подписок|  
|Столбцы с уникальными ограничениями или индексами|Публикации моментальных снимков или публикации транзакций, разрешающие использование обновляемых подписок|  
|Все столбцы в публикации слиянием SQL Server 7.0|В публикациях слиянием SQL Server 7.0 к столбцам фильтр применен быть не может.|  
|Отметка времени|Публикации моментальных снимков или публикации транзакций SQL Server 7.0, которые разрешают использование обновляемых подписок|  
  
 <sup>1</sup> Если вы публикуете таблицу в публикации слиянием и эта таблица уже содержит столбец типа данных `uniqueidentifier` с `ROWGUIDCOL` набор свойств, репликация может использовать этот столбец вместо создания дополнительного столбца с именем **rowguid**. В этом случае должен быть опубликован существующий столбец.  
  
 Сведения об определении или изменении фильтра столбцов см. в разделе [Define and Modify a Column Filter](define-and-modify-a-column-filter.md).  
  
## <a name="filtering-considerations"></a>Вопросы применения фильтров  
 При фильтрации данных учитывайте следующие требования:  
  
-   В публикацию должны быть включены все столбцы, на которые имеются ссылки в фильтрах строк. Иными словами, нельзя использовать фильтр столбцов для исключения столбца, который используется в фильтре строк.  
  
-   Если добавление или изменение фильтра производится после инициализации подписок, то подписки должны быть инициализированы повторно.  
  
-   Максимальное число байтов, разрешенное для столбца, используемого в фильтре, равно 1024 для статьи в публикации слиянием и 8000 для статьи в публикации транзакций.  
  
-   В фильтрах строк или фильтрах соединения не допускаются ссылки на столбцы со следующими типами данных:  
  
    -   `varchar(max) and nvarchar(max)`  
  
    -   `varbinary(max)`  
  
    -   `text and ntext`  
  
    -   `image`  
  
    -   `XML`  
  
    -   `UDT`  
  
-   Репликация транзакций позволяет реплицировать индексированное представление либо в виде представления, либо в виде таблицы. Если выполняется репликация представления в виде таблицы, отфильтровать столбцы из таблицы не удастся.  
  
 Фильтры строк не предназначены для работы в нескольких базах данных. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] намеренно ограничивает выполнение `sp_replcmds` (в котором применяются фильтры) владельца базы данных (`dbo`). `dbo` Не имеет межбазовых прав доступа. Благодаря добавлению CDC (системы отслеживания измененных данных) в [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] логика `sp_replcmds` вносит в таблицы отслеживания изменений данные, которые могут возвращаться и запрашиваться пользователем. По соображениям безопасности [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ограничивает выполнение этой логики, чтобы злонамеренный `dbo` нельзя highjack этом пути выполнения. Например, злонамеренный `dbo` может добавить в CDC-таблицы триггеры, которые впоследствии могут сработать в контексте пользователя, вызвавшего `sp_replcmds`, в данном случае агента чтения журнала.  Если учетная запись, под которой запущен агент, имеет более высокие права доступа, злонамеренный `dbo` может повысить свой уровень прав.  
  
## <a name="see-also"></a>См. также  
 [Публикация данных и объектов базы данных](publish-data-and-database-objects.md)  
  
  
