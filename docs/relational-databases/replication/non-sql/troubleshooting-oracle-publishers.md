---
title: "Диагностика издателей Oracle | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "публикация Oracle [репликация SQL Server], устранение неполадок"
  - "устранение неполадок [репликация SQL Server], публикация Oracle"
ms.assetid: be94f1c1-816b-4b1d-83f6-2fd6f5807ab7
caps.latest.revision: 62
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 62
---
# Диагностика издателей Oracle
  В этой теме рассматривается ряд вопросов, которые могут возникнуть при настройке и использовании издателя Oracle.  
  
## Ошибка, касающаяся клиентского и сетевого программного обеспечения Oracle  
 Учетная запись, под которой [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] запускается на распространителе, должны быть разрешения на чтение и выполнение разрешения для каталога (и всех подкаталогов), в котором установлено клиентское сетевое по Oracle. Если разрешения не предоставляются или клиентские компоненты Oracle не установлены должным образом, пользователь получает следующее сообщение об ошибке:  
  
 «Не удалось подключиться к серверу с помощью [поставщика Microsoft OLE DB для Oracle]. Клиентские и сетевые компоненты Oracle не найдены. Эти компоненты поставляются корпорацией Oracle и являются частью установочного пакета клиентского программного обеспечения Oracle 7.3.3 или более поздней версии. Поставщик не может функционировать, пока эти компоненты не будут установлены».  
  
 Если на распространителе устанавливается подходящее клиентское программное обеспечение Oracle, то убедитесь в том, что [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] остановлен, а затем перезапустите его после завершения установки клиентского ПО. Это необходимо [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] для распознавания клиентских компонентов.  
  
 Если проверено, что эти разрешения предоставлены и что компоненты установлены должным образом, но эта ошибка продолжает возникать, убедитесь в правильности значений настроек в разделе реестра HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDTC\MTxOCI.  
  
-   Для Oracle 10g правильными являются следующие значения настроек:  
  
    -   OracleOciLib = oci.dll  
  
    -   OracleSqlLib = orasql10.dll  
  
    -   OracleXaLib = oraclient10.dll  
  
-   Для Oracle 9i правильными являются следующие значения настроек:  
  
    -   OracleOciLib = oci.dll  
  
    -   OracleSqlLib = orasql9.dll  
  
    -   OracleXaLib = oraclient9.dll  
  
## Распространителю SQL Server не удается подключиться к экземпляру базы данных Oracle  
 Если распространителю [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] не удается подключиться к издателю Oracle, необходимо убедиться в следующем:  
  
-   Необходимое программное обеспечение Oracle установлено на распространителе.  
  
-   База данных Oracle доступна в режиме в «сети» и к ней не удается подключиться при помощи такого средства, как SQL*Plus.  
  
-   Имя входа, которое репликация использует для подключения к издателю Oracle, имеет достаточно разрешений. Дополнительные сведения см. в разделе [настроить издатель Oracle](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md).  
  
-   Имена TNS, определенные во время настройки издателя Oracle, приводятся в файле tnsnames.ora.  
  
-   Используются правильные значения Oracle Home и пути. Даже если есть только один набор исполняемых файлов Oracle, установленных на распространителе [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], проверьте, чтобы были правильно установлены переменные среды, относящиеся к Oracle Home. При изменении значений переменных среды необходимо остановить и перезапустить [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], чтобы эти изменения вступили в действие.  
  
 Дополнительные сведения о настройке и проверке подключения см. в разделе «Установка и настройка клиентского сетевого по Oracle на [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] распространителя» в [настроить издатель Oracle](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md).  
  
