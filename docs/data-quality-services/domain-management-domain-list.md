---
title: "Управление доменами: список доменов | Microsoft Docs"
ms.custom: ""
ms.date: "11/08/2011"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "data-quality-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dqs.dm.domainlist.f1"
ms.assetid: 8df305f0-97ea-4226-811b-979ed862e1f0
caps.latest.revision: 13
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 13
---
# Управление доменами: список доменов
  В этом разделе описываются элементы управления в списке доменов **Управление доменами** страницы в [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). Эта панель управления используется для выбора домена с целью выполнения операций управления. Одна панель управления используется для всех страниц с вкладками на странице **Управление доменами** .  
  
## Параметры  
  
### Список доменов  
 **Домен**  
 Этот список содержит все домены в базе знаний. Операции, выполняемые на страницах с вкладками на правой панели, будут применяться к домену, выбранному в списке. Дополнительные сведения см. в разделе  
  
 **Создание составного домена**  
 Создание нового составного домена в базе знаний. Эта команда отображает диалоговое окно **Создание составного домена** . Для доступа к этой команде щелкните домен правой кнопкой мыши или значок над списком доменов. Дополнительные сведения см. в разделе [Create a Composite Domain](../data-quality-services/create-a-composite-domain.md).  
  
 **Создание домена**  
 Создание нового домена в базе знаний. Эта команда отображает диалоговое окно **Создание домена** . Для доступа к этой команде щелкните домен правой кнопкой мыши или значок над списком доменов. Дополнительные сведения см. в статье [Create a Domain](../data-quality-services/create-a-domain.md).  
  
 **Создать копию выбранного домена**  
 Создание точной копии выбранного домена и добавление его в базу знаний. Ее именем будет имя домена, из которого она была создана, с добавлением «– Copy» к имени. Эта команда доступна, либо, щелкнув правой кнопкой мыши домен и выберите команду **Создать копию**, либо щелкнуть значок над списком доменов. Команда не доступна для составного домена.  
  
 **Импортировать домен из файла данных**  
 Импорт домена из файла DQS. Эта команда отображает диалоговое окно **Импорт из файла данных** , в котором можно просмотреть файловую систему и выбрать файл DQS для отдельного или составного домена. Для доступа к этой команде щелкните значок над списком доменов. Дополнительные сведения см. в статье [Import a Domain from a .dqs File](../data-quality-services/import-a-domain-from-a-dqs-file.md).  
  
 **Удалить домен**  
 Удаление выбранного домена из базы знаний. Эта команда отображает диалоговое окно **Службы SQL Server Data Quality Services** . Если нажать кнопку **Да**, домен и все его данные будут окончательно удалены. Для доступа к этой команде щелкните домен правой кнопкой мыши или значок над списком доменов.  
  
 **Создание связанного домена**  
 Создание домена, связанного с выбранным доменом. Эта команда отображает диалоговое окно **Создание домена** . Эта команда доступна, щелкнув правой кнопкой мыши домен и выберите команду **Создать связанный домен** связанный с выбранным доменом. Домен, с которым устанавливается связь, отображается в диалоговом окне «Создание домена». Команда недоступна для составного домена. Не существует команды для отмены связи двух доменов; чтобы сделать это, удалите связанный домен. Нельзя создать связанный домен для связанного домена. Дополнительные сведения см. в статье [Create a Linked Domain](../data-quality-services/create-a-linked-domain.md).  
  
 Значения связанного домена такие же, как у домена, с которым он связан. Отличаются только имя и свойства домена. Если изменить правило домена, значение домена, ссылочный источник данных или связь на основе термина в домене, с которым установлена связь, правило домена, значение домена, ссылочная источник данных или связь на основе термина в связанном домене также изменятся. Кроме того, если изменить значение в связанном домене, изменение отразится в домене, с которым установлена связь.  
  
 **Экспортировать базу знаний**  
 Экспорт всей базы знаний в файл DQS. Эта команда отображает диалоговое окно **Экспорт в файл данных** . Для доступа к этой команде щелкните значок **Экспортировать данные базы знаний** в верхней части страницы или в разделе **Экспорт** в контекстном меню доменов на панели списка доменов. Дополнительные сведения см. в статье [Export a Knowledge Base to a .dqs File](../data-quality-services/export-a-knowledge-base-to-a-dqs-file.md).  
  
 **Экспортировать домен**  
 Экспорт домена в файл DQS. Эта команда отображает диалоговое окно **Экспорт в файл данных** . Эта команда доступна в **Экспорт** меню на панели меню в верхней части страницы, или щелкнуть правой кнопкой мыши в области списка доменов. Дополнительные сведения см. в статье [Export a Domain to a .dqs File](../data-quality-services/export-a-domain-to-a-dqs-file.md).  
  
  