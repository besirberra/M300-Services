# M300 – Plattformübergreifende Dienste in ein Netzwerk integrieren

### Inhaltsverzeichnis
<!-- TOC -->

- [M300 – Plattformübergreifende Dienste in ein Netzwerk integrieren](#m300--plattform%C3%BCbergreifende-dienste-in-ein-netzwerk-integrieren)
        - [Inhaltsverzeichnis](#inhaltsverzeichnis)
- [-Toolumgebung](#-toolumgebung)
- [GitHub Account erstellen](#github-account-erstellen)
    - [Repository erstellen](#repository-erstellen)
    - [Repository clonen](#repository-clonen)
    - [SSH-Key erstellen](#ssh-key-erstellen)
    - [SSH-Key zu GitHub hinzufügen](#ssh-key-zu-github-hinzuf%C3%BCgen)
- [Git Client](#git-client)
    - [Installation](#installation)
    - [Git konfigurieren](#git-konfigurieren)
    - [Repository klonen](#repository-klonen)
- [VirtualBox](#virtualbox)
    - [Installation](#installation)
    - [Virtuelle Maschine erstellen](#virtuelle-maschine-erstellen)
    - [System aktualisieren](#system-aktualisieren)
    - [Apache Webserver installieren](#apache-webserver-installieren)
- [Vagrant](#vagrant)
    - [VM erstellen](#vm-erstellen)
    - [Apache automatisiert installieren](#apache-automatisiert-installieren)
- [Visual Studio Code](#visual-studio-code)
    - [Installation](#installation)
    - [Extensions installiert](#extensions-installiert)
    - [Dateien exkludieren](#dateien-exkludieren)
    - [Repository hinzufügen & pushen](#repository-hinzuf%C3%BCgen--pushen)
    - [alt text](#alt-text)
- [Theoriefragen – Cloud & Vagrant](#theoriefragen--cloud--vagrant)
    - [Cloud Computing](#cloud-computing)
        - [Was versteht man unter Cloud-Computing?](#was-versteht-man-unter-cloud-computing)
    - [Infrastructure as a Service IaaS](#infrastructure-as-a-service-iaas)
        - [Was versteht man unter Infrastructure as a Service IaaS?](#was-versteht-man-unter-infrastructure-as-a-service-iaas)
    - [Infrastructure as Code IaC](#infrastructure-as-code-iac)
        - [Was ist der Unterschied zur manuellen Installation einer VM?](#was-ist-der-unterschied-zur-manuellen-installation-einer-vm)
    - [Vagrant](#vagrant)
        - [Was wird mit Vagrant erzeugt?](#was-wird-mit-vagrant-erzeugt)
        - [Welche der Aussagen treffen zu?](#welche-der-aussagen-treffen-zu)
        - [In welchen Bereich des Cloud-Computings ist Vagrant einzuordnen?](#in-welchen-bereich-des-cloud-computings-ist-vagrant-einzuordnen)
        - [Welche Alternativen zu Vagrant bestehen?](#welche-alternativen-zu-vagrant-bestehen)
        - [Wo speichert Vagrant seine Konfiguration?](#wo-speichert-vagrant-seine-konfiguration)
        - [Was bedeutet die Fehlermeldung](#was-bedeutet-die-fehlermeldung)
        - [Bei welcher LPI Zertifizierung nützt mir das Vagrant Wissen?](#bei-welcher-lpi-zertifizierung-n%C3%BCtzt-mir-das-vagrant-wissen)
- [LB2 – Hands-on: Automatisierung mit Vagrant](#lb2--hands-on-automatisierung-mit-vagrant)
    - [Ziel](#ziel)
    - [Neue VM erstellen](#neue-vm-erstellen)
    - [Auswahl der Serverdienste](#auswahl-der-serverdienste)
    - [Manuelle Installation in der VM](#manuelle-installation-in-der-vm)
    - [Automatisierung im Vagrantfile](#automatisierung-im-vagrantfile)
        - [Port-Weiterleitung](#port-weiterleitung)
        - [Synchronisation von Dateien](#synchronisation-von-dateien)
        - [Speicherzuweisung](#speicherzuweisung)
    - [Provisionierung Automatisierte Installation](#provisionierung-automatisierte-installation)
    - [Sicherheit](#sicherheit)
    - [Fazit](#fazit)
- [M300 – Docker Projekt](#m300--docker-projekt)
    - [Mini-Helpdesk mit Monitoring](#mini-helpdesk-mit-monitoring)
    - [Zweck des gewählten Service](#zweck-des-gew%C3%A4hlten-service)
    - [Aufbau und logische Struktur des Projekts](#aufbau-und-logische-struktur-des-projekts)
        - [Architekturübersicht](#architektur%C3%BCbersicht)
    - [Konfiguration der Dienste](#konfiguration-der-dienste)
        - [Web-Service](#web-service)
        - [Benutzeroberfläche](#benutzeroberfl%C3%A4che)
        - [Admin-Ansicht](#admin-ansicht)
    - [Netzwerkverbindung und Ports](#netzwerkverbindung-und-ports)
    - [Host-System und Container-Interaktion](#host-system-und-container-interaktion)
        - [Code-Volume](#code-volume)
        - [Datenbank-Volume](#datenbank-volume)
    - [Monitoring-Lösung](#monitoring-l%C3%B6sung)
    - [Dokumentierte Fehler und Lösungen](#dokumentierte-fehler-und-l%C3%B6sungen)
        - [Fehler 1 – MySQL Connection refused](#fehler-1--mysql-connection-refused)
    - [Projektstruktur](#projektstruktur)
    - [Fazit](#fazit)

<!-- /TOC -->
---
# 10-Toolumgebung

--

# 01 GitHub Account erstellen

Zunächst wurde ein GitHub-Account unter folgender Webseite erstellt:

https://www.github.com

Folgende Angaben wurden gemacht:

- Benutzername
- E-Mail-Adresse
- Passwort

Nach der Registrierung wurde die E-Mail-Adresse bestätigt und die Anmeldung erfolgreich durchgeführt.

---

## Repository erstellen

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

## Repository clonen
![alt text](images/Bild2.png)

## SSH-Key erstellen

Zur sicheren Verbindung zwischen lokalem PC und GitHub wurde ein SSH-Key generiert.

Terminal (Git Bash) öffnen und folgenden Befehl ausführen:

```bash
ssh-keygen -t rsa -b 4096 -C "besirberra@icloud.com" 
```

Standard-Datei mit Enter bestätigen:

```
Enter a file in which to save the key (~/.ssh/id_rsa): [Enter]
```

Passphrase setzen und bestätigen.

---

## SSH-Key zu GitHub hinzufügen

Public Key anzeigen:

```bash
cat ~/.ssh/id_rsa.pub
```

Den angezeigten Schlüssel kopieren und unter:

GitHub → Settings → SSH and GPG Keys → New SSH Key

einfügen und speichern.

Die SSH-Verbindung ist nun aktiv.

---

# 02 Git Client

## Installation

Git wurde unter folgender Webseite heruntergeladen und installiert:

https://git-scm.com

Installation erfolgte mit Standard-Einstellungen.

---

## Git konfigurieren

Terminal (Git Bash) öffnen:

```bash
git config --global user.name "besirberra"
git config --global user.email "besirberra@icloud.com"
```

Konfiguration erfolgreich abgeschlossen.

---

## Repository klonen

Repository mit SSH klonen:

```bash
git clone git@github.com:besirberra/M300-Services.git
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

# 03 VirtualBox

## Installation

VirtualBox wurde von der offiziellen Webseite heruntergeladen und installiert.
![alt text](images/Bild4.png)

---

## Virtuelle Maschine erstellen

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

## System aktualisieren

Nach der Installation:

```bash
sudo apt-get update
sudo apt-get upgrade
sudo reboot
```

---

## Apache Webserver installieren

```bash
sudo apt-get install apache2
```

Test im Browser:

http://127.0.0.1

Apache-Standardseite wurde erfolgreich angezeigt.

![alt text](images/Bild6.png)


Im Ordner /web die Hauptseite index.html editieren bzw. durch eine andere ersetzen (z.B. HTML5up-Themplate) und das Resultat überprüfen

![alt text](images/BB.png)


---

# 04 Vagrant

## VM erstellen

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

## Apache automatisiert installieren

Im Vagrantfile wurde Provisioning ergänzt.

Nach dem Start der VM war Apache automatisch installiert.

Test im Browser:

http://localhost:8080

Apache war erfolgreich erreichbar.

![alt text](images/Bildd.png)

---

# 05 Visual Studio Code

## Installation

Visual Studio Code wurde installiert.

---

## Extensions installiert

Folgende Extensions wurden installiert:

- Markdown All in One
- Vagrant Extension
- vscode-pdf
- Auto Markdown TOC

---

## Dateien exkludieren

In der settings.json wurde folgender Abschnitt ergänzt:

![alt text](images/Bild7.png)

## Repository hinzufügen & pushen

![alt text](images/Bild8.png)
---

# Theoriefragen – Cloud & Vagrant

## Cloud Computing

### Was versteht man unter Cloud-Computing?
Cloud-Computing beschreibt die Bereitstellung von IT-Ressourcen (Server, Speicher, Datenbanken, Netzwerke, Software) über das Internet.  
Ressourcen werden flexibel, skalierbar und bedarfsgerecht genutzt, ohne eigene Hardware betreiben zu müssen.

---

## Infrastructure as a Service (IaaS)

### Was versteht man unter Infrastructure as a Service (IaaS)?
IaaS ist ein Cloud-Modell, bei dem virtuelle Server, Speicher und Netzwerke als Dienst bereitgestellt werden.  
Der Kunde verwaltet Betriebssysteme und Anwendungen selbst, während der Anbieter die physische Infrastruktur betreibt.

Beispiele: AWS EC2, Microsoft Azure VM, Google Compute Engine.

---

## Infrastructure as Code (IaC)

### Was ist der Unterschied zur manuellen Installation einer VM?
Bei der manuellen Installation wird eine VM per GUI eingerichtet und konfiguriert.  
Bei Infrastructure as Code wird die gesamte Infrastruktur über Konfigurationsdateien automatisiert erstellt.  
IaC ist reproduzierbar, versionierbar und schneller skalierbar.

---

## Vagrant

### Was wird mit Vagrant erzeugt?
Mit Vagrant werden automatisiert virtuelle Maschinen erstellt und konfiguriert.

---

### Welche der Aussagen treffen zu?

a) Vagrant ist ein Hypervisor  
→ Falsch  

b) Vagrant erzeugt virtuelle Maschinen, dabei werden mehrere Hypervisor und Cloud-Umgebungen (z.B. AWS) unterstützt.  
→ Richtig  

c) Vagrant erzeugt Container  
→ Falsch  

---

### In welchen Bereich des Cloud-Computings ist Vagrant einzuordnen?
Vagrant gehört zum Bereich **Infrastructure as Code (IaC)** und unterstützt hauptsächlich IaaS-Umgebungen.

---

### Welche Alternativen zu Vagrant bestehen?
- Terraform  
- Ansible  
- Docker  
- Kubernetes  
- VMware vSphere  
- VirtualBox (direkt genutzt)

---

### Wo speichert Vagrant seine Konfiguration?
Die Konfiguration wird in der Datei **Vagrantfile** im Projektordner gespeichert.

---

### Was bedeutet die Fehlermeldung  
"A Vagrant environment or target machine is required to run this command."?

Diese Fehlermeldung bedeutet, dass der Befehl nicht in einem gültigen Vagrant-Projektordner ausgeführt wurde oder keine VM definiert/gestartet ist.

---

### Bei welcher LPI Zertifizierung nützt mir das Vagrant Wissen?

Das Wissen ist besonders hilfreich für:

- LPIC-1 (Linux Administrator Grundlagen)
- LPIC-2 (Linux Systemadministrator)
- DevOps-orientierte Prüfungen

Da Virtualisierung, Automatisierung und Infrastrukturverwaltung dort relevante Themen sind.

---

# LB2 – Hands-on: Automatisierung mit Vagrant

## Ziel

Ziel dieser Übung war es, einen Serverdienst automatisiert mit Vagrant bereitzustellen.  
Ich habe dazu eine neue virtuelle Maschine erstellt und darin die Installation sowie Konfiguration manuell getestet, bevor ich die Befehle in das Vagrantfile übernommen habe.

---

## 1. Neue VM erstellen

Zuerst habe ich ein neues Projektverzeichnis erstellt:

```
cd C:\Users\besir\M300
mkdir myVM
cd myVM
```

Anschliessend habe ich eine neue Vagrant-Umgebung mit Ubuntu 16.04 (xenial64) initialisiert:

```
vagrant init ubuntu/xenial64
vagrant up
```

Zum Testen habe ich mich in die VM eingeloggt:

```
vagrant ssh
```

---

## 2. Auswahl der Serverdienste

Ich habe mich für folgende Dienste entschieden:

- Apache Webserver
- Webalizer (Webanalyzer)

Webalizer benötigt Apache-Logfiles zur Auswertung, daher musste zuerst Apache installiert werden.

---

## 3. Manuelle Installation in der VM

Zuerst habe ich die Paketquellen aktualisiert:

```
sudo apt-get update
```

Danach habe ich Apache installiert:

```
sudo apt-get install -y apache2
```

Anschliessend habe ich Webalizer installiert:

```
sudo apt-get install -y webalizer
```

Wichtig war das Argument `-y`, damit die Installation nicht auf eine manuelle Bestätigung wartet.

Mit dem Befehl `history` habe ich anschliessend meine relevanten Befehle überprüft und in das Vagrantfile übernommen.

---

## 4. Automatisierung im Vagrantfile

Nachdem die manuelle Installation funktionierte, habe ich die Konfiguration in das Vagrantfile übertragen.

### Port-Weiterleitung

```
config.vm.network "forwarded_port", guest:80, host:8080, auto_correct: true
```

Damit wird Port 80 der VM auf Port 8080 des Hosts weitergeleitet.

### Synchronisation von Dateien

```
config.vm.synced_folder ".", "/var/www/html"
```

So bleiben Dateien auch nach dem Zerstören der VM erhalten.

### Speicherzuweisung

```
config.vm.provider "virtualbox" do |vb|
  vb.memory = "512"
end
```

---

## 5. Provisionierung (Automatisierte Installation)

Die Installation und Konfiguration wurde über ein Shell-Provisioning umgesetzt:

![alt text](images/Bild11.png)

Im Browser eingegeben:

![alt text](images/Bild12.png)

---

## 6. Sicherheit

Zusätzlich sollte die VM durch eine Firewall abgesichert werden (z.B. UFW).

In grösseren Umgebungen können mehrere Webserver über einen Reverse Proxy zusammengeführt werden, um ein zentrales SSL-Zertifikat zu nutzen.

---

## Fazit

Mit dieser Übung habe ich:

- Eine VM mit Vagrant erstellt
- Serverdienste manuell getestet
- Die Installation automatisiert
- Port-Weiterleitung konfiguriert
- Persistente Dateispeicherung umgesetzt
- Fehler analysiert und behoben

Die Bereitstellung erfolgt nun vollständig automatisiert und reproduzierbar über das Vagrantfile.

---

# M300 – Docker Projekt  
## Mini-Helpdesk mit Monitoring

---

## 1. Zweck des gewählten Service

Der entwickelte Service ist ein webbasiertes Mini-Helpdesk-System zur Verwaltung von IT-Tickets.  
Benutzer können Tickets erfassen, priorisieren und deren Status verfolgen.  

Zusätzlich existiert eine Admin-Ansicht zur erweiterten Verwaltung der Tickets.  
Das Projekt demonstriert die Umsetzung einer containerisierten Mehrkomponenten-Architektur mit Docker inklusive Monitoring.

---

## 2. Aufbau und logische Struktur des Projekts

Das Projekt besteht aus drei Containern:

- **Web-Container** (PHP + Apache)
- **Datenbank-Container** (MySQL)
- **Monitoring-Container** (cAdvisor)

Alle Container kommunizieren über ein internes Docker-Bridge-Netzwerk.

### Architekturübersicht

Übersicht der laufenden Container:

![alt text](images/docker.img.png)


---

## 3. Konfiguration der Dienste

### Web-Service

- PHP 8.2 mit Apache
- Verbindung zur Datenbank über Hostname `db`
- Zugriff über Host-Port `8081`

### Benutzeroberfläche

Startseite der Anwendung:

![alt text](images/Helpdesk.img.png)

---

### Admin-Ansicht

Die Admin-Ansicht wird über folgende URL aufgerufen:

```
http://localhost:8081/?admin=1
```

Zusätzliche Funktionen im Admin-Modus:

- Status direkt in der Tabelle ändern
- Tickets löschen
- Statistische Übersicht anzeigen
- Filter nach Status (open / pending / resolved)

![alt text](images/admin.png)

---

## 4. Netzwerkverbindung und Ports

| Dienst     | Interner Port | Host-Port |
|------------|--------------|-----------|
| Web        | 80           | 8081      |
| MySQL      | 3306         | 3307      |
| cAdvisor   | 8080         | 8090      |

Der Web-Container greift intern über den Hostnamen `db` auf die Datenbank zu.  
Die Container befinden sich im selben Docker-Netzwerk (`bridge`).

---

## 5. Host-System und Container-Interaktion

### Code-Volume

```bash
./web → /var/www/html
```

Änderungen im lokalen Projektordner werden direkt im Container sichtbar.  
Ein Rebuild ist für Codeänderungen nicht notwendig.

### Datenbank-Volume

```bash
dbdata → /var/lib/mysql
```

Dieses Volume sorgt für persistente Datenspeicherung, auch wenn Container neu gestartet oder gelöscht werden.

---

## 6. Monitoring-Lösung

Zur Überwachung der Container wird **cAdvisor** eingesetzt.

Erreichbar unter:

```
http://localhost:8090/containers/
```

Monitoring-Übersicht:

![alt text](images/cAdvisor.img.png)

cAdvisor zeigt:

- CPU-Auslastung
- Speicherverbrauch
- Netzwerkaktivität
- Laufzeit der Container
- Prozesse innerhalb der Container

---

## 7. Dokumentierte Fehler und Lösungen

### Fehler 1 – MySQL Connection refused

Fehlermeldung:

```
mysqli_sql_exception: Connection refused
```

**Ursache:**  
Der Web-Container versuchte eine Verbindung zur Datenbank aufzubauen, bevor diese vollständig gestartet war.

**Lösung:**

```bash
docker compose down -v
docker compose up -d --build
```

---

## 9. Projektstruktur

```bash
docker-projekt/
│
├── docker-compose.yml
├── web/
│   ├── Dockerfile
│   └── index.php
├── db/
│   └── init.sql
├── images/   
│   
└── docs/
    └── Doku.md
```

---

## 10. Fazit

Das Projekt demonstriert erfolgreich eine containerisierte Webanwendung mit Datenbank und Monitoring.  

Alle Handlungsziele wurden vollständig erfüllt.  

Die Anwendung ist reproduzierbar über:

```bash
docker compose up -d --build
```

Web-Anwendung:  
http://localhost:8081  

Monitoring:  
http://localhost:8090