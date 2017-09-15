---
title: "Развертывание пакета развертывания модели при помощи MDSModelDeploy | Документы Microsoft"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: fb2a4df4-5e0d-4b34-818f-383dbde1b15c
caps.latest.revision: 16
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a678aee3bb185cf8dd44cb69d3c0027c090a81d3
ms.contentlocale: ru-ru
ms.lasthandoff: 08/02/2017

---
# <a name="deploy-a-model-deployment-package-by-using-mdsmodeldeploy"></a>Развертывание пакета развертывания модели при помощи MDSModelDeploy
  В [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]средство MDSModelDeploy используется для развертывания пакетов, содержащих:  
  
-   только объекты модели;  
  
-   объекты модели и данные.  
  
 Если необходимо развернуть пакет, содержащий только объекты модели, можно воспользоваться мастером развертывания моделей в веб-приложении [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] . Дополнительные сведения см. в статье [Deploy a Model Deployment Package by Using the Wizard](../master-data-services/deploy-a-model-deployment-package-by-using-the-wizard.md).  
  
> [!IMPORTANT]  
>  Пакеты могут быть развернуты только в выпуске [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , в котором они были созданы. Это означает, что пакеты, созданные в среде [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] , не могут быть развернуты в [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] или более поздних версиях.  
  
## <a name="prerequisites"></a>Предварительные требования  
 Чтобы выполнить эту процедуру:  
  
-   необходимо иметь разрешение на доступ к функциональной области **Администрирование системы** в целевой среде служб [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] ;  
  
-   должен существовать пакет развертывания модели. Дополнительные сведения см. в статье  [Create a Model Deployment Package by Using MDSModelDeploy](../master-data-services/create-a-model-deployment-package-by-using-mdsmodeldeploy.md).  
  
-   В среде, в которой выполняется развертывание модели, необходимо обладать правами администратора. Дополнительные сведения см. в статье [Администраторы (службы Master Data Services)](../master-data-services/administrators-master-data-services.md).  
  
-   При обновлении модели данных развертываемая версия не может быть **Заблокирована** или **Зафиксирована**.  
  
### <a name="to-deploy-a-model-deployment-package"></a>Развертывание пакетов развертывания модели  
  
1.  Определите, производится развертывание новой модели, копии модели или обновление скопированной ранее модели. Дополнительные сведения см. в разделе [Варианты развертывания модели (службы Master Data Services)](../master-data-services/model-deployment-options-master-data-services.md).  
  
2.  Откройте командную строку администратора и перейдите к MDSModelDeploy.exe.  
  
    -   Если службы MDS установлены в папку по умолчанию, то эта программа находится в каталоге *диск*:\Program Files\Microsoft SQL Server\130\Master Data Services\Configuration.  
  
    -   Если службы MDS не установлены в местоположение по умолчанию, то найдите файл MDSModelDeploy.exe на локальном компьютере.  
  
3.  Необязательно. Просмотрите параметры и справку.  
  
    -   Чтобы показать все доступные параметры, введите `MDSModelDeploy` и нажмите клавишу ВВОД.  
  
    -   Чтобы вывести справку для параметра, введите следующую строку, где *OptionName* — имя параметра: `MDSModelDeploy help OptionName`.  
  
4.  Необязательно. При наличии нескольких веб-приложений определите имя развертываемой службы, введя следующую команду, и нажмите клавишу ВВОД.  
  
    ```  
    MDSModelDeploy listservices  
    ```  
  
     Возвращается список значений, например `MDS1, Default Web Site, MDS`. Первое значение в этом списке (в данном случае `MDS1`) необходимо для развертывания модели.  
  
5.  В зависимости от выполняемой задачи (создание модели, копирование модели или обновление модели) наберите в командной строке следующий текст и нажмите клавишу ВВОД.  
  
    -   Создание новой модели:  
  
        ```  
        MDSModelDeploy deploynew -package PackageName -model ModelName -service ServiceName  
        ```  
  
    -   Создание копии модели:  
  
        ```  
        MDSModelDeploy deployclone -package PackageName  
        ```  
  
    -   Обновление существующей модели и ее данных:  
  
        ```  
        MDSModelDeploy deployupdate -package PackageName -version VersionName  
        ```  
  
    > [!IMPORTANT]  
    >  Если средство MDSModelDeploy используется для обновления существующей модели и ее данных и пакет не содержит сущность, атрибут или элемент, имеющиеся в целевой модели, MDSModelDeploy не удаляет из модели эту сущность, атрибут или элемент.  
  
     Здесь *PackageName* — имя файла пакета (PKG), *ModelName* — имя новой модели, *VersionName* — имя версии, а *ServiceName* — полученное на предыдущем шаге имя службы. Убедитесь, что имена модели и версии в точности соответствуют заданным названиям с учетом регистра.  
  
6.  После успешного развертывания пакета отображается сообщение «Операция MDSModelDeploy успешно завершена».  
  
 **Примечания.**  
  
-   Если имя представления подписки в пакете совпадает с именем представления подписки в существующей модели, отображается предупреждение **Deployer subscription view renamed** (Представление подписки программы развертывания переименовано) и создается представление *modelname.subscriptionviewname*. Если это имя уже используется, то представление подписки не создается.  
  
-   Процесс развертывания состоит из четырех шагов.  
  
    1.  Создаются объекты модели.  
  
    2.  Создаются бизнес-правила.  
  
    3.  Создаются представления подписки.  
  
    4.  Производится заполнение основных данных.  
  
-   Если при создании новой или клонированной модели процесс на любом этапе завершается ошибкой, модель удаляется.  
  
     При обновлении в случае неудачного завершения любого из первых трех шагов переход к следующему шагу не производится. Однако откат уже внесенных изменений также не выполняется. Если процесс развертывания завершается неудачей в шаге 4, обновляются те элементы, которые могут обновиться.  
  
## <a name="next-steps"></a>Следующие шаги  
 Атрибуты файлов и разрешения для пользователей и групп не включаются в пакеты развертывания модели. При развертывании модели их нужно обновить вручную. Дополнительные сведения см. в разделе:  
  
-   [Назначение разрешения для объекта модели (службы Master Data Services)](../master-data-services/assign-model-object-permissions-master-data-services.md)  
  
## <a name="see-also"></a>См. также:  
 [Развертывание моделей &#40; Службы Master Data Services &#41;](../master-data-services/deploying-models-master-data-services.md)  
  
  