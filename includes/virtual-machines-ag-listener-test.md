---
author: rockboyfor
ms.service: virtual-machines
ms.topic: include
origin.date: 10/26/2018
ms.date: 11/26/2018
ms.author: v-yeche
ms.openlocfilehash: d579e7a4fd83c1a0ce335e0b2357dcbafb217398
ms.sourcegitcommit: 61c8de2e95011c094af18fdf679d5efe5069197b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62097675"
---
In questo passaggio si testa il listener del gruppo di disponibilità usando un'applicazione client in esecuzione nella stessa rete.

Questi sono i requisiti per la connettività client:

* Le connessioni client al listener devono provenire da computer che si trovano in un servizio cloud diverso da quello che ospita le repliche di disponibilità AlwaysOn.
* Se le repliche AlwaysOn si trovano in subnet diverse, i client devono specificare *MultisubnetFailover=True* nella stringa di connessione. Questa condizione comporta l'esecuzione di tentativi di connessione paralleli alle repliche nelle diverse subnet. Questo scenario include la distribuzione di un gruppo di disponibilità AlwaysOn tra più aree.

È ad esempio possibile connettersi al listener da una delle macchine virtuali nella stessa rete virtuale di Azure (ma non quello che ospita una replica). Un modo semplice per completare questo test consiste nel provare a connettere SQL Server Management Studio al listener del gruppo di disponibilità. Un altro metodo semplice consiste nell'eseguire [SQLCMD.exe](https://technet.microsoft.com/library/ms162773.aspx) come indicato di seguito:

    sqlcmd -S "<ListenerName>,<EndpointPort>" -d "<DatabaseName>" -Q "select @@servername, db_name()" -l 15

> [!NOTE]
> Se il valore EndpointPort è *1433*, non è necessario specificarlo nella chiamata. La chiamata precedente presuppone inoltre che il computer client sia aggiunto allo stesso dominio e che al chiamante siano state concesse autorizzazioni per il database tramite l'autenticazione di Windows.
> 
> 

Durante il test del listener, eseguire il failover del gruppo di disponibilità per assicurarsi che i client possano connettersi al listener attraverso i failover.

<!-- Update_Description: update meta properties -->