## Издатель Oracle связан с другим распространителем  
 Издатель Oracle может быть связан только с одним распространителем [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Если с издателем Oracle связан иной распространитель, он должен быть удален перед использованием другого распространителя. Если вначале не удалить распространитель, выводится одно из следующих сообщений об ошибке:  
  
-   «Экземпляр сервера oracle "\<*OraclePublisherName*>" был ранее настроен на использование ' \<*SQLServerDistributorName*> "в качестве своего распространителя. Чтобы начать работу с "\<*NewSQLServerDistributorName*>" в качестве своего распространителя, необходимо удалить текущую конфигурацию репликации на экземпляре сервера Oracle, будут удалены все публикации на этом экземпляре сервера.»  
  
-   «Сервер oracle "\<*OracleServerName*>" уже определен в качестве издателя "\<*OraclePublisherName*>" на распространителе "\<*SQLServerDistributorName*>.*\< Имябазыданныхраспространителя>*". Удалите издатель или общий синоним "*\< ИмяСинонима>*" для повторного создания.»  
  
 При удалении издателя Oracle объекты репликации в базе данных Oracle автоматически очищаются. Однако в некоторых случаях необходима ручная очистка объектов репликации Oracle. Для ручной очистки объектов репликации Oracle, созданных при репликации, выполните следующее:  
  
1.  Подключитесь к издателю Oracle с разрешениями администратора базы данных.  
  
2.  Выполните команду SQL `DROP PUBLIC SYNONYM MSSQLSERVERDISTRIBUTOR;`.  
  
3.  Выполните команду SQL `DROP USER <replication_administrative_user_schema>``CASCADE;`.  
  
## Ошибка SQL Server 21663 возникает из-за отсутствия первичного ключа  
 Статьи в публикациях транзакций должны иметь правильный первичный ключ. Если они не имеют правильного первичного ключа, при попытке добавления статьи выдается следующее сообщение об ошибке:  
  
 «Найти допустимый первичный ключ для исходной таблицы [\<*ВладелецТаблицы*>]. [ \<*TableName*>]»  
  
 Дополнительные сведения о требованиях для первичных ключей см. в подразделе «Уникальные индексы и ограничения» раздела [вопросы проектирования и ограничений издателей Oracle](../../../relational-databases/replication/non-sql/design-considerations-and-limitations-for-oracle-publishers.md).  
  
## Ошибка SQL Server 21642, связанная с повторяющимся именем входа связанного сервера  
 При первоначальной настройке издателя Oracle создается запись связанного сервера для соединения издателя и распространителя. Связанный сервер имеет то же имя, что и служба Oracle TNS. При попытке создать связанный сервер с тем же именем выводится следующее сообщение об ошибке:  
  
 «Для разнородных издателей необходим связанный сервер. Связанный сервер с именем "*\< ИмяСвязанногоСервера>*" уже существует. Удалите связанный сервер или выберите другое имя издателя».  
  
 Эта ошибка может возникнуть при попытке непосредственно создать связанный сервер, или если ранее была удалена связь между издателем Oracle и распространителем [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], и теперь предпринимается попытка перенастроить издатель. Если эта ошибка появляется при попытке перенастроить издатель, удалите связанный сервер с [sp_dropserver & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-dropserver-transact-sql.md).  
  
 Если необходимо подключиться к издателю Oracle через соединение связанного сервера, создайте другое имя службы TNS и затем использовать это имя при вызове [sp_addlinkedserver & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md). Сведения о создании имен службы TNS см. в документации Oracle.  
  
## Ошибка SQL Server 21617  
 Публикация Oracle использует приложение Oracle SQL*PLUS для загрузки пакета вспомогательного кода издателя в базу данных Oracle. Перед попыткой настроить издатель Oracle [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] проверяет, что SQL\*а также доступны по системному пути на распространителе. Если SQL\*а также не может быть загружена, отображается следующее сообщение об ошибке:  
  
 «Не удается запустить SQL*PLUS. Убедитесь, что на распространителе установлена текущая версия клиентской программы Oracle».  
  
 Попытайтесь найти SQL\*PLUS на распространителе. Для установки клиента Oracle 10g имя этого исполняемого файла — sqlplus.exe. Обычно данная программа устанавливается в каталог %ORACLE_HOME%/bin. Чтобы убедиться, что путь SQL\*PLUS содержится в системном пути, проверьте значение системной переменной **пути**:  
  
1.  Щелкните правой кнопкой мыши **Мой компьютер**, а затем нажмите кнопку **Свойства**.  
  
2.  Щелкните **Дополнительно** а затем щелкните **переменные среды**.  
  
3.  В **переменные среды** диалогового **системные переменные** выберите **путь** переменной, а затем щелкните **Изменить**.  
  
4.  В **Изменение системной переменной** диалоговое окно: Если путь к папке, содержащей sqlplus.exe не присутствует в **значение переменной** текстовое поле, измените строку, чтобы включить его.  
  
5.  Щелкните **ОК** на каждом открытом диалоговом чтобы выйти и сохранить изменения.  
  
 Если на распространителе не удается найти sqlplus.exe, установите на распространителе текущую версию клиентского программного обеспечения Oracle. Дополнительные сведения см. в разделе [настроить издатель Oracle](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md).  
  
## Ошибка SQL Server 21620  
 При соединении с базой данных Oracle, версия которой предшествует версии 8.1, для публикации Oracle необходимо, чтобы версия клиентского программного обеспечения Oracle, установленного на распространителе, была не ниже 9. При соединении с базой данных Oracle 8.1 или более поздней версии рекомендуется, чтобы версия клиентского программного обеспечения Oracle была не ниже 10.  
  
 Перед попыткой настройки издателя Oracle выполняется проверка того, что версия SQL*PLUS, доступная по системному пути на распространителе, не ниже 9. Если это не так, выводится следующее сообщение об ошибке:  
  
 «Версия SQL*PLUS, доступная через переменную системного пути, в настоящее время недостаточна для поддержки публикации Oracle. Убедитесь, что на распространителе установлена текущая версия клиентской программы Oracle».  
  
 Если на распространителе установлено несколько версий клиентского программного обеспечения Oracle, убедитесь, что самая последняя версия не ниже 9, и что переменная системного пути ссылается вначале на эту версию (ссылки на другие версии могут использоваться, если самая последняя версия располагается первой). Дополнительные сведения о редактировании переменной системного пути см. в приводимом выше разделе «Ошибка SQL Server 21617».  
  
## Ошибка SQL Server 21624 или 21629  
 Для 64-разрядных распространителей публикация Oracle использует поставщика Oracle OLEDB для Oracle (OraOLEDB.Oracle). Убедитесь, что поставщик OLEDB для Oracle установлен и зарегистрирован на распространителе. Если поставщик не установлен и не зарегистрирован, появляется одно из следующих сообщений, или оба эти сообщения:  
  
-   «Не удается найти зарегистрированный поставщик OLEDB для Oracle (OraOLEDB.Oracle) на распространителе '%s'. Убедитесь, что на распространителе установлена и зарегистрирована текущая версия поставщика OLEDB для Oracle».  
  
-   «Раздел реестра CLSID, указывающий, что поставщик OLEDB для Oracle (OraOLEDB.Oracle) был зарегистрирован, но отсутствует на распространителе. Убедитесь, что на распространителе установлен и зарегистрирован поставщик OLEDB для Oracle».  
  
 Если используется клиентское программное обеспечение Oracle версии 10g, поставщиком является OraOLEDB10.dll, для версии 9i — это OraOLEDB.dll. Поставщик устанавливается в каталог %ORACLE_HOME%\BIN (например, в «C:\oracle\product\10.1.0\Client_1\bin»). Если обнаружено, что поставщик Oracle OLEDB не установлен на распространителе, установите его с установочного диска клиентского программного обеспечения Oracle, предоставляемого корпорацией Oracle. Дополнительные сведения см. в разделе [настроить издатель Oracle](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md).  
  
 Если поставщик Oracle OLEDB установлен, убедитесь, что он зарегистрирован. Для регистрации DLL-библиотеки поставщика выполните следующую команду из каталога, в котором установлена DLL-библиотека, а затем остановите и перезапустите экземпляр [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]:  
  
1.  `regsvr32 OraOLEDB10.dll` или `regsvr32 OraOLEDB.dll`.  
  
## Возникает ошибка SQL Server 21626 или 21627  
 Чтобы убедиться, что издательская среда Oracle настроена верно, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] пытается подключиться к издателю Oracle с учетными данными, которые были указаны во время настройки. Если распространителю [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] не удается подключиться к издателю Oracle, появляется одно из следующих сообщений:  
  
