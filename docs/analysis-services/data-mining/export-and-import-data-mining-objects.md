---
title: "Экспорт и импорт объектов интеллектуального анализа данных | Microsoft Docs"
ms.custom: ""
ms.date: "03/06/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "резервное копирование баз данных [службы Analysis Services]"
  - "экспорт моделей интеллектуального анализа данных"
  - "экспорт структур интеллектуального анализа данных"
  - "структуры интеллектуального анализа данных [службы Analysis Services], создание"
  - "структуры интеллектуального анализа данных [расширения интеллектуального анализа данных], экспорт"
  - "модели интеллектуального анализа данных [службы Analysis Services], миграция"
ms.assetid: 10a83b13-2640-4ff5-80c8-a35e1d692908
caps.latest.revision: 23
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 23
---
# Экспорт и импорт объектов интеллектуального анализа данных
  В дополнение к функциям, реализованным в решениях резервного копирования, восстановления из копии и миграции служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], интеллектуальный анализ данных SQL Server обеспечивает возможность быстрой передачи структур и моделей интеллектуального анализа данных с одного сервера на другой с помощью расширений интеллектуального анализа данных.  
  
 Если в решении интеллектуального анализа данных используется не многомерная, а реляционная база данных, то передача данных с помощью инструкций **EXPORT** и **IMPORT** осуществляется намного быстрее и проще, чем с помощью восстановления базы данных или развертывания всего решения.  
  
 В этом разделе приводятся общие сведения о передаче структур и моделей интеллектуального анализа данных с помощью инструкций DMX. Подробные сведения о синтаксисе, а также примеры см. в разделах [EXPORT (DMX)](../../dmx/export-dmx.md) и [IMPORT (DMX)](../../dmx/import-dmx.md).  
  
> [!NOTE]  
>  Для экспорта или импорта объектов из базы данных служб Microsoft SQL Server Analysis Services необходимо обладать правами администратора базы данных или сервера.  
  
## Экспорт структур интеллектуального анализа данных  
 При экспорте структуры интеллектуального анализа данных инструкция EXPORT автоматически экспортирует все связанные модели. Если требуется обеспечить управление экспортируемыми объектами, каждый объект нужно указывать по имени.  
  
 Если структура интеллектуального анализа данных обработана, а результаты сохранены в кэше, как это осуществляется по умолчанию при экспорте структуры интеллектуального анализа данных, определение содержит сводку данных, на которых основывается данная структура. Чтобы удалить эту сводку, необходимо очистить связанный со структурой интеллектуального анализа данных кэш, выполнив операцию **Process Clear Structure** . Дополнительные сведения см. в разделе [Обработка структуры интеллектуального анализа данных](../../analysis-services/data-mining/process-a-mining-structure.md).  
  
### Экспорт моделей интеллектуального анализа данных  
 Чтобы вместе с моделью интеллектуального анализа данных и его структурой экспортировать источник данных, а также определение представления источников данных, можно использовать ключевое слово **WITH DEPENDENCIES** .  
  
 При экспорте модели интеллектуального анализа данных, не включающем экспорт зависимостей, инструкция EXPORT экспортирует определение модели интеллектуального анализа данных и ее структуру интеллектуального анализа данных, но не определение источников данных. В результате, после импорта модели ее можно просматривать немедленно, но если понадобится заново обработать модель интеллектуального анализа данных на целевом сервере или выполнить запрос базовых данных, потребуется создать соответствующий источник данных на целевом сервере.  
  
## Импорт структур и моделей интеллектуального анализа данных  
 При импорте объекта интеллектуального анализа данных этот объект импортируется на сервер и в базу данных, с которыми установлено соединение в момент выполнения инструкции IMPORT. Если в файле импорта содержится ссылка на несуществующую на сервере базу данных, эта база данных будет создана.  
  
 Структуру или модель интеллектуального анализа данных можно также импортировать с помощью команды **Restore** . Модели или структуры будут восстановлены в базе данных с тем же именем, что и в базе данных, из которой они были экспортированы. Дополнительные сведения см. в статье [Restore Options](../../analysis-services/multidimensional-models/restore-options.md).  
  
## Замечания  
 Невозможно импортировать модель или структуру на сервер, если на этом сервере уже существует модель или структура с таким же именем. Кроме того, невозможно экспортировать объект интеллектуального анализа данных и затем изменить имя этого объекта в файле экспорта. Следовательно, если предполагается возможность возникновения конфликта имен, следует либо удалить объект интеллектуального анализа данных на целевом сервере, либо переименовать этот объект интеллектуального анализа данных до выполнения операции экспорта определения.  
  
## См. также  
 [Управление решениями и объектами интеллектуального анализа данных](../../analysis-services/data-mining/management-of-data-mining-solutions-and-objects.md)  
  
  