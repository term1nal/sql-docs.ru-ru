---
title: Параметры (текстовый редактор - обычный текст - "Общие") | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.Plain_Text.General
ms.assetid: 53bfa594-ba36-4c9c-8dd5-4c2dcce7d2dc
caps.latest.revision: 22
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: b66c8286d3ae062307175e689f222f33ea3be6a0
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2018
ms.locfileid: "37150995"
---
# <a name="options-text-editor---plain-text---general-page"></a>Options (Text Editor - Plain Text - General Page)
  Используйте это диалоговое окно для смены режима изменения текстового редактора, который используется для редактирования документа, не связанного с определенным языком разработки. Для отображения этих настроек выберите пункт **Параметры** в меню **Сервис** , раскройте узел **Текстовый редактор**, щелкните **Неформатированный текст** , а затем выберите **Общие**.  
  
## <a name="setting-options-in-multiple-locations"></a>Настройка параметров в нескольких местах  
 Параметры для обычного текстового редактора можно также задать в диалоговом окне **Все языки/Общие** . Если диалоговое окно **Все языки** используется для задания различных параметров для других редакторов среды [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] , таких как DMX или MDX, необходимо сбросить параметры обычного текстового редактора с помощью этого окна.  
  
## <a name="statement-completion"></a>Завершение операторов  
 **Автоматически отображать список членов**  
 Редактор обычного текста не поддерживает эту возможность.  
  
 **Скрывать дополнительные члены**  
 Редактор обычного текста не поддерживает эту возможность.  
  
 **Сведения о параметрах**  
 Редактор обычного текста не поддерживает эту возможность.  
  
## <a name="settings"></a>Настройки  
 **Разрешить виртуальное пространство**  
 Вставьте пробелы в конце каждой строки текста. Установите этот флажок для размещения комментариев в постоянном положении относительно текста.  
  
 **Перенос по словам**  
 Позволяет отобразить любую часть текста, выходящую горизонтально за пределы видимого редактора, на следующей строке. Установка этого флажка включает параметр **Отображать символы переноса строк** .  
  
 **Отображать символы переноса по словам**  
 Отображает символ в виде обратной стрелки там, где длинная строка переносится на следующую строку. Снимите этот флажок, если индикаторы не должны отображаться.  
  
> [!NOTE]  
>  Эти стрелки-напоминания не добавляются в код и не выводятся на печать. Они предназначены только для уведомления.  
  
 **Применять команды вырезания или копирования к пустым строкам, когда текст не выделен**  
 Этот флажок определяет работу редактора в случае, когда точка вставки расположена на пустой строке, ничего не выбрано и запущена команда **Копировать** или **Вырезать**.  
  
 Если флажок установлен, то копируется или вырезается пустая строка. Если затем выбрать **Вставить**, то будет вставлена новая пустая строка.  
  
 Если флажок снят, ничего не копируется и не вырезается. Если затем выбрать команду **Вставить**, то будет вставлено то, что было скопировано в буфер обмена ранее. Если ничего не было скопировано, ничего не будет вставлено.  
  
 Эта установка не оказывает влияния на команды **Копировать** и **Вырезать** в случае, если строка не пуста. Если ничего не выделено, копируется или вырезается вся строка. Если затем выбрать команду **Вставить**, вставляется текст всей строки, включая символ конца строки.  
  
## <a name="display"></a>Отобразить  
 **Номера строк**  
 Позволяет отобразить номер строки рядом с каждой строкой текста.  
  
> [!NOTE]  
>  Номера строк не добавляются в текст и не печатаются. Они предназначены только для уведомления.  
  
 **Включить URL-адреса однократным щелчком**  
 Измените курсор на указывающую руку при его проходе над URL-адресом в редакторе. Можно щелкнуть URL-адрес для отображения указанной страницы в браузере.  
  
 **Панель навигации**  
 Этот флажок недоступен.  
  
  