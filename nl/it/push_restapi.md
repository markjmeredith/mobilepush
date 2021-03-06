---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# API REST Push Notifications
{: #push-api-rest}
Ultimo aggiornamento: 22 maggio 2017
{: .last-updated}

Puoi utilizzare una API (application program interface) REST (Representational State Transfer) per {{site.data.keyword.mobilepushshort}}. Puoi anche utilizzare l'SDK e l'[API Push ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://imfpush.{DomainName}/imfpush/){: new_window} per sviluppare ulteriormente le tue applicazioni client.

Con la API REST Push, i client e le applicazioni server di backend possono accedere alle funzioni {{site.data.keyword.mobilepushshort}}.

- Registrazioni di dispositivi
- Registrazioni
- messaggi
- Sottoscrizioni
- Tag
- Webhook

Per ottenere l'URL di base per la API REST, completa seguente procedura:

1. Crea un'applicazione di backend nella sezione Contenitori tipo del catalogo IBM Cloud® scegliendo MobileFirst Services Starter. In questo modo viene eseguito il bind del servizio {{site.data.keyword.mobilepushshort}} all'applicazione. Puoi anche creare un'istanza del servizio di push e lasciarla senza binding. 
1. Nella pagina principale del catalogo IBM Cloud, vai nell'area **Applicazioni** e quindi seleziona la tua applicazione.
3. Fai clic su **OPZIONI MOBILI**. I valori GUID di applicazione e instradamento sono visualizzati nella parte superiore della pagina dei dettagli per la tua applicazione. La schermata Visualizza credenziali mostra le informazioni sull'AppSecret. Puoi ottenere il segreto applicazione dalle opzioni mobili e anche il segreto client per alcune API.

Puoi inoltre utilizzare la riga di comando per ottenere le credenziali del servizio:

```
    cf create-service-key {push_instance_name} {key_name}

 cf service-key {push_instance_name} {key_name}
```
	{: codeblock}

## Intestazione Accept-Language
{: #push-api-rest-accept}

L'intestazione "Accept-Language" specifica quale lingua utilizzare per i messaggi di errore generati in output dalla [API REST Push ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://imfpush.{DomainName}/imfpush/){: new_window}. Per i messaggi di errore sono supportate le
                seguenti lingue: cinese (semplificato), cinese, (tradizionale), inglese (US), tedesco, francese,
                italiano, giapponese, coreano, portoghese e spagnolo.


## Filtri API REST di Push
{: #push-api-rest-filters}

I filtri definiscono un criterio di ricerca che limita i dati restituiti da una API GET di {{site.data.keyword.mobilepushshort}}. Applica i filtri sul risultato dell'operazione Get che desideri filtrare. Il filtro limita il numero di voci incluse nel risultato. d esempio, puoi utilizzare un filtro per cercare tag il cui nome inizia con "test". 

I filtri possono essere generati utilizzando la seguente sintassi:

**name**: il nome campo su cui viene applicato il filtro.

**operator**: (corrispondenza esatta) oppure =@ (contiene la sottostringa) che descrive la corrispondenza di filtro da utilizzare.

**expression**: i valori da includere nel risultato.

Quando in un'espressione vengono visualizzati una virgola o una barra rovesciata, è necessario eseguirne l'escape
                con una barra rovesciata.

Quando utilizzi più filtri, puoi combinarli utilizzando la logica AND e OR.

- Per la logica AND, utilizza più filtri nella query.
- Per la logica OR, utilizza una virgola nell'espressione di filtro.
- Sia per la logica AND che per quella OR: una singola query può avere sia la logica AND sia quella OR. Ogni filtro viene valutato singolarmente prima che i filtri vengano combinati
                        in un'espressione AND.

Per l'API GET di dispositivo, sono supportate le seguenti combinazioni:
-Il nome è il campo piattaforma.
- Fatta eccezione per la piattaforma, l'operatore può essere == oppure =@
- Per la piattaforma, l'operatore deve essere ==. Se viene utilizzato l'operatore =@, il valore può essere una sottostringa.
- Se viene utilizzato ==, il valore deve essere una stringa di corrispondenza esatta.

Per la API GET di sottoscrizione, sono supportate le seguenti combinazioni:

- Il nome può essere uno di questi campi: tagName o deviceId
- Fatta eccezione per la piattaforma, l'operatore può essere == oppure =@
- Per la piattaforma, l'operatore deve essere ==
- Se viene utilizzato l'operatore =@, il valore può essere una sottostringa. Se viene utilizzato l'operatore ==, il valore deve essere una stringa di corrispondenza esatta.
- Per la API GET di tag, sono supportate le seguenti combinazioni:
- Il nome può essere uno dei seguenti campi: “name” o “description”
- Se viene utilizzato l'operatore =@, il valore può essere una sottostringa.
- Se viene utilizzato ==, il valore deve essere una stringa di corrispondenza esatta.


## Codici di risposta del servizio Push Notifications
{: #push-api-response-codes}

Stato: 405 Metodo non consentito - È previsto un metodo appropriato
