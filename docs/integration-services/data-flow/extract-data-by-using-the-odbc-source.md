---
title: "Извлечение данных с помощью источника ODBC | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 10f25703-49a2-4d45-abab-6b4da2a57ba5
caps.latest.revision: 8
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 8
---
# Извлечение данных с помощью источника ODBC
  Эта процедура описывает, как извлечь данные с использованием источника ODBC. Чтобы добавить и настроить источник ODBC, пакет должен уже содержать не менее одной задачи потока данных.  
  
### Извлечение данных с использованием ODBC-источника  
  
1.  В среде [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]откройте необходимый пакет служб [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] .  
  
2.  Щелкните вкладку **Поток данных** , а затем с панели **Панель элементов**перетащите источник ODBC в область конструктора.  
  
3.  Дважды щелкните источник ODBC.  
  
4.  В диалоговом окне **Редактор источников ODBC** , на странице **Диспетчер соединений** выберите существующий диспетчер соединений ODBC или щелкните **Создать** , чтобы создать новый диспетчер соединений.  
  
5.  Выберите метод доступа к данным.  
  
    -   **Имя таблицы**. Выберите таблицу или представление в базе данных или введите регулярное выражение для обозначения таблицы, к которой подключается диспетчер подключений ODBC.  
  
         Этот список содержит только первые 1000 таблиц. Если база данных содержит больше 1000 таблиц, можно ввести начальную часть имени таблицы или воспользоваться символом-шаблоном (*), чтобы ввести любую часть имени для вывода нужных таблиц.  
  
    -   **Команда SQL**. Введите команду SQL или нажмите кнопку **Обзор** , чтобы загрузить SQL-запрос из текстового файла.  
  
6.  Можно щелкнуть **Предварительный просмотр** , чтобы рассмотреть до 200 строк данных, извлеченных источником ODBC.  
  
7.  Чтобы обновить сопоставление между внешними и выходными столбцами, щелкните **Столбцы** и выберите другие столбцы в списке **Внешний столбец** .  
  
8.  В случае необходимости обновите имена выходных столбцов, изменив значения в списке **Выходной столбец** .  
  
9. Чтобы настроить выход ошибок, щелкните **Вывод ошибок**.  
  
10. Нажмите кнопку **ОК**.  
  
11. Чтобы сохранить обновленный пакет, выберите пункт **Сохранить выбранные элементы** в меню **Файл** .  
  
## См. также  
 [Редактор источника ODBC (страница "Диспетчер соединений")](../../integration-services/data-flow/odbc-source-editor-connection-manager-page.md)   
 [Редактор источника ODBC (страница "Столбцы")](../../integration-services/data-flow/odbc-source-editor-columns-page.md)   
 [Редактор источника ODBC (страница "Вывод ошибок")](../../integration-services/data-flow/odbc-source-editor-error-output-page.md)  
  
  