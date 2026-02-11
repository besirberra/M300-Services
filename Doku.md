# M300 – Plattformübergreifende Dienste in ein Netzwerk integrieren

---

# 01 – GitHub Account

## 1.1 GitHub Account erstellen

Zunächst wurde ein GitHub-Account unter folgender Webseite erstellt:

https://www.github.com

Folgende Angaben wurden gemacht:

- Benutzername
- E-Mail-Adresse
- Passwort

Nach der Registrierung wurde die E-Mail-Adresse bestätigt und die Anmeldung erfolgreich durchgeführt.

---

## 1.2 Repository erstellen

Nach der Anmeldung wurde ein neues Repository erstellt.

Vorgehen:

1. Klick auf **Start a project**
2. Repository Name: `M300-Services`
3. Beschreibung optional ergänzt
4. Sichtbarkeit: **Public**
5. Option **Initialize this repository with a README** aktiviert
6. Klick auf **Create repository**

Das Repository wurde erfolgreich erstellt.

---

## 1.3 SSH-Key erstellen

Zur sicheren Verbindung zwischen lokalem PC und GitHub wurde ein SSH-Key generiert.

Terminal (Git Bash) öffnen und folgenden Befehl ausführen:

```bash
ssh-keygen -t rsa -b 4096 -C "meine-email@example.com"
```

Standard-Datei mit Enter bestätigen:

```
Enter a file in which to save the key (~/.ssh/id_rsa): [Enter]
```

Passphrase setzen und bestätigen.

---

## 1.4 SSH-Key zu GitHub hinzufügen

Public Key anzeigen:

```bash
cat ~/.ssh/id_rsa.pub
```

Den angezeigten Schlüssel kopieren und unter:

GitHub → Settings → SSH and GPG Keys → New SSH Key

einfügen und speichern.

Die SSH-Verbindung ist nun aktiv.

---

# 02 – Git Client

## 2.1 Installation

Git wurde unter folgender Webseite heruntergeladen und installiert:

https://git-scm.com

Installation erfolgte mit Standard-Einstellungen.

---

## 2.2 Git konfigurieren

Terminal (Git Bash) öffnen:

```bash
git config --global user.name "MeinUsername"
git config --global user.email "meine-email@example.com"
```

Konfiguration erfolgreich abgeschlossen.

---

## 2.3 Repository klonen

Repository mit SSH klonen:

```bash
git clone git@github.com:MeinUsername/M300-Services.git
```

In das Repository wechseln:

```bash
cd M300-Services
```

Status prüfen:

```bash
git status
```

Ergebnis:

```
Your branch is up to date with 'origin/main'.
nothing to commit, working tree clean
```

---

# 03 – VirtualBox

## 3.1 Installation

VirtualBox wurde von der offiziellen Webseite heruntergeladen und installiert.

---

## 3.2 Virtuelle Maschine erstellen

Neue VM mit folgenden Einstellungen erstellt:

- Name: M300_Ubuntu_22.04_Desktop
- Typ: Linux
- Version: Ubuntu (64-bit)
- RAM: 2048 MB
- CPU: 2 Kerne
- Festplatte: 25 GB
- Typ: VMDK
- Dynamisch alloziert

Ubuntu ISO eingebunden und Betriebssystem erfolgreich installiert.

---

## 3.3 System aktualisieren

Nach der Installation:

```bash
sudo apt-get update
sudo apt-get upgrade
sudo reboot
```

---

## 3.4 Apache Webserver installieren

```bash
sudo apt-get install apache2
```

Test im Browser:

http://127.0.0.1

Apache-Standardseite wurde erfolgreich angezeigt.

---

# 04 – Vagrant

## 4.1 VM erstellen

Im gewünschten Verzeichnis:

```bash
mkdir myVM
cd myVM
vagrant init ubuntu/xenial64
vagrant up --provider virtualbox
```

SSH-Verbindung zur VM herstellen:

```bash
vagrant ssh
```

Die Verbindung wurde erfolgreich aufgebaut.

---

## 4.2 Apache automatisiert installieren

Im Vagrantfile wurde Provisioning ergänzt.

Nach dem Start der VM war Apache automatisch installiert.

Test im Browser:

http://localhost:8080

Apache war erfolgreich erreichbar.

---

# 05 – Visual Studio Code

## 5.1 Installation

Visual Studio Code wurde installiert.

---

## 5.2 Extensions installiert

Folgende Extensions wurden installiert:

- Markdown All in One
- Vagrant Extension
- vscode-pdf
- Auto Markdown TOC

---

## 5.3 Dateien exkludieren

In der settings.json wurde folgender Abschnitt ergänzt:

```json
"files.exclude": {
  "**/.git": true,
  "**/.svn": true,
  "**/.hg": true,
  "**/.vagrant": true,
  "**/.DS_Store": true
}
```

---

# Bilder in Markdown einfügen

## Ordnerstruktur

```
M300-Services/
│
├── Doku.md
└── images/
```

## Bild einfügen

```markdown
![Beschreibung](images/bildname.png)
```

Beispiel:

```markdown
![VirtualBox Übersicht](images/virtualbox.png)
```

---

## Bilder pushen

```bash
git add -A
git commit -m "Screenshots ergänzt"
git push
```