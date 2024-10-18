<p align="center">
  <a href="#how-to-build-manually">Manually</a> •
  <a href="#docker-images">Docker</a> •
  <a href="#how-to-create-a-keypair">Keypair</a> •
  <a href="#packages">Binaries</a> •
  <a href="#env-variables">Variables</a><br>
  [<a href="README-FR.md">French</a>] | [<a href="README-DE.md">Deutsch</a>] | [<a href="README-NL.md">Nederlands</a>] | [<a href="README-TW.md">繁體中文</a>] | [<a href="README-ZH.md">简体中文</a>] | [<a href="README-RU.md">Русский</a>]<br>
</p>

# SctgDesk Server-Programm

![Docker Pulls](https://img.shields.io/docker/pulls/sctg/sctgdesk-server)
[![build](https://github.com/sctg-development/sctgdesk-server/actions/workflows/multiarch-docker-hub.yml/badge.svg)](https://github.com/sctg-development/sctgdesk-server/actions/workflows/multiarch-docker-hub.yml)
[![build](https://github.com/sctg-development/sctgdesk-server/actions/workflows/macos-intel-build.yml/badge.svg)](https://github.com/sctg-development/sctgdesk-server/actions/workflows/macos-intel-build.yml)
[![build](https://github.com/sctg-development/sctgdesk-server/actions/workflows/windows.yml/badge.svg)](https://github.com/sctg-development/sctgdesk-server/actions/workflows/windows.yml)

[**Binärer Download**](https://github.com/sctg-development/sctgdesk-server/releases)

[**API-Dokumentation**](https://sctg-development.github.io/sctgdesk-api-server/)

Dies ist eine modifizierte Version von RustDesk Server, die kostenlos und Open Source ist.

*   Der erste Unterschied besteht darin, dass diese Version die neue Version *tcp* -Modus, der in der RustDesk Server Pro-Version enthalten ist.
*   Der zweite Unterschied besteht darin, dass diese Version eine vorläufige Implementierung des Rustdesk Server Pro API-Servers enthält.
    *   Unterstützung für das persönliche Adressbuch
    *   Unterstützung für freigegebenes Adressbuch auf Gruppenebene
        *   schreibgeschützt, Lese-/Schreibzugriff, admin
    *   Unterstützung für freigegebenes Adressbuch auf Benutzerebene
        *   schreibgeschützt, Lese-/Schreibzugriff, admin
*   Der dritte Unterschied besteht darin, dass diese Version eine vorläufige Implementierung einer einfachen Webkonsole enthält.

Die Webkonsole ist unter der Adresse `http://<server-ip>:21114/` mit Login "admin" und Passwort "Hello,world!" .\
Sie können die API-Dokumentation auf dem builtins API-Server unter der Adresse `http://<server-ip>:21114/api/doc/`.

Eine nicht-interaktive API-Dokumentation finden Sie unter [sctgdesk-api-server repo](https://sctg-development.github.io/sctgdesk-api-server/).

## Markieren Sie das Projekt

**Wenn Sie meine Arbeit schätzen, denken Sie bitte darüber nach, ihr einen Stern zu geben! 🤩 oder ein** [![](https://img.shields.io/static/v1?label=Sponsor\&message=%E2%9D%A4\&logo=GitHub\&color=%23fe8e86)](https://github.com/sponsors/sctg-development)

## TL; DR

Sie können Folgendes verwenden `docker-compose.yml` Datei zum Starten des Servers:

```yaml
version: '3'

networks:
  sctgdesk-net:
    external: false

services:
  hbbs:
    container_name: hbbs
    ports:
      - 21114:21114
      - 21115:21115
      - 21116:21116
      - 21116:21116/udp
      - 21118:21118
    image: sctg/sctgdesk-server:latest
    command: hbbs -r sctgdesk.example.com:21117
    volumes:
      - ./data:/usr/local/share/sctgdesk
    networks:
      - sctgdesk-net
    depends_on:
      - hbbr
    restart: unless-stopped

  hbbr:
    container_name: hbbr
    ports:
      - 21117:21117
      - 21119:21119
    image: sctg/sctgdesk-server:latest
    command: hbbr
    volumes:
      - ./data:/usr/local/share/sctgdesk
    networks:
      - sctgdesk-net
    restart: unless-stopped
```

und starten Sie den Server mit:

```bash
mkdir -p data
docker-compose up 
```

## Binärdateien

Binärdateien sind für die folgenden Plattformen verfügbar:

*   Linux x86\_64 statisch verknüpft
*   Linux arm64 statisch verknüpft
*   Linux armv7 statisch verknüpft
*   MacOS Intel
*   MacOS Apple Silicon
*   Windows x86\_64

### Standardmäßiger Admin-Benutzer

Der Standard-Admin-Benutzer wird mit dem Benutzernamen `admin` und das Passwort `Hello,world!`. Sie können das Passwort nach der ersten Anmeldung in der Webkonsole ändern.

## Eigenständige API-Version

Die eigenständige API-Version ist eine Version des Servers, die den API-Server und die Webkonsole, aber nicht den Rendez-Vous-Server enthält.\
Die Standalone-Version steht in einem eigenen Repository zur Verfügung [sctgdesk-api-server](https://github.com/sctg-development/sctgdesk-api-server).\
Informationen zu allen Problemen im Zusammenhang mit der API oder der Webkonsole finden Sie in der [sctgdesk-api-server](https://github.com/sctg-development/sctgdesk-api-server) Aufbewahrungsort.

## Screenshots

### Webkonsole

<img width="1085" alt="login" src="https://github.com/sctg-development/sctgdesk-server/assets/165936401/fe72a374-8a98-4606-8632-3d919f9317c9">

<img width="1285" alt="dashboard" src="https://github.com/sctg-development/sctgdesk-api-server/assets/165936401/0bb148d6-8723-491f-88c5-b98331d64f61">

<img width="1085" alt="devices" src="https://github.com/sctg-development/sctgdesk-server/assets/165936401/6ae55861-f65c-4950-a068-f22eef3ad81a">

<img width="1084" alt="users" src="https://github.com/sctg-development/sctgdesk-server/assets/165936401/8d225841-43f5-44f4-8d41-5b6ca3324096">

<img width="1087" alt="groups" src="https://github.com/sctg-development/sctgdesk-server/assets/165936401/d84ce3d3-1d19-4765-883f-001f313a4a1e">

<img width="1089" alt="address books" src="https://github.com/sctg-development/sctgdesk-server/assets/165936401/db13010b-077a-4e14-943b-9d8de3266f82">

<img width="730" alt="rues" src="https://github.com/sctg-development/sctgdesk-api-server/assets/165936401/3a990deb-d8bb-4725-a47d-435ec3667fee">

<img width="621" alt="add rules" src="https://github.com/sctg-development/sctgdesk-api-server/assets/165936401/355f3903-2b54-4b08-abd0-e33c84a260ed">

### API-Dokumentation

<img width="1502" alt="apidoc" src="https://github.com/sctg-development/sctgdesk-server/assets/165936401/88fe7910-fe62-43e5-a16c-70dc1201e040">

### Verwendung im Rustdesk-Client

<img width="913" alt="Capture d’écran 2024-05-24 à 12 14 34" src="https://github.com/sctg-development/sctgdesk-server/assets/165936401/1b253577-dce2-4163-9a49-ba4b3da37812">

<img width="923" alt="Capture d’écran 2024-05-24 à 12 07 21" src="https://github.com/sctg-development/sctgdesk-server/assets/165936401/c49b3aba-b13f-4b15-a69c-d492a90e774a">

<img width="927" alt="Capture d’écran 2024-05-24 à 12 07 32" src="https://github.com/sctg-development/sctgdesk-server/assets/165936401/f447f5fa-bc77-4bc6-858a-c6cadf9b7f6c">

## Generieren von Autoupdate-Links

Wir haben unseren Client so modifiziert, dass er die Autoupdate-Links vom API-Server und nicht von Github-Versionen abruft.\
Damit die Autoupdate-Links funktionieren, müssen Sie Ihren Client so ändern, dass die Autoupdate-Links vom API-Server abgerufen werden. Das [Wie Sie es tun können](https://github.com/sctg-development/sctgdesk/blob/481d3516fef1daa145d8044594187cb11959f8be/src/common.rs#L953L972):

```rust
// src/common.rs
#[tokio::main(flavor = "current_thread")]
async fn check_software_update_() -> hbb_common::ResultType<()> {
    let url=format!("{}/api/software/releases/latest",get_api_server("".to_owned(), "".to_owned())).to_owned();
    log::info!("URL for checking software updates: {}", url);
    //let url = "https://github.com/rustdesk/rustdesk/releases/latest";
    let latest_release_response = create_http_client_async().get(url).send().await?;
    let latest_release_version = latest_release_response
        .url()
        .path()
        .rsplit('/')
        .next()
        .unwrap_or_default();

    let response_url = latest_release_response.url().to_string();

    if get_version_number(&latest_release_version) > get_version_number(crate::VERSION) {
        *SOFTWARE_UPDATE_URL.lock().unwrap() = response_url;
    }
    Ok(())
}
```

# Sicherheit

Der eingebettete API-Server ist weder gesichert noch gegen DDOS-Angriffe geschützt. Es empfiehlt sich, einen Reverseproxy vor dem API-Server zu verwenden. NGINX ist für diesen Zweck eine gute Wahl. HAProxy ist auch eine gute Wahl.\
Wir verwenden HAProxy vor dem API-Server in unserer Produktionsumgebung.
Dies ist unsere Konfigurationsdatei für HAProxy, sie wird nur als Beispiel zur Verfügung gestellt. Sie sollten es an Ihre eigenen Bedürfnisse anpassen.:

```haproxy
global
    log /dev/log    local0
    log /dev/log    local1 notice
    chroot /var/lib/haproxy
    stats socket /run/haproxy/admin.sock mode 660 level admin expose-fd listeners
    stats timeout 30s
    user haproxy
    group haproxy
    daemon

defaults
    log global
    retries 2
    timeout connect 3000ms
    timeout server 5000ms
    timeout client 5000ms

frontend hbbs_wss
    bind 0.0.0.0:21120 ssl crt /etc/haproxy/hbb.pem
    default_backend hbbs_wss_backend

frontend hbbs_api
    mode http
    option forwardfor
    bind 0.0.0.0:21114 ssl crt /etc/haproxy/api.pem
    http-request set-header X-Forwarded-Proto https
    default_backend hbbs_api_backend

frontend hbbs_api_443
    mode http
    option forwardfor
    bind 0.0.0.0:443 ssl crt /etc/haproxy/api.pem
    http-request set-header X-Forwarded-Proto https
    filter compression
    compression algo gzip
    compression type text/css text/html text/javascript application/javascript text/plain text/xml application/json
    compression offload
    default_backend hbbs_api_backend

frontend hbbr_wss
    bind 0.0.0.0:21121 ssl crt /etc/haproxy/hbb.pem
    default_backend hbbr_wss_backend

backend hbbs_api_backend
    mode http
    server srv_main 127.0.0.1:21113

backend hbbs_wss_backend
    server srv_main 127.0.0.1:21118

backend hbbr_wss_backend
    server srv_main 127.0.0.1:21119
```

Der hbbs-Server wird mit

```service
[Unit]
Description=Rustdesk Signal Server

[Service]
Type=simple
LimitNOFILE=1000000
ExecStart=/usr/bin/hbbs --api-port=21113 -k AucFCOYVWNHRkJnx13FFh7C0tmUZ3nei5wXKmlfK6WPYthz65fRavaA5HO/OIz2kq+bCSlAqBkZgvikwVGqw/Q== --mask=10.10.0.235/24 -r rendez-vous.example.org -R rendez-vous.example.org
#Environment="RUST_LOG=debug"
Environment="ALWAYS_USE_RELAY=Y"
Environment="OAUTH2_CREATE_USER=1"
Environment="S3CONFIG_FILE=s3config.toml"
Environment="OAUTH2_CONFIG_FILE=oauth2.toml"
WorkingDirectory=/var/lib/rustdesk-server/
User=
Group=
Restart=always
StandardOutput=append:/var/log/rustdesk-server/hbbs.log
StandardError=append:/var/log/rustdesk-server/hbbs.error
# Restart service after 10 seconds if node service crashes
RestartSec=10

[Install]
WantedBy=multi-user.target
```

# Unerwünschten Zugriff einschränken

Um den Zugriff auf Ihren Server einzuschränken, können Sie die Schaltfläche `--logged-in-only` oder setzen Sie die Option `LOGGED_IN_ONLY=Y` Umgebungsvariable für die `hbbs` Server. Dadurch wird die Kontrolle auf angemeldete Benutzer beschränkt.

Auch wenn diese Option aktiviert ist, können sich Benutzer weiterhin auf dem Rendez-vous-Server registrieren, aber sie können den Peer eines anderen Benutzers nicht steuern. Wenn jemand versucht, einen Peer zu steuern, ohne angemeldet zu sein, erhält er eine Fehlermeldung:

<img width="524" alt="Error message for unauthenticated control attempt" src="https://github.com/user-attachments/assets/cfa46504-39d8-46a7-9072-3ece6818b4a3">

Wenn Sie diese Funktion aktivieren, können Sie Ihrem Server eine zusätzliche Sicherheitsebene hinzufügen und unbefugten Zugriff verhindern.

**Konfigurierend `LOGGED_IN_ONLY`**

So aktivieren Sie diese Funktion:

1.  Legen Sie die `LOGGED_IN_ONLY=Y` Umgebungsvariable für die `hbbs` Server.
2.  Alternativ können Sie die Schaltfläche `--logged-in-only` beim Ausführen der Option `hbbs` Server.

**Beispiel**

So legen Sie die `LOGGED_IN_ONLY` Umgebungsvariablen, können Sie die folgende Zeile zu Ihrer `~/.bashrc` Datei oder Äquivalent:

```bash
export LOGGED_IN_ONLY=Y
```

# RustDesk Server-Programm

[![build](https://github.com/sctg-development/sctgdesk-server/actions/workflows/multiarch-docker-hub.yml/badge.svg)](https://github.com/sctg-development/sctgdesk-server/actions/workflows/multiarch-docker-hub.yml)
[![build](https://github.com/sctg-development/sctgdesk-server/actions/workflows/macos-intel-build.yml/badge.svg)](https://github.com/sctg-development/sctgdesk-server/actions/workflows/macos-intel-build.yml)
[![build](https://github.com/sctg-development/sctgdesk-server/actions/workflows/windows.yml/badge.svg)](https://github.com/sctg-development/sctgdesk-server/actions/workflows/windows.yml)

[**Herunterladen**](https://github.com/sctgdesk/sctgdesk-server/releases)

[**Manuell**](https://rustdesk.com/docs/en/self-host/)

[**Häufig gestellte Fragen**](https://github.com/rustdesk/rustdesk/wiki/FAQ)

Hosten Sie Ihren eigenen RustDesk-Server selbst, er ist kostenlos und Open Source.

## So erstellen Sie manuell

Zuerst benötigen Sie eine funktionierende Rust-Entwicklungs-Toolchain und eine funktionierende Node ≥ 20-Installation.

*   Unices (Linux, MacOS, etc.):

```bash
DATABASE_URL=sqlite://$(pwd)/db_v2.sqlite3 cargo build --release
```

*   Fenster mit cmd.exe Schale:

```cmd
set "DATABASE_URL=sqlite://%CD%/db_v2.sqlite3" && cargo build --release
```

Drei ausführbare Dateien werden in target/release generiert.

*   hbbs - RustDesk ID/Rendezvous Server mit API-Server
*   hbbr - RustDesk Relay Server
*   rustdesk-utils - RustDesk CLI-Dienstprogramme

Aktualisierte Binärdateien finden Sie auf der Seite [Auslösungen](https://github.com/sctg-development/sctgdesk-server/releases) Seite.

Alle nach der Veröffentlichung von v1.1.99-40 veröffentlichten Binärdateien werden mit Github Actions bestätigt. Sie können den Nachweis überprüfen, indem Sie die sha256sum der Binärdatei mit `https://search.sigstore.dev/?hash=<sha256>` Zum Beispiel.

Wenn Sie zusätzliche Funktionen wünschen [RustDesk Server Pro](https://rustdesk.com/pricing.html) könnte besser zu Ihnen passen.

Wenn Sie einen eigenen Server entwickeln möchten, [rustdesk-server-demo](https://github.com/rustdesk/rustdesk-server-demo) könnte ein besserer und einfacherer Start für Sie sein als dieses Repository.

## Docker-Bilder

Docker-Images werden automatisch generiert und in jedem GitHub-Release veröffentlicht.

Diese Images werden erstellt für: `ubuntu-22.04` Mit der einzigen Hinzufügung der Hauptbinärdateien (`hbbr` und `hbbs`). Sie sind erhältlich auf [Docker-Hub](https://hub.docker.com/r/sctg/sctgdesk-server/) mit diesen Tags:

| Architektur | Bild:Tag |
| --- | --- |
| AMD64 | `sctg/sctgdesk-server:latest` |
| arm64v8 | `sctg/sctgdesk-server:latest` |
| arm32v7 | `sctg/sctgdesk-server:latest` |

Sie können diese Bilder direkt mit `docker run` mit diesen Befehlen:

```bash
docker run --name hbbs --net=host -v "$PWD/data:/usr/local/share/sctgdesk" -d sctg/sctgdesk-server:latest hbbs -r <relay-server-ip[:port]> 
docker run --name hbbr --net=host -v "$PWD/data:/usr/local/share/sctgdesk" -d sctg/sctgdesk-server:latest hbbr 
```

oder ohne `--net=host`, aber die P2P-Direktverbindung kann nicht funktionieren.

Bei Systemen, die SELinux verwenden, `/root` bis `/root:z` ist erforderlich, damit die Container ordnungsgemäß ausgeführt werden können. Alternativ kann die SELinux-Containertrennung vollständig deaktiviert werden, indem die Option `--security-opt label=disable`.

```bash
docker run --name hbbs -p 21114:21114 -p 21115:21115 -p 21116:21116 -p 21116:21116/udp -p 21118:21118 -v "$PWD/data:/usr/local/share/sctgdesk" -d sctg/sctgdesk-server:latest hbbs -r <relay-server-ip[:port]> 
docker run --name hbbr -p 21117:21117 -p 21119:21119 -v "$PWD/data:/usr/local/share/sctgdesk" -d sctg/sctgdesk-serverlatest hbbr 
```

Das `relay-server-ip` ist die IP-Adresse (oder der DNS-Name) des Servers, auf dem diese Container ausgeführt werden. Das **wahlfrei** `port` muss verwendet werden, wenn Sie einen anderen Port als **21117** für `hbbr`.

Sie können auch docker-compose verwenden, indem Sie diese Konfiguration als Vorlage verwenden:

```yaml
version: '3'

networks:
  sctgdesk-net:
    external: false

services:
  hbbs:
    container_name: hbbs
    ports:
      - 21114:21114
      - 21115:21115
      - 21115:21115
      - 21116:21116
      - 21116:21116/udp
      - 21118:21118
    image: sctg/sctgdesk-server:latest
    command: hbbs -r sctgdesk.example.com:21117
    volumes:
      - ./data:/usr/local/share/sctgdesk
    networks:
      - sctgdesk-net
    depends_on:
      - hbbr
    restart: unless-stopped

  hbbr:
    container_name: hbbr
    ports:
      - 21117:21117
      - 21119:21119
    image: sctg/sctgdesk-server-server:latest
    command: hbbr
    volumes:
      - ./data:/usr/local/share/sctgdesk
    networks:
      - sctgdesk-net
    restart: unless-stopped
```

Bearbeiten Sie Zeile 16 so, dass sie auf Ihren Relay-Server verweist (der auf Port 21117 lauscht). Sie können bei Bedarf auch die Lautstärkezeilen (Zeile 18 und Zeile 33) bearbeiten.

(docker-compose-Guthaben geht an @lukebarone und @QuiGonLeong)

> Beachten Sie, dass hier sctg/sctgdesk-server-server:latest in China durch die neueste Versionsnummer auf dockerhub ersetzt werden kann, z. B. sctg/sctgdesk-server-server:1.1.99-37. Andernfalls kann es sein, dass die alte Version aufgrund der Bildbeschleunigung gezogen wird.

## So erstellen Sie ein Schlüsselpaar

Für die Verschlüsselung wird ein Schlüsselpaar benötigt; Sie können es bereitstellen, wie bereits erläutert, aber Sie benötigen eine Möglichkeit, eines zu erstellen.

Mit diesem Befehl können Sie ein Schlüsselpaar generieren:

```bash
/usr/bin/rustdesk-utils genkeypair
```

Wenn Sie die `rustdesk-utils` Paket, das auf Ihrem System installiert ist, können Sie denselben Befehl mit docker aufrufen:

```bash
docker run --rm --entrypoint /usr/bin/rustdesk-utils  sctg/sctgdesk-server-server:latest genkeypair
```

Die Ausgabe sieht in etwa wie folgt aus:

```text
Public Key:  8BLLhtzUBU/XKAH4mep3p+IX4DSApe7qbAwNH9nv4yA=
Secret Key:  egAVd44u33ZEUIDTtksGcHeVeAwywarEdHmf99KM5ajwEsuG3NQFT9coAfiZ6nen4hfgNICl7upsDA0f2e/jIA==
```

## Pakete

Für jede Binärdatei stehen separate .deb Pakete zur Verfügung, die Sie in der [Auslösungen](https://github.com/sctg-development/sctgdesk-server/releases).
Diese Pakete sind für die folgenden Distributionen gedacht:

*   Ubuntu 22.04 LTS
*   MacOS Intel oder Apple Silicon
*   Windows x86\_64 oder i686

## ENV-Variablen

hbbs und hbbr können mit diesen ENV-Variablen konfiguriert werden.
Sie können die Variablen wie gewohnt angeben oder eine `.env` Datei.

| variabel | Binär | Beschreibung |
| --- | --- | --- |
| ALWAYS_USE_RELAY | HBBS | Wenn auf **"Y"** Direkte Peer-Verbindung nicht zulässig |
| DOWNGRADE_START_CHECK | HBBR | Verzögerung (in Sekunden) vor der Downgrade-Prüfung |
| DOWNGRADE_THRESHOLD | HBBR | Schwellenwert für die Downgrade-Prüfung (Bit/ms) |
| SCHLÜSSEL | HBBS/HBBR | Wenn gesetzt, erzwingt die Verwendung eines bestimmten Schlüssels, wenn auf **"\_"** Erzwingen Sie die Verwendung einer beliebigen Taste |
| LIMIT_SPEED | HBBR | Geschwindigkeitsbegrenzung (in Mb/s) |
| OAUTH2\_CONFIG_FILE | HBBS | Pfad für OAuth2-Konfigurationsdatei |
| OAUTH2\_CREATE_USER | HBBS | Wenn auf **"1"** Erstellen eines Benutzers, wenn er nicht vorhanden ist |
| HAFEN | HBBS/HBBR | Abhöranschluss (21116 für HBBS - 21117 für HBBR) |
| RELAIS | HBBS | IP-Adresse/DNS-Name der Rechner, auf denen hbbr läuft (durch Komma getrennt) |
| RUST_LOG | alle | Debug-Level setzen (Fehler|Warn|Info|Debug|Trace) |
| S3CONFIG_FILE | HBBS | Pfad für S3-Konfigurationsdatei |
| SINGLE_BANDWIDTH | HBBR | Maximale Bandbreite für eine einzelne Verbindung (in Mbit/s) |
| TOTAL_BANDWIDTH | HBBR | Maximale Gesamtbandbreite (in Mbit/s) |
