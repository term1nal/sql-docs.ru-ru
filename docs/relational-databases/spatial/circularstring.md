---
title: "CircularString | Microsoft Docs"
ms.custom: ""
ms.date: "06/02/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-spatial"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9fe06b03-d98c-4337-9f89-54da98f49f9f
caps.latest.revision: 27
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 27
---
# CircularString
  Объект **CircularString** — это коллекция, состоящая из нуля или большего количества непрерывных круговых сегментов дуги. Сегмент дуги — это сегмент кривой, определяемый тремя точками на двумерной плоскости; первая точка не может совпадать с третьей. Если все три точки сегмента дуги лежат на одной прямой, сегмент дуги считается линейным сегментом.  
  
> [!IMPORTANT]  
>  Подробное описание и примеры использования новых возможностей обработки пространственных данных, добавленных в [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], в том числе подтипа **CircularString**, можно получить, загрузив технический документ [Новые возможности обработки пространственных данных в SQL Server 2012](http://go.microsoft.com/fwlink/?LinkId=226407).  
  
## Экземпляры CircularString  
 На следующем рисунке показаны допустимые экземпляры **CircularString** .  
  
 ![5ff17e34-b578-4873-9d33-79500940d0bc](../../relational-databases/spatial/media/5ff17e34-b578-4873-9d33-79500940d0bc.gif)
  
### Правильные экземпляры  
 Экземпляр **CircularString** принимается, если он пуст или содержит нечетное количество точек, n, где n > 1. Следующие экземпляры **CircularString** правильные.  
  
```  
DECLARE @g1 geometry = 'CIRCULARSTRING EMPTY';  
DECLARE @g2 geometry = 'CIRCULARSTRING(1 1, 2 0, -1 1)';  
DECLARE @g3 geometry = 'CIRCULARSTRING(1 1, 2 0, 2 0, 2 0, 1 1)';  
```  
  
 `@g3` показывает, что экземпляр **CircularString** может быть правильным, но недопустимым. Следующее объявление экземпляра CircularString неверно. Это объявление вызывает исключение `System.FormatException`.  
  
```  
DECLARE @g geometry = 'CIRCULARSTRING(1 1, 2 0, 2 0, 1 1)';  
```  
  
### Допустимые экземпляры  
 Допустимый экземпляр **CircularString** должен быть пуст или иметь следующие атрибуты:  
  
-   Он должен содержать хотя бы один сегмент дуги (то есть не менее трех точек).  
  
-   Последняя конечная точка каждого из отрезков дуги в последовательности, кроме последнего, должна совпадать с первой конечной точкой следующего сегмента в последовательности.  
  
-   Количество точек должно быть нечетным.  
  
-   Он не должен перекрываться собой.  
  
-   Хотя экземпляры **CircularString** могут содержать линейные сегменты, эти линейные сегменты должны определяться тремя лежащими на одной прямой точками.  
  
 В следующем примере показаны допустимые экземпляры **CircularString** .  
  
```  
DECLARE @g1 geometry = 'CIRCULARSTRING EMPTY';  
DECLARE @g2 geometry = 'CIRCULARSTRING(1 1, 2 0, -1 1)';  
DECLARE @g3 geometry = 'CIRCULARSTRING(1 1, 2 0, 2 0, 1 1, 0 1)';  
DECLARE @g4 geometry = 'CIRCULARSTRING(1 1, 2 2, 2 2)';  
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid(),@g4.STIsValid();  
```  
  
 Для определения окружности экземпляр **CircularString** должен содержать как минимум два сегмента дуги. Для определения окружности экземпляр **CircularString** не может содержать один сегмент дуги (например, (1 1, 3 1, 1 1)). Для определения окружности используйте (1 1, 2 2, 3 1, 2 0, 1 1).  
  
 В следующем примере показаны недопустимые экземпляры CircularString.  
  
```  
DECLARE @g1 geometry = 'CIRCULARSTRING(1 1, 2 0, 1 1)';  
DECLARE @g2 geometry = 'CIRCULARSTRING(0 0, 0 0, 0 0)';  
SELECT @g1.STIsValid(), @g2.STIsValid();  
```  
  
### Экземпляры с точками, лежащими на прямой  
 Сегмент дуги будет считаться линейным сегментом в следующих случаях.  
  
-   Когда все три точки лежат на одной прямой (например, (1 3, 4 4, 7 5)).  
  
-   Когда первая и средняя точки совпадают, а третья точка отличается от них (например, (1 3, 1 3, 7 5)).  
  
-   Когда средняя и последняя точки совпадают, а первая точка отличается от них (например, (1 3, 4 4, 4 4)).  
  
## Примеры  
  
### A. Создание экземпляра Geometry с пустым экземпляром CircularString  
 В этом примере показано, как создать пустой экземпляр **CircularString** :  
  
```tsql  
DECLARE @g geometry;  
SET @g = geometry::Parse('CIRCULARSTRING EMPTY');  
```  
  
### Б. Создание экземпляра Geometry с экземпляром CircularString, содержащим один сегмент дуги  
 В следующем примере показывается создание экземпляра **CircularString** с одним сегментом дуги (полукруга):  
  
```tsql  
DECLARE @g geometry;  
SET @g = geometry:: STGeomFromText('CIRCULARSTRING(2 0, 1 1, 0 0)', 0);  
SELECT @g.ToString();  
```  
  
### В. Создание экземпляра Geometry с помощью экземпляра CircularString с несколькими сегментами дуги  
 В следующем примере показывается создание экземпляра **CircularString** более чем с одним сегментом дуги (круга):  
  
```tsql  
DECLARE @g geometry;  
SET @g = geometry::Parse('CIRCULARSTRING(2 1, 1 2, 0 1, 1 0, 2 1)');  
SELECT 'Circumference = ' + CAST(@g.STLength() AS NVARCHAR(10));    
```  
  
 Получается следующий вывод.  
  
```  
Circumference = 6.28319  
```  
  
 Сравните вывод, получаемый при использовании **LineString** вместо **CircularString**:  
  
```tsql  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(2 1, 1 2, 0 1, 1 0, 2 1)', 0);  
SELECT 'Perimeter = ' + CAST(@g.STLength() AS NVARCHAR(10));  
```  
  
 Получается следующий вывод.  
  
```  
Perimeter = 5.65685  
```  
  
 Обратите внимание, что значение в примере **CircularString** близко к 2∏, то есть действительному углу для окружности.  
  
### Г. Объявление и создание экземпляра Geometry с экземпляром CircularString в одной инструкции  
 В этом фрагменте кода показывается объявление и создание экземпляра **geometry** с экземпляром **CircularString** в одной инструкции:  
  
```tsql  
DECLARE @g geometry = 'CIRCULARSTRING(0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0)';  
```  
  
### Д. Создание экземпляра Geography с экземпляром CircularString  
 В следующем примере показывается объявление и создание экземпляра **geography** с экземпляром **CircularString**:  
  
```tsql  
DECLARE @g geography = 'CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
```  
  
### Е. Создание экземпляра Geometry с экземпляром CircularString, представляющим прямую  
 В следующем примере показывается создание экземпляра **CircularString** , представляющего прямую:  
  
```tsql  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('CIRCULARSTRING(0 0, 1 2, 2 4)', 0);  
```  
  
## См. также:  
 [Основные сведения о типах пространственных данных](../../relational-databases/spatial/spatial-data-types-overview.md)   
 [CompoundCurve](../../relational-databases/spatial/compoundcurve.md)   
 [MakeValid (тип данных geography)](../../t-sql/spatial-geography/makevalid-geography-data-type.md)   
 [MakeValid (тип данных geometry)](../../t-sql/spatial-geometry/makevalid-geometry-data-type.md)   
 [STIsValid (тип данных geometry)](../../t-sql/spatial-geometry/stisvalid-geometry-data-type.md)   
 [STIsValid (тип данных geography)](../../t-sql/spatial-geography/stisvalid-geography-data-type.md)   
 [STLength (тип данных geometry)](../../t-sql/spatial-geometry/stlength-geometry-data-type.md)   
 [STStartPoint (тип данных geometry)](../../t-sql/spatial-geometry/ststartpoint-geometry-data-type.md)   
 [STEndpoint (тип данных geometry)](../../t-sql/spatial-geometry/stendpoint-geometry-data-type.md)   
 [STPointN (тип данных geometry)](../../t-sql/spatial-geometry/stpointn-geometry-data-type.md)   
 [STNumPoints (тип данных geometry)](../../t-sql/spatial-geometry/stnumpoints-geometry-data-type.md)   
 [STIsRing (тип данных geometry)](../../t-sql/spatial-geometry/stisring-geometry-data-type.md)   
 [STIsClosed (тип данных geometry)](../../t-sql/spatial-geometry/stisclosed-geometry-data-type.md)   
 [STPointOnSurface (тип данных geometry)](../../t-sql/spatial-geometry/stpointonsurface-geometry-data-type.md)   
 [LineString](../../relational-databases/spatial/linestring.md)  
  
  