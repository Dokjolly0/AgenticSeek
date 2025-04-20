<p align="center">
<img align="center" src="./media/whale_readme.jpg">
<p>

--------------------------------------------------------------------------------
[English](./README.md) | Italiano | [中文](./README_CHS.md) | [繁體中文](./README_CHT.md)  | [Français](./README_FR.md) | [日本語](./README_JP.md)

# AgenticSeek: AI simile a Manus alimentato da agenti Deepseek R1.

**Un'alternativa completamente locale a Manus AI**, un assistente AI abilitato alla voce che codifica, esplora il filesystem, naviga sul web e corregge i propri errori senza inviare un singolo byte di dati al cloud. Basato su modelli di ragionamento come DeepSeek R1, questo agente autonomo funziona interamente sul tuo hardware, mantenendo i tuoi dati privati.

[![Visita AgenticSeek](https://img.shields.io/static/v1?label=Sito%20Web&message=AgenticSeek&color=blue&style=flat-square)](https://fosowl.github.io/agenticSeek.html) ![Licenza](https://img.shields.io/badge/licenza-GPL--3.0-green) [![Discord](https://img.shields.io/badge/Discord-Unisciti%20a%20Noi-7289DA?logo=discord&logoColor=white)](https://discord.gg/XSTKZ8nP) [![Twitter](https://img.shields.io/twitter/url/https/twitter.com/fosowl.svg?style=social&label=Aggiornamenti%20%40Fosowl)](https://x.com/Martin993886460)

> 🛠️ **Lavori in Corso** - Cerchiamo collaboratori!

https://github.com/user-attachments/assets/4bd5faf6-459f-4f94-bd1d-238c4b331469

> *Fai una ricerca approfondita su startup AI a Osaka e Tokyo, trova almeno 5, poi salva in research_japan.txt*

> *Puoi creare un gioco Tetris in C?*

> *Vorrei impostare un nuovo indice di progetto come mark2.*

## Caratteristiche:

- **100% Locale**: Niente cloud, gira sul tuo hardware. I tuoi dati restano tuoi.

- **Interazione con il filesystem**: Usa bash per navigare e manipolare i file con facilità.

- **Codifica Autonoma**: Scrive, debugga ed esegue codice in Python, C, Golang e altri linguaggi in arrivo.

- **Routing degli agenti**: Sceglie automaticamente l'agente giusto per il compito.

- **Pianificazione**: Per task complessi, attiva più agenti per pianificare ed eseguire.

- **Navigazione Web Autonoma**: Esplora il web in autonomia.

- **Memoria**: Gestione efficiente della memoria e delle sessioni.

---

## Installazione

Assicurati di avere Chrome Driver, Docker e Python3.10 (o superiore) installati.

Per problemi relativi a Chrome Driver, vedi la sezione **Chromedriver**.

### 1️⃣ **Clona il repository e configura**

```sh
git clone https://github.com/Fosowl/agenticSeek.git
cd agenticSeek
mv .env.example .env
```

### 2️ **Crea un ambiente virtuale**

```sh
python3 -m venv agentic_seek_env
source agentic_seek_env/bin/activate     
# Su Windows: agentic_seek_env\Scripts\activate
```

### 3️⃣ **Installa i pacchetti**

**Installazione Automatica:**

```sh
./install.sh
```

**Manualmente:**

```sh
pip3 install -r requirements.txt
# oppure
python3 setup.py install
```

---

## Configurazione per eseguire LLM localmente

**Raccomandiamo di utilizzare almeno Deepseek 14B, modelli più piccoli avranno difficoltà con i task, specialmente nella navigazione web.**

**Avvia il tuo provider locale**  

Avvia il tuo provider locale, ad esempio con ollama:

```sh
ollama serve
```

Vedi sotto per una lista dei provider locali supportati.

**Aggiorna il config.ini**

Modifica il file config.ini impostando provider_name su un provider supportato e provider_model su `deepseek-r1:14b`

NOTA: `deepseek-r1:14b` è un esempio, usa un modello più grande se l'hardware lo permette.

```sh
[MAIN]
is_local = True
provider_name = ollama # oppure lm-studio, openai, ecc..
provider_model = deepseek-r1:14b
provider_server_address = 127.0.0.1:11434
```

**Lista dei provider locali**

| Provider  | Locale? | Descrizione                                               |
|-----------|--------|-----------------------------------------------------------|
| ollama    | Sì    | Esegui LLM localmente con facilità usando ollama come provider |
| lm-studio  | Sì    | Esegui LLM localmente con LM studio (imposta `provider_name` a `lm-studio`)|
| openai    | Sì     |  Usa API compatibile con OpenAI  |

Passo successivo: [Avvia i servizi ed esegui AgenticSeek](#Avvia-servizi-ed-esegui)  

*Vedi la sezione **Problemi noti** in caso di difficoltà*

*Vedi la sezione **Esegui con un'API** se il tuo hardware non supporta Deepseek localmente*

*Vedi la sezione **Configurazione** per una spiegazione dettagliata del file config.*

---

## Configurazione per eseguire con un'API

Imposta il provider desiderato nel `config.ini`

```sh
[MAIN]
is_local = False
provider_name = openai
provider_model = gpt-4o
provider_server_address = 127.0.0.1:5000
```

ATTENZIONE: Assicurati che non ci siano spazi alla fine nel file di configurazione.

Imposta `is_local` a True se usi un'API locale basata su OpenAI.

Modifica l'indirizzo IP se la tua API basata su OpenAI è eseguita su un server remoto.

Passo successivo: [Avvia i servizi ed esegui AgenticSeek](#Avvia-servizi-ed-esegui)

*Vedi la sezione **Problemi noti** in caso di difficoltà*

*Vedi la sezione **Configurazione** per una spiegazione dettagliata del file config.*

---

## Avvia servizi ed esegui

Attiva l'ambiente virtuale se necessario.
```sh
source agentic_seek_env/bin/activate
```

Avvia i servizi richiesti. Questo avvierà tutti i servizi dal docker-compose.yml, inclusi:
    - searxng
    - redis (richiesto da searxng)
    - frontend

```sh
sudo ./start_services.sh # MacOS
start ./start_services.cmd # Windows
```

**Opzione 1:** Esegui con l'interfaccia CLI.

```sh
python3 cli.py
```

**Opzione 2:** Esegui con l'interfaccia Web.

Nota: Attualmente consigliamo di usare la CLI. L'interfaccia web è in sviluppo attivo.

Avvia il backend.

```sh
python3 api.py
```

Vai su `http://localhost:3000/` per visualizzare l'interfaccia web.

Nota: L'interfaccia web al momento non supporta lo streaming dei messaggi.

---

## Utilizzo

Assicurati che i servizi siano attivi con `./start_services.sh` ed esegui AgenticSeek con `python3 main.py`

```sh
sudo ./start_services.sh
python3 cli.py
```

Verrà mostrato il prompt `>>> ` indicando che AgenticSeek è pronto a ricevere istruzioni.
Puoi anche usare il riconoscimento vocale impostando `listen = True` nel config.

Per uscire, digita `goodbye`.

Ecco alcuni esempi di utilizzo:

### Codifica/Bash

> *Crea un gioco del serpente in Python*

> *Mostrami come moltiplicare matrici in C*

> *Crea un blackjack in Golang*

### Ricerca web

> *Cerca sul web startup tecnologiche interessanti in Giappone che lavorano su ricerca AI avanzata*

> *Puoi trovare online chi ha creato AgenticSeek?*

> *Usa un calcolatore di carburante online per stimare il costo di un viaggio da Nizza a Milano*

### File system

> *Riesci a trovare dove si trova contract.pdf? L'ho perso*

> *Mostrami quanto spazio ho libero sul disco*

> *Segui il readme e installa il progetto in /home/path/project*

### Conversazione

> *Parlami di Rennes, Francia*

> *Dovrei fare un dottorato?*

> *Qual è la migliore routine di allenamento?*

Dopo aver inserito la tua richiesta, AgenticSeek assegnerà l'agente più adatto al task.

Essendo un prototipo iniziale, il sistema di routing degli agenti potrebbe non sempre assegnare l'agente corretto.

Si consiglia quindi di essere molto espliciti su cosa si desidera e su come l'AI dovrebbe procedere. Ad esempio, se vuoi una ricerca web, non chiedere:

`Conosci dei bei paesi per viaggi da soli?`

Ma piuttosto:

`Fai una ricerca web e trova quali sono i migliori paesi per viaggi da soli`

---

## **Bonus: Configurazione per eseguire LLM su un server remoto**  

Se hai un computer potente o un server che puoi utilizzare, ma vuoi accedervi dal tuo laptop, puoi eseguire il LLM su un server remoto.

Sul tuo "server" che eseguirà il modello AI, ottieni l'indirizzo IP

```sh
ip a | grep "inet " | grep -v 127.0.0.1 | awk '{print $2}' | cut -d/ -f1 # IP locale
curl https://ipinfo.io/ip # IP pubblico
```

Nota: Su Windows o macOS, usa ipconfig o ifconfig rispettivamente per trovare l'IP.

Clona il repository ed entra nella cartella `server/`.

```sh
git clone --depth 1 https://github.com/Fosowl/agenticSeek.git
cd agenticSeek/server/
```

Installa i requisiti specifici del server:

```sh
pip3 install -r requirements.txt
```

Esegui lo script del server.

```sh
python3 app.py --provider ollama --port 3333
```

Puoi scegliere tra `ollama` e `llamacpp` come servizio LLM.

Sul tuo computer personale:

Modifica il file `config.ini` impostando `provider_name` a `server` e `provider_model` a `deepseek-r1:xxb`.
Imposta `provider_server_address` all'indirizzo IP della macchina che esegue il modello.

```sh
[MAIN]
is_local = False
provider_name = server
provider_model = deepseek-r1:70b
provider_server_address = x.x.x.x:3333
```

Passo successivo: [Avvia i servizi ed esegui AgenticSeek](#Avvia-servizi-ed-esegui)  

---

## Sintesi vocale

La funzionalità di sintesi vocale è disabilitata di default. Per abilitarla, imposta `listen = True` nel file config.ini:

```
listen = True
```

Quando abilitata, il riconoscimento vocale ascolta una parola chiave di attivazione (il nome dell'agente) prima di elaborare l'input. Puoi personalizzare il nome nell'opzione `agent_name`:

```
agent_name = Friday
```

Per un riconoscimento ottimale, usa un nome inglese comune come "John" o "Emma".

Una volta che vedi apparire la trascrizione, pronuncia il nome dell'agente per attivarlo (es. "Friday").

Pronuncia la tua richiesta chiaramente.

Termina la richiesta con una frase di conferma per far procedere il sistema. Esempi:
```
"do it", "go ahead", "execute", "run", "start", "thanks", "would ya", "please", "okay?", "proceed", "continue", "go on", "do that", "go it", "do you understand?"
```

## Configurazione

Esempio config:
```
[MAIN]
is_local = True
provider_name = ollama
provider_model = deepseek-r1:32b
provider_server_address = 127.0.0.1:11434
agent_name = Friday
recover_last_session = False
save_session = False
speak = False
listen = False
work_dir =  /Users/mlg/Documents/ai_folder
jarvis_personality = False
languages = en zh
[BROWSER]
headless_browser = False
stealth_mode = False
```

**Spiegazione**:

- is_local -> Esegue l'agente localmente (True) o su server remoto (False).

- provider_name -> Provider da usare (es: `ollama`, `server`, `lm-studio`, `deepseek-api`).

- provider_model -> Modello utilizzato, es: deepseek-r1:32b.

- provider_server_address -> Indirizzo server, es: 127.0.0.1:11434 per locale. Imposta a qualsiasi valore per API non locali.

- agent_name -> Nome dell'agente, es: Friday. Usato come parola di attivazione per TTS.

- recover_last_session -> Riprende l'ultima sessione (True) o no (False).

- save_session -> Salva i dati della sessione (True) o no (False).

- speak -> Abilita output vocale (True) o no (False).

- listen -> Abilita input vocale (True) o no (False).

- work_dir -> Cartella accessibile all'AI. es: /Users/user/Documents/.

- jarvis_personality -> Usa una personalità tipo JARVIS (True) o no (False). Modifica semplicemente il prompt.

- languages -> Lingue supportate, necessarie per il routing degli agenti. Evita troppe lingue simili.

- headless_browser -> Esegue il browser senza finestra visibile (True) o no (False).

- stealth_mode -> Rende più difficile il rilevamento come bot. Richiede installazione manuale dell'estensione anticaptcha.

## Provider supportati

| Provider  | Locale? | Descrizione                                               |
|-----------|--------|-----------------------------------------------------------|
| ollama    | Sì    | Esegui LLM localmente con ollama                         |
| server    | Sì    | Hosta il modello su un'altra macchina                    |
| lm-studio  | Sì    | Esegui LLM localmente con LM studio                      |
| openai    | Dipende  | Usa API ChatGPT (non privato) o API compatibili OpenAI  |
| deepseek-api  | No     | API Deepseek (non privato)                             |
| huggingface| No    | API Hugging-Face (non privato)                          |
| togetherAI | No    | Usa API Together AI (non privato)                       |

Per selezionare un provider modifica il config.ini:

```
is_local = True
provider_name = ollama
provider_model = deepseek-r1:32b
provider_server_address = 127.0.0.1:5000
```

# Problemi noti

## Problemi con Chromedriver

**Errore noto #1:** *versione chromedriver non corrispondente*

`Exception: Failed to initialize browser: Message: session not created: This version of ChromeDriver only supports Chrome version 113
Current browser version is 134.0.6998.89 with binary path`

Si verifica se la versione di ChromeDriver non corrisponde a quella del browser installato.

Scarica l'ultima versione corrispondente:

https://developer.chrome.com/docs/chromedriver/downloads

Per Chrome versione 115 o superiore:

https://googlechromelabs.github.io/chrome-for-testing/

![alt text](./media/chromedriver_readme.png)

## FAQ

**D: Di che hardware ho bisogno?**  

| Dimensione Modello  | GPU  | Commento                                               |
|-----------|--------|-----------------------------------------------------------|
| 7B        | 8GB Vram | ⚠️ Sconsigliato. Performance scadenti, allucinazioni frequenti. |
| 14B        | 12 GB VRAM (es. RTX 3060) | ✅ Usabile per task semplici. Difficoltà con web browsing. |
| 32B        | 24+ GB VRAM (es. RTX 4090) | 🚀 Buona riuscita nella maggior parte dei task. |
| 70B+        | 48+ GB Vram (es. mac studio) | 💪 Eccellente. Consigliato per uso avanzato. |

**D: Perché Deepseek R1 invece di altri modelli?**  

Deepseek R1 eccelle nel ragionamento e uso di strumenti per le sue dimensioni. Modelli alternativi funzionano, ma Deepseek è la scelta primaria.

**D: Ottengo un errore eseguendo `cli.py`. Cosa faccio?**  

Verifica che il servizio locale sia attivo (`ollama serve`), che `config.ini` sia corretto e che le dipendenze siano installate. In caso contrario, apri una issue.

**D: È veramente eseguibile al 100% localmente?**  

Sì, con provider come Ollama o lm-studio, tutto il processo (voce, LLM, sintesi) avviene localmente. Le opzioni cloud (API OpenAI) sono opzionali.

**D: Perché usare AgenticSeek invece di Manus?**

Nato come progetto personale, punta a modelli locali e privacy. Ispirato a Jarvis/Friday di Iron Man per l'aspetto "cool", ma funzionalmente simile a Manus come alternativa locale e open-source.

## Contribuisci

Cerchiamo sviluppatori per migliorare AgenticSeek! Consulta le issue aperte o le discussioni.

[Guida al contributo](./docs/CONTRIBUTING.md)

## Maintainers:
 > [Fosowl](https://github.com/Fosowl)
 > [steveh8758](https://github.com/steveh8758)
