---
author: rockboyfor
ms.service: virtual-machines
ms.topic: include
origin.date: 10/26/2018
ms.date: 11/26/2018
ms.author: v-yeche
ms.openlocfilehash: 8861396db6f6b680ddb55ce020e5579dc25b118e
ms.sourcegitcommit: 61c8de2e95011c094af18fdf679d5efe5069197b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62097676"
---
È importante tenere presente che esistono due modi per configurare un listener del gruppo di disponibilità in Azure. Questi metodi differiscono nel tipo di servizio di bilanciamento del carico di Azure usato quando si crea il listener. Nella tabella seguente sono descritte le differenze:

| Tipo di servizio di bilanciamento del carico | Implementazione | Usare questo tipo nei seguenti casi: |
| --- | --- | --- |
| **Esterno** |Usa l'*indirizzo IP virtuale pubblico* del servizio cloud che ospita le macchine virtuali. |È necessario accedere al listener dall'esterno della rete virtuale, ad esempio da Internet. |
| **Interno** |Usa un *servizio di bilanciamento del carico interno* con un indirizzo privato per il listener. |È possibile accedere al listener solo dall'interno della stessa rete virtuale. Questa modalità di accesso include la VPN da sito a sito in scenari ibridi. |

> [!IMPORTANT]
> Per un listener che usa l'indirizzo VIP pubblico del servizio cloud (servizio di bilanciamento del carico esterno), non si incorrerà in spese di uscita fin quando il client, il listener e i database si troveranno nella stessa area di Azure. In caso contrario, i dati restituiti tramite il listener vengono considerati in uscita e vengono addebitati i normali costi di trasferimento dati. 
> 
> 

Un servizio di bilanciamento del carico interno può essere configurato solo nelle reti virtuali con ambito a livello di area. Le reti virtuali esistenti che sono state configurate per un gruppo di affinità non possono usare un servizio di bilanciamento del carico interno. Per altre informazioni, vedere [Panoramica del bilanciamento del carico interno](../articles/load-balancer/load-balancer-internal-overview.md).

<!-- Update_Description: update meta properties -->