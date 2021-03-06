---
title: Диалоговое окно "Свойства проекта" | Документация Майкрософт
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.ssms.isprojectprop.general.f1
- sql12.ssis.ssms.isprojectprop.permissions.f1
ms.assetid: d5cf52f5-1fe2-438a-98a3-fe117360acf8
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d657e1339f454045a4a1e536610a58cd27e94c8d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/02/2018
ms.locfileid: "48054234"
---
# <a name="project-properties-dialog-box"></a>Диалоговое окно свойств проекта
  Проект служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] представляет собой единицу развертывания. Каждый проект может содержать пакеты, параметры и ссылки на среду. Проект является защищаемым объектом и может определять разрешения для участников базы данных. При повторном развертывании проекта предыдущая версия проекта может быть сохранена в каталоге служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 Параметры проекта и пакета могут быть использованы для присвоения значений свойствам внутри пакетов во время выполнения. Некоторым параметрам необходимо заранее присвоить значения, чтобы пакет можно было выполнить. При использовании ссылок на переменные среды в значениях параметров требуется, чтобы эти ссылки присутствовали в проекте перед выполнением.  
  
 **Выбор действия**  
  
-   [Открытие диалогового окна «Свойства проекта»](#open_dialog)  
  
-   [Задание параметров на странице «Общие»](#general)  
  
-   [Задание параметров на странице «Разрешения»](#permissions)  
  
##  <a name="open_dialog"></a> Открытие диалогового окна «Свойства проекта»  
  
1.  В среде [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]установите соединение с сервером служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
     Устанавливается соединение с экземпляром компонента [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] , в котором размещена база данных SSISDB.  
  
2.  В обозревателе объектов разверните дерево для отображения узла **Каталоги служб Integration Services** .  
  
3.  Разверните узел **SSISDB** .  
  
4.  Разверните папку, содержащую проект, свойства которого требуется установить.  
  
5.  Щелкните правой кнопкой мыши проект и выберите пункт **Свойства**.  
  
##  <a name="general"></a> Задание параметров на странице «Общие»  
 Используйте страницу «Общие» для просмотра свойств проекта.  
  
 **Название**  
 Выводит список имен проекта.  
  
 **Идентификатор**  
 Выводит список идентификаторов проекта.  
  
 **Описание**  
 Показывает необязательное описание проекта.  
  
 **Версия проекта**  
 Выводит список версий проекта.  
  
 **Дата развертывания**  
 Отображает дату и время развертывания или повторного развертывания проекта.  
  
##  <a name="permissions"></a> Задание параметров на странице «Разрешения»  
 Страница **Разрешения** используется для просмотра и установки явных разрешений для проекта.  
  
 Обзор  
 Нажмите кнопку **Обзор** для выбора пользователей и ролей, которым необходимо установить разрешения с помощью диалогового окна **Просмотр всех участников** .  
  
 **Название**  
 Выводит список имен пользователя или роли.  
  
 **Тип**  
 Выводит список типов пользователя или роли.  
  
 **Разрешение**  
 Выводит список разрешений.  
  
 **Grantor**  
 Выводит список пользователей или ролей, которым предоставляют разрешение.  
  
 **Право предоставил**  
 Если выбрано поле **Предоставить** , то будет предоставлено разрешение для выбранного пользователя или роли.  
  
 **Запретить**  
 Если выбрано поле **Запретить** , то разрешение будет запрещено для выбранного пользователя или роли.  
  
  
