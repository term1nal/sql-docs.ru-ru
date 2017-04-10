---
title: "Соединение с подпиской Microsoft Azure | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-backup-restore"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: cca5a270-643f-4677-8802-98464f19f82a
caps.latest.revision: 4
author: "dagiro"
ms.author: "v-dagir"
manager: "jhubbard"
caps.handback.revision: 4
---
# Соединение с подпиской Microsoft Azure
Параметр **Соединиться с подпиской Майкрософт** используется для регистрации существующего контейнера больших двоичных объектов в экземпляре SQL Server.  С помощью параметров, приведенных в диалоговом окне, в контейнере больших двоичных объектов будет создан подписанный URL-адрес и политика подписанных URL-адресов, после чего будут созданы учетные данные SQL Server.  Это диалоговое окно открывается при использовании задачи резервного копирования или восстановления в SQL Server Management Studio. Для выполнения операции требуется URL-адрес устройства.

## Ограничение
Параметр **Соединиться с подпиской Майкрософт** работает только с учетной записью хранилища Azure, созданной с помощью модели развертывания управления службами (классической модели развертывания).  Дополнительные сведения о моделях развертывания Azure см. в статье [Azure Resource Manager и классическое развертывание](https://azure.microsoft.com/en-us/documentation/articles/resource-manager-deployment-model/).

## Параметры
**Вход**     
Вход с использованием соответствующей учетной записи Azure.

**Выберите подписку для использования**      
Выбор нужной подписки в раскрывающемся списке.

**Выберите учетную запись хранения**  
Выбор нужной учетной записи хранения в раскрывающемся списке.

**Выберите контейнер больших двоичных объектов**   
Выбор нужного контейнера больших двоичных объектов в раскрывающемся списке.

**Истечение срока действия политики подписанных URL-адресов**   
Срок действия политики подписанных URL-адресов истекает в указанную дату.  Заданная по умолчанию дата истечения срока действия — один год после создания.  При необходимости значение можно изменить.

**Подписанный URL-адрес создан**   
В поле форматированного текста будет отображаться созданный подписанный URL-адрес.

**Создать учетные данные**   
Кнопка для создания политики подписанных URL-адресов и подписанного URL-адреса и последующего создания учетных данных SQL Server.