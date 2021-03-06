---
title: Требования к системе для драйвера JDBC | Документация Майкрософт
ms.custom: ''
ms.date: 07/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 447792bb-f39b-49b4-9fd0-1ef4154c74ab
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a2ddf8f5c03d6f4c6724075e7209d800e10f7e39
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ru-RU
ms.lasthandoff: 10/01/2018
ms.locfileid: "47724302"
---
# <a name="system-requirements-for-the-jdbc-driver"></a>Требования к системе для драйвера JDBC
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Чтобы получить доступ к данным из базы данных [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] или [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] с помощью драйвера [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], на компьютере должны быть установлены следующие компоненты:

- [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] ([скачать](download-microsoft-jdbc-driver-for-sql-server.md))
- Среда выполнения Java

## <a name="java-runtime-environment-requirements"></a>Требования к среде выполнения Java  
 Начиная с версии Microsoft JDBC Driver 7.0 для SQL Server реализована поддержка пакета SDK для Sun Java SE (JDK) 10.0 и среды выполнения Java (JRE) 10.0.

 Начиная с версии Microsoft JDBC Driver 6.4 для SQL Server поддерживается пакет SDK для Sun Java SE (JDK) 9.0 и среда выполнения Java (JRE) 9.0.

 Начиная с версии Microsoft JDBC Driver 4.2 для SQL Server, поддерживается пакет SDK для Sun Java SE (JDK) 8.0 и среда выполнения Java (JRE) 8.0. Поддержка спецификации API JDBC была расширена за счет включения API JDBC 4.1 и 4.2.  
  
 Начиная с версии Microsoft JDBC Driver 4.1 для SQL Server, поддерживается пакет SDK для Sun Java SE (JDK) 7.0 и среда выполнения Java (JRE) 7.0.  
  
 Начиная с [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)] поддержка спецификации API Java Database Connectivity (JDBC) была расширена до API JDBC 4.0. Версия API JDBC 4.0 впервые появилась в составе комплекта разработчика Sun Java SE (JDK) 6.0 и среды выполнения Java (JRE) 6.0. JDBC 4.0 является супермножеством API JDBC 3.0.  
  
 При развертывании [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] в операционных системах Windows и UNIX необходимо использовать пакеты установки *sqljdbc_\<версия>_enu.exe* и *sqljdbc_\<версия>_enu.tar.gz* соответственно. Дополнительные сведения о развертывании драйвера JDBC см. в разделе [развертывание драйвера JDBC](../../connect/jdbc/deploying-the-jdbc-driver.md) раздела.  
  
**Microsoft JDBC Driver 7.0 для SQL Server**  

  Драйвер JDBC 7.0 содержит две библиотеки классов JAR в каждом пакете установки: **mssql-jdbc-7.0.0.jre8.jar** и **mssql-jdbc-7.0.0.jre10.jar**.

  JDBC Driver 7.0 рассчитан на совместимость и корректную работу со всеми основными эквивалентами виртуальных машин Java от Sun, но протестирован только в Sun JRE 8.0 и 10.0.
  
  В следующей таблице приведены сводные данные о поддержке, которую обеспечивают два JAR-файла в составе Microsoft JDBC Driver 7.0 для SQL Server:  
  
  |JAR|Соответствие версии JDBC|Рекомендуемая версия Java|Описание|  
|---------|-----------------------------|----------------------|-----------------|   
|mssql-jdbc-7.0.0.jre8.jar|4.2|8|Требуется среда выполнения Java (JRE) версии 8.0. Использование JRE 7.0 или ниже выдает исключение.<br /><br /> Новые возможности в 7.0 включают: поддержка JDK 10, уровень совместимости по умолчанию обновлен для спецификации JDBC 4.2, поддержка пространственных типов данных, свойство соединения cancelQueryTimeout, запросить границ методов свойство useBulkCopyForBatchInsert соединения, данные Обнаружение и классификация сведения расширения компонента UTF-8 и поддержки CityHash. |    
|mssql-jdbc-7.0.0.jre10.jar|4.3|10|Требуется среда выполнения Java (JRE) 10.0. С помощью 9.0 с JRE или ниже выдает исключение.<br /><br /> Новые возможности в 7.0 включают: поддержка JDK 10, уровень совместимости по умолчанию обновлен для спецификации JDBC 4.2, поддержка пространственных типов данных, свойство соединения cancelQueryTimeout, запросить границ методов свойство useBulkCopyForBatchInsert соединения, данные Обнаружение и классификация сведения расширения компонента UTF-8 и поддержки CityHash. |    


  7.0 драйвер JDBC также доступна на центрального репозитория Maven и можно добавить в проект Maven, добавив следующий код в файл POM. XML:  
  
 ```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>7.0.0.jre10</version>
</dependency>
```      
  
