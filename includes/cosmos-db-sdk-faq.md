---
author: SnehaGunda
ms.service: cosmos-db
ms.topic: include
ms.date: 11/09/2018
ms.author: sngun
ms.openlocfilehash: 99dddd86c9348c9791d3012b382298bb020e63c9
ms.sourcegitcommit: 3102f886aa962842303c8753fe8fa5324a52834a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "60326857"
---
**1. In che modo i clienti verranno avvisati circa l'SDK in fase di ritiro?**

Microsoft invierà una notifica anticipata 12 mesi prima fine del supporto dell'SDK in fase di ritiro per agevolare la transizione a un SDK supportato. I clienti verranno anche informati tramite vari canali di comunicazione, ad esempio il portale di gestione di Azure, il centro sviluppatori e comunicazioni dirette indirizzate agli amministratori dei servizi indicati.

**2. I clienti potranno creare applicazioni usando la versione dell'SDK di Azure Cosmos DB "in fase di ritiro" durante il periodo di 12 mesi?** 

Sì, durante il periodo di tolleranza di 12 mesi ai clienti sarà garantito l'accesso completo per creare, distribuire e modificare applicazioni tramite la versione dell'SDK di Azure Cosmos DB "in fase di ritiro". Durante il periodo di tolleranza di 12 mesi, i clienti sono invitati a eseguire la migrazione a una versione supportata più recente dell'SDK di Azure Cosmos DB.

**3. I clienti potranno creare e modificare applicazioni usando una versione dell'SDK di Azure Cosmos DB ritirata dopo il periodo di notifica di 12 mesi?**

Dopo il periodo di notifica di 12 mesi, l'SDK verrà ritirato. La piattaforma Azure Cosmos DB non consentirà alcun tentativo di accesso ad Azure Cosmos DB da applicazioni che usano una versione di SDK ritirata. Inoltre, Microsoft non fornirà più il supporto tecnico per la versione di SDK ritirata.

**4. Cosa accade alle applicazioni in esecuzione del cliente che usano una versione non supportata dell'SDK di Azure Cosmos DB?**

Qualsiasi tentativo di connessione al servizio Azure Cosmos DB con una versione di SDK ritirata verrà rifiutato. 

**5. Le nuove funzioni e funzionalità verranno applicate anche a tutti gli SDK non ritirati?**

Le nuove funzioni e funzionalità verranno aggiunte solo alle nuove versioni. Se si usa una versione di SDK precedente non ritirata, le richieste inviate ad Azure Cosmos DB continueranno a funzionare come in precedenza, ma non sarà possibile accedere alle nuove funzionalità.  

**6. Come si deve procedere se non è possibile aggiornare l'applicazione prima della data del ritiro?**

Si consiglia di effettuare l'aggiornamento alla versione di SDK più recente quanto prima. Una volta che un SDK è stato contrassegnato per il ritiro, l'utente ha a disposizione 12 mesi per aggiornare l'applicazione. Se, per qualunque motivo, non è possibile completare l'aggiornamento dell'applicazione entro questo periodo di tempo, contattare il [team di Cosmos DB](mailto:askcosmosdb@microsoft.com) e richiedere assistenza prima della data prevista per il ritiro.

