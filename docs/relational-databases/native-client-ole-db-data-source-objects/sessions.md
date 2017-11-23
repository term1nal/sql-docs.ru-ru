---
title: "Сеансы | Документы Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-data-source-objects
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- sessions [OLE DB]
- SQL Server Native Client OLE DB provider, sessions
ms.assetid: 3a980816-675c-4fba-acc9-429297d85bbd
caps.latest.revision: "31"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8744d7c911c7290418e430d2dcfe97b3c1dd7cf9
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/17/2017
---
# <a name="sessions"></a>Сеансы
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Объект [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] сеанс поставщика OLE DB для собственного клиента представляет одно соединение с экземпляром [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Поставщик OLE DB для собственного клиента требует, чтобы сеансы разделили область транзакции для источника данных. Все объекты команд, созданные из определенного объекта сеанса, участвуют в локальной или распределенной транзакции объекта сеанса.  
  
 Первый объект сеанса, созданный на инициализированном источнике данных, получает соединение [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], установленное при инициализации. Когда все ссылки на интерфейсах объекта сеанса освобождены, соединение с экземпляром [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] становится доступным другому объекту сеанса, созданному на источнике данных.  
  
 Дополнительный объект сеанса, созданный на источнике данных, устанавливает собственное соединение с экземпляром [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], указанным источником данных. Соединение с экземпляром [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] удаляется, когда приложение освобождает все ссылки на объекты, созданные в этом сеансе.  
  
 В следующем примере демонстрируется использование [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] поставщика OLE DB для собственного клиента для подключения к [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] базы данных:  
  
```  
int main()  
{  
    // Interfaces used in the example.  
    IDBInitialize*      pIDBInitialize      = NULL;  
    IDBCreateSession*   pIDBCreateSession   = NULL;  
    IDBCreateCommand*   pICreateCmd1        = NULL;  
    IDBCreateCommand*   pICreateCmd2        = NULL;  
    IDBCreateCommand*   pICreateCmd3        = NULL;  
  
    // Initialize COM.  
    if (FAILED(CoInitialize(NULL)))  
    {  
        // Display error from CoInitialize.  
        return (-1);  
    }  
  
    // Get the memory allocator for this task.  
    if (FAILED(CoGetMalloc(MEMCTX_TASK, &g_pIMalloc)))  
    {  
        // Display error from CoGetMalloc.  
        goto EXIT;  
    }  
  
    // Create an instance of the data source object.  
    if (FAILED(CoCreateInstance(CLSID_SQLNCLI10, NULL,  
        CLSCTX_INPROC_SERVER, IID_IDBInitialize, (void**)  
        &pIDBInitialize)))  
    {  
        // Display error from CoCreateInstance.  
        goto EXIT;  
    }  
  
    // The InitFromPersistedDS function   
    // performs IDBInitialize->Initialize() establishing  
    // the first application connection to the instance of SQL Server.  
    if (FAILED(InitFromPersistedDS(pIDBInitialize, L"MyDataSource",  
        NULL, NULL)))  
    {  
        goto EXIT;  
    }  
  
    // The IDBCreateSession interface is implemented on the data source  
    // object. Maintaining the reference received maintains the   
    // connection of the data source to the instance of SQL Server.  
    if (FAILED(pIDBInitialize->QueryInterface(IID_IDBCreateSession,  
        (void**) &pIDBCreateSession)))  
    {  
        // Display error from pIDBInitialize.  
        goto EXIT;  
    }  
  
    // Releasing this has no effect on the SQL Server connection  
    // of the data source object because of the reference maintained by  
    // pIDBCreateSession.  
    pIDBInitialize->Release();  
    pIDBInitialize = NULL;  
  
    // The session created next receives the SQL Server connection of  
    // the data source object. No new connection is established.  
    if (FAILED(pIDBCreateSession->CreateSession(NULL,  
        IID_IDBCreateCommand, (IUnknown**) &pICreateCmd1)))  
    {  
        // Display error from pIDBCreateSession.  
        goto EXIT;  
    }  
  
    // A new connection to the instance of SQL Server is established to support the  
    // next session object created. On successful completion, the  
    // application has two active connections on the SQL Server.  
    if (FAILED(pIDBCreateSession->CreateSession(NULL,  
        IID_IDBCreateCommand, (IUnknown**) &pICreateCmd2)))  
    {  
        // Display error from pIDBCreateSession.  
        goto EXIT;  
    }  
  
    // pICreateCmd1 has the data source connection. Because the  
    // reference on the IDBCreateSession interface of the data source  
    // has not been released, releasing the reference on the session  
    // object does not terminate a connection to the instance of SQL Server.  
    // However, the connection of the data source object is now   
    // available to another session object. After a successful call to   
    // Release, the application still has two active connections to the   
    // instance of SQL Server.  
    pICreateCmd1->Release();  
    pICreateCmd1 = NULL;  
  
    // The next session created gets the SQL Server connection  
    // of the data source object. The application has two active  
    // connections to the instance of SQL Server.  
    if (FAILED(pIDBCreateSession->CreateSession(NULL,  
        IID_IDBCreateCommand, (IUnknown**) &pICreateCmd3)))  
    {  
        // Display error from pIDBCreateSession.  
        goto EXIT;  
    }  
  
EXIT:  
    // Even on error, this does not terminate a SQL Server connection   
    // because pICreateCmd1 has the connection of the data source   
    // object.  
    if (pICreateCmd1 != NULL)  
        pICreateCmd1->Release();  
  
    // Releasing the reference on pICreateCmd2 terminates the SQL  
    // Server connection supporting the session object. The application  
    // now has only a single active connection on the instance of SQL Server.  
    if (pICreateCmd2 != NULL)  
        pICreateCmd2->Release();  
  
    // Even on error, this does not terminate a SQL Server connection   
    // because pICreateCmd3 has the connection of the   
    // data source object.  
    if (pICreateCmd3 != NULL)  
        pICreateCmd3->Release();  
  
    // On release of the last reference on a data source interface, the  
    // connection of the data source object to the instance of SQL Server is broken.  
    // The example application now has no SQL Server connections active.  
    if (pIDBCreateSession != NULL)  
        pIDBCreateSession->Release();  
  
    // Called only if an error occurred while attempting to get a   
    // reference on the IDBCreateSession interface of the data source.  
    // If so, the call to IDBInitialize::Uninitialize terminates the   
    // connection of the data source object to the instance of SQL Server.  
    if (pIDBInitialize != NULL)  
    {  
        if (FAILED(pIDBInitialize->Uninitialize()))  
        {  
            // Uninitialize is not required, but it fails if an  
            // interface has not been released. Use it for  
            // debugging.  
        }  
        pIDBInitialize->Release();  
    }  
  
    if (g_pIMalloc != NULL)  
        g_pIMalloc->Release();  
  
    CoUninitialize();  
  
    return (0);  
}  
```  
  
 Подключение [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] объектов сеанса поставщика OLE DB для собственного клиента к экземпляру [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] могут возникнуть существенные издержки для приложений, которые постоянно создают и освобождают объекты сеанса. Издержки можно уменьшить путем управления [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] эффективно объектами сеанса поставщика OLE DB для собственного клиента. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Можно сохранить собственного приложения поставщика OLE DB для клиента [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] подключения объекта сеанса активным, поддерживая ссылку по крайней мере один интерфейс объекта.  
  
 Например, поддержание пула ссылок на объект создания команды сохраняет активными соединения для этих объектов сеанса в пуле. Объекты сеанса, при необходимости, код обслуживания пула передает действительный **IDBCreateCommand** указатель на интерфейс методу приложения, требующему сеанс. Когда сеанс более не требуется методу приложения, метод возвращает указатель интерфейса коду обслуживания пула, а не освобождает ссылку приложения на объект создания команды.  
  
> [!NOTE]  
>  В приведенном выше примере **IDBCreateCommand** используется интерфейс, так как **ICommand** интерфейс реализует **GetDBSession** метод, единственный метод в области команд или набора строк, позволяющий объекту определить сеанс, в котором он был создан. Поэтому объект команды, и только объект команды, позволяет приложению получить указатель объекта источника данных, из которого могут быть созданы дополнительные сеансы.  
  
## <a name="see-also"></a>См. также:  
 [Объекты источника данных &#40; OLE DB &#41;](../../relational-databases/native-client-ole-db-data-source-objects/data-source-objects-ole-db.md)  
  
  