---
title: "Создание проекта служб DQS | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "data-quality-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dqs.dqproject.newdqproject.f1"
helpviewer_keywords: 
  - "создание, проект служб DQS"
  - "проект служб DQS, создание"
ms.assetid: 19c52d2b-d28e-4449-ab59-5fe0dc326cd9
caps.latest.revision: 10
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 10
---
# Создание проекта служб DQS
  В этом разделе описывается создание проекта служб DQS с помощью программы [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]. Проект качества данных используется для выполнения очистки или сопоставления данных в службах [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS).  
  
##  <a name="BeforeYouBegin"></a> Перед началом  
  
###  <a name="Prerequisites"></a> Предварительные требования  
 Необходимо иметь соответствующие базы знаний для использования в проекте качества данных для выполнения очистки или сопоставления данных.  
  
###  <a name="Security"></a> Безопасность  
  
####  <a name="Permissions"></a> Разрешения  
 Для создания проекта служб DQS необходимо иметь роль dqs_kb_editor или dqs_kb_operator в базе данных DQS_MAIN.  
  
##  <a name="Create"></a> Создание проекта служб DQS  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Запустите клиентское приложение DQS](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  На главном экране [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] щелкните **Создать проект служб DQS**.  
  
3.  На экране **Новый проект служб DQS**   
  
    1.  в поле **Имя** введите имя нового проекта служб DQS.  
  
    2.  (Необязательно) В **Описание** Введите описание для нового проекта качества данных.  
  
    3.  В списке **Использовать базу знаний** выберите базу знаний для использования в проекте служб DQS.  **Сведения базы знаний: \< Knowledge_Base_Name >** области справа отображаются имена доменов, доступные в выбранной базе знаний.  
  
    4.  В области **Выбор действия** выберите действие, которое требуется выполнить с помощью этого проекта служб DQS:  
  
        -   **Очистка**. Выберите это действие для очистки источника данных.  
  
        -   **Сопоставление**. Выберите это действие, чтобы выполнить сопоставление. Это действие доступно только в том случае, если база знаний, выбранная для проекта служб DQS, содержит политику сопоставления.  
  
4.  Нажмите **Создать** , чтобы создать проект служб DQS.  
  
##  <a name="FollowUp"></a> Дальнейшие действия. После создания проекта качества данных  
 После того как проект качества данных создан, откроется мастер для выполнения выбранного действия: очистки или сопоставления. Дополнительные сведения об очистке и сопоставлению см. в разделе [очистки данных](../data-quality-services/data-cleansing.md) и [сопоставления данных](../data-quality-services/data-matching.md).  
  
  