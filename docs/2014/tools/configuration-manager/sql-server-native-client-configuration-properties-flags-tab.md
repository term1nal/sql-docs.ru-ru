---
title: Свойства конфигурации SQL Server Native Client (вкладка "Флаги") | Документы Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- configmgr-client
ms.topic: conceptual
ms.assetid: 59af121d-c8b9-4faa-91a1-b664f2c9b441
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ee61cc969c3510c71f975fb8f0934b835a55baa3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/02/2018
ms.locfileid: "48182904"
---
# <a name="sql-server-native-client-configuration-properties-flags-tab"></a>Свойства конфигурации собственного клиента SQL Server (вкладка «Флаги»)
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] на этом компьютере связываются с серверами [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] при помощи протоколов, предоставляемых библиотечным файлом собственного клиента [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . На этой странице можно настроить компьютер клиента на запрос зашифрованного соединения на основе протокола SSL. Если не удается установить зашифрованное соединение, подключение завершится с ошибкой.  
  
 Процесс входа в систему всегда шифруется. Указанные далее параметры применимы только к шифрованию данных. Дополнительные сведения о том, как [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] выполняет шифрование обмена данными, а также инструкции по настройке клиента на доверие к корневому центру сертификата сервера см. в статьях "Шифрование соединений с [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]" и "Инструкции. Включение зашифрованных соединений с компонентом [!INCLUDE[ssDE](../../includes/ssde-md.md)] (диспетчер конфигурации[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] )" в электронной документации по [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="options"></a>Параметры  
 **Принудительное шифрование протокола**  
 Запрос соединения с использованием SSL.  
  
 **Надежный сертификат сервера**  
 При установке значения **Нет**клиентский процесс выполняет попытку проверки сертификата сервера. И клиент, и сервер должны обладать сертификатами, выданными общим центром сертификации. Если на компьютере клиента нет сертификата или если проверка сертификата заканчивается неудачей, соединение закрывается.  
  
 При установке значения **Да**клиент не проверяет сертификат сервера, тем самым позволяя использовать самозаверяющий сертификат.  
  
 Флаг**Доверять сертификату сервера** используется, только если флаг **Принудительное шифрование протокола** имеет значение **Да**.  
  
  
