---
title: srv_getbindtoken (интерфейс API расширенных хранимых процедур) | Документы Майкрософт
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: reference
apiname:
- srv_getbindtoken
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_getbindtoken
ms.assetid: c947d011-08ac-4fb8-b925-3da6e0999277
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 75b520afbca6115cbd3fccc928838e99d3831fef
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/01/2018
ms.locfileid: "47659408"
---
# <a name="srvgetbindtoken-extended-stored-procedure-api"></a>srv_getbindtoken (API-интерфейс расширенных хранимых процедур)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Используйте вместо этого интеграцию со средой CLR.  
  
 Получает токен привязки транзакции в текущем сеансе клиента, который вызывает расширенную хранимую процедуру.  
  
 После этого расширенная хранимая процедура может использовать **sp_bindsession** для привязки любого созданного ею на том же сервере сеанса к существующей транзакции, чтобы новый сеанс мог совместно использовать одно пространство блокировки транзакций с клиентским сеансом, вызвавшим расширенную хранимую процедуру.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
int srv_getbindtoken (  
SRV_PROC*  
srvproc  
,  
char*  
bindtoken  
);  
```  
  
## <a name="arguments"></a>Аргументы  
 *srvproc*  
 Указатель на структуру SRV_PROC, который представляет собой дескриптор соединения с клиентом. В этой структуре содержатся все сведения, которые библиотека API-интерфейса расширенных хранимых процедур использует для управления обменом данными между приложением и клиентом.  
  
 *bindtoken*  
 Указатель на буфер, в который будет скопирован токен привязки. Токен привязки представлен как строка, оканчивающаяся нулевым байтом. Указываемый буфер должен иметь длину не менее 255 байт.  
  
## <a name="returns"></a>Возвращает  
 SUCCEED или FAIL.  
  
## <a name="remarks"></a>Remarks  
  
### <a name="to-bind-an-extended-stored-procedure-session-to-the-client-session-that-called-it-so-they-share-the-same-transaction-lock-space"></a>Привязка сеанса расширенной хранимой процедуры к сеансу вызывающего ее клиента для совместного использования пространства блокировки транзакций  
  
1.  Расширенная хранимая процедура вызывает функцию **svr_getbindtoken**, чтобы получить токен привязки для текущей транзакции в сеансе. Токен возвращается в параметре *bindtoken*.  
  
2.  Расширенная хранимая процедура открывает новый сеанс на том же сервере. В этом сеансе расширенная хранимая процедура использует токен привязки в хранимой процедуре **sp_bindsession** для привязки нового сеанса к той же транзакции. Расширенная хранимая процедура может создать несколько сеансов и привязать их к одной транзакции.  
  
3.  Связанный сеанс освобождается при возврате из расширенной хранимой процедуры или когда **sp_bindsession** вызывается с пустой строкой.  
  
    > [!NOTE]  
    >  Только один связанный сеанс может получить доступ к общему соединению в один момент времени. Если один сеанс в настоящий момент выполняет инструкцию на сервере или ожидает результаты с сервера, то никакой другой сеанс, совместно использующий это связанное соединение, не может получить доступ к серверу, пока текущий сеанс не завершит выполнение инструкции. Если сеанс пытается получить доступ к соединению, пока сервер занят, то для этого сеанса возвращается ошибка, указывающая, что соединение используется, и конфликтующему сеансу следует повторить попытку позже.  
  
> [!IMPORTANT]  
>  Необходимо тщательно просмотреть исходный код расширенных хранимых процедур и проверить скомпилированные библиотеки DLL перед их установкой на рабочий сервер. Сведения о проверке безопасности см. на следующем [веб-сайте Майкрософт](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/).  
  
## <a name="see-also"></a>См. также:  
 [sp_bindsession (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-bindsession-transact-sql.md)   
 [sp_getbindtoken (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-getbindtoken-transact-sql.md)  
  
  
