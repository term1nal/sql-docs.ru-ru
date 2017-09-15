---
title: "Соединение с компонентом Database Engine с использованием расширенной защиты | Документы Майкрософт"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- spoofing attacks
- service binding
- luring attacks
- Schannel
- channel binding
- Extended Protection
ms.assetid: ecfd783e-7dbb-4a6c-b5ab-c6c27d5dd57f
caps.latest.revision: 22
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 894f04fe8bf8df95bb288acab897f3274fbacb18
ms.contentlocale: ru-ru
ms.lasthandoff: 08/02/2017

---
# <a name="connect-to-the-database-engine-using-extended-protection"></a>Соединение с компонентом Database Engine с использованием расширенной защиты
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] поддерживает **расширенную защиту** , начиная с версии [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]. **Расширенная защита для проверки подлинности** представляет собой функцию сетевых компонентов, реализуемую операционной системой. **Расширенная защита** поддерживается в Windows 7 и Windows Server 2008 R2. **Расширенная защита** входит в пакет обновления для более старых операционных систем [!INCLUDE[msCoName](../../includes/msconame-md.md)] . [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] при помощи **расширенную защиту**.  
  
> [!IMPORTANT]  
>  В Windows **Расширенная защита** не включается по умолчанию. Дополнительные сведения о включении функции **Расширенная защита** в Windows см. в разделе [Расширенная защита для проверки подлинности](http://support.microsoft.com/kb/968389).  
  
## <a name="description-of-extended-protection"></a>Описание расширенной защиты  
 **Расширенная защита** предусматривает привязку служб и каналов для предотвращения релейных атак при проверке подлинности. Во время проведения релейной атаки при проверке подлинности клиент, который может выполнить проверку подлинности NTLM (например, через проводник Windows, [!INCLUDE[msCoName](../../includes/msconame-md.md)] Outlook, приложение .NET SqlClient и т. д.), подключается к атакующему (например, злонамеренному файловому серверу CIFS). Атакующий использует учетные данные клиента, чтобы замаскироваться под него и пройти проверку подлинности службы (например, экземпляра службы [!INCLUDE[ssDE](../../includes/ssde-md.md)] ).  
  
 Существуют две разновидности этой атаки.  
  
-   При атаке с заманиванием клиент добровольно подключается к атакующему.  
  
-   При атаке с подделкой пакетов клиент намеревается подключиться к достоверной службе, но не знает, что маршрутизатор DNS или IP (или оба) заражен и перенаправляет соединение к атакующему, а не к службе.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] поддерживает привязку служб и каналов, чтобы сократить возможность проведения таких атак на экземпляр [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
### <a name="service-binding"></a>привязка служб  
 Привязка служб направлена против атак с заманиванием, требуя от клиента отправки подписанного имени участника-службы (SPN) для службы [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , с которой клиент пытается соединиться. При обработке ответа проверки подлинности служба проверяет, совпадает ли полученное в пакете имя участника-службы с ее собственным именем участника-службы. Если имеет место заманивающая атака, то клиент включит подписанное имя участника-службы атакующего. Атакующий не сможет передать этот пакет, чтобы пойти проверку подлинности как клиент в реальной службе [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , поскольку он включает имя участника-службы атакующего. Привязка служб требует небольших разовых затрат, но не противодействует атакам с подделкой пакетов. Привязка службы происходит, когда клиентское приложение не использует шифрование для подключения к [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
### <a name="channel-binding"></a>привязка каналов  
 Привязка канала устанавливает защищенный канал (Schannel) между клиентом и экземпляром службы [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Служба проверяет подлинность клиента, сравнивая его токен привязки данного канала (СВТ) со своим собственным маркером СВТ. Привязка канала противодействует как заманивающим атакам, так и атакам с подделкой пакетов. Однако она требует более значительных затрат времени выполнения из-за шифрования системой защиты на транспортном уровне (TLS) всего трафика сеанса. Привязка канала происходит, когда клиентское приложение использует шифрование для подключения к [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]вне зависимости от принудительного применения шифрования клиентом или сервером.  
  
> [!WARNING]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] и поставщики данных [!INCLUDE[msCoName](../../includes/msconame-md.md)] для [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] поддерживают протоколы TLS 1.0 и SSL 3.0. Если применить другой протокол (например, TLS 1.1 или TLS 1.2), внеся изменения на уровне операционной системы SChannel, при подключении к [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] может возникнуть ошибка.  
  
### <a name="operating-system-support"></a>Поддержка операционных систем  
 Дополнительные сведения о поддержке **расширенной защиты**в ОС Windows можно найти по следующим ссылкам:  
  
-   [Интегрированная проверка подлинности Windows с расширенной защитой](http://msdn.microsoft.com/library/dd639324.aspx)  
  
-   [Советы по безопасности от Microsoft (973811), расширенная защита для проверки подлинности](http://www.microsoft.com/technet/security/advisory/973811.mspx)  
  
## <a name="settings"></a>Настройки  
 Имеются три параметра соединения [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , влияющие на привязку служб и привязку каналов. Эти параметры можно настроить с помощью диспетчера конфигурации [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] или с помощью WMI, для их просмотра можно воспользоваться аспектом **Параметры протокола сервера** управления на основе политик.  
  
-   **Принудительное шифрование**  
  
     Возможные значения — **Вкл.** и **Выкл.** Для использования привязки каналов параметр **Принудительное шифрование** должен быть установлен в значение **Вкл.**и все клиенты должны принудительно выполнять шифрование. При значении **Выкл.**гарантируется только привязка служб. Параметр**Принудительное шифрование** — это один из флажков на вкладке **Свойства протоколов для MSSQLSERVER (вкладка "Флаги")** в диспетчере конфигурации [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   **Расширенная защита**  
  
     Возможными значениями являются **Выкл.**, **Разрешено**и **Обязательно**. Параметр **Расширенная защита** позволяет настраивать уровень **расширенной защиты** для каждого экземпляра [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Параметр**Расширенная защита** находится на дополнительной вкладке **Свойства протоколов для MSSQLSERVER** в диспетчере конфигурации [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
    -   Если задано значение **Выкл.**, **Расширенная защита** отключается. Экземпляр [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] принимает соединения от всех клиентов, независимо от того, является клиент защищенным или нет. При задании**Выкл.** обеспечивается совместимость с предыдущими версиями операционных систем и версиями без установленных обновлений, но этот режим отличается меньшей безопасностью. Этот параметр может быть использован только в том случае, если известно, что клиентские операционные системы не поддерживают расширенную защиту.  
  
    -   Если задано **Разрешено**, функция **Расширенная защита** требуется для соединений от операционных систем, поддерживающих функцию **Расширенная защита**. **Расширенная защита** не используется для подключений из операционных систем, не поддерживающих **расширенную защиту**. Соединения незащищенных клиентских приложений, выполняемых на защищенных клиентских операционных системах, отклоняются. Этот параметр обеспечивает более высокий уровень защиты, чем **Выкл**, но, тем не менее, не обеспечивает самый высокий уровень защиты. Рекомендуется использовать этот параметр в смешанной среде, где определенные операционные системы поддерживают функцию **Расширенная защита** , а некоторые нет.  
  
    -   Если выбрано **Обязательно**, то будут приниматься только соединения от защищенных приложений на защищенных операционных системах. Этот параметр обеспечивает наиболее высокий уровень защиты, но из операционных систем, которые не поддерживают **расширенную защиту** , нельзя будет подключиться к [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   **Принятые имена участников-служб NTLM**  
  
     Переменная **Принятые имена участников-служб NTLM** необходима в том случае, когда для сервера известно более одного имени участника-службы. Когда клиент попытается подключиться к серверу с допустимым именем участника-службы, которое неизвестно серверу, то привязка службы завершится ошибкой. Чтобы избежать этого, пользователь может указать несколько имен участников-служб, представляющих сервер, с помощью параметра **Принятые имена участников-служб NTLM**. Переменная**Принятые имена участников-служб NTLM** содержит последовательность имен участников-служб, перечисленных через точку с запятой. Например, чтобы разрешить имена участников-служб **MSSQLSvc/ HostName1.Contoso.com** и **MSSQLSvc/ HostName2.Contoso.com**, введите **MSSQLSvc/HostName1.Contoso.com;MSSQLSvc/HostName2.Contoso.com** в поле **Принятые имена участников-служб NTLM** . Максимальная длина этой переменной 2 048 символов. Параметр**Принятые имена участников-служб NTLM** находится на дополнительной вкладке **Свойства протоколов для MSSQLSERVER** в диспетчере конфигурации [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="enabling-extended-protection-for-the-database-engine"></a>Включение расширенной защиты для компонента Database Engine  
 Чтобы обеспечить **расширенную защиту**, и на клиенте и на сервере должна работать операционная система, поддерживающая **расширенную защиту**. Кроме того, должно быть включено использование **расширенной защиты** . Дополнительные сведения о включении **расширенной защиты** в операционной системе см. в разделе [Расширенная защита при проверке подлинности](http://support.microsoft.com/kb/968389).  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] поддерживает **расширенную защиту** , начиная с версии [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]. **Расширенная защита** для некоторых предыдущих версий [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] будет доступна в следующих выпусках. После включения параметра **Расширенная защита** на компьютере сервера выполните следующие шаги, чтобы включить **расширенную защиту**.  
  
1.  В меню **Пуск** выберите последовательно **Все программы**, **Microsoft SQL Server** и **Диспетчер конфигурации SQL Server**.  
  
2.  Разверните узел **Конфигурация сети SQL Server**, щелкните правой кнопкой мыши **Протоколы для** *\<*Имя_экземпляра*>*, а затем выберите пункт **Свойства**.  
  
3.  Для привязки каналов и служб на вкладке **Дополнительно** установите значение **Расширенная защита** для соответствующих параметров.  
  
4.  Кроме того, если сервер имеет несколько имен участников-служб, то на вкладке **Дополнительно** настройте поле **Принятые имена участников-служб NTLM** , как описано в разделе «Параметры».  
  
5.  Для привязки канала на вкладке **Флаги** установите параметр **Принудительное шифрование** в значение **Вкл.**  
  
6.  Перезапустите службу [!INCLUDE[ssDE](../../includes/ssde-md.md)] .  
  
## <a name="configuring-other-sql-server-components"></a>Настройка других компонентов SQL Server  
 Дополнительные сведения о настройке [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]см. в разделе [Расширенная защита для проверки подлинности служб Reporting Services](../../reporting-services/security/extended-protection-for-authentication-with-reporting-services.md).  
  
 При использовании IIS для получения доступа к данным [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] по соединению с протоколами HTTP или HTTPS службы [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] могут использовать расширенную защиту, реализуемую IIS. Дополнительные сведения о настройке IIS для использования расширенной защиты см. в разделе [Настройка расширенной защиты в IIS 7.5](http://go.microsoft.com/fwlink/?LinkId=181105).  
  
## <a name="see-also"></a>См. также:  
 [Сетевая конфигурация сервера](../../database-engine/configure-windows/server-network-configuration.md)   
 [Конфигурация клиентской сети](../../database-engine/configure-windows/client-network-configuration.md)   
 [Общие сведения о расширенной защите для проверки подлинности](http://go.microsoft.com/fwlink/?LinkID=177943)   
 [Интегрированная проверка подлинности Windows с расширенной защитой](http://go.microsoft.com/fwlink/?LinkId=179922)  
  
  