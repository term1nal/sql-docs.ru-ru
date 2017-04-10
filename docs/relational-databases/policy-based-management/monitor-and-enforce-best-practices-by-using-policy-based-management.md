---
title: "Наблюдение с помощью управления на основе политик и принудительное применение рекомендаций с помощью управления на основе политик | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Лучшие решения [компонент Database Engine]"
ms.assetid: 46788407-187e-4b0b-bfe4-529af8d77c60
caps.latest.revision: 27
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 27
---
# Наблюдение с помощью управления на основе политик и принудительное применение рекомендаций с помощью управления на основе политик
  Управление на основе политик позволяет отслеживать рекомендации для [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] предоставляет набор файлов политик, которые можно импортировать в качестве политик рекомендаций, а затем оценивать эти политики для набора целей, включающего экземпляры, объекты экземпляров, базы данных или объекты базы данных. Политики можно оценивать вручную или устанавливать их для оценки набора целей согласно расписанию либо тому или иному событию. Дополнительные сведения об управлении на основе политик см. в статье [Администрирование серверов с помощью управления на основе политик](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md).  
  
## Политика и правила для компонента Database Engine  
 В следующей таблице приводится список политик, включенных в установку [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], а также сведения о правилах рекомендаций, которые вычисляет каждая политика. Политики хранятся в виде XML-файлов и должны импортироваться в [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Дополнительные сведения об импорте политик см. в статье [Импорт политики управления на основе политик](../../relational-databases/policy-based-management/import-a-policy-based-management-policy.md).  
  
|Имя политики|Правило рекомендации|  
|-----------------|------------------------|  
|Алгоритм шифрования асимметричных ключей|[Стойкость шифрования асимметричных ключей](../../relational-databases/policy-based-management/asymmetric-keys-encryption-strength.md)|  
|Размещение резервной копии и файла данных|[Файлы резервной копии и файлы базы данных должны находиться на отдельных устройствах](../Topic/Backup%20Files%20Must%20Be%20on%20Separate%20Devices%20from%20the%20Database%20Files.md)|  
|Расположение файлов данных и журнала|[Размещение файлов данных и файлов журнала на различных дисках](../../relational-databases/policy-based-management/place-data-and-log-files-on-separate-drives.md)|  
|Автоматическое закрытие базы данных|[Задание значения OFF для параметра базы данных AUTO_CLOSE](../../relational-databases/policy-based-management/set-the-auto-close-database-option-to-off.md)|  
|Автоматическое сжатие базы данных|[Задание значения параметра базы данных AUTO_SHRINK, равного OFF](../../relational-databases/policy-based-management/set-the-auto-shrink-database-option-to-off.md)|  
|Параметры сортировки базы данных|[Задание параметров сортировки пользовательских баз данных в соответствии с параметрами баз данных master и model](../Topic/Set%20the%20Collation%20of%20User-defined%20Databases%20to%20Match%20Those%20of%20the%20master%20and%20model%20Databases.md)|  
|Проверка страниц базы данных|[Задание значения CHECKSUM для параметра базы данных PAGE_VERIFY](../../relational-databases/policy-based-management/set-the-page-verify-database-option-to-checksum.md)|  
|Состояние страницы базы данных|[Проверка целостности базы данных с потенциально поврежденными страницами](../../relational-databases/policy-based-management/check-integrity-of-database-with-suspect-pages.md)|  
|Разрешения гостя|[Разрешения гостя для пользовательских баз данных](../../relational-databases/policy-based-management/guest-permissions-on-user-databases.md)|  
|Дата последнего успешного резервного копирования|[Устаревшая резервная копия](../../relational-databases/policy-based-management/outdated-backup.md)|  
|Роли Public не предоставлены разрешения на сервер|[Разрешения роли сервера public](../../relational-databases/policy-based-management/server-public-permissions.md)|  
|SQL Server: перекрытие 64-разрядной маски сходства|[Correct Affinity Mask and Affinity Input and Output Mask Overlap](../../relational-databases/policy-based-management/correct-affinity-mask-and-affinity-input-and-output-mask-overlap.md)|  
|SQL Server: маска сходства|[Сохранение значения маски сходства по умолчанию](../../relational-databases/policy-based-management/keep-the-affinity-mask-default-value.md)|  
|SQL Server: пороговый интервал ожидания блокированных процессов|[Увеличение или отключение порога заблокированных процессов](../../relational-databases/policy-based-management/increase-or-disable-blocked-process-threshold.md)|  
|SQL Server: трассировка по умолчанию|[Отключение предусмотренных по умолчанию файлов журнала трассировки](../../relational-databases/policy-based-management/default-trace-log-files-disabled.md)|  
|SQL Server: динамические блокировки|[Сохранение предусмотренного по умолчанию значения параметра конфигурации блокировок](../../relational-databases/policy-based-management/keep-the-locks-configuration-option-default-value.md)|  
|SQL Server: использование упрощенных пулов|[Отключение использования упрощенных пулов](../../relational-databases/policy-based-management/disable-lightweight-pooling.md)|  
|SQL Server: режим входа|[Выбор режима проверки подлинности](../../relational-databases/security/choose-an-authentication-mode.md)|  
|SQL Server: максимальная степень параллелизма|[Задание параметра максимальной степени параллелизма для оптимальной производительности](../../relational-databases/policy-based-management/set-the-max-degree-of-parallelism-option-for-optimal-performance.md)|  
|SQL Server: максимальное число рабочих потоков для 32-разрядной версии SQL Server 2000|[Проверка параметра максимального числа рабочих потоков](../../relational-databases/policy-based-management/verify-max-worker-threads-setting.md)|  
|SQL Server: максимальное число рабочих потоков для 64-разрядной версии SQL Server 2000|[Проверка параметра максимального числа рабочих потоков](../../relational-databases/policy-based-management/verify-max-worker-threads-setting.md)|  
|SQL Server: максимальное число рабочих потоков для SQL Server 2005 и более поздних версий|[Проверка параметра максимального числа рабочих потоков](../../relational-databases/policy-based-management/verify-max-worker-threads-setting.md)|  
|SQL Server: размер сетевого пакета|[Размер сетевого пакета не должен превышать 8060 байт](../../relational-databases/policy-based-management/network-packet-size-should-not-exceed-8060-bytes.md)|  
|SQL Server: истечение действия пароля|[Истечение срока действия пароля имени входа SQL Server](../../relational-databases/policy-based-management/sql-server-login-password-expiration.md)|  
|SQL Server: политика паролей|[Стойкость пароля имени входа SQL Server](../../relational-databases/policy-based-management/sql-server-login-password-strength.md)|  
|Шифрование пользовательских баз данных симметричным ключом|[Симметричные ключи в пользовательских базах данных](../../relational-databases/policy-based-management/symmetric-keys-on-user-databases.md)|  
|Симметричный ключ для базы данных master|[Симметричные ключи в системных базах данных](../../relational-databases/policy-based-management/symmetric-keys-on-system-databases.md)|  
|Симметричный ключ для системных баз данных|[Симметричные ключи в системных базах данных](../../relational-databases/policy-based-management/symmetric-keys-on-system-databases.md)|  
|Доверенная база данных|[Бит доверия](../../relational-databases/policy-based-management/trustworthy-bit.md)|  
|Журнал событий Windows: ошибка из-за повреждения дискового ресурса кластера|[Определение неполадок хост-адаптера SCSI](../../relational-databases/policy-based-management/detect-scsi-host-adapter-issues.md)|  
|Журнал событий Windows: ошибка управления драйвером устройства|[Ошибка управления драйвером устройства](../../relational-databases/policy-based-management/device-driver-control-error.md)|  
|Журнал событий Windows, ошибка: устройство не готово|[Ошибка отсутствия готовности устройства](../../relational-databases/policy-based-management/device-not-ready-error.md)|  
|Журнал событий Windows: ошибка запроса ввода-вывода|[Detect Failed Input and Output Requests](../../relational-databases/policy-based-management/detect-failed-input-and-output-requests.md)|  
|Журнал событий Windows: предупреждение об отложенном вводе-выводе|[Check Disk Input and Output Subsystem for IO Delay Problems](../../relational-databases/policy-based-management/check-disk-input-and-output-subsystem-for-io-delay-problems.md)|  
|Журнал событий Windows: ошибка ввода-вывода при сбое страницы физической памяти|[Input and Output Error During Hard Page Fault](../../relational-databases/policy-based-management/input-and-output-error-during-hard-page-fault.md)|  
|Журнал событий Windows: ошибка при повторном считывании|[Проверка на наличие проблем повторного чтения в подсистеме дискового ввода-вывода](../../relational-databases/policy-based-management/check-disk-input-output-subsystem-for-read-retry-problems.md)|  
|Журнал событий Windows: ошибка из-за истечения времени ожидания ввода-вывода системы хранения|[Время ожидания ввода-вывода для системы хранения](../../relational-databases/policy-based-management/storage-system-input-output-time-out.md)|  
|Журнал событий Windows: сбой в системе|[Непредвиденные сбои системы](../../relational-databases/policy-based-management/unexpected-system-failures.md)|  
  
## См. также:  
 [Работа с аспектами управления на основе политик](../../relational-databases/policy-based-management/working-with-policy-based-management-facets.md)  
  
  