**Microsoft JDBC Driver 6.4 для SQL Server**  

  Драйвер JDBC 6.4 содержит три библиотеки классов JAR в каждом пакете установки: **mssql-jdbc-6.4.0.jre7.jar**, **mssql-jdbc-6.4.0.jre8.jar** и **mssql-jdbc-6.4.0.jre9.jar**.

  JDBC Driver 6.4 рассчитан на поддержку всеми основными эквивалентами виртуальных машин Java Sun, однако протестирован только в Sun JRE 7.0, 8.0 и 9.0.
  
  В следующей таблице приводится сводная информация о поддержке, которую обеспечивают три JAR-файла, входящие в состав драйвера Microsoft JDBC Drivers 6.4 для SQL Server:  
  
  |JAR|Соответствие версии JDBC|Рекомендуемая версия Java|Описание|  
|---------|-----------------------------|----------------------|-----------------|   
|mssql-jdbc-6.4.0.jre7.jar|4.1|7|Требуется среда выполнения Java (JRE) версии 7.0. Использование JRE 6.0 или ниже выдает исключение.<br /><br /> Новые возможности в 6.4 включают: проверка подлинности Azure AD для Linux, метод субъект и пароль для автоматического обнаружения сферы в имени участника-службы для проверки подлинности между доменами, ограниченное делегирование Kerberos, время ожидания запроса, время ожидания сокета, Kerberos и подготовленных Дескриптор инструкции, повторного использования. |  
|mssql-jdbc-6.4.0.jre8.jar|4.2|8|Требуется среда выполнения Java (JRE) версии 8.0. Использование JRE 7.0 или ниже выдает исключение.<br /><br /> Новые возможности в 6.4 включают: проверка подлинности Azure AD для Linux, метод субъект и пароль для автоматического обнаружения сферы в имени участника-службы для проверки подлинности между доменами, ограниченное делегирование Kerberos, время ожидания запроса, время ожидания сокета, Kerberos и подготовленных Дескриптор инструкции, повторного использования. |    
|mssql-jdbc-6.4.0.jre9.jar|4.3|9|Требуется среда выполнения Java (JRE) версии 9.0. Использование JRE 8.0 или ниже выдает исключение.<br /><br /> Новые возможности в 6.4 включают: проверка подлинности Azure AD для Linux, метод субъект и пароль для автоматического обнаружения сферы в имени участника-службы для проверки подлинности между доменами, ограниченное делегирование Kerberos, время ожидания запроса, время ожидания сокета, Kerberos и подготовленных Дескриптор инструкции, повторного использования. |

Он будет доступен в центральном репозитории Maven JDBC Driver 6.4 и можно добавить в проект Maven, добавив следующий код в файл POM. XML 

 ```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.4.0.jre9</version>
</dependency>
```

**Microsoft JDBC Driver 6.2 для SQL Server:**  
  
  Драйвер JDBC 6.2 содержит две библиотеки классов JAR: **mssql-jdbc-6.2.2.jre7.jar** и **mssql-jdbc-6.2.2.jre8.jar**. 
  
 Драйвер JDBC Driver 6.2 рассчитан на поддержку всеми основными эквивалентами виртуальных машин Java Sun, однако протестирован только в Sun JRE 5.0, 6.0, 7.0 и 8.0.
  
 В следующей таблице приводится сводная информация о поддержке, которую обеспечивают два JAR-файла, входящие в состав драйверов Microsoft JDBC Driver 6.0 и 4.2 для SQL Server:  
  
|JAR|Соответствие версии JDBC|Рекомендуемая версия Java|Описание|  
|---------|-----------------------------|----------------------|-----------------|
|MSSQL-jdbc-6.2.2.jre7.jar|4.1|7|Требуется среда выполнения Java (JRE) версии 7.0. Использование JRE 6.0 или ниже выдает исключение.<br /><br /> Новые возможности в 6.2 включают: проверка подлинности Azure AD для Linux, метод субъект и пароль для автоматического обнаружения сферы в имени участника-службы для проверки подлинности между доменами, ограниченное делегирование Kerberos, время ожидания запроса, время ожидания сокета, Kerberos и подготовленных Дескриптор инструкции, повторного использования. |  
|MSSQL-jdbc-6.2.3.jre8.jar|4.2|8|Требуется среда выполнения Java (JRE) версии 8.0. Использование JRE 7.0 или ниже выдает исключение.<br /><br /> Новые возможности в 6.2 включают: проверка подлинности Azure AD для Linux, метод субъект и пароль для автоматического обнаружения сферы в имени участника-службы для проверки подлинности между доменами, ограниченное делегирование Kerberos, время ожидания запроса, время ожидания сокета, Kerberos и подготовленных Дескриптор инструкции повторного использования|    

  Он будет доступен в центральном репозитории Maven JDBC Driver 6.2 и можно добавить в проект Maven, добавив следующий код в файл POM. XML 
  
 ```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.2.2.jre8</version>
</dependency>
```    

 **Microsoft JDBC Driver 6.0 и 4.2 для SQL Server:**  
  
  Драйверы JDBC Driver 6.0 и 4.2 включают две библиотеки классов JAR в каждом пакете установки: **sqljdbc41.jar**, и **sqljdbc42.jar**. 
  
 Драйверы JDBC Driver 6.0 и 4.2 рассчитаны на поддержку всеми основными эквивалентами виртуальных машин Java Sun, однако протестированы только в Sun JRE 5.0, 6.0, 7.0 и 8.0. 
  
 В следующей таблице приводится сводная информация о поддержке, которую обеспечивают два JAR-файла, входящие в состав драйверов Microsoft JDBC Driver 6.0 и 4.2 для SQL Server:  
  
