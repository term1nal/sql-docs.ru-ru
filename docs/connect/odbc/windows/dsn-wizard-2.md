---
title: "Экран мастера 2 (драйвер ODBC для SQL Server) источника данных | Документы Microsoft"
ms.custom: 
ms.date: 09/27/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 76326eeb-1144-4b9f-85db-50524c655d30
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: ea362cd05de5d1ba17ca717d94354d5786119bab
ms.openlocfilehash: e861bc52621e520a27e930dd22f1a1eb9613cc76
ms.contentlocale: ru-ru
ms.lasthandoff: 10/06/2017

---
# <a name="data-source-wizard-screen-2"></a>Экран 2 мастера источников данных

Укажите метод проверки подлинности и настройте записи расширенного клиента Microsoft SQL Server и имя входа и пароль, который будет использовать драйвер ODBC для SQL Server для подключения к SQL Server во время настройки источника данных.

## <a name="options"></a>Параметры

### <a name="with-integrated-windows-authentication"></a>С помощью встроенной проверки подлинности Windows

Указывает, что драйвер запрашивать безопасное (или доверительное) соединение с SQL Server. Если выбран данный режим, при установке соединений с использованием данного источника данных SQL Server будет использовать встроенную систему безопасности входа в систему, вне зависимости от того, какой режим безопасности установлен на сервере. Не учитываются любые предоставляемые идентификаторы входа и пароли. Системный администратор SQL Server должен связать имя входа Windows с Идентификатором имени входа SQL Server (например, с помощью SQL Server Management Studio).

Дополнительно можно указать для сервера имя участника-службы.

### <a name="with-active-directory-integrated-authentication"></a>С помощью встроенной проверки подлинности Active Directory

Указывает, что драйвер пройти проверку подлинности SQL Server с помощью Azure Active Directory. При выборе SQL Server использует Azure Active Directory интегрированной безопасности входа в систему для установления соединения, использующие этот источник данных, независимо от того, какой режим безопасности входа в систему на сервере.

### <a name="with-sql-server-authentication"></a>С помощью проверки подлинности SQL Server

Указывает, что драйвер пройти проверку подлинности SQL Server с помощью идентификатора входа и пароль.

### <a name="with-active-directory-password-authentication"></a>С помощью проверки подлинности пароль Active Directory

Указывает, что драйвер пройти проверку подлинности SQL Server с помощью Azure Active Directory идентификатор входа и пароль.

### <a name="login-id"></a>Идентификатор входа

Указывает идентификатор входа, драйвер использует при подключении к SQL Server, если **с проверкой подлинности SQL Server с помощью идентификатора входа и пароль, введенный пользователем** или **с использованием идентификатора входа проверки подлинности пароль с Active Directory и пароль, введенный пользователем** выбран. Это относится только к соединениям, установленным для определения настроек по умолчанию сервера; это не относится к последующим соединениям, установленным с использованием данного источника данных, после того как он был создан.

### <a name="password"></a>Пароль

Указывает пароль, драйвер использует при подключении к SQL Server, если **с проверкой подлинности SQL Server с помощью идентификатора входа и пароль, введенный пользователем** или **с использованием идентификатора входа проверки подлинности пароль с Active Directory и пароль, введенный пользователем** выбран. Это относится только к соединениям, установленным для определения настроек по умолчанию сервера; это не относится к последующим соединениям, установленным с использованием нового источника данных.

Оба **идентификатора входа** и **пароль** будут отключены, если **с помощью встроенной проверки подлинности Windows** или **с интегрированные службы Active Directory Проверка подлинности** выбран.

### <a name="next"></a>Дальше

Переход к следующей странице мастера.

### <a name="back"></a>Назад

Возврат к предыдущему экрану мастера.

## <a name="next-steps"></a>Следующие шаги

[Первый экран мастера источника данных](../../../connect/odbc/windows/dsn-wizard-1.md)

[Мастер источника данных 3](../../../connect/odbc/windows/dsn-wizard-3.md)

