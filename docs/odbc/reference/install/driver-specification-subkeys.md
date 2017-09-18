---
title: "Драйвер спецификации подразделов | Документы Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- subkeys [ODBC], driver specification subkeys
- driver specification subkeys [ODBC]
- registry entries for components [ODBC], driver specification subkeys
- drivers subkey [ODBC]
ms.assetid: b4d802ef-b199-4e64-b7a5-6f2b3e5e2c80
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f45130c81f9fc4f669cf95d4bde72155f519c1aa
ms.contentlocale: ru-ru
ms.lasthandoff: 09/09/2017

---
# <a name="driver-specification-subkeys"></a>Спецификация подразделы драйверов
Каждый драйвер, перечисленных в подразделе драйверы ODBC имеется подраздел свои собственные. Этот подраздел содержит имя, совпадающее с именем соответствующего значения в подразделе драйверов ODBC. Значения в этом подразделе перечислены полные пути драйвера и установки драйвера библиотеки DLL, значения ключевых слов драйвера, возвращенных **SQLDrivers**, а счетчик использования. Форматы значений, как показано в следующей таблице.  
  
|Имя|Тип данных|data|  
|----------|---------------|----------|  
|APILevel|REG_SZ|**0** &#124; **1** &#124; **2**|  
|ConnectFunctions|REG_SZ|{**Y**&#124;** N**} {**Y**&#124;** N**} {**Y**&#124;** N**}|  
|CreateDSN|REG_SZ|*Описание драйвера*|  
|Драйвер|REG_SZ|*путь к библиотеке DLL драйвера*|  
|DriverODBCVer|REG_SZ|*nn.nn*|  
|FileExtns|REG_SZ|**\*.** *файл extension1*[**,\*.** *файл extension2*]...|  
|FileUsage|REG_SZ|**0** &#124; **1** &#124; **2**|  
|Программа установки|REG_SZ|*путь к библиотеке DLL установки*|  
|SQLLevel|REG_SZ|**0** &#124; **1** &#124; **2**|  
|UsageCount|REG_DWORD|*count*|  
  
 В следующей таблице показано использование каждого из ключевых слов.  
  
|Ключевое слово|Использование|  
|-------------|-----------|  
|**APILevel**|Число, указывающее ODBC интерфейса уровень соответствия, поддерживаемых драйвером:<br /><br /> 0 = нет<br /><br /> 1 = поддерживается уровня 1<br /><br /> 2 = поддерживается уровня 2<br /><br /> Это должен быть таким же, как значение, возвращаемое для параметра SQL_ODBC_INTERFACE_CONFORMANCE в **SQLGetInfo**.|  
|**CreateDSN**|Имя одного или нескольких источников данных, создаваемый при установке драйвера. Сведения о системе должен включать один раздел спецификации источника данных для каждого источника данных, в списке **CreateDSN** ключевое слово. В этих разделах не должно содержать **драйвер** ключевое слово, так как это указано в разделе спецификации драйвера, но должны содержать достаточно информации для **ConfigDSN** функции в драйвере DLL-файлов для создания спецификации источника данных без отображения все диалоговые окна установки. Формат раздела спецификации источника данных, в разделе [подразделов спецификации источника данных](../../../odbc/reference/install/data-source-specification-subkeys.md).|  
|**ConnectFunctions**|Строка трех символов, указывающее, поддерживает ли драйвер **SQLConnect**, **SQLDriverConnect**, и **SQLBrowseConnect**. Если драйвер поддерживает **SQLConnect**, первым символом «Y»; в противном случае это «N». Если драйвер поддерживает **SQLDriverConnect**, второй символ «Y»; в противном случае это «N». Если драйвер поддерживает **SQLBrowseConnect**, третьего знака: «Y»; в противном случае — значение «N». Например, если драйвер поддерживает **SQLConnect** и **SQLDriverConnect** , но не **SQLBrowseConnect**, строка трех символов — «YYN».|  
|**DriverODBCVer**|Строка символов с помощью версии ODBC, который поддерживает драйвер. Версия представляется в виде *nn.nn*, где первые две цифры являются основной номер версии, а две следующие — дополнительный номер версии. Для версии ODBC, описанные в данном руководстве драйвер должен возвращать «03.00».<br /><br /> Это должен быть таким же, как значение, возвращаемое для параметра SQL_DRIVER_ODBC_VER в **SQLGetInfo**.|  
|**FileExtns**|Для драйверов на основе файлов разделенных запятыми список расширений файлов, драйвер может использовать. Например, указать драйвер dBASE \*.dbf и форматированный текст файла драйвера может указать \*.txt,\*CSV-файл. Пример того, как приложение может использовать эти сведения см. в разделе **FileUsage** ключевое слово.|  
|**FileUsage**|Число, указывающее, как драйвер файловых напрямую обрабатывает файлы в источнике данных.<br /><br /> 0 = драйвер не является файловым драйвером. Например драйвер ORACLE — это драйвер на основе СУБД.<br /><br /> 1 = файлы будет обрабатываться на основе файла драйвера в источнике данных, как таблицы. Например драйвер Xbase считает каждый файл Xbase таблицы.<br /><br /> 2 = файлов будет обрабатываться на основе файла драйвера в источнике данных как каталог. Например драйвер Microsoft® Access считает каждый файл Microsoft Access всей базы данных.<br /><br /> Приложения можно использовать для определения того, как пользователи будут выбирать данные. Например Xbase и Paradox пользователи часто прибегают к данных, хранящихся в файлах, пока ORACLE и Microsoft Access пользователей обычно обработки данных, хранящихся в таблицах.<br /><br /> Когда пользователь выбирает **открыть файл данных** из **файл** меню, приложение может отображать **Windows по открытию** стандартным диалоговым окном. Список типов файлов использовать расширений файлов, указанных с **FileExtns** ключевое слово для драйверов, которые указывают **FileUsage** значение 1 и «Y» как второй знак значения ** ConnectFunctions** ключевое слово. После пользователь выбирает файл, приложение может вызвать **SQLDriverConnect** с **ДРАЙВЕР** ключевое слово, а затем выполните **ВЫБЕРИТЕ \* FROM *имя таблицы * ** инструкции.<br /><br /> Когда пользователь выбирает **импорта данных** из **файл** меню, приложение может отображать список описаний для драйверов, которые указывают **FileUsage** значение 0 или 2 и «Y» как второй знак значения **ConnectFunctions** ключевое слово. После пользователь выбирает драйвер, приложение может вызвать **SQLDriverConnect** с **ДРАЙВЕР** ключевое слово и затем отображения пользовательского **Выбор таблицы** диалоговое окно.|  
|**SQLLevel**|Число, указывающее грамматику SQL-92, поддерживаемых драйвером:<br /><br /> 0 = SQL-92 запись<br /><br /> 1 = переходные FIPS127-2<br /><br /> 2 = SQL-92 промежуточное<br /><br /> 3 = Полный SQL-92<br /><br /> Это должен быть таким же, как значение, возвращаемое для параметра SQL_SQL_CONFORMANCE в **SQLGetInfo**.|  
  
 Сведения о счетчиках использования см. в разделе [об использовании инвентаризации](../../../odbc/reference/install/usage-counting.md) ранее в этом разделе.  
  
 Приложение не может установить счетчик использования. ODBC поддерживает это число.  
  
 Например предположим, что драйвер для файлов форматированный текст имеет драйвер DLL с именем Text.dll, установки отдельного драйвера DLL с именем Txtsetup.dll и установлен в три раза. Если драйвер поддерживает уровень соответствия API уровня 1, поддерживает уровень соответствия грамматики минимальную SQL, обрабатывает файлы как таблицы и можно использовать файлы с расширениями txt и CSV, значения в подразделе текст может выглядеть следующим образом:  
  
```  
APILevel : REG_SZ : 1  
ConnectFunctions : REG_SZ : YYN  
Driver : REG_SZ : C:\WINDOWS\SYSTEM32\TEXT.DLL  
DriverODBCVer : REG_SZ : 03.00.00  
FileExtns : REG_SZ : *.txt,*.csv  
FileUsage : REG_SZ : 1  
Setup : REG_SZ : C:\WINDOWS\SYSTEM32\TXTSETUP.DLL  
SQLLevel : REG_SZ : 0  
UsageCount : REG_DWORD : 0x3  
```