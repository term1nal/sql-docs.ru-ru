---
title: "Пошаговое руководство. Настройка масштабного развертывания Integration Services | Microsoft Docs"
ms.custom: ""
ms.date: "01/18/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: cabb78a2-f234-46c3-842d-53aa2df8dfb3
caps.latest.revision: 10
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 7
---
# Пошаговое руководство. Настройка масштабного развертывания Integration Services

Для настройки масштабного развертывания [!INCLUDE[ssISnoversion_md](../includes/ssisnoversion-md.md)] требуется выполнить указанные ниже задачи. 

> [!NOTE] При установке масштабного развертывания на одном компьютере рекомендуется установить главную и рабочую роли одновременно. При одновременной установке компонентов автоматически создается конечная точка для подключения к главной роли масштабного развертывания. 

* [Установка главной роли масштабного развертывания](#InstallMaster)

* [Установка рабочей роли масштабного развертывания](#InstallWorker)

* [Установка сертификата клиента рабочей роли масштабного развертывания](#InstallCert)

* [Открытие порта брандмауэра](#Firewall)

* [Запуск службы главной и рабочей роли масштабного развертывания](#Start)

* [Включение главной роли масштабного развертывания](#EnableMaster)

* [Включение режима проверки подлинности SQL Server](#EnableAuth)

* [Включение рабочей роли масштабного развертывания](#EnableWorker)

## <a name="a-nameinstallmastera-install-scale-out-master"></a><a name="InstallMaster"></a> Установка главной роли масштабного развертывания

Чтобы включить возможности главной роли масштабного развертывания, следует установить службы ядра СУБД, [!INCLUDE[ssISnoversion_md](../includes/ssisnoversion-md.md)] и компонент главной роли масштабного развертывания при настройке [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)]. 

Сведения о настройке служб ядра СУБД и [!INCLUDE[ssISnoversion_md](../includes/ssisnoversion-md.md)] см. в разделах [Установка ядра СУБД SQL Server](../database-engine/install-windows/install-sql-server-database-engine.md) и [Установка служб Integration Services](../integration-services/install-windows/install-integration-services.md).
> [!NOTE]
> Во время установки ядра СУБД выберите смешанный режим проверки подлинности на странице "Настройка ядра СУБД". 

**Чтобы установить главную роль масштабного развертывания, используйте мастер установки [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] или командную строку.**

- Шаги для выполнения в мастере установки [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)]
  1.  На странице **Выбор компонентов** выберите элемент **Мастер масштабирования** в категории [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].   
  ![Выбор главной роли](../integration-services/media/feature-select-master.PNG)
  
  2.  На странице **Конфигурация сервера** выберите учетную запись для запуска **службы главной роли масштабного развертывания SQL Server Integration Services** и **Тип запуска**.  
  ![Конфигурация сервера](../integration-services/media/server-config.PNG)
  3.  На странице **Настройка мастера масштабирования служб Integration Services** укажите номер порта, который главная роль масштабного развертывания использует для связи с рабочей ролью. По умолчанию номер порта равен 8391.  
  ![Master Config](../integration-services/media/master-config.PNG "Master Config")
  4.  Укажите SSL-сертификат, используемый для защиты связи между главной и рабочей ролями масштабного развертывания, выполнив одно из указанных ниже действий.
    * Позвольте процессу установки создать самозаверяющий SSL-сертификат по умолчанию, выбрав **Создать SSL-сертификат**. Сертификат по умолчанию устанавливается в доверенных корневых центрах сертификации на локальном компьютере.
    * Выберите существующий SSL-сертификат на локальном компьютере, выбрав **Использовать существующий SSL-сертификат** и нажав кнопку **Обзор**. Отпечаток сертификата отображается в текстовом поле. При нажатии кнопки **Обзор** отображаются сертификаты, хранящиеся в доверенных корневых центрах сертификации на локальном компьютере. Выбранный вами сертификат должен храниться здесь.       
![Master Config 2](../integration-services/media/master-config-2.PNG "Master Config 2")
  5.  Завершите работу мастера установки [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)].
- Шаги для выполнения в командной строке

    Следуйте инструкциям в разделе [Установка SQL Server из командной строки](../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md). Задайте параметры для главной роли масштабного развертывания, выполнив указанные ниже действия.
  1.  Добавьте IS_Master в параметр /FEATURES.
  2.  Настройте главную роль масштабного развертывания с помощью следующих параметров: /ISMASTERSVCACCOUNT, /ISMASTERSVCPASSWORD, /ISMASTERSVCSTARTUPTYPE, /ISMASTERSVCPORT, /ISMASTERSVCTHUMBPRINT (необязательно).
  
## <a name="a-nameinstallworkera-install-scale-out-worker"></a><a name="InstallWorker"></a> Установка рабочей роли масштабного развертывания
 
Чтобы включить возможности рабочей роли масштабного развертывания, следует установить [!INCLUDE[ssISnoversion_md](../includes/ssisnoversion-md.md)] и компонент рабочей роли масштабного развертывания в программе установки [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)].

**Чтобы установить рабочую роль масштабного развертывания, используйте мастер установки [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] или командную строку.**

- Шаги для выполнения в мастере установки [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)]
  1.  На странице **Выбор компонентов** выберите **Рабочая роль масштабирования** в категории [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].   
  ![Выбор рабочей роли](../integration-services/media/feature-select-worker.PNG)
  2. На странице **Конфигурация сервера** выберите учетную запись для запуска **службы рабочей роли масштабного развертывания SQL Server Integration Services** и выберите **Тип запуска**.    
  ![Server Config 2](../integration-services/media/server-config-2.PNG "Server Config 2")
  3. На странице **Настройка рабочей роли масштабирования служб Integration Services** укажите конечную точку для связи с главной ролью масштабного развертывания. 
    - Для **одиночной** среды конечная точка создается автоматически при одновременной установке главной и рабочей ролей масштабного развертывания. 
    - Для среды из **нескольких компьютеров** конечная точка состоит из имени или IP-адреса компьютера с главной ролью масштабного развертывания, а также номера порта, указанного во время установки главной роли масштабного развертывания.    
   ![Worker Config 1](../integration-services/media/worker-config-1.PNG "Worker Config 1")
    
  4. Для среды из **нескольких компьютеров** укажите SSL-сертификат клиента, используемый для проверки главной роли масштабного развертывания. Для **одиночной** среды указывать SSL-сертификат клиента не нужно. 
  
     > [!NOTE] Если SSL-сертификат, используемый главной ролью масштабного развертывания, является самозаверяющим, соответствующий SSL-сертификат клиента требуется установить на компьютере с рабочей ролью масштабного развертывания. Если указать путь к файлу SSL-сертификата клиента на странице **Настройка рабочей роли масштабирования служб Integration Services**, он будет установлен автоматически; в противном случае требуется установить этот сертификат вручную позже. 
     
     Нажмите кнопку **Обзор**, чтобы найти файл сертификата (CER). Чтобы использовать SSL-сертификат по умолчанию, выберите файл SSISScaleOutMaster.cer, расположенный в папке \<диск\>:\Program Files\Microsoft SQL Server\140\DTS\Binn на компьютере с установленной главной ролью масштабного развертывания.   
   ![Worker Config 2](../integration-services/media/worker-config-2.PNG "Worker Config 2")
  5. Завершите работу мастера установки [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)].
- Шаги для выполнения в командной строке

    Следуйте инструкциям в разделе [Установка SQL Server из командной строки](../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md). Задайте параметры, связанные с рабочей ролью масштабного развертывания, выполнив указанные ниже действия.
    1.  Добавьте IS_Worker в параметр /FEATURES.
    2. Настройте рабочую роль масштабного развертывания с помощью следующих параметров: /ISWORKERSVCACCOUNT, /ISWORKERSVCPASSWORD, /ISWORKERSVCSTARTUPTYPE, /ISWORKERSVCMASTER (необязательно), /ISWORKERSVCCERT (необязательно).

 
## <a name="a-nameinstallcerta-install-scale-out-worker-client-certificate"></a><a name="InstallCert"><a/> Установка сертификата клиента рабочей роли масштабного развертывания

Во время установки рабочей роли масштабного развертывания сертификат рабочей роли создается и устанавливается на компьютере автоматически. Кроме того, соответствующий сертификат клиента SSISScaleOutWorker.cer устанавливается в папку \<диск\>:\Program Files\Microsoft SQL Server\140\DTS\Binn. Чтобы главная роль масштабного развертывания проверяла подлинность рабочей роли, следует добавить этот сертификат клиента в корневое хранилище локального компьютера, где находится главная роль.
  
Чтобы добавить сертификат клиента в корневое хранилище, дважды щелкните файл CER и нажмите кнопку **Установить сертификат** в диалоговом окне сертификата. Отображается **Мастер импорта сертификатов**.  

## <a name="a-namefirewalla-open-firewall-port"></a><a name="Firewall"><a/> Открытие порта брандмауэра

Откройте порт, указанный во время установки главной роли масштабного развертывания, используя брандмауэр Windows на компьютере с главной ролью масштабного развертывания.
    
## <a name="a-namestarta-start-sql-server-scale-out-master-and-worker-services"></a><a name="Start"></a> Запуск службы главной и рабочей роли масштабного развертывания

Если во время описанной выше установки для служб не задан автоматический тип запуска, запустите службы: "Главная служба развертывания SQL Server Integration Services 14.0" (SSISScaleOutMaster140) и "Рабочая роль развертывания SQL Server Integration Services 14.0" (SSISScaleOutWorker140). 

> [!NOTE]
>После открытия порта в брандмауэре требуется перезапустить рабочую роль масштабного развертывания.
   
## <a name="a-nameenablemastera-enable-scale-out-master"></a><a name="EnableMaster"></a> Включение главной роли масштабного развертывания

Щелкните **Включить этот сервер в качестве мастера масштабирования SSIS** в диалоговом окне **Создать каталог** при создании каталога SSISDB в [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio_md](../includes/ssmanstudio-md.md)].

## <a name="a-nameenableautha-enable-sql-server-authentication-mode"></a><a name="EnableAuth"></a> Включение режима проверки подлинности SQL Server
Если проверка подлинности [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] не включена во время установки ядра СУБД, включите режим проверки подлинности SQL Server в экземпляре [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)], где находится каталог SSISDB. 

