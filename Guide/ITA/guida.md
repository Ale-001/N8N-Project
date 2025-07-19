# 🚀 Guida all'Installazione di n8n in Locale su Windows 11 con Docker

Questa guida ti spiega come installare ed eseguire **n8n** in locale su un computer Windows 11 utilizzando **Docker**. È pensata per utenti principianti, passo dopo passo.

---

## ✅ Requisiti

### 1. Sistema operativo

- Windows 11

---

### 2. Scaricare WSL

```bash
wsl --install
```

---

### 3. Software da installare

- [Docker Desktop per Windows](https://www.docker.com/products/docker-desktop/)
- Facoltativo: un editor di testo (es. Visual Studio Code o Notepad++)

---

## 📦 1. Installazione di Docker Desktop

1. Vai al sito ufficiale: [https://www.docker.com/products/docker-desktop/](https://www.docker.com/products/docker-desktop/)
2. Clicca su **Download for Windows (Windows 11)**
3. Esegui l’installer `.exe` scaricato.
4. Segui la procedura guidata e **riavvia il computer** se richiesto.(Check: Use WSL 2 instead od Hyper-V)
5. Avvia Docker Desktop e verifica che sia **attivo** (icona balena nella barra delle applicazioni).

Verifica della versione

```bash
docker --version
```

---

## 🗂️ 2. Creazione della cartella di progetto

1. Apri **Esplora File**
2. Crea una cartella per il progetto, ad esempio:  
   `C:\Users\TUO_NOME\n8n-docker`

---

## 📝 3. Creazione del container

### Tramite cli

Non va
```bash
docker run -it -d --name n8n -p 5678:5678 -v ~/.n8n_data:/home/node/.n8n docker.io/n8nio/n8n
```

Oppure

Comando Funzionante

```bash
docker run -it -d --name n8n -p 5678:5678 -v C:/Users/biond/n8n_data:/home/node/.n8n -e N8N_BASIC_AUTH_ACTIVE=true -e N8N_BASIC_AUTH_USER=admin -e N8N_BASIC_AUTH_PASSWORD=admin123 n8nio/n8n
```

```bash
docker run -it -d --name n8n `
  -p 5678:5678 `
  -v C:/Users/biond/n8n_data:/home/node/.n8n `
  -e N8N_BASIC_AUTH_ACTIVE=true `
  -e N8N_BASIC_AUTH_USER=admin `
  -e N8N_BASIC_AUTH_PASSWORD=admin123 `
  n8nio/n8n
```

### Tramite file `docker-compose.yml` da testare

1. All'interno della cartella `n8n-docker`, crea un file chiamato `docker-compose.yml`
2. Incolla il seguente contenuto:

```yaml
version: "3.1"

services:
  n8n:
    image: n8nio/n8n
    ports:
      - "5678:5678"
    volumes:
      - ./n8n-data:/home/node/.n8n
    restart: always
    environment:
      - N8N_BASIC_AUTH_ACTIVE=true
      - N8N_BASIC_AUTH_USER=admin
      - N8N_BASIC_AUTH_PASSWORD=admin123
      - TZ=Europe/Rome
```

🔒 **Nota**: Cambia le credenziali `N8N_BASIC_AUTH_USER` e `N8N_BASIC_AUTH_PASSWORD` per maggiore sicurezza.

---

## 🔄 4. Avvio di n8n tramite Docker

1. Apri il prompt dei comandi o PowerShell:
   - Premi `Win + S`, cerca `cmd` o `powershell`, clicca con il tasto destro e scegli “Esegui come amministratore”
2. Naviga nella cartella del progetto:

```bash
cd C:\Users\TUO_NOME\n8n-docker
```

3. Avvia il container:

```bash
docker-compose up -d
```

✅ Questo comando scarica l’immagine Docker di n8n e avvia il servizio in background.

---

## 🌐 5. Accedere all’interfaccia web di n8n

1. Apri il browser
2. Vai a: [http://localhost:5678](http://localhost:5678)
3. Inserisci le credenziali (es. admin / admin123)

---

## 📁 6. Dove vengono salvati i dati?

- I dati persistenti di n8n vengono salvati nella cartella `n8n-data` all'interno della directory del progetto.
- Puoi fare backup semplicemente copiando questa cartella.

---

## 🛑 7. Comandi utili

### Fermare n8n:

```bash
docker-compose down
```

### Riavviare n8n:

```bash
docker-compose up -d
```

### Vedere i log in tempo reale:

```bash
docker-compose logs -f
```

---

## 🔧 8. Risoluzione dei problemi

| Problema                           | Soluzione                                                               |
|------------------------------------|-------------------------------------------------------------------------|
| Docker non si avvia               | Riavvia il computer, controlla se WSL è attivo                          |
| Porta 5678 già in uso             | Modifica la porta nel file `docker-compose.yml`                         |
| n8n non carica nel browser        | Verifica che il container sia attivo con `docker ps`                    |
| Vuoi resettare tutto              | Esegui `docker-compose down -v` (attenzione: cancella i dati)          |

---

## 📚 Link Utili

- [Documentazione ufficiale di n8n](https://docs.n8n.io)
- [Docker Hub n8n](https://hub.docker.com/r/n8nio/n8n)
- [Guida n8n self-hosting](https://docs.n8n.io/hosting/)

---

## ✅ Fine!

Hai ora un'istanza di n8n perfettamente funzionante in locale su Windows 11! 🎉
