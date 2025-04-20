# Guida all'Installazione di AgenticSeek (Windows e Linux)

Questa guida ti aiuterà a installare AgenticSeek su **Windows** e **Linux** passo dopo passo.

---

## ✅ Requisiti

- Python **3.10** o superiore
- Docker
- Chrome + ChromeDriver
- Git
- (Opzionale ma consigliato) `ollama` o `lm-studio` per eseguire LLM localmente

---

## 🔧 Installazione su **Windows**

### 1. Clona il repository

Apri il terminale (cmd o PowerShell):

```sh
git clone https://github.com/Fosowl/agenticSeek.git
cd agenticSeek
move .env.example .env
```

### 2. Crea un ambiente virtuale

```sh
python -m venv agentic_seek_env
agentic_seek_env\Scripts\activate
```

### 3. Installa le dipendenze

**Automatico (consigliato):**

```sh
install.bat
```

**Manuale:**

```sh
pip install -r requirements.txt
```

### 4. Avvia i servizi

```sh
start start_services.cmd
```

### 5. Esegui l'assistente

```sh
python cli.py
```

---

## 🐧 Installazione su **Linux**

### 1. Clona il repository

```sh
git clone https://github.com/Fosowl/agenticSeek.git
cd agenticSeek
mv .env.example .env
```

### 2. Crea un ambiente virtuale

```sh
python3 -m venv agentic_seek_env
source agentic_seek_env/bin/activate
```

### 3. Installa le dipendenze

**Automatico (consigliato):**

```sh
./install.sh
```

**Manuale:**

```sh
pip3 install -r requirements.txt
```

### 4. Avvia i servizi

```sh
sudo ./start_services.sh
```

### 5. Esegui l'assistente

```sh
python3 cli.py
```

---

## ⚙️ Configurazione di un LLM Locale

Modifica il file `config.ini`:

```ini
[MAIN]
is_local = True
provider_name = ollama
provider_model = deepseek-r1:14b
provider_server_address = 127.0.0.1:11434
```

Assicurati che Ollama sia attivo:

```sh
ollama serve
```

---

## 🧠 Suggerimenti

- Per evitare problemi con ChromeDriver, scarica la versione compatibile dal sito ufficiale.
- Puoi abilitare l'input vocale modificando il file `config.ini` (`listen = True`).
- Se hai un server potente, puoi eseguire il modello lì e collegarti dal tuo portatile.

---

Per ulteriori dettagli, consulta il [README ufficiale](./README.md).