---
author: WenJason
ms.service: dns
ms.topic: include
origin.date: 11/25/2018
ms.date: 12/24/2018
ms.author: victorh
ms.openlocfilehash: 74031a8dbc9b64d6a09533789eed1296ff334d47
ms.sourcegitcommit: 3102f886aa962842303c8753fe8fa5324a52834a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "60563351"
---
Una zona DNS viene usata per ospitare i record DNS per un particolare dominio. Per iniziare a ospitare il dominio in DNS di Azure, è necessario creare una zona DNS per il nome di dominio. Ogni record DNS per il dominio viene quindi creato all'interno di questa zona DNS.

Il dominio "contoso.com", ad esempio, può contenere diversi record DNS, come "mail.contoso.com" (per un server di posta) e "www.contoso.com" (per un sito Web).

Creazione di una zona DNS in DNS di Azure:

* Il nome della zona deve essere univoco all'interno del gruppo di risorse e la zona non deve esistere già, altrimenti l'operazione non riesce.
* Lo stesso nome di zona può essere usato di nuovo in un gruppo di risorse diverso o in un'altra sottoscrizione di Azure.
* Se più zone condividono lo stesso nome, a ogni istanza vengono assegnati indirizzi di server dei nomi diversi. È possibile configurare solo un set di indirizzi con il registrar.

> [!NOTE]
> Non è necessario essere proprietari di un dominio per creare una zona DNS con questo nome di dominio in DNS di Azure, ma è necessario essere proprietari del dominio per configurare i server dei nomi DNS di Azure come server dei nomi corretti per il nome di dominio con il registrar.
> 
> Per altre informazioni, vedere [Delegare un dominio a DNS di Azure](../articles/dns/dns-domain-delegation.md).