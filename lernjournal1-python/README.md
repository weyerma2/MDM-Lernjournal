# Lernjournal 1 Python

## Repository und Library

| | Bitte ausfüllen |
| -------- | ------- |
| Repository (URL)  | https://github.com/weyerma2/lernjournal1
| Kurze Beschreibung der App-Funktion | Eine Web-App, die Texte in Grossbuchstaben umwandelt und hochgeladene Bilder in Graustufen konvertiert |
| Verwendete Library aus PyPi (Name) | Flask, Pillow |
| Verwendete Library aus PyPi (URL) | https://pypi.org/project/Flask/, https://pypi.org/project/Pillow/ |
| ... | |
| ... | |

## App, Funktionalität
Texteingabe → Umwandlung in GROSSBUCHSTABEN

Bildeingabe (PNG/JPG) → Konvertierung in Graustufen

Ausgabe wird dynamisch im selben HTML-Template angezeigt

Einfache Benutzeroberfläche mit HTML + Bootstrap

#### Ansicht im Web-UI:
!!!!!
ERGàNZEN!!!!

### Funktionen Transformation
Der User kann ein Bild hochladen oder einen Text schreiben.

#### Ansicht im Web-UI:

<img width="1360" alt="Screenshot 2025-03-17 at 12 16 38" src="" />

#### Code der Applikation:

<img width="703" alt="Screenshot 2025-03-18 at 10 16 50" src="" />

### Trigger Text Informationen
Bei der Eingabe durch den User und mit dem Trigger des Buttons "Add Task" wird zudem eine Operation durchgeführt, welche den Text untersucht und folgende Informationen zur eingabe anzeigt:
-Originaleingabe
-Umkehrung des Textes
-Anzahl der Wörter
-Anzahl der Buchstaben (Char)
-Palindrome*

*https://de.wikipedia.org/wiki/Palindrom 

#### Ansicht Web-UI:

<img width="311" alt="Screenshot 2025-03-17 at 12 15 30" src="" />

#### Code der Application:

<img width="644" alt="Screenshot 2025-03-18 at 10 17 03" src="" />


## Dependency Management

Nach der Entwicklung der Applikation wurden die Dependencies mit folgendem Prozess generiert:

1. pip freeze > requirements.txt

Entsprechend stehen im Projekt die Dependencies zur Verfügung.

### requirements.txt Inhalt:

<img width="511" alt="Screenshot 2025-03-17 at 12 03 07" src="" />


## Deployment

Azure

<img width="511" alt="Screenshot 2025-03-17 at 12 03 07" src="" />

