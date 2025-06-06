# Projekt 1 Python

## Übersicht

| | Bitte ausfüllen |
| -------- | ------- |
| Variante | Eigenes Projekt |
| Datenherkunft | CSV (REST-API Export mit XML/CSV Format), aus einer Business API (Sales Cockpit Export) |
| Datenherkunft | https://erp.menuandmore.ch (interne Geschäftsapi) |
| ML-Algorithmus | 	LightGBM, XGBoost, Lineare Regression, Keras NeuralNet |
| Repo URL | https://github.com/weyerma2/forecast_mam |

## Dokumentation

### Data Scraping
Zugriff auf REST-API mit BasicAuth + Zertifikat (.pfx)
Export im CSV-Format per GET-Request (mit Parametern wie Zeitraum, Artikelnummer, Lieferstatus etc.)
Daten werden in MongoDB persistiert (mdm_project1)
Zusätzlich speicherung der CSV-Datei lokal (/data/fetched_data.csv)

### Training

Trainingsnotebook: backend/model.ipynb

# Modelle trainiert
lgbm_model.pkl (LightGBM)
xgb_model.pkl (XGBoost)
linear_model.pkl und linear_model_v2.pkl
neuralnet_model.keras (Keras Sequential Model)

Encoding via artikel_encoding_map.pkl, Standardisierung mit scaler.pkl

### ModelOps Automation
Persistenz der Modelle als .pkl/.keras
Vorbereitung auf automatisiertes Preprocessing (Mapping, Skalierung)
Manuelles Deployment-Skript vorhanden (app.py)

### Deployment

Flask-App (backend/app.py) stellt Modelle bereit
# Dockerisierung mit
Dockerfile
docker-compose.yaml
Deployment-fähig z. B. für Azure Web App oder Container Instances