-   «Невозможно подключиться к серверу базы данных Oracle "%s" с помощью поставщика OLEDB для Oracle (OraOLEDB.Oracle)».  
  
 При появлении этих сообщений проверьте подключение к базе данных Oracle, непосредственно запустив SQL*PLUS при помощи тех же имени входа и пароля, которые были указаны во время настройки издателя Oracle. Дополнительные сведения см. выше, в подразделе «Распространителю SQL Server не удается подключиться к экземпляру базы данных Oracle» этого раздела.  
  
## Ошибка SQL Server 21628  
 Для 64-разрядных распространителей публикация Oracle использует поставщика Oracle OLEDB для Oracle (OraOLEDB.Oracle). [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] создает запись реестра, чтобы разрешить поставщику Oracle выполнять процесс с [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. При наличии проблем с чтением этой записи реестра или занесением данных в эту запись выводится следующее сообщение об ошибке:  
  
 «Не удалось обновить реестр распространителя "%s", чтобы позволить поставщику OLEDB для Oracle (OraOLEDB.Oracle) запускаться в процессе с [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Убедитесь, что пользователю с текущим именем входа разрешается вносить изменения в разделы реестра, принадлежащие [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]».  
  
 Публикации Oracle необходимо, параметр реестра существует и будет присвоено **1** для 64-разрядных распространителей. Если запись не существует, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] будет пытаться создать ее. Если запись существует, но имеет значение **0**, параметр не будет изменен, настройки издателя Oracle завершится сбоем.  
  
 Для просмотра и изменения установки реестра выполните следующие действия:  
  
1.  Нажмите кнопку **Пуск**, затем щелкните **Выполнить**.  
  
2.  В **запуска** диалоговом **regedit**, а затем нажмите кнопку **ОК**.  
  
3.  Перейдите в HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\\*\< имя_экземпляра>*\Providers.  
  
     В папке для поставщиков (Providers) должна находиться папка с именем OraOLEDB.Oracle. В этой папке должен быть значение DWORD **AllowInProcess**, со значением **1**.  
  
4.  Если выяснилось, что **AllowInProcess** равен **0**, обновите запись реестра для **1**:  
  
    1.  Щелкните правой кнопкой мыши запись и нажмите кнопку **Изменить**.  
  
    2.  В **Изменение строки** диалоговом **1** в **значение** поле.  
  
## Возникает ошибка SQL Server 21684  
 Если административная учетная запись пользователя не имеет достаточных прав доступа, выводится следующее сообщение об ошибке:  
  
 «Разрешений, связанных с именем входа администратора для издателя Oracle «%s», недостаточно».  
  
 Чтобы проверить разрешения, предоставленные пользователю, выполните следующий запрос: `SELECT * from session_privs`. Результат выполнения должен быть аналогичен следующему:  
  
 `PRIVILEGE`  
  
 `------------------`  
  
 `CREATE SESSION`  
  
 `CREATE TABLE`  
  
 `CREATE PUBLIC SYNONYM`  
  
 `DROP PUBLIC SYNONYM`  
  
 `CREATE VIEW`  
  
 `CREATE SEQUENCE`  
  
 `CREATE PROCEDURE`  
  
 `CREATE TRIGGER`  
  
## Проблемы, связанные с разрешениями для пользовательской схемы репликации  
 Схема пользователей репликации должна иметь разрешения, описанные в «Создание пользовательской схемы вручную» в [настроить издатель Oracle](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md).  
  
## Ошибка Oracle ORA-01000  
 Репликация использует курсоры в издателе Oracle в процессе добавления статей в публикацию. Во время этого процесса возможно превышение максимально допустимого количества курсоров, доступных на издателе. Если это происходит, возникает следующая ошибка:  
  
 «ORA-01000: превышение максимального числа открытых курсоров»  
  
 Чтобы избежать этой проблемы, убедитесь, что **max_open_cursors** в базах данных Oracle установлено достаточно большое число (по крайней мере, 1000). Дополнительные сведения об этой установке приводятся в документации Oracle.  
  
## Ошибка Oracle ORA-01555  
 Следующая ошибка базы данных Oracle относится не к репликации моментального снимка, а к тому, как Oracle строит подходящие для чтения представления данных:  
  
 "ORA-01555: слишком старый моментальный снимок"  
  
 При помощи объектов, называемых сегментами отката, Oracle создает пригодные для чтения представления данных на момент выдачи инструкции SQL. Ошибка «слишком старый моментальный снимок» может возникнуть, если данные отката переписываются другими, одновременно выполняющими сеансами. До версии Oracle 9i для уменьшения частоты появления этой ошибки рекомендовался метод увеличения размера или количества сегментов отката и назначения больших транзакций для определенных сегментов отката.  
  
 В Oracle 9i корпорация Oracle ввела концепцию табличного пространства UNDO, заменяющую сегмент отката. Для предотвращения ошибки «слишком старый моментальный снимок» в Oracle 9i рекомендуется следующее:  
  
-   Создайте табличное пространство UNDO с достаточным количеством свободного места.  
  
-   Установите гарантию хранения для табличного пространства (для версий Oracle 10G и выше).  
  
-   Настройте параметры инициализации Oracle UNDO_MANAGEMENT и UNDO_RETENTION.  
  
 Дополнительные сведения об исключении причин ошибки «слишком старый моментальный снимок» см. в документации Oracle.  
  
## Ошибка Oracle ORA-22285  
 Если в таблице имеется столбец BFILE, данные для столбца хранятся в файловой системе. Административной учетной записи репликации должно быть предоставлено право доступа в каталог, в котором хранятся данные. С этой целью должно использоваться следующее синтаксическое выражение:  
  
 `GRANT READ ON DIRECTORY <directory_name> TO <replication_administrative_user_schema>`  
  
 Если право доступа не предоставлено, агент чтения журнала выводит следующее сообщение об ошибке:  
  
 «ORA-22285: несуществующий каталог или файл для операции FILEOPEN»  
  
## Выполнены изменения, требующие перенастройки издателя  
 Для изменения таблиц метаданных репликации или процедур необходимо удалить и перенастроить издатель. Чтобы перенастроить издатель, необходимо удалить издатель и настроить его вновь при помощи среды [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], Transact-SQL или объектов RMO. Сведения о настройке издателя см. в разделе [настроить издатель Oracle](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md).  
  
 **Для удаления издателя Oracle (**SQL Server Management Studio**)**  
  
1.  Подключитесь к распространителю для издателя Oracle в среде [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], а затем раскройте узел сервера.  
  
2.  Щелкните правой кнопкой мыши **репликации**, а затем нажмите кнопку **Свойства распространителя**.  
  
3.  На **издателей** Страница **Свойства распространителя** диалоговом снимите флажок для издателя Oracle.  
  
4.  Нажмите кнопку **ОК**.  
  
 **Удаление издателя Oracle (Transact-SQL)**  
  
-   Выполнение **sp_dropdistpublisher**. Дополнительные сведения см. в разделе [sp_dropdistpublisher & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md).  
  
## См. также:  
 [Настройка издателя Oracle](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)   
 [Обзор публикации Oracle](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md)  
  
  