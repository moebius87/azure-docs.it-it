---
title: Installare l'interfaccia della riga di comando del controller di dominio/sistema operativo | Documentazione Microsoft
description: Installare l'interfaccia della riga di comando del controller di dominio/sistema operativo.
services: container-service
documentationcenter: ''
author: rgardler
manager: timlt
editor: ''
tags: acs, azure-container-service
keywords: Contenitori, Micro-Service, controller di dominio/sistema operativo, Azure
ms.service: container-service
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/10/2016
ms.author: rogardle
ms.openlocfilehash: e2601d5200f0b8ebcfb856bffb871f01b3acb215
ms.sourcegitcommit: 3102f886aa962842303c8753fe8fa5324a52834a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "60557588"
---
> [!NOTE]
> Questa procedura è necessaria per l'uso di cluster ACS basati su controller di dominio/sistema operativo. Non è necessario eseguirla per i cluster ACS basati su Swarm.
> 
> 

È prima di tutto necessario [connettersi ai cluster ACS basati su controller di dominio/sistema operativo](../articles/container-service/container-service-connect.md). Dopo la connessione, è possibile installare l'interfaccia della riga di comando del controller di dominio/sistema operativo nel computer client con i comandi seguenti:

```bash
sudo pip install virtualenv
mkdir dcos && cd dcos
wget https://raw.githubusercontent.com/mesosphere/dcos-cli/master/bin/install/install-optout-dcos-cli.sh
chmod +x install-optout-dcos-cli.sh
./install-optout-dcos-cli.sh . http://localhost --add-path yes
```

Se si usa una versione precedente di Python, è possibile che vengano visualizzati avvisi di tipo "InsecurePlatformWarnings". È possibile ignorare questi avvisi.

Per iniziare senza riavviare la shell, eseguire:

```bash
source ~/.bashrc
```

Questo passaggio non sarà necessario quando si avviano nuove shell.

È ora possibile verificare che l'interfaccia della riga di comando sia stata installata:

```bash
dcos --help
```