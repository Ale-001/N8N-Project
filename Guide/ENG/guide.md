# 🚀 Guide to Installing n8n Locally on Windows 11 with Docker

This guide explains how to install and run **n8n** locally on a Windows 11 computer using **Docker**. It is designed for beginners, step by step.

---

## ✅ Requirements

### 1. Operating System

- Windows 11

---

### 2. Scaricare WSL

```bash
wsl --install
```

---

### 3. Software to Install

- [Docker Desktop for Windows](https://www.docker.com/products/docker-desktop/)
- Optional: a text editor (e.g., Visual Studio Code or Notepad++)

---

## 📦 1. Installing Docker Desktop

1. Visit the official site: [https://www.docker.com/products/docker-desktop/](https://www.docker.com/products/docker-desktop/)
2. Click on **Download for Windows (Windows 11)**
3. Run the downloaded `.exe` installer.
4. Follow the installation steps and **restart your computer** if prompted.(check: Use WSL 2 instead od Hyper-V)
5. Launch Docker Desktop and make sure it is **running** (whale icon in the system tray).

---

## 🗂️ 2. Create the Project Folder

1. Open **File Explorer**
2. Create a folder for the project, for example:  
   `C:\Users\YOUR_NAME\n8n-docker`

---

## 📝 3. Create the `docker-compose.yml` File

1. Inside the `n8n-docker` folder, create a file named `docker-compose.yml`
2. Paste the following content:

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

🔒 **Note**: Change the credentials `N8N_BASIC_AUTH_USER` and `N8N_BASIC_AUTH_PASSWORD` for better security.

---

## 🔄 4. Starting n8n with Docker

1. Open Command Prompt or PowerShell:
   - Press `Win + S`, search for `cmd` or `powershell`, right-click and choose “Run as administrator”
2. Navigate to the project folder:

```bash
cd C:\Users\YOUR_NAME\n8n-docker
```

3. Start the container:

```bash
docker-compose up -d
```

✅ This command pulls the Docker image for n8n and starts the service in the background.

---

## 🌐 5. Accessing the n8n Web Interface

1. Open your web browser
2. Go to: [http://localhost:5678](http://localhost:5678)
3. Enter the login credentials (e.g., admin / admin123)

---

## 📁 6. Where is the Data Stored?

- Persistent data for n8n is stored in the `n8n-data` folder inside the project directory.
- You can back it up simply by copying this folder.

---

## 🛑 7. Useful Commands

### Stop n8n:

```bash
docker-compose down
```

### Restart n8n:

```bash
docker-compose up -d
```

### View logs in real-time:

```bash
docker-compose logs -f
```

---

## 🔧 8. Troubleshooting

| Issue                             | Solution                                                                 |
|----------------------------------|--------------------------------------------------------------------------|
| Docker won't start               | Restart your PC, check if WSL is enabled                                 |
| Port 5678 already in use         | Change the port in the `docker-compose.yml` file                         |
| n8n not loading in browser       | Check if the container is running with `docker ps`                       |
| Want to reset everything         | Run `docker-compose down -v` (warning: this deletes data)                |

---

## 📚 Useful Links

- [Official n8n Documentation](https://docs.n8n.io)
- [n8n on Docker Hub](https://hub.docker.com/r/n8nio/n8n)
- [n8n Self-Hosting Guide](https://docs.n8n.io/hosting/)

---

## ✅ Done!

You now have a fully functional local instance of n8n on Windows 11! 🎉