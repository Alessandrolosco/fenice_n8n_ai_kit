# Fenice N8N AI Kit

**Fenice N8N AI Kit** è un template Docker Compose open-source progettato per inizializzare rapidamente un ambiente completo di AI self-hosted e sviluppo low-code, focalizzato sulla risposta a questionari basati su documenti.

Combina la piattaforma self-hosted n8n con componenti AI compatibili per costruire workflow AI locali che elaborano documenti e rispondono a questionari in modo sicuro e privato.

## Obiettivo

Questo kit permette di rispondere a questionari basandosi sui documenti caricati, utilizzando intelligenza artificiale per estrarre, analizzare e sintetizzare informazioni rilevanti dai documenti archiviati.

## Componenti Inclusi

Basandosi sul file `docker-compose.yml`, i componenti principali del sistema sono:

- **PostgreSQL (postgres)**: Database relazionale utilizzato da n8n per archiviare workflow, credenziali e dati operativi. Gestisce grandi quantità di dati in modo sicuro e affidabile.

- **n8n**: Piattaforma low-code con oltre 400 integrazioni e componenti AI avanzati. È il cuore del sistema, permettendo di creare workflow automatizzati per elaborare documenti, interrogare AI e generare risposte a questionari.

- **Qdrant**: Database vettoriale open-source ad alte prestazioni per l'archiviazione e la ricerca semantica di vettori AI. Utilizzato per indicizzare e ricercare contenuti documentali in modo efficiente.

- **Ollama**: Piattaforma cross-platform per installare e eseguire modelli di linguaggio locali (LLM) come Llama3.2. Fornisce l'intelligenza artificiale necessaria per comprendere e rispondere alle domande.

- **Ollama-pull-llama**: Servizio di inizializzazione che scarica automaticamente il modello Llama3.2 al primo avvio, assicurando che l'AI sia pronta all'uso.

- **Open-WebUI**: Interfaccia web user-friendly per interagire con i modelli AI tramite chat. Permette di testare e utilizzare l'AI in modo intuitivo.

- **Redis (broker)**: Broker di messaggi utilizzato da Paperless-ngx per gestire code e comunicazioni asincrone.

- **PostgreSQL (db)**: Database dedicato per Paperless-ngx, separato da quello di n8n per una migliore organizzazione.

- **Paperless-ngx (webserver)**: Sistema di gestione documenti open-source per archiviare, organizzare, ricercare e OCR documenti PDF e altri file. È il repository centrale per i documenti su cui basare le risposte ai questionari.

## Installazione

### Clonare il Repository

```bash
git clone https://github.com/[tuo-repo]/fenice_n8n_ai_kit.git
cd fenice_n8n_ai_kit
cp .env.example .env  # Aggiorna segreti e password nel file .env
```

### Avviare con Docker Compose

#### Per utenti Nvidia GPU

```bash
docker compose --profile gpu-nvidia up
```

> [!NOTA]
> Se non hai mai utilizzato la GPU Nvidia con Docker, segui le istruzioni di Ollama: https://github.com/ollama/ollama/blob/main/docs/docker.md.

#### Per utenti AMD GPU su Linux

```bash
docker compose --profile gpu-amd up
```

#### Per Mac / Apple Silicon

```bash
docker compose up
```

#### Per tutti gli altri (CPU)

```bash
docker compose --profile cpu up
```

## Utilizzo Rapido

1. Apri http://localhost:5678/ nel browser per accedere a n8n e configurarlo (solo al primo avvio).

2. Carica i tuoi documenti in Paperless-ngx accedendo a http://localhost:8010/. Utilizza le cartelle `consume` e `export` per importare documenti.

3. Crea workflow in n8n per elaborare i documenti: usa nodi AI con Ollama per LLM e Qdrant per vettori, integrandoli con Paperless per recuperare documenti.

4. Interagisci con l'AI tramite Open-WebUI su http://localhost:6641/ per testare risposte a questionari.

5. Costruisci workflow che, ricevendo un questionario, cercano nei documenti archiviati e generano risposte basate su di essi.

## Aggiornamenti

Per aggiornare i container alle versioni più recenti:

```bash
docker compose pull
docker compose up
```

## Letture Consigliate

- [Documentazione n8n](https://docs.n8n.io/) - Guida completa per workflow e nodi AI.
- [Documentazione Paperless-ngx](https://docs.paperless-ngx.com/) - Come gestire documenti.
- [Ollama](https://ollama.com/) - Per modelli AI locali.
- [Qdrant](https://qdrant.tech/) - Database vettoriale.

## Licenza

Questo progetto è sotto licenza Apache License 2.0 - consulta il file LICENSE per dettagli.

## Supporto

Unisciti alla comunità su [n8n Forum](https://community.n8n.io/) per condividere progetti, porre domande e proporre idee. La comunità e il team sono pronti ad aiutare con qualsiasi sfida.
