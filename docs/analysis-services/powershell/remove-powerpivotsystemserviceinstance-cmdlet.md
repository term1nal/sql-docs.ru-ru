---
title: "Командлет &#171;Remove-PowerPivotSystemServiceInstance&#187; | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: bc46094a-5584-47ba-8883-77dc79373a5d
caps.latest.revision: 10
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 10
---
# Командлет &#171;Remove-PowerPivotSystemServiceInstance&#187;
  Удаляет экземпляр системной службы [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] из фермы.  
  
 **Применимо для следующих объектов:** SharePoint 2010 и SharePoint 2013.  
  
## Синтаксис  
  
```  
Remove-PowerPivotSystemServiceInstance [-Confirm <switch>] [-DeleteLocal <switch>] [-Identity <PowerPivotMidTierServiceInstancePipeBind>] [<CommonParameters>]  
```  
  
## Description  
 Командлет Remove-PowerPivotSystemServiceInstance удаляет сведения об экземпляре системной службы [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] из фермы. Не удаляет программные файлы. Чтобы удалить программные файлы, нужно отменить их установку.  
  
 При удалении системной службы [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] не забудьте выполнить командлет Remove-PowerPivotEngineServiceInstance, чтобы удалить связанный экземпляр служб Analysis Services, а затем командлет Remove-PowerPivotServiceApplication, чтобы удалить все приложения службы PowerPivot. Приложения службы больше не будут работать после удаления служб.  
  
 Чтобы отменить это изменение, можно выполнить команду New-PowerPivotSystemServiceInstance -Provision:$true и заново включить сведения об экземпляре.  
  
## Параметры  
  
### -Identity \<PowerPivotMidTierServiceInstancePipeBind>  
 Указывает идентификатор GUID экземпляра системной службы [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)], который необходимо удалить. На каждом сервере приложений, где установлена надстройка [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] для SharePoint, имеется один экземпляр службы.  
  
|||  
|-|-|  
|Обязательно?|false|  
|Позиция?|0|  
|Значение по умолчанию||  
|Принимать входные данные конвейера?|true|  
|Принимать символы-шаблоны?|false|  
  
### -DeleteLocal \<switch>  
 Удаляет экземпляр системной службы [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)], установленный на локальном компьютере, после чего можно удалить экземпляр без указания удостоверения объекта.  
  
|||  
|-|-|  
|Обязательно?|false|  
|Позиция?|именованный|  
|Значение по умолчанию||  
|Принимать входные данные конвейера?|false|  
|Принимать символы-шаблоны?|false|  
  
### -Confirm \<switch>  
 Выводит приглашение для подтверждения перед выполнением команды. Это значение включено по умолчанию. Чтобы исключить подтверждения в команде, укажите параметр Confirm:$ false.  
  
|||  
|-|-|  
|Обязательно?|false|  
|Позиция?|именованный|  
|Значение по умолчанию||  
|Принимать входные данные конвейера?|false|  
|Принимать символы-шаблоны?|false|  
  
### \<Общие параметры>  
 Этот командлет поддерживает общие параметры: Verbose, Debug, ErrorAction, ErrorVariable, WarningAction, WarningVariable, OutBuffer и OutVariable. Дополнительные сведения см. в разделе [Об общих параметрах](http://go.microsoft.com/fwlink/?linkID=227825).  
  
## Входы и выходы  
 Входной тип — это тип объектов, которые можно направить в командлет. Тип возвращаемого значения — это тип объектов, возвращаемых командлетом.  
  
|||  
|-|-|  
|Входные данные|Нет.|  
|Выходные данные|Нет.|  
  
## Пример 1  
  
```  
C:\PS>Remove-PowerPivotSystemServiceInstance -deletelocal  
```  
  
 В этом примере показано, как удалить экземпляр системной службы [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)], работающий на локальном сервере приложений.  
  
## Пример 2  
  
```  
C:\PS>Remove-PowerPivotSystemServiceInstance -identity 1234567-890a-bcde-fghijklmn  
```  
  
 В этом примере показано, как удалить конкретную системную службу [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] на основе ее удостоверения.  
  
  