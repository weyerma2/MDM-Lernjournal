# Projekt 2 Java

## Übersicht

| | Bitte ausfüllen |
| -------- | ------- |
| Variante | Vorhandenes Modell  |
| Datensatz (wenn selbstgewählt) | 	Bildformat (JPEG), Beispielbild „pizza.jpg“ zur Testverarbeitung |
| Datensatz (wenn selbstgewählt) | im Projekt |
| Modell (wenn selbstgewählt) | https://github.com/deepjavalibrary/djl/tree/master/model-zoo |
| ML-Algorithmus | Convolutional Neural Network (CNN) – EfficientNet (ONNX) via DJL |
| Repo URL | https://github.com/weyerma2/insulin-calculator |



## Dokumentation

### Daten
Upload von JPEG-/PNG-Bildern über die Web-Oberfläche (upload.html)
Beispielbild pizza.jpg zur Testinferenz vorhanden
Abruf von Nährwertdaten via Ninja API (Klasse SwissFoodApiClient)

### Training
Kein eigenes Training enthalten
Verwendung eines vortrainierten Modells aus dem DJL Model Zoo
Modell wird beim Start dynamisch geladen (EfficientNet oder MobilenetV2)

### Inference / Serving
PredictionService.java verwendet DJL zur Inferenz
Eingabe: Benutzerbild → Modell → Erkennung des Lebensmittels
# Output
ermitteltes Lebensmittel → Insulinempfehlung auf Basis von Nährwertdaten aus der API

### Deployment
Dockerfile zur Containerisierung der Spring Boot Anwendung
docker-compose.yaml für lokalen Start mit Container

Azure Web App for Containers
<img width="511" alt="Screenshot 2025-03-17 at 12 03 07" src="https://github.com/weyerma2/MDM-Lernjournal/blob/main/projekt2-java/images/azure.jpeg" />    
