---
title: "Резервное копирование SQL Server на URL-адрес — рекомендации и устранение неполадок | Microsoft Docs"
ms.custom: ""
ms.date: "08/09/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-backup-restore"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: de676bea-cec7-479d-891a-39ac8b85664f
caps.latest.revision: 26
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 26
---
# Резервное копирование SQL Server на URL-адрес — рекомендации и устранение неполадок
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  В этом разделе рассматриваются рекомендации и советы по устранению неполадок SQL Server при создании резервных копий и восстановлении с помощью службы хранилища больших двоичных объектов Windows Azure.  
  
 Дополнительную информацию по использованию службы хранилища больших двоичных объектов Windows Azure для операций резервного копирования или восстановления SQL Server см. в разделах:  
  
-   [Резервное копирование и восстановление SQL Server с помощью службы хранилища BLOB-объектов Microsoft Azure](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)  
  
-   [Tutorial: SQL Server Backup and Restore to Windows Azure Blob Storage Service](../Topic/Tutorial:%20SQL%20Server%20Backup%20and%20Restore%20to%20Windows%20Azure%20Blob%20Storage%20Service.md)  
  
## Управление резервными копиями  
 В следующем списке перечислены общие рекомендации по управлению резервным копированием.  
  
-   Рекомендуется присваивать каждому файлу уникальное имя, чтобы предотвратить случайное перезаписывание больших двоичных объектов.  
  
-   При создании контейнера рекомендуется установить уровень доступа **private**, чтобы большие двоичные объекты в контейнере могли читать или записывать только те пользователи или учетные записи, которые предоставили необходимую информацию для проверки подлинности.  
  
-   Для баз данных SQL Server на экземпляре SQL Server, который работает на виртуальной машине Windows Azure, используйте учетную запись хранилища в том же регионе, что и виртуальная машина, чтобы избежать затрат на передачу данных между регионами. Использование одного региона также обеспечивает оптимальную производительность операций резервного копирования и восстановления.  
  
-   Сбой во время резервного копирования может привести к созданию неработоспособного файла резервной копии. Рекомендуется периодически проводить поиск неудачных резервных копий и удалять файлы больших двоичных объектов. Дополнительные сведения см. в разделе [Deleting Backup Blob Files with Active Leases](../../relational-databases/backup-restore/deleting-backup-blob-files-with-active-leases.md).  
  
-   Использование параметра **WITH COMPRESSION** во время резервного копирования может уменьшить стоимость хранения и транзакционные издержки хранения. Также может сократиться время, необходимое для выполнения резервного копирования.  
  
## Обработка больших файлов  
  
