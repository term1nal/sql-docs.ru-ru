---
title: Создание хранимых процедур | Документы Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2dd6079f245b2206186b29f3f3880ff99fd8dac7
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/10/2018
ms.locfileid: "34025221"
---
# <a name="creating-stored-procedures"></a>Создание хранимых процедур
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Для использования любой хранимой процедуры необходимо, чтобы она была связана с классом среды CLR или модели COM. Класс должен быть установлен на сервере, обычно в виде [!INCLUDE[msCoName](../../includes/msconame-md.md)] ActiveX® библиотеки динамической компоновки (DLL) и зарегистрирован как сборка на сервере или в [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] базы данных.  
  
 Хранимые процедуры регистрируются на сервере или в базе данных. Серверные хранимые процедуры могут вызываться из контекста любого запроса. Доступ к хранимым процедурам базы данных имеется, только если контекст базы данных представляет собой базу данных, в которой определена хранимая процедура. Если функции из одной сборки вызывают функции из другой сборки, то необходимо зарегистрировать обе сборки в одном и том же контексте (сервера или базы данных). Для сервера или развернутой [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] базы данных на сервере, можно использовать [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] для регистрации сборки. Для проекта служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] можно использовать конструктор служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] для регистрации сборки в проекте.  
  
> [!IMPORTANT]  
>  Использование сборок COM может представлять угрозу безопасности. По этой причине, а также по ряду других сборки COM в службах [!INCLUDE[ssASversion10](../../includes/ssasversion10-md.md)]являются устаревшими. Поддержка сборок COM в последующих версиях может быть прекращена.  
  
## <a name="registering-a-server-assembly"></a>Регистрация серверной сборки  
 В обозревателе объектов в среде [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] список серверных сборок приведен в папке «Сборки» под экземпляром служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Серверные сборки могут содержать как сборки .NET (среды CLR), так и библиотеки COM.  
  
### <a name="to-create-a-server-assembly"></a>Создание серверной сборки  
  
1.  Разверните экземпляр [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] в обозревателе объектов щелкните правой кнопкой мыши **сборки** папки, а затем щелкните **новую сборку**. При этом отображаются **Регистрация серверной сборки** диалоговое окно.  
  
2.  Для **тип** укажите тип сборки:  
  
    -   Для DLL-библиотеки управляемого кода (среда CLR) задайте сборку .NET.  
  
    -   Для DLL-библиотеки собственного кода (COM) укажите COM DLL.  
  
3.  Для **имя файла**, укажите DLL-Библиотеку, содержащую хранимые процедуры.  
  
4.  Для **имя сборки**, укажите имя для сборки.  
  
5.  Если для отладочной сборки библиотеки будет использовать для отладки хранимых процедур, выберите **включить отладочные данные** флажок. Дополнительные сведения об отладке хранимых процедур см. в разделе [отладки хранимых процедур](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/debugging-stored-procedures.md).  
  
6.  Можно щелкнуть **ОК** для регистрации сборки, немедленно, или на панель инструментов диалогового окна поле, можно щелкнуть команду **сценарий** меню, чтобы создать скрипт действие регистрации в окно запроса, файл или буфер обмена.  
  
 После регистрации серверной сборки ее можно настроить, щелкнув правой кнопкой мыши в обозревателе объектов и выбрав **свойства**.  
  
## <a name="registering-a-database-assembly-on-the-server"></a>Регистрация сборки базы данных на сервере  
 В обозревателе объектов в среде [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] список сборок базы данных приведен в папке «Сборки» под базой данных служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Сборки баз данных могут содержать как сборки .NET (среда CLR), так и библиотеки COM.  
  
### <a name="to-create-a-database-assembly-on-a-server"></a>Создание сборки базы данных на сервере  
  
1.  Разверните экземпляр [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] базы данных в обозревателе объектов щелкните правой кнопкой мыши **сборки** папки, а затем щелкните **новую сборку**. При этом отображаются **регистрация сборки базы данных** диалоговое окно.  
  
2.  Для **тип** укажите тип сборки:  
  
    -   Для DLL-библиотеки управляемого кода (среда CLR) задайте сборку .NET.  
  
    -   Для DLL-библиотеки собственного кода (COM) укажите COM DLL.  
  
3.  Для **имя файла**, укажите DLL-Библиотеку, содержащую хранимые процедуры.  
  
4.  Для **имя сборки**, укажите имя для сборки.  
  
5.  Если для отладочной сборки библиотеки будет использовать для отладки хранимых процедур, выберите **включить отладочные данные** флажок. Дополнительные сведения об отладке хранимых процедур см. в разделе [отладки хранимых процедур](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/debugging-stored-procedures.md).  
  
6.  Можно щелкнуть **ОК** для регистрации сборки, немедленно, или на панель инструментов диалогового окна поле, можно щелкнуть команду **сценарий** меню, чтобы создать скрипт действие регистрации в окно запроса, файл или буфер обмена.  
  
 После регистрации сборки базы данных, его можно настроить, щелкнув правой кнопкой мыши в обозревателе объектов и выбрав **свойства**.  
  
## <a name="registering-a-database-assembly-in-a-project"></a>Регистрация сборки базы данных в проекте  
 В обозревателе объектов в среде [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] список сборок базы данных приведен в папке «Сборки» под проектом служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Сборки баз данных могут содержать как сборки .NET (среда CLR), так и библиотеки COM.  
  
### <a name="to-create-a-database-assembly-in-an-analysis-service-project"></a>Создание сборки базы данных в проекте служб Analysis Service  
  
1.  Разверните экземпляр [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] базы данных в обозревателе объектов щелкните правой кнопкой мыши **сборки** папки, а затем щелкните **создать ссылку на сборку**. При этом отображаются **добавить ссылку** диалоговое окно. **.NET** вкладке **добавить ссылку** диалоговом окне приводится список существующих сборок .NET (среды CLR), пока **проекты** содержится список проектов.  
  
2.  Можно щелкнуть существующий компонент или проект и нажмите кнопку **добавить** Чтобы добавить его в [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] проекта. Чтобы добавить ссылку на DLL-библиотеку COM, щелкните **Обзор** вкладку, чтобы найти файл. **Выбранные проекты и компоненты** список содержит имя, тип, версия и расположение для каждого компонента, добавляется в проект.  
  
3.  По окончании выбора компонентов для добавления щелкните **ОК** их добавления в [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] проекта.  
  
## <a name="script-format-for-an-assembly"></a>Формат скрипта для сборки  
 Регистрация сборки .NET довольно проста. Сборка .NET добавляется к базе данных в бинарном виде с использованием следующего формата:  
  
```  
<Create>  
   <ObjectDefinition>  
      <Assembly>  
         <Files>  
            <File>  
               <Name>filename</Name>  
               <Type>filetype</Type>  
               <Data>  
                  <Block>binarydatablock</Block>  
                  <Block>binarydatablock</Block>  
                  ...  
               </Data>  
            </File>  
         </Files>  
         <PermissionSet>PermissionSet</PermissionSet>  
      </Assembly>  
   <ObjectDefinition>  
</Create>  
```  
  
## <a name="see-also"></a>См. также  
 [Управление сборками многомерной модели](../../analysis-services/multidimensional-models/multidimensional-model-assemblies-management.md)   
 [Определение хранимых процедур](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)  
  
  
