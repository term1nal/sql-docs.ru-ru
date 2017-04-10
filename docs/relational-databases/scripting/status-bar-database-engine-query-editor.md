---
title: "Строка состояния (редактор запросов к ядру СУБД) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e7f2d6f4-bb94-4cf5-a096-c34397e679af
caps.latest.revision: 7
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 7
---
# Строка состояния (редактор запросов к ядру СУБД)
  В строках состояния в окнах редактора запросов компонента [!INCLUDE[ssDE](../../includes/ssde-md.md)] могут быть цветовые обозначения, указывающие, к какому экземпляру [!INCLUDE[ssDE](../../includes/ssde-md.md)] подключено данное окно.  
  
1.  **Перед началом работы выполните следующие действия.**  [Цвета строки состояния](#StatusBarColors)  
  
2.  **Задание цвета состояния сервера в:**  [обозревателе объектов](#SetOEServerColor), [зарегистрированном сервере](#SetRegServerColor)  
  
3.  **Использование цвета состояния:**  [открытие редактора запросов с помощью цвета сервера](#OpenServerColor), [открытие редактора запросов с помощью цвета состояния](#OpenSpecColor)  
  
##  <a name="StatusBarColors"></a> Цвета строки состояния  
 Можно привязать цвет строки состояния к определенному узлу с помощью **обозревателя объектов** или в окне **Зарегистрированные серверы**. Цвета можно указать только для узлов сервера, подключенных к экземпляру компонента [!INCLUDE[ssDE](../../includes/ssde-md.md)], но не для узлов для других технологических решений SQL Server. Также можно указывать пользовательский цвет строки состояния при каждом подключении нового окна редактора запросов компонента [!INCLUDE[ssDE](../../includes/ssde-md.md)] к экземпляру компонента [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Затем можно открывать окно редактора запросов с помощью цвета состояния, определенного для узла сервера, или указать уникальный цвет для этого окна редактора.  
  
 Задавать пользовательский цвет строки состояния для узла сервера в обозревателе объектов необходимо при установке соединения. Чтобы изменить цвет, связанный с существующим узлом сервера, необходимо разорвать соединение, затем подключиться снова, указав новый цвет.  
  
##  <a name="SetOEServerColor"></a> Задание цвета состояния для сервера в обозревателе объектов  
 **Задание цвета состояния сервера в обозревателе объектов**  
  
1.  В **обозревателе объектов**нажмите кнопку **Подключение** , затем выберите **Компонент Database Engine...**.  
  
2.  В диалоговом окне **Соединение с сервером** выберите **Параметры >>**.  
  
3.  Установите флажок **Использовать пользовательский цвет** .  
  
4.  Чтобы выбрать цвет, нажмите кнопку **Выбрать...** .  
  
5.  Выберите основной или пользовательский цвет, затем нажмите кнопку ОК.  
  
6.  Укажите остальные сведения о подключении, а затем нажмите кнопку **Соединение** .  
  
##  <a name="SetRegServerColor"></a> Указание цвета состояния для зарегистрированного сервера  
 **Указание цвета состояния для зарегистрированного сервера**  
  
1.  В списке **Зарегистрированные серверы**щелкните правой кнопкой мыши узел сервера и выберите пункт **Свойства...**.  
  
2.  В диалоговом окне **Изменение данных регистрации серверов** перейдите на вкладку **Свойства соединения** .  
  
3.  Установите флажок **Использовать пользовательский цвет** .  
  
4.  Чтобы выбрать цвет, нажмите кнопку **Выбрать...** .  
  
5.  Выберите основной или пользовательский цвет, затем нажмите кнопку ОК.  
  
6.  Нажмите кнопку **Сохранить** в диалоговом окне **Изменение данных регистрации серверов** .  
  
##  <a name="OpenServerColor"></a> Открытие редактора с помощью цвета сервера  
 **Открытие окна редактора с помощью цвета сервера**  
  
-   Щелкните правой кнопкой мыши узел сервера в **обозревателе объектов** или в окне **Зарегистрированные серверы** и нажмите кнопку **Создать запрос**.  
  
-   Также можно выделить узел сервера, затем нажать кнопку **Создать запрос** на панели инструментов.  
  
-   Строка состояния в окне редактора будет отображаться цветом, определенным для связанного сервера.  
  
##  <a name="OpenSpecColor"></a> Открытие редактора с помощью цвета состояния  
 **Открытие окна редактора с помощью цвета состояния**  
  
-   Откройте меню **Файл** , выберите **Создать**, затем выберите **Запрос к ядру СУБД**.  
  
-   В диалоговом окне **Соединение с сервером** выберите **Параметры >>**.  
  
-   Установите флажок **Использовать пользовательский цвет** .  
  
-   Чтобы выбрать цвет, нажмите кнопку **Выбрать...** .  
  
-   Выберите основной или пользовательский цвет, затем нажмите кнопку ОК.  
  
-   Укажите остальные сведения о подключении, а затем нажмите кнопку **Соединение** .  
  
## См. также:  
 [Редакторы запросов и текста (SQL Server Management Studio)](../../relational-databases/scripting/query-and-text-editors-sql-server-management-studio.md)  
  
  