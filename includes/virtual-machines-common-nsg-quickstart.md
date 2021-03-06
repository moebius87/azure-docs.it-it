---
title: File di inclusione
description: File di inclusione
services: virtual-machines-windows
author: rockboyfor
ms.service: virtual-machines-windows
ms.topic: include
origin.date: 09/12/2018
ms.date: 11/12/2018
ms.author: v-yeche
ms.custom: include file
ms.openlocfilehash: ec6cbcbc93fe87634c87caeb0041b75ec916a22f
ms.sourcegitcommit: 3102f886aa962842303c8753fe8fa5324a52834a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "60405401"
---
Per aprire una porta, o creare un endpoint, in una macchina virtuale (VM) di Azure si crea un filtro di rete su una subnet o un'interfaccia di rete di VM. Questi filtri, che consentono di controllare il traffico in ingresso e in uscita, vengono inseriti in un gruppo di sicurezza di rete collegato alla risorsa che riceve il traffico.

L'esempio in questo articolo illustra come creare un filtro di rete che usa la porta TCP 80 standard. Si presuppone di avere già avviato i servizi appropriati e di avere aperto le eventuali regole del firewall del sistema operativo nella macchina virtuale.

Dopo aver creato una macchina virtuale configurata per elaborare le richieste Web sulla porta TCP 80 standard, è possibile:

1. Creare un gruppo di sicurezza di rete.

2. Creare una regola di sicurezza in ingresso che consente il traffico e assegnare valori alle impostazioni seguenti:

   - **Intervalli di porte di destinazione**: 80

   - **Intervalli di porte di origine**: * (consente qualsiasi porta di origine)

   - **Valore di priorità**: Immettere un valore che è minore di 65.500 e maggiore priorità rispetto al valore predefinito di catch-all negare regola in ingresso.

3. Associare il gruppo di sicurezza di rete alla subnet o all'interfaccia di rete della macchina virtuale.

    Anche se questo esempio usa una regola semplice per consentire il traffico HTTP, è possibile usare anche regole e gruppi di sicurezza di rete per creare configurazioni di rete più complesse.