---
title: Esempio di script dell'interfaccia della riga di comando di Azure - Creare una rete per applicazioni multilivello | Documentazione Microsoft
description: Esempio di script dell'interfaccia della riga di comando di Azure - Creare una rete virtuale per applicazioni multilivello
services: virtual-network
documentationcenter: virtual-network
author: KumudD
manager: twooley
editor: ''
tags: ''
ms.assetid: ''
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: ''
ms.workload: infrastructure
ms.date: 03/20/2018
ms.author: kumud
ms.openlocfilehash: 9bd6fac54c4f6c86c4e1c624ffc26f626e938e49
ms.sourcegitcommit: 44a85a2ed288f484cc3cdf71d9b51bc0be64cc33
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/28/2019
ms.locfileid: "64715691"
---
# <a name="create-a-network-for-multi-tier-applications-script-sample"></a>Esempio di script per la creazione di una rete per applicazioni multilivello

Questo script di esempio crea una rete virtuale con subnet front-end e back-end. Il traffico verso la subnet front-end è limitato a HTTP e SSH, mentre il traffico verso la subnet back-end è limitato a MySQL sulla porta 3306. Dopo aver eseguito lo script, saranno presenti due macchine virtuali, una in ogni subnet in cui è possibile distribuire server Web e software MySQL.

È possibile eseguire lo script da Azure [Cloud Shell](https://shell.azure.com/bash) o da un'installazione locale dell'interfaccia della riga di comando di Azure. Se si usa l'interfaccia della riga di comando in locale, per questo script è necessaria la versione 2.0.28 o successiva. Per trovare la versione installata, eseguire `az --version`. Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure](/cli/azure/install-azure-cli). Se si esegue l'interfaccia della riga di comando in locale, è anche necessario eseguire `az login` per creare una connessione con Azure.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a>Script di esempio


[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/virtual-network-multi-tier-application/virtual-network-multi-tier-application.sh  "Virtual network for multi-tier application")]

## <a name="clean-up-deployment"></a>Pulire la distribuzione 

Eseguire questo comando per rimuovere il gruppo di risorse, la macchina virtuale e tutte le risorse correlate:

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a>Spiegazione dello script

Questo script usa i comandi seguenti per creare un gruppo di risorse, una rete virtuale e i gruppi di sicurezza di rete. Ogni comando della tabella seguente include collegamenti alla documentazione specifica del comando:

| Comando | Note |
|---|---|
| [az group create](/cli/azure/group) | Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse. |
| [az network vnet create](/cli/azure/network/vnet) | Consente di creare una rete virtuale e una subnet front-end di Azure. |
| [az network subnet create](/cli/azure/network/vnet/subnet) | Consente di creare una subnet back-end. |
| [az network public-ip create](/cli/azure/network/public-ip) | Consente di creare un indirizzo IP pubblico per accedere alla macchina virtuale da Internet. |
| [az network nic create](/cli/azure/network/nic) | Consente di creare interfacce di rete virtuale e di associarle alle subnet front-end e back-end della rete virtuale. |
| [az network nsg create](/cli/azure/network/nsg) | Consente di creare gruppi di sicurezza di rete associati alle subnet front-end e back-end. |
| [az network nsg rule create](/cli/azure/network/nsg/rule) |Consente di creare regole del gruppo di sicurezza di rete che consentono o bloccano porte specifiche su subnet specifiche. |
| [az vm create](/cli/azure/vm) | Consente di creare macchine virtuali e associa una NIC a ogni VM. Questo comando specifica anche l'immagine della macchina virtuale da usare e le credenziali di amministrazione. |
| [az group delete](/cli/azure/group) | Consente di eliminare un gruppo di risorse e tutte le risorse in esso contenute. |

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sull'interfaccia della riga di comando di Azure, vedere la [documentazione sull'interfaccia della riga di comando di Azure](/cli/azure).

Altri esempi di script dell'interfaccia della riga di comando della rete virtuale sono disponibili in [Virtual network CLI samples](../cli-samples.md) (Esempi di interfaccia della riga di comando della rete virtuale).