-   Операция резервного копирования [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] выполняется в несколько потоков, чтобы оптимизировать передачу данных к службам хранилищ больших двоичных объектов Windows Azure.  Однако производительность зависит от различных факторов, в том числе от пропускной способности ISV и размера базы данных. Если планируется создавать резервные копии больших баз данных или файловых групп в локальной базе данных SQL Server, вначале рекомендуется проверить пропускную способность. В [соглашении об уровне обслуживания для службы хранилища Azure](http://azure.microsoft.com/support/legal/sla/storage/v1_0/) определены максимальные значения времени обработки для больших двоичных объектов, которыми можно руководствоваться.  
  
-   При создании резервных копий больших файлов очень важно использовать параметр **WITH COMPRESSION** в соответствии с рекомендациями, приведенными в разделе **Управление резервным копированием** .  
  
## Устранение неполадок при резервном копирование или восстановлении по URL-адресу  
 Ниже приведено несколько простых способов устранения ошибок при создании резервной копии или восстановлении из службы хранилища больших двоичных объектов Windows Azure.  
  
 Чтобы избежать ошибок из-за неподдерживаемых параметров или ограничений, просмотрите список ограничений и информацию о поддержке для команд BACKUP и RESTORE в статье [Резервное копирование и восстановление SQL Server с помощью службы хранилища BLOB-объектов Microsoft Azure](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md).  
  
 **Ошибки проверки подлинности:**  
  
-   WITH CREDENTIAL — это новый параметр, который необходимо использовать при создании резервных копий или восстановлении с помощью службы хранилища больших двоичных объектов Windows Azure. Ниже приводятся возможные ошибки, связанные с учетными данными.  
  
     Учетные данные, заданные в команде **BACKUP** или **RESTORE** , не существуют. Чтобы избежать этой проблемы, можно включить инструкцию T-SQL для создания учетных данных, если она отсутствует в инструкции резервного копирования. Ниже приводится пример, который можно использовать.  
  
    ```  
    IF NOT EXISTS  
    (SELECT * FROM sys.credentials   
    WHERE credential_identity = 'mycredential')  
    CREATE CREDENTIAL <credential name> WITH IDENTITY = 'mystorageaccount'  
    ,SECRET = '<storage access key> ;  
  
    ```  
  
-   Учетные данные существуют, но учетная запись, которая используется для запуска команды резервного копирования, не имеет разрешения доступа к учетным данным. Используйте учетную запись для входа в роль **db_backupoperator**с разрешением **Изменение любых учетных данных**.  
  
-   Проверьте имя учетной записи хранилища и значение ключа. Информация, которая хранится в учетных данных, должна соответствовать значениям свойств учетной записи хранилища Windows Azure, которые используются в операциях резервного копирования и восстановления.  
  
 **Ошибки и сбои резервного копирования:**  
  
-   Параллельное выполнение резервного копирования в один большой двоичный объект вызывает сбой одной из резервных копий с ошибкой **Ошибка инициализации** .  
  
-   Используйте следующие журналы об ошибке, чтобы помочь при устранении неполадок в резервных ошибках:  
  
    -   Установите флаг трассировки 3051, чтобы включить ведение записей в конкретном журнале ошибок в следующем формате:  
  
         BackupToUrl-\<instname>-\<dbname>-action-\<PID>.log, где \<action> может принимать одно из следующих значений:  
  
        -   **DB**  
  
        -   **FILELISTONLY**  
  
        -   **LABELONLY**  
  
        -   **HEADERONLY**  
  
        -   **VERIFYONLY**  
  
    -   Дополнительную информацию можно найти в журнале событий Windows или в журналах приложений с именем «SQLBackupToUrl».  
  
-   При восстановлении из сжатой резервной копии может появиться следующее сообщение об ошибке:  
  
    -   **Возникло SqlException 3284. Серьезность: 16, состояние: 5**  
        **Метка файла сообщения на устройстве https://mystorage.blob.core.windows.net/mycontainer/TestDbBackupSetNumber2_0.bak не согласована. Перезапустите инструкцию Restore с тем же размером блока, который использовался при создании резервного набора данных. Возможно, следует указать «65536».**  
  
         Чтобы устранить эту ошибку, издайте инструкцию **BACKUP** повторно и укажите для нее значение **BLOCKSIZE = 65536**.  
  
-   Ошибка во время архивации из-за больших двоичных объектов с активной арендой: сбой операции архивации может привести к появлению больших двоичных объектов с активными арендами.  
  
     Если эта инструкция резервного копирования повторяется, то операция резервного копирования может завершиться со следующей ошибкой:  
  
     **Резервное копирование на URL-адрес получило исключение из удаленной конечной точки. Сообщение об исключении: удаленный сервер возвратил ошибку: (412) в настоящее время существует аренда для большого двоичного объекта, однако для запроса не указан идентификатор аренды**.  
  
     Если инструкция восстановления выполнялись в резервном файле большого двоичного объекта с активной арендой, операция резервного копирования может завершиться со следующей ошибкой:  
  
     **Сообщение об исключении: удаленный сервер вернул ошибку: (409) конфликт…**  
  
     Если возникает такая ошибка, файлы больших двоичных объектов следует удалить. Дополнительные сведения об этом сценарии и устранении этой проблемы см. в разделе [Deleting Backup Blob Files with Active Leases](../../relational-databases/backup-restore/deleting-backup-blob-files-with-active-leases.md).  
  
## Ошибки прокси-сервера  
 При использовании прокси-серверов для доступа к Интернету возможны следующие проблемы.  
  
 **Регулирование соединений прокси-серверами.**  
  
 Прокси-серверы могут иметь параметры, ограничивающие количество соединений в минуту. Процесс резервного копирования на URL-адрес является многопоточным, в связи с чем заданное ограничение может быть превышено. В этом случае прокси-сервер разрывает соединение. Чтобы устранить эту проблему, измените параметры прокси-сервера таким образом, чтобы SQL Server его не использовал.   Далее приведено несколько примеров типов или сообщений об ошибках, которые можно встретить в журнале ошибок.  
  
-   Сбой записи в "http://storageaccount.blob.core.windows.net/container/BackupAzurefile.bak". При архивации на URL-адрес получено исключение из удаленной конечной точки. Сообщение об исключении: не удалось прочитать данные из транспортного соединения. Соединение было закрыто.  
  
-   Произошла неустранимая ошибка ввода-вывода в файле "http://storageaccount.blob.core.windows.net/container/BackupAzurefile.bak". Не удалось получить данные ошибки из удаленной конечной точки.  
  
     Сообщение 3013, уровень 16, состояние 1, строка 2  
  
     Процесс BACKUP DATABASE завершается аварийно.  
  
-   BackupIoRequest::ReportIoError: ошибка записи в устройство резервного копирования http://storageaccount.blob.core.windows.net/container/BackupAzurefile.bak. Ошибка операционной системы. Процесс резервного копирования на URL-адрес получил исключение от удаленной конечной точки. Сообщение об исключении: не удалось прочитать данные из транспортного соединения. Соединение было закрыто.  
  
 Если включить подробный уровень ведения журнала с помощью флага трассировки 3051, то в журналы также может быть занесено следующее сообщение.  
  
 Код состояния HTTP 502, ошибка прокси-сервера сообщения о состоянии HTTP (количество HTTP-запросов в минуту превышает установленный предел. Обратитесь к администратору сервера ISA.  )  
  
 **Параметры прокси-сервера по умолчанию не используются.**  
  
 Иногда, если не выбраны параметры по умолчанию, это приводит к ошибкам аутентификации на прокси-сервере наподобие следующей: *Произошла неустранимая ошибка ввода-вывода в файле "http://storageaccount.blob.core.windows.net/container/BackupAzurefile.bak". При архивации на URL-адрес получено исключение из удаленной конечной точки. Сообщение об исключении: удаленный сервер вернул ошибку: (407)* **требуется аутентификация на прокси-сервере**.  
  
 Чтобы устранить эту проблему, создайте файл конфигурации, позволяющий процессу резервного копирования по URL-адресу использовать параметры прокси-сервера по умолчанию. Для этого выполните следующие действия.  
  
1.  Создайте файл конфигурации BackuptoURL.exe.config со следующим XML-кодом:  
  
    ```  
    <?xml version ="1.0"?>  
    <configuration>   
                    <system.net>   
                                    <defaultProxy enabled="true" useDefaultCredentials="true">   
                                                    <proxy usesystemdefault="true" />   
                                    </defaultProxy>   
                    </system.net>  
    </configuration>  
  
    ```  
  
2.  Поместите файл конфигурации в папку Binn на экземпляре SQL Server. Например, если SQL Server установлен на диске C компьютера, поместите файл конфигурации сюда: *C:\Program Files\Microsoft SQL Server\MSSQL13.\<имя_экземпляра>\>\MSSQL\Binn*.  
  
## См. также:  
 [Восстановление из резервных копий в Microsoft Azure](../../relational-databases/backup-restore/restoring-from-backups-stored-in-microsoft-azure.md)  
[BACKUP (Transact-SQL)](../../t-sql/statements/backup-transact-sql.md)  
[RESTORE (Transact-SQL)](RESTORE%20\(Transact-SQL\).md)
  