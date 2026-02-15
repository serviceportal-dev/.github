# Serviceportal

## Installation

## Lokale Entwicklungsumgebung mit Docker Compose

Mit der folgenden `docker-compose.yml` kann das Serviceportal auf einem lokalen Rechner gestartet werden. Dabei werden sowohl die Webapplikation als auch die benötigte Datenbank automatisch in separaten Containern bereitgestellt.

Die Konfiguration ist ausschliesslich für lokale Entwicklungs- und Testzwecke vorgesehen.

---

## Funktionsweise

Beim Start werden zwei Container erstellt:

- **Web-Container (`serviceportal-local`)**  
  Enthält die Applikation und stellt sie lokal über Port `8080` bereit.

- **Datenbank-Container (`serviceportal-local_db`)**  
  Stellt eine MariaDB-Datenbank für die lokale Nutzung bereit.

Die benötigten Daten werden in temporären lokalen Verzeichnissen gespeichert, sodass keine bestehenden Systeme beeinflusst werden.

---

## Demodaten laden (optional)

Über die Umgebungsvariable

```yaml
DB_LOAD_DEMO_DATA=true
```

kann beim ersten Start automatisch eine minimale Demodatenbasis geladen werden.
Dies ermöglicht eine sofortige Inbetriebnahme ohne manuelle Datenbankinitialisierung.

### Hinweis zum Datenbankpasswort 👋

Das in der `docker-compose.yml` definierte Passwort ist kein produktives oder sicherheitsrelevantes Passwort, muss jedoch unverändert bleiben, da es für das automatische Laden der Demodaten in der lokalen Entwicklungsumgebung erforderlich ist.

### docker-compose.yml

```powershell
name: serviceportal

services:
  web:
    container_name: serviceportal-local
    hostname: serviceportal-local
    image: algonetic/deb12-mason:latest
    volumes:
      - $TEMP/serviceportal-local/html:/var/www/html
    ports:
      - "8080:80"
    environment:
      - DB_HOST=db-service-ssp
      - DB_NAME=db_local_602151
      - DB_USER=apache
      - DB_PASS=geHeimXX
      - DB_LOAD_DEMO_DATA=true # Optional; default: false
    networks: 
      - default
    restart: no
  db-service-ssp:
    container_name: serviceportal-local_db
    image: mariadb:10.11
    volumes:
      - $TEMP/serviceportal-local/db:/var/lib/mysql
    environment:
      MYSQL_DATABASE: db_local_602151
      MYSQL_USER: apache
      MYSQL_ROOT_PASSWORD: geHeimXX
    networks: 
      - default
networks:
  default:
    external: false
    name: local-network

```

### Windows (PowerShell) für Container-Start mit Datenbank auf externem DB-Server

```powershell
docker run --hostname=serviceportal.example.ch --name "serviceportal-local" `
    --env=NODE_ENV=development `
    --env=DB_HOST="dbhost.example.ch" `
    --env=DB_NAME="db_ssp" `
    --env=DB_PASS="**********" `
    --network=bridge -p 8080:80 `
    --restart=no `
    algonetic/deb12-mason:latest
``` 

## Front-end (Templates)

1. `cd /var/www/`
2. `git clone git@github-serviceportal:serviceportal-dev/html.git`

## Backend (Controller)

1. `cd /usr/local/lib/site_perl`
2. `git clone git@github-modules:serviceportal-dev/ScreenPoint.git`
3. `git clone git@github-autoload:serviceportal-dev/auto.git`

<!--

**Here are some ideas to get you started:**

🙋‍♀️ A short introduction - what is your organization all about?
🌈 Contribution guidelines - how can the community get involved?
👩‍💻 Useful resources - where can the community find your docs? Is there anything else the community should know?
🍿 Fun facts - what does your team eat for breakfast?
🧙 Remember, you can do mighty things with the power of [Markdown](https://docs.github.com/github/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)
-->
