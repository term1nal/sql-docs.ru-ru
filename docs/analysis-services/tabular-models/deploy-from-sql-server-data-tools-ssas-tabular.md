---
title: "Развертывание из SQL Server Data Tools (табличные службы SSAS) | Документы Microsoft"
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
- sql13.asvs.bidtoolset.deploystatus.f1
ms.assetid: 67dde3fe-ba43-41f3-b56c-c656029ee93f
caps.latest.revision: 17
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: adb50d35f60359d6bd1e18cacff6e80722665d59
ms.contentlocale: ru-ru
ms.lasthandoff: 09/01/2017

---
# <a name="deploy-from-sql-server-data-tools"></a>Развертывание из SQL Server Data Tools
  Используйте задачи в этом разделе для развертывания решения табличной модели с помощью команды «развертывание» в SSDT.  
  
##  <a name="bkmk_deploy"></a> Configure deployment options and deployment server properties  
 Перед развертыванием решения табличной модели прежде всего необходимо указать параметры развертывания и свойства сервера развертывания. Дополнительные сведения о свойствах развертывания и параметрах см. в разделе [развертывание решений табличной модели](../../analysis-services/tabular-models/tabular-model-solution-deployment-ssas-tabular.md).  
  
#### <a name="to-configure-options-and-properties"></a>Чтобы настроить параметры и свойства  
  
1.  В SSDT в **обозревателе решений**, щелкните правой кнопкой мыши имя проекта и нажмите кнопку **свойства**.  
  
2.  В  **\<имя проекта > свойства** диалоговое окно, в **варианты развертывания**, задайте значения свойств, если он отличается от значения по умолчанию.  
  
    > [!NOTE]  
    >  Для моделей в режиме кэширования **Режим запроса** всегда **В памяти**.  
  
    > [!NOTE]  
    >  **Параметры олицетворения** нельзя задать для моделей в режиме DirectQuery.  
  
3.  В области **Сервер развертывания**укажите значения свойств **Сервер** (имя), **Выпуск**, **База данных** (имя) и **Имя куба** , если они отличаются от заданных по умолчанию, и нажмите кнопку **ОК**.  
  
> [!NOTE]  
>  Можно также указать параметр свойства сервера развертывания по умолчанию, чтобы все создаваемые проекты были автоматически развернуты на указанном сервере. Дополнительные сведения см. в разделе [Настройка моделирования данных и свойств развертывания](../../analysis-services/tabular-models/configure-default-data-modeling-and-deployment-properties-ssas-tabular.md).  
  
##  <a name="bkmk_deploy_proc"></a>Развертывание табличной модели  
  
#### <a name="to-deploy-a-tabular-model"></a>Развертывание табличной модели
  
-   В SSDT на **построения** меню, нажмите кнопку **развернуть \<имя проекта >**.  
  
     Появится диалоговое окно **Развертывание** , в котором будет отображаться состояние развертывания метаданных и обработки каждой таблицы (если для свойства "Вариант обработки" не выбрано значение "Не обрабатывать"), включенной в модель. После завершения процесса развертывания, используйте SSMS подключитесь к экземпляру служб Analysis Services и убедитесь, что был создан новый объект шаблона базы данных или клиентские приложения для подключения к развернутой модели.  
  
##  <a name="bkmk_deploy_status"></a> Состояние развертывания  
 Диалоговое окно **Развертывание** позволяет отслеживать ход выполнения операций развертывания. Операцию развертывания также можно остановить.  
  
 **Состояние**  
 Сообщает об успешности операции развертывания.  
  
 **Сведения**  
 Перечисляет развернутые элементы метаданных, состояние для каждого элемента метаданных и выдает сообщения о любых неполадках.  
  
 **Остановить развертывание**  
 Щелкните, чтобы остановить операцию развертывания. Этот параметр полезен, если операция развертывания занимает слишком много времени либо обнаружено слишком много ошибок.  
  
## <a name="see-also"></a>См. также:  
 [Развертывание решений табличной модели](../../analysis-services/tabular-models/tabular-model-solution-deployment-ssas-tabular.md)   
 [Настройка моделирования данных по умолчанию и свойств развертывания](../../analysis-services/tabular-models/configure-default-data-modeling-and-deployment-properties-ssas-tabular.md)  
  
  