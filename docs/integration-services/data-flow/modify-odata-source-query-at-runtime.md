---
title: "Изменение запроса источника OData во время выполнения | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: bcbba7f4-6e5d-46e6-a73a-3f17d3ff376a
caps.latest.revision: 7
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 7
---
# Изменение запроса источника OData во время выполнения
  Можно изменить запрос источника OData во время выполнения, добавив выражение в свойство **[OData Source].[Query]** задачи потока данных.  
  
 Обратите внимание, что столбцы должны оставаться такими же, что и во время разработки. В противном случае произойдет ошибка при выполнении пакета. Обязательно укажите те же столбцы (в том же порядке) при использовании параметра $select запроса. Более безопасная альтернатива применению параметра $select состоит в том, чтобы отменить выбор ненужных столбцов непосредственно в пользовательском интерфейсе исходного компонента.  
  
 Существует несколько способов для динамической установки значения запроса во время выполнения. Ниже перечислены некоторые из наиболее распространенных методов.  
  
## Предоставление запроса в качестве параметра  
 Следующая процедура позволяет предоставить пакету доступ к запросу, используемому компонентом источника OData, в качестве параметра.  
  
1.  Щелкните правой кнопкой мыши **Задача потока данных** и выберите пункт **Параметризация…** .  
  
2.  В диалоговом окне **Параметризация** выберите **[\<имя исходного компонента OData>].[Query]** для параметра **Свойство**.  
  
3.  Выберите, следует ли значение **создать новый параметр** или **использовать существующий параметр**.  
  
4.  Если установлен флажок **Создать новый параметр**, выполните следующие действия.  
  
    1.  Введите **имя** и **описание** для параметра.  
  
    2.  Укажите **значение** по умолчанию для данного параметра.  
  
    3.  Укажите **область** (**пакет** или **проект**) для параметра.  
  
    4.  Укажите, является ли параметр **обязательным** или нет.  
  
5.  Чтобы закрыть диалоговое окно, нажмите кнопку **ОК** .  
  
## Использование выражения  
 Этот метод удобен для динамического построения строки запроса во время выполнения. В этом примере переменная MaxRows будет установлена с помощью других средств (скрипт, параметр и т. д.).  
  
1.  Выберите **задачу потока данных** , содержащую ваш **источник OData**.  
  
2.  В окне **Свойства** выделите свойство **Выражения** .  
  
3.  Нажмите кнопку с многоточием (...), чтобы открыть **Редактор выражений свойств**.  
  
4.  Выберите свойство **[OData Source].[Query]**.  
  
5.  Нажмите кнопку с многоточием (...) для элемента **Выражение**.  
  
6.  Введите **выражение**.  
  
7.  Нажмите кнопку **ОК**.  
  
> [!WARNING]  
>  Обратите внимание, что при использовании такого подхода необходимо убедиться, чтобы значения были правильно закодированы в URL-адресе. При получении значений из входных данных пользователя (например, установке отдельных значений параметра запроса из параметра) необходимо убедиться, что значения проверяются, чтобы избежать потенциальных атак путем инжекции кода SQL.  
  
  