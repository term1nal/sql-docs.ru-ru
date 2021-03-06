---
title: Статические курсоры | Документация Майкрософт
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- cursors [ADO], static
- static cursors [ADO]
ms.assetid: cce93ace-c4ed-4c6c-940c-28a50ff2fd12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e8815522ee4f9a4221887696a23a201910d7cfad
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/01/2018
ms.locfileid: "47654192"
---
# <a name="static-cursors"></a>Статические курсоры
Статический курсор всегда отображает результирующий набор, который был сначала открытия курсора. В зависимости от реализации, статические курсоры доступны только для чтения или чтения и записи и предоставить прямой и обратной прокрутки. Статический курсор обычно не обнаруживает изменения, внесенные в членство, порядок или значения результирующего набора, после открытия курсора. Статические курсоры могут быть обнаружены свои собственные обновления, удаления и вставки, несмотря на то, что они не требуются для этого.  
  
 Статические курсоры никогда не обнаружить другие обновления, удаления и вставки. Предположим, например, статический курсор извлекает строки и другое приложение, а затем обновляет этой строки. Если приложение refetches строку из статического курсора, значения, которые видит ничем не отличаются, несмотря на изменения, внесенные другим приложением. Поддерживаются все типы прокрутки, но поставщиков может поддерживать или не поддерживать закладки.  
  
 Если приложение не требуется для обнаружения изменения данных и требуется прокрутка, статический курсор является лучшим выбором. Используйте **adOpenStatic CursorTypeEnum** для указания, что вы хотите использовать статический курсор в ADO.  
  
## <a name="see-also"></a>См. также  
 [Однопроходные курсоры](../../../ado/guide/data/forward-only-cursors.md)   
 [Управляемые набором ключей курсоры](../../../ado/guide/data/keyset-cursors.md)   
 [Динамические курсоры](../../../ado/guide/data/dynamic-cursors.md)
