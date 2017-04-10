---
title: "Использование кода на языке R в Transact-SQL (службы SQL Server R Services) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/10/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
dev_langs: 
  - "R"
ms.assetid: 4e6fe30d-a105-4d5b-bc05-5e5204753847
caps.latest.revision: 36
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 28
---
# Использование кода на языке R в Transact-SQL (службы SQL Server R Services)
В этом руководстве приведены короткие примеры синтаксиса для работы с языком R в службах SQL Server R Services.    
    
    
Они могут послужить отправной точкой, если вы не знакомы со службами SQL Server R Services и хотите узнать основные принципы определения скриптов R в хранимых процедурах T-SQL, указания входных данных и определения выходных данных.    
    
**Предварительные требования.** Для запуска кода на языке R в службах SQL Server R Services требуется подключение к экземпляру SQL Server, на котором уже установлены службы R Services.     
    
## Часть 1. Основные операции  

В последующих разделах вы узнаете, как расширить хранимую процедуру, добавив параметры, и как настроить входные и выходные данные.   
  
### 1.1. Проверка того, работает ли среда выполнения R в SQL Server  

В этом запросе используется системная хранимая процедура [sp_execute_external_script](https://msdn.microsoft.com/library/mt604368.aspx), служащая для вызова R в контексте SQL Server. В примере запрос SQL передается в качестве входных данных в среду выполнения R, которая возвращает кадр данных в SQL Server.     
    
1. В меню "Пуск" Windows найдите среду Microsoft SQL Server Management Studio.     
2. Если ее не удается найти, возможно, ее необходимо установить: [Скачивание SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).    
3. В диалоговом окне **Соединение с сервером** введите имя сервера или экземпляра с включенными службами SQL Server R Services. В этих примерах необходимо использовать для входа учетную запись с правами на создание базы данных, выполнение инструкций SELECT и просмотр таблиц.  Откройте новое окно **Запрос** и вставьте следующую инструкцию, чтобы проверить, все ли работает:    
    
    ```sql   
    exec sp_execute_external_script  
      @language =N'R',    
      @script=N'OutputDataSet<-InputDataSet',      
      @input_data_1 =N'select 1 as hello'    
      with result sets (([hello] int not null));    
    go    
    ```   
       
       
  
### <a name="bkmk_SSMSBasics"></a>1.2. Создание простых тестовых данных  
    
Перед разработкой сложного решения для обработки и анализа данных необходимо понимать различия между SQL Server и R.    
  
1. Создайте временную таблицу данных, выполнив следующую инструкцию T-SQL.     
   
    ```sql    
    CREATE TABLE #MyData ([Col1] int not null) ON [PRIMARY]    
    INSERT INTO #MyData   VALUES (1);    
    INSERT INTO #MyData   Values (10);    
    INSERT INTO #MyData   Values (100) ;    
    GO    
    ```    
5. После создания таблицы используйте следующую инструкцию, чтобы выполнить запрос к ней:  
    ```sql  
    SELECT * from #MyData  
    ```  

**Результаты**  
  
|Col1 |   
|----|   
|1|   
|10|   
|100|   
  
    
### 1.3. Получение тестовых данных с помощью скрипта R    
  
После создания таблицы выполните следующую инструкцию:  
  
  ```sql    
    execute sp_execute_external_script    
      @language = N'R'    
    , @script = N' OutputDataSet <- InputDataSet;'    
    , @input_data_1 = N' SELECT *  FROM #MyData;'    
    WITH RESULT SETS (([NewColName] int NOT NULL));
  ```    
    
Она должна вернуть те же значения, но с новым именем столбца.  
  
**Примечания**    
- Параметр *@language* определяет вызываемое расширение языка (в данном случае R).    
- В параметре *@script* определяются команды, передаваемые в среду выполнения R в виде текста в Юникоде. Также можно добавить текст в переменную типа **nvarchar** и затем вызвать ее.    
- Строка `N'OutputDataSet <- InputDataSet;'` передает входные данные, содержащиеся в переменной по умолчанию с именем **InputDataSet**, в среду R, а затем возвращает результаты, не выполняя других операций. Обратите внимание на то, что в языке R учитывается регистр, поэтому в именах входных и выходных переменных должен использоваться правильный регистр, иначе произойдет ошибка.    
   
    
Чтобы указать другую входную или выходную переменную, используйте параметр *@input_data_1_name* и введите допустимый идентификатор SQL. В этом примере имена выходной и входной переменных были изменены на *SQLOut* и *SQLIn* соответственно:    
    
```sql    
    execute sp_execute_external_script    
      @language = N'R'    
    , @script = N' SQLOut <- SQLIn;'    
    , @input_data_1 = N' SELECT 12 as Col;'    
    , @input_data_1_name  = N'SQLIn'    
    , @output_data_1_name =  N'SQLOut'    
    WITH RESULT SETS (([NewColName] int NOT NULL));    
```    
    
**Примечания**    
- Чтобы использовать дополнительные параметры *@input_data_1_name* и *@output_data_1_name*, сначала необходимо задать обязательные параметры *@input_data_1* и *@output_data_1*.    
- Типы данных, поддерживаемые в языках SQL и R, не совпадают, поэтому при передаче данных из SQL Server в R и наоборот часто производится преобразование типов. Дополнительные сведения см. в разделе [Работа с типами данных R](../../advanced-analytics/r-services/working-with-r-data-types.md).    
- В качестве параметра можно передать только один входной набор данных. Возвращаться может также только один набор данных. Однако вы можете вызывать другие наборы данных из кода R, а в дополнение к набору данных могут возвращаться выходные данные других типов. Кроме того, вы можете добавить ключевое слово OUTPUT к любому параметру, чтобы он возвращался с результатами.      
- Схема возвращаемого набора данных (R data.frame) определяется инструкцией `WITH RESULT SETS`. Попробуйте опустить ее и посмотрите, что получится.    
- Табличные результаты возвращаются в области **Значения**. Сообщения, возвращаемые средой выполнения R, приводятся в области **Сообщения**.     
  
### 1.4. Формирование результатов с помощью R    
    
Можно также создать значения с помощью скрипта R и оставить пустой строку ввода запроса в _@input_data_1_. Можно также использовать допустимую инструкцию SQL SELECT в качестве заполнителя, но не использовать результаты SQL в скрипте R.    
    
```sql    
    execute sp_execute_external_script    
      @language = N'R'    
    , @script = N' mytextvariable <- c("hello", " ", "world");    
                         OutputDataSet <- as.data.frame(mytextvariable);'    
    , @input_data_1 = N' SELECT 1 as Temp1'    
    WITH RESULT SETS (([col] char(20) NOT NULL));    
```    
    
**Результаты**    
    
    
 |*col* |    
 |-----|    
 |*hello*|    
 |     |    
 |*мир*|    
    

Попробуйте разные версии примера Hello World, приведенные выше.     
    
```sql    
    execute sp_execute_external_script    
      @language = N'R'    
    , @script = N' OutputDataSet<- data.frame(c("hello"), " ", c("world"));'    
    , @input_data_1 = N'  '    
    WITH RESULT SETS (([col1] varchar(20) , [col2] char(1), [col3] varchar(20) ));    
```    
    
    
**Результаты**    
    
    
 |*col1* | *col2* | *col3*|    
 |-------|-------|-------    
 |*hello*|  |*мир*|    
    
Обратите внимание, что обе инструкции создают вектор с тремя значениями, но во втором примере возвращаются три столбца с одной строкой, а в первом — один столбец с тремя строками. Почему?
    
Дело в том, что язык R предоставляет множество способов работы со столбцами значений: векторы, матрицы, массивы и списки. Хотя операции с ними отличаются высокой эффективностью и гибкостью, они не всегда отвечают ожиданиям разработчиков SQL.  Некоторые функции R выполняют неявное преобразование объекта данных для списков и матриц.

> [!TIP] 
> 
> Всегда проверяйте результаты и определяйте, сколько столбцов данных будет возвращать код на языке R и какие типы будут иметь данные.    
>     
> Независимо от того, используются ли в коде R матрицы, векторы или какие-то другие структуры данных, помните, что результат, который выводится из скрипта R в хранимую процедуру, должен иметь тип **data.frame**.      
  
  
## Часть 2. Преобразование данных и другие проблемы  
  
Этот раздел содержит общие сведения о некоторых проблемах, которые следует учитывать при выполнении кода R в SQL Server.  
  
+ Типы данных — варианты приведения и преобразования, а также неявные преобразования  
+ Табличные наборы результатов — способы изменения столбцов и строк данных в языке R    
  
### 2.1. Неявное приведение типов данных  
    
В языках R и SQL Server используются разные типы данных, поэтому при переносе данных из R в базу данных и наоборот необходимо учитывать ряд ограничений. В приведенных ниже примерах иллюстрируются некоторые из распространенных проблем.   
    
    
1. Выполните следующую инструкцию для умножения матриц с помощью языка R. В этом скрипте один столбец из трех значений преобразуется в матрицу с одним столбцом.  Затем R неявно приводит вторую переменную (`y`) к матрице с одним столбцом, чтобы аргументы соответствовали друг другу.  
    
    ```sql    
    execute sp_execute_external_script    
      @language = N'R'    
      , @script = N'    
        x <- as.matrix(InputDataSet);    
        y <- array(12:15);    
      OutputDataSet <- as.data.frame(x %*% y);'    
     , @input_data_1 = N' SELECT [Col1]  from #MyData;'    
      WITH RESULT SETS (([Col1] int, [Col2] int, [Col3] int, Col4 int));    
    ```    
**Результаты**

|Col1|Col2|Col3|Col4|
|---|---|---|---|
|12|13|14|15|
|120|130|140|150|
|1200|1300|1400|1500|
 
  
      
2. Теперь запустите следующий похожий скрипт и посмотрите, что произойдет, если изменить длину массива. 
   
    ```sql    
    execute sp_execute_external_script    
      @language = N'R'    
      , @script = N'    
        x <- as.matrix(InputDataSet);    
        y <- array(12:14);    
      OutputDataSet <- as.data.frame(y %*% x);'    
      , @input_data_1 = N' SELECT [Col1]  from #MyData;'    
      WITH RESULT SETS (([Col1] int ));    
    ```    

**Результаты**    
    
|Col1|
|---|    
|1542|    
  
  На этот раз код R вернет одно значение в качестве результата. Такой результат допустим, так как оба аргумента являются векторами одинаковой длины, поэтому код R вернет скалярное произведение в виде матрицы.    
    
   
  
### 2.2. Слияние или перемножение столбцов разной длины    
    
  
Следующий скрипт иллюстрирует поведение R, которое может быть неожиданным для разработчика базы данных.   
  
Скрипт определяет новый числовой массив, длина которого равна 6, и сохраняет его в переменной R `df1`. Затем числовой массив объединяется с целыми числами из таблицы #MyData, которая содержит три значения, для формирования нового кадра данных — `df2`.   
    
```sql    
    execute sp_execute_external_script    
      @language = N'R'    
    , @script = N'    
               df1 <- as.data.frame( array(1:6) );    
               df2 <- as.data.frame( c( InputDataSet , df1 ));    
               OutputDataSet <- df2'    
    , @input_data_1 = N' SELECT [Col1]  from #MyData;'    
    WITH RESULT SETS (( [Col2] int not null, [Col3] int not null ));    
```    
    
**Результаты**    
    
|*Col2*|*Col3*|    
|----|----|    
|1|1|    
|10|2|    
|100|3|    
|1|4|    
|10|5|    
|100|6|    
    
В языке R есть множество функций, которые создают табличные выходные данные, но выполняют другие операции со значениями в зависимости от объекта данных R. Так как эта хранимая процедура [!INCLUDE[tsql](../../includes/tsql-md.md)] требует, чтобы как входные, так и выходные данные передавались в виде кадра данных, вы часто будете использовать функции для преобразования столбцов и строк в кадры данных и наоборот.    
    
Если у вас есть сомнения по поводу того, какой объект данных R используется, добавьте функцию R `str()` или одну из функций определения (`is.matrix`, `is.vector` и т. д.) для проверки результатов и получения фактической схемы и типов значений.    
  
  
Дополнительные сведения см. в статье Хедли Уикема (Hadley Wickham), посвященной [структурам данных R](http://adv-r.had.co.nz/Data-structures.html).    
    
### 2.3. Определение типов данных и проверка схем   
Очевидно, что необходимо точно знать, сколько столбцов будет возвращено из кода на языке R и какой тип данных будет иметь каждый столбец.     
    
  
В скрипте R можно использовать функцию `str()` для получения сведений о схеме данных возвращаемого объекта R в виде информационного сообщения в . 

Например, приведенная ниже инструкция возвращает схему таблицы #MyData.    
        
```sql    
    execute sp_execute_external_script    
      @language = N'R'    
    , @script = N' str(InputDataSet);'    
    , @input_data_1 = N' SELECT *  FROM #MyData;'    
      WITH RESULT SETS undefined;    
```    
    
    
**Результаты**    
    
*Сообщения STDOUT из внешнего скрипта:*    
*"data.frame": 3 наблюдения 1 переменной:*    
*Сообщения STDOUT из внешнего скрипта:*    
*$ Col1: int 1   10   100*    
    
  
  
### 2.4. Приведение или преобразование столбцов   
  
При передаче данных из SQL Server в R часто приходится приводить или преобразовывать типы данных, чтобы обеспечить их правильную обработку.    
  
При использовании запроса SQL в качестве входных данных для кода на языке R производится несколько преобразований данных:    
- SQL Server передает данные из запроса в процесс R, которым управляет служба Launchpad, и преобразует их во внутреннее представление.    
- Среда выполнения R загружает данные в переменную data.frame и выполняет собственные операции с данными.    
- Ядро СУБД возвращает данные в среду Management Studio или другой клиент, используя типы данных SQL Server.  
    
1. Выполните приведенный ниже запрос к хранилищу данных AdventureWorksDW. Входной запрос данных определяет таблицу данных по продажам, которая должна использоваться при создании прогноза.   
  
    ```sql    
    execute sp_execute_external_script    
       @language = N'R'    
      , @script = N' str(InputDataSet);'    
      , @input_data_1 = N'
           SELECT ReportingDate    
         , CAST(ModelRegion as varchar(50)) as ProductSeries    
         , Amount    
           FROM [AdventureworksDW2016CTP3].[dbo].[vTimeSeries]     
           WHERE [ModelRegion] = ''M200 Europe''    
           ORDER BY ReportingDate ASC ;'    
        WITH RESULT SETS undefined;    
    ```    
  
2. Теперь изучите результаты функции `str`, чтобы увидеть, как среда R обработала входные данные.
      
**Результаты**    
    
  *Сообщения STDOUT из внешнего скрипта: "data.frame":    37 наблюдений 3 переменных:*    
  *Сообщения STDOUT из внешнего скрипта: $ ReportingDate: POSIXct, формат: "2010-12-24 23:00:00" "2010-12-24 23:00:00"*    
  *Сообщения STDOUT из внешнего скрипта: $ ProductSeries: фактор с 1 уровнем "M200 Europe",..: 1 1 1 1 1 1 1 1 1 1 ...*    
  *Сообщения STDOUT из внешнего скрипта: $ Amount       : num  3400 16925 20350 16950 16950*    
    
    
**Примечания**    
    
- Некоторые типы данных SQL Server не поддерживаются языком R. Поэтому во избежание ошибок следует указывать столбцы по отдельности и использовать для некоторых из них приведение типа.    
- Строковый предикат в предложении WHERE должен заключаться в два набора одинарных кавычек.    
- Столбец datetime был возвращен как тип данных R **POSIXct**.    
- Столбец [ProductSeries] был определен (правильно) как **фактор**.    
     
  
### 2.5. Использование нескольких наборов входных данных   
В качестве параметра можно передать только один входной набор данных. Однако вы можете вызывать другие наборы данных из кода на языке R с помощью RODBC.     
  
Например, в приведенном ниже примере осуществляется вызов пакета RODBC, причем данные указываются в инструкции SELECT.    
    
```sql    
    @script = N' 
       <other R code here>;    
       library(RODBC);    
       connStr <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");        dbhandle <- odbcDriverConnect(connStr)    
       OutputDataSet <- sqlQuery(dbhandle, "SELECT * from <table_name>");    
       <more R code combining the data>'    
```

Рекомендуется использовать RODBC для получения из SQL Server наборов данных меньшего размера, например уточняющих запросов или списков факторов, а параметр @input_data — для получения больших наборов данных, например используемых для обучения модели. 


### 2.6. Создание нескольких наборов выходных данных

В SQL Server 2016 выходные данные R из хранимой процедуры sp_execute_external_script ограничены одним кадром или набором данных. (Это ограничение может быть снято в будущем.)   
Однако в дополнение к набору данных могут возвращаться выходные данные других типов. Например, для обучения модели может использоваться один набор входных данных, но возвращаться может таблица статистических данных, а также модель обучения в виде объекта.    
    
Кроме того, вы можете добавить ключевое слово `OUTPUT` к любому входному параметру, чтобы он возвращался с результатами.   
    
### 2.7. Параллельная обработка    
    
Если вы работаете с большим набором данных и запрос SQL, получающий данные, может создать параллельный план запроса, то скрипт R можно выполнять в параллельном режиме, присвоив параметру *@parallel* значение 1. Обычно это бывает полезно при анализе большого набора результатов. При использовании этого параметра необходимо заранее задать схему результатов с помощью предложения WITH RESULT SETS.    
    
Однако этот параметр не будет иметь никакого эффекта, если необходимо обучить модель, которая использует все строки. В таких случаях рекомендуется применять пакеты **ScaleR**. Эти пакеты могут автоматически распределять обработку без указания значения *@parallel =1* в вызове процедуры sp_execute_external_script.    
    
      
  
## Часть 3. Упаковка функций R в хранимые процедуры  
  
Язык R может выполнять множество статистических функций. Чтобы воспроизвести их с помощью T-SQL, может потребоваться написание сложного кода.  Но с помощью служб R можно запускать служебные скрипты R в хранимой процедуре для поддержки следующих задач:   
    
- применение математических и статистических функций R к данным SQL Server;    
    
- создание функций с табличными значениями или скалярных функций, использующих код на языке R.    
     

 Как правило, вызовы этих функций R инкапсулируются в хранимых процедурах, чтобы было проще передавать параметры. Проиллюстрируем этот процесс. Одна и та же функция предоставляется в коде R в вызове динамической хранимой процедуры sp_execute_external_script, а также в хранимой процедуре, которая позволяет параметризовать функцию языка R.
 
      
### 3.1. Создание случайных чисел  
  
В приведенной ниже инструкции используется одна из функций R из пакета `stats`, который загружается по умолчанию при установке служб R. Показанная здесь функция `rnorm` создает 20 случайных чисел с нормальным распределением и средним значением 100.    

Ниже приведен необходимый код R.

```r
as.data.frame(rnorm(20, mean = 100));
```

Эта инструкция вызывает функцию из T-SQL и выводит результаты в SQL Server.  
   
```sql    
EXEC sp_execute_external_script    
      @language = N'R'    
    , @script = N' 
         OutputDataSet <- as.data.frame(rnorm(20, mean = 100));'    
    , @input_data_1 = N'   ;'    
      WITH RESULT SETS (([Density] float NOT NULL));    
```    

Затем хранимая процедура упаковывается в другую хранимую процедуру, чтобы было проще передавать параметры. Необходимо определить каждый из входных параметров в аргументе _@params_ и сопоставить их по имени с соответствующим параметром R.

```sql
CREATE PROCEDURE MyRNorm (@mynorm int, @mymean int)
AS
    EXEC sp_execute_external_script    
      @language = N'R'    
    , @script = N'
         OutputDataSet <- as.data.frame(rnorm(mynorm, mymean));'    
    , @input_data_1 = N'   ;' 
    , @params = N' @mynorm int, @mymean int'  
    , @mynorm = @mynorm
    , @mymean = @mymean
    WITH RESULT SETS (([Density] float NOT NULL));    
```

Вызовите новую хранимую процедуру и передайте значения.

```sql
exec MyRNorm @mynorm = 20,@mymean = 100
```  
    
### 3.2. Дополнительные способы использования служебных функций R  
  
В этом примере вызывается один из служебных пакетов R и используется его функция `memory.limit()` с целью получения памяти для текущей среды. Пакет `utils` по умолчанию устанавливается, но не загружается.    
    
```sql    
execute sp_execute_external_script    
      @language = N'R'    
    , @script = N'    
        library(utils);    
        mymemory <- memory.limit();    
        OutputDataSet <- as.data.frame(mymemory);'    
    , @input_data_1 = N' ;'    
     WITH RESULT SETS (([Col1] int not null));    
```    

В следующем примере с помощью функции R .Machine возвращается максимальная длина целых чисел, которые поддерживаются на текущем компьютере, и выводится на консоль.

```R
localmax <- .Machine$integer.max;
localmax;
```

```sql
execute sp_execute_external_script
  @language = N'R'
  , @script = N'
      localmax <- .Machine$integer.max;
      OutputDataSet <- as.data.frame(localmax);'
  , @input_data_1 = N'select [Col1]  from #MyData;'
  WITH RESULT SETS (([MaxIntValue] int not null));
```     
    
Но не всегда использование языка R является оптимальным. Некоторые операции с множествами, которые специалисты по обработке и анализу данных традиционно выполняют на языке R, в SQL Server могут быть гораздо более эффективны. Пример сравнения производительности функций R и настраиваемых функций T-SQL см. в разделе [Сквозное решение обработки и анализа данных](../../advanced-analytics/r-services/data-science-end-to-end-walkthrough.md). 

В каждом конкретном случае следует решить, как рациональнее выполнить данную операцию: с помощью R, T-SQL или какого-либо иного средства.    
    
    
    
### Дополнительные ресурсы    
    
[Глубокое погружение в обработку и анализ данных: использование пакетов RevoScaleR](../../advanced-analytics/r-services/data-science-deep-dive-using-the-revoscaler-packages.md) — в этом пошаговом руководстве приводятся практические рекомендации по выполнению распространенных задач обработки и анализа данных.    
[Комплексное решение для обработки и анализа данных](../../advanced-analytics/r-services/data-science-end-to-end-walkthrough.md) — в этом пошаговом руководстве показан процесс разработки и развертывания, в котором совмещаются подходы на основе языков SQL и R.       
[Дополнительные аналитические функции для разработчика SQL](../../advanced-analytics/r-services/in-database-advanced-analytics-for-sql-developers-tutorial.md) — показан весь процесс ввода модели в эксплуатацию для разработчика SQL.     
    
    
    
    