---
title: Log di diagnostica Azure Stream all'area di lavoro di Log Analitica in Monitoraggio di Azure
description: Informazioni su come trasmettere log di diagnostica di Azure a un'area di lavoro di Log Analitica in Monitoraggio di Azure.
author: johnkemnetz
services: azure-monitor
ms.service: azure-monitor
ms.topic: conceptual
ms.date: 04/18/2019
ms.author: johnkem
ms.subservice: logs
ms.openlocfilehash: b17978da3195b364f868d33ab7ad9faa1544e9ec
ms.sourcegitcommit: 3102f886aa962842303c8753fe8fa5324a52834a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "60237998"
---
# <a name="stream-azure-diagnostic-logs-to-log-analytics-workspace-in-azure-monitor"></a>Log di diagnostica Azure Stream all'area di lavoro di Log Analitica in Monitoraggio di Azure

**[Log di diagnostica di Azure](diagnostic-logs-overview.md)**  possono essere trasmessi quasi in tempo reale per un'area di lavoro di Log Analitica in Monitoraggio di Azure usando il portale, i cmdlet di PowerShell o CLI di Azure.

## <a name="what-you-can-do-with-diagnostics-logs-in-a-log-analytics-workspace"></a>Operazioni eseguibili con diagnostica di log in un'area di lavoro di Log Analitica

Monitoraggio di Azure fornisce uno strumento di Progettazione query e analitica log flessibile che consente di approfondire i dati di log non elaborati generati dalle risorse di Azure. Le funzionalità includono:

* **Query di log** -scrittura di query avanzate su dati del registro, correlare i log da diverse origini e generano grafici che possono essere aggiunti al dashboard di Azure.
* **Avvisi** -rilevare quando uno o più eventi corrispondano a una particolare query e vengono notificati con una chiamata di posta elettronica o webhook tramite avvisi di monitoraggio di Azure.
* **Analisi avanzata**: applicare algoritmi di machine learning e criteri di ricerca per identificare i possibili problemi risultanti dai log.

## <a name="enable-streaming-of-diagnostic-logs-to-log-analytics-workspace"></a>Abilitare lo streaming dei log di diagnostica all'area di lavoro di Log Analitica