При отключенной проверке подлинности SQL Server выполнение пакетов не блокируется. Тем не менее журнал выполнения не сможет осуществлять запись в SSISDB.

## <a name="a-nameenableworkera-enable-scale-out-worker"></a><a name="EnableWorker"></a> Включение рабочей роли масштабного развертывания
Чтобы включить рабочую роль масштабного развертывания, выполните хранимую процедуру *[catalog].[enable_worker_agent]*, используя **WorkerAgentId** в качестве параметра. 

После регистрации рабочей роли масштабного развертывания в главной роли вы получаете значение **WorkerAgentId** из представления базы данных *[catalog].[worker_agents]* в SSISDB. Регистрация занимает несколько минут после запуска главной и рабочей ролей.

### <a name="example"></a>Пример
В этом примере рабочая роль масштабного развертывания включается на компьютере MachineA.
```tsql
SELECT WorkerAgentId, MachineName FROM [catalog].[worker_agents]
GO
-- Result: --
-- WorkerAgentId                           MachineName --
-- 6583054A-E915-4C2A-80E4-C765E79EF61D    MachineA    --

EXEC [catalog].[enable_worker_agent] '6583054A-E915-4C2A-80E4-C765E79EF61D'
GO 
```
## <a name="next-steps"></a>Следующие шаги
Настройка функции масштабного развертывания завершена. Теперь вы можете выполнять пакеты в масштабном развертывании. Дополнительные сведения см. в разделе [Выполнение пакетов в масштабном развертывании служб Integration Services (SSIS)](../integration-services/run-packages-in-integration-services-ssis-scale-out.md).