|JAR|Соответствие версии JDBC|Рекомендуемая версия Java|Описание|  
|---------|-----------------------------|----------------------|-----------------|   
|sqljdbc41.jar|4.1|7|Требуется среда выполнения Java (JRE) версии 7.0. Использование JRE 6.0 или ниже выдает исключение.<br /><br /> В число новых возможностей в пакетах 6.0 и 4.2 входит массовое копирование и соответствие JDBC 4.1.<br /><br /> Кроме того, новые возможности в пакете 6.0 включают: подготовленный прозрачное подключение к групп доступности AlwaysOn, улучшения в параметр извлечения метаданных для Always Encrypted, возвращающего табличное значение параметров, аутентификация Azure Active Directory, запросы и международных доменных имен (IDN)|  
|sqljdbc42.jar|4.2|8|Требуется среда выполнения Java (JRE) версии 8.0. Использование JRE 7.0 или ниже выдает исключение.<br /><br /> В число новых возможностей в пакетах 6.0 и 4.2 входит массовое копирование, соответствие JDBC 4.1 и соответствие JDBC 4.2.<br /><br /> Кроме того, новые возможности в пакете 6.0 включают: подготовленный прозрачное подключение к групп доступности AlwaysOn, улучшения в параметр извлечения метаданных для Always Encrypted, возвращающего табличное значение параметров, аутентификация Azure Active Directory, запросы и международных доменных имен (IDN)|  
  
 **Microsoft JDBC Driver 4.1 для SQL Server:**  
  
 Драйвер JDBC Driver 4.1 включает в себя один библиотеки классов JAR в каждом пакете установки: **sqljdbc41.jar**.  
    
|JAR|Описание|  
|---------|-----------------|  
|sqljdbc41.jar|Библиотека классов **sqljdbc41.jar** включает поддержку для API JDBC 4.0. Она включает в себя все функции драйвера JDBC 4.0, а также методы API JDBC 4.0. JDBC 4.1 не поддерживается (выдается исключение SQLFeatureNotSupportedException).<br /><br /> Библиотеке классов **sqljdbc41.jar** требуется среда выполнения Java (JRE) версии 7.0. С помощью **sqljdbc41.jar** в JRE 6.0 и 5.0 возникло исключение.<br /><br /> 
  
 Драйвер JDBC разработан и поддерживается при использовании со всеми основными аналогами виртуальных машин Java от Sun, но его проверка выполнялась в Sun JRE 5.0, 6.0 и 7.0.  
  
 В следующей таблице приводится сводная информация о поддержке, которую обеспечивает JAR-файл, входящий в состав драйвера Microsoft JDBC Driver 4.1 для SQL Server.  
  
|JAR|Версия JDBC|JRE (можно выполнять)|JDK (можно компилировать)|  
|---------|------------------|---------------------|-------------------------|   
|sqljdbc41.jar|4|7|7 6 5|  
  
## <a name="sql-server-requirements"></a>Требования к SQL Server  
 Драйвер JDBC поддерживает подключения к базе данных Azure SQL и SQL Server. Для драйвера Microsoft JDBC 4.2 и 4.1 для SQL Server поддержка начинается с SQL Server 2008.
  
## <a name="operating-system-requirements"></a>Требования к операционной системе  
 Драйвер JDBC разработан для использования с любой операционной системой, поддерживающей использование виртуальной машины Java (JVM). Однако официально протестированы только системы Sun Solaris, SUSE Linux и Windows.  
  
## <a name="supported-languages"></a>Поддерживаемые языки  
 Драйвер JDBC поддерживает все параметры сортировки столбцов [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Дополнительные сведения о параметрах сортировки, поддерживаемых драйвером JDBC, см. в разделе [международные функции драйвера JDBC](../../connect/jdbc/international-features-of-the-jdbc-driver.md).  
  
 Дополнительные сведения о параметрах сортировки см. в разделе "Использование параметров сортировки" электронной документации [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>См. также:  
 [Общие сведения о драйвере JDBC](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