È possibile abilitare la trasmissione dei log di diagnostica a livello di codice tramite il portale o tramite le [API REST di Monitoraggio di Azure](https://docs.microsoft.com/rest/api/monitor/diagnosticsettings). In entrambi i casi, si crea un'impostazione di diagnostica in cui specificare un'area di lavoro Log Analytics, le categorie di log e le metriche da inviare all'area di lavoro. Una **categoria di log** di diagnostica è un tipo di log che una risorsa può fornire.

L'area di lavoro Log Analytics non deve trovarsi nella stessa sottoscrizione della risorsa che emette log, purché l'utente che configura l'impostazione abbia un accesso RBAC appropriato a entrambe le sottoscrizioni.

> [!NOTE]
> L'invio delle metriche multidimensionali tramite impostazioni di diagnostica non è attualmente supportato. Le metriche con dimensioni sono esportate come metriche a singola dimensione di tipo flat e aggregate a livello di valori di dimensione.
>
> *Ad esempio*: la metrica "Messaggi in arrivo" su un hub eventi può essere esplorata e rappresentata in un grafico a livello di singola coda. Tuttavia, in caso di esportazione tramite impostazione di diagnostica, la metrica verrà rappresentata come tutti i messaggi in ingresso in tutte le code nell'hub eventi.
>
>

## <a name="stream-diagnostic-logs-using-the-portal"></a>Eseguire lo streaming dei log di diagnostica usando il portale
1. Nel portale, passare a monitoraggio di Azure e fare clic su **le impostazioni di diagnostica** nel **impostazioni** menu.


2. Facoltativamente filtrare l'elenco in base al tipo di risorsa o al gruppo di risorse, quindi fare clic sulla risorsa per cui si vuole specificare un'impostazione di diagnostica.

3. Se non esiste un'impostazione sulla risorsa selezionata, viene chiesto di creare un'impostazione. Fare clic su "Attiva diagnostica".

   ![Aggiungi impostazione di diagnostica - Nessuna impostazione esistente](media/diagnostic-logs-stream-log-store/diagnostic-settings-none.png)

   Se esistono già impostazioni sulla risorsa, verrò visualizzato un elenco di impostazioni già configurate per questa risorsa. Fare clic su "Add diagnostic setting" (Aggiungi impostazione di diagnostica).

   !["Add diagnostic setting" (Aggiungi impostazione di diagnostica) - impostazioni esistenti](media/diagnostic-logs-stream-log-store/diagnostic-settings-multiple.png)

3. Assegnare all'impostazione un nome e selezionare la casella **Invia a Log Analytics**, quindi selezionare un'area di lavoro Log Analytics.

   !["Add diagnostic setting" (Aggiungi impostazione di diagnostica) - impostazioni esistenti](media/diagnostic-logs-stream-log-store/diagnostic-settings-configure.png)

4. Fare clic su **Save**.

Dopo qualche istante, la nuova impostazione viene visualizzata nell'elenco delle impostazioni per questa risorsa e vengono trasmessi i log di diagnostica a tale area di lavoro non appena vengono generati nuovi dati di eventi. Si noti che potrebbero passare fino a quindici minuti tra l'emissione di un evento e la sua apparizione in Log Analytics.

### <a name="via-powershell-cmdlets"></a>Tramite i cmdlet di PowerShell

[!INCLUDE [updated-for-az](../../../includes/updated-for-az.md)]

Per abilitare la trasmissione tramite i [cmdlet di Azure PowerShell](../../azure-monitor/platform/powershell-quickstart-samples.md), è possibile usare il cmdlet `Set-AzDiagnosticSetting` con i parametri seguenti:

```powershell
Set-AzDiagnosticSetting -ResourceId [your resource ID] -WorkspaceID [resource ID of the Log Analytics workspace] -Categories [list of log categories] -Enabled $true
```

Si noti che la proprietà ID dell'area di lavoro assume l'intero ID della risorsa Azure dell'area di lavoro e non l'ID/chiave dell'area di lavoro visualizzata nel portale Log Analytics.

### <a name="via-azure-cli"></a>Tramite l'interfaccia della riga di comando di Azure

Per abilitare lo streaming tramite l'[interfaccia della riga di comando di Azure](../../azure-monitor/platform/cli-samples.md), è possibile usare il comando [az monitor diagnostic-settings create](/cli/azure/monitor/diagnostic-settings#az-monitor-diagnostic-settings-create).

```azurecli
az monitor diagnostic-settings create --name <diagnostic name> \
    --workspace <log analytics name or object ID> \
    --resource <target resource object ID> \
    --resource-group <log analytics workspace resource group> \
    --logs '[
    {
        "category": <category name>,
        "enabled": true
    }
    ]'
```

È possibile aggiungere altre categorie al log di diagnostica aggiungendo dizionari alla matrice JSON passata come parametro `--logs`.

L'argomento `--resource-group` è obbligatorio solo se `--workspace` non è un ID oggetto.

## <a name="how-do-i-query-the-data-from-a-log-analytics-workspace"></a>Come si eseguono query i dati da un'area di lavoro di Log Analitica?

Nel pannello del log nel portale di monitoraggio di Azure, è possibile eseguire una query dei log di diagnostica come parte della soluzione gestione dei Log sotto la tabella AzureDiagnostics. Esistono inoltre [diverse soluzioni di monitoraggio per risorse di Azure](../../azure-monitor/insights/solutions.md) è possibile installare per ottenere informazioni dettagliate immediate sui dati di log inviati in Monitoraggio di Azure.

### <a name="known-limitation-column-limit-in-azurediagnostics"></a>Limitazioni note: limite di colonna in AzureDiagnostics
Poiché molte risorse inviare tutti i tipi di dati vengono inviati alla stessa tabella (_AzureDiagnostics_), lo schema della tabella è il set degli schemi di tutti i tipi di dati diversi raccolti con privilegi avanzati. Ad esempio, se è stato creato le impostazioni di diagnostica per la raccolta di tipi di dati seguenti, tutti inviati alla stessa area di lavoro:
- Controllare i log di 1 risorsa (con un schema costituito da colonne A, B e C)  
- Log degli errori di 2 risorse (con un schema costituito da colonne D, E e F)  
- Log dei flussi di dati di 3 di risorsa (con un schema costituito da colonne G, H e ho)  
 
La tabella AzureDiagnostics apparirà come segue, con alcuni dati di esempio:  
 
| ResourceProvider | Categoria | Una  | b | C | D | E | F | G | H | I |
| -- | -- | -- | -- | -- | -- | -- | -- | -- | -- | -- |
| Microsoft.Resource1 | Log di controllo | x1 | y1 | z1 |
| Microsoft.Resource2 | ErrorLogs | | | | q1 | w1 | e1 |
| Microsoft.Resource3 | DataFlowLogs | | | | | | | j1 | k1 | l1|
| Microsoft.Resource2 | ErrorLogs | | | | q2 | w2 | e2 |
| Microsoft.Resource3 | DataFlowLogs | | | | | | | j3 | k3 | l3|
| Microsoft.Resource1 | Log di controllo | x5 | y5 | z5 |
| ... |
 
È previsto un limite esplicito di ogni singola tabella di Log di Azure non utilizzare le colonne contenenti più di 500. Una volta raggiunto, verranno eliminate tutte le righe contenenti dati con una colonna all'esterno i primi 500 in fase di inserimento. La tabella AzureDiagnostics è particolarmente sensibili per essere interessate questo limite. In genere ciò accade in quanto un'ampia gamma di origini dati vengono inviati alla stessa area di lavoro o diverse origini di dati molto dettagliati inviate alla stessa area di lavoro. 
 
#### <a name="azure-data-factory"></a>Data factory di Azure  
Azure Data Factory, a causa di un set molto dettagliato dei log, è una risorsa che è noto per essere particolarmente interessate da questo limite. In particolare:  
- *Parametri dell'utente definiti nei confronti di qualsiasi attività nella pipeline*: esisterà una nuova colonna per ogni parametro denominato in modo univoco utenti su qualsiasi attività creata. 
- *Attività input e output*: queste variano in un'attività a altra e generare una grande quantità di colonne loro natura dettagliato. 
 
Come con le proposte di soluzione più ampia riportato di seguito, si consiglia di isolare i log di Azure Data Factory nella propria area di lavoro per ridurre al minimo le probabilità di questi log alcun impatto sugli altri tipi di log vengono raccolti in aree di lavoro. Si prevede di avere curata i log per Azure Data Factory è disponibile a breve.
 
#### <a name="workarounds"></a>Soluzioni alternative
A breve termine, fino a quando non viene ridefinito il limite di 500 colonne, è consigliabile separare i tipi di dati dettagliati in aree di lavoro separate per ridurre la possibilità di raggiungere il limite.
 
Durata, diagnostica di Azure verrà spostati da uno schema unificato, di tipo sparsa in singole tabelle per ogni tipo di dati; combinazione con il supporto per tipi dinamici, ciò migliorerà notevolmente l'usabilità dei dati da inserire i log di Azure tramite il meccanismo di diagnostica di Azure. È possibile già verificarlo per selezionare i tipi di risorse di Azure, ad esempio [Azure Active Directory](https://docs.microsoft.com/azure/active-directory/reports-monitoring/howto-analyze-activity-logs-log-analytics) oppure [Intune](https://docs.microsoft.com/intune/review-logs-using-azure-monitor) i log. Per notizie sui nuovi tipi di risorse in Azure che supportano questi log dettagliati su, vedere la [gli aggiornamenti di Azure](https://azure.microsoft.com/updates/) blog!


## <a name="next-steps"></a>Passaggi successivi

* [Altre informazioni sui log di diagnostica di Azure](diagnostic-logs-overview.md)

