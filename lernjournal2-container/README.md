# Lernjournal 2 Container

## Docker Web-Applikation

### Verwendete Docker Images

| | Bitte ausfüllen |
| -------- | ------- |
| Image 1 | Name/Bezeichnung |
| Image 1 | URL Docker Hub |
| Image 2 | ML EfficientNet-Lite4 |
| Image 2 | https://hub.docker.com/r/weyerma2/lernjournal |
| ... | ... |
| Docker Compose | https://github.com/weyerma2/lernjournal2 |

### Dokumentation manuelles Deployment
# 1. Lokale Umgebung aktivieren (z. B. conda, venv)
conda activate ai_env

# 2. Abhängigkeiten installieren
pip install -r requirements.txt

# 3. App starten
python app.py

<img width="511" alt="Screenshot 2025-03-17 at 12 03 07" src="https://github.com/weyerma2/MDM-Lernjournal/blob/main/lernjournal2-container/images/html.jpeg" />

### Dokumentation Docker-Compose Deployment

services:
  lernjournal:
    image: weyerma2/lernjournal:v1
    ports:
      - "8000:8000"
    restart: unless-stopped

# 1. Docker Compose starten
docker compose up -d

# 2. Logs anzeigen
docker compose logs -f

# 3. Stoppen
docker compose down

## Deployment ML-App

# Image taggen
docker tag onnx-img weyerma2/lernjournal:v1

# Docker Login
docker login

# Image pushen
docker push weyerma2/lernjournal:v1

<img width="511" alt="Screenshot 2025-03-17 at 12 03 07" src="https://github.com/weyerma2/MDM-Lernjournal/blob/main/lernjournal2-container/images/docker.jpeg" />

### Variante und Repository

| Gewähltes Beispiel | Bitte ausfüllen |
| -------- | ------- |
| onnx-sentiment-analysis | Nein |
| onnx-image-classification | Ja |
| Repo URL Fork | https://github.com/weyerma2/lernjournal2 |
| Docker Hub URL | https://hub.docker.com/r/weyerma2/lernjournal | 

### Dokumentation lokales Deployment

# Lokales Docker Image bauen
docker build -t onnx-img .

# Container lokal ausführen
docker run -p 8000:8000 onnx-img


### Dokumentation Deployment Azure Web App

# App Service Plan (Linux) erstellen
az appservice plan create --name lernjournal2-plan --resource-group lernjournal --is-linux --sku B1 --location westeurope

# Web App mit Docker-Image erstellen
az webapp create --resource-group lernjournal --plan lernjournal2-plan --name lernjournal2weyerma2 --deployment-container-image-name weyerma2/lernjournal:v1



### Dokumentation Deployment ACA

# Resource Provider registrieren
az provider register -n Microsoft.OperationalInsights --wait
# Log Analytics Workspace erstellen
az monitor log-analytics workspace create --resource-group lernjournal --workspace-name lernjournal2-logs --location westeurope
# ACA Environment erstellen (inkl. Logs)
az containerapp env create --name lernjournal2-env --resource-group lernjournal --location westeurope --logs-workspace-id $(az monitor log-analytics workspace show --resource-group lernjournal --workspace-name lernjournal2-logs --query customerId -o tsv) --logs-workspace-key $(az monitor log-analytics workspace get-shared-keys --resource-group lernjournal --workspace-name lernjournal2-logs --query primarySharedKey -o tsv)
# ACA App deployen
az containerapp create --name lernjournal2 --resource-group lernjournal --environment lernjournal2-env --image weyerma2/lernjournal:v1 --target-port 8000 --ingress external


### Dokumentation Deployment ACI

# Resource Provider für ACI registrieren
az provider register --namespace Microsoft.ContainerInstance --wait

# Log Analytics Workspace erstellen
az monitor log-analytics workspace create --resource-group lernjournal --workspace-name lernjournal2aci-logs --location westeurope

# Workspace-Daten abrufen (für Verknüpfung)
$logId = az monitor log-analytics workspace show --resource-group lernjournal --workspace-name lernjournal2aci-logs --query customerId -o tsv
$logKey = az monitor log-analytics workspace get-shared-keys --resource-group lernjournal --workspace-name lernjournal2aci-logs --query primarySharedKey -o tsv

#  ACI mit Logging deployen
az container create --resource-group lernjournal --name lernjournal2 --image weyerma2/lernjournal --os-type Linux --cpu 1 --memory 1.0 --ports 8000 --dns-name-label lernjournal2aci --location westeurope

<img width="511" alt="Screenshot 2025-03-17 at 12 03 07" src="https://github.com/weyerma2/MDM-Lernjournal/blob/main/lernjournal2-container/images/azure.jpeg" />