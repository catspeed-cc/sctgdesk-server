<p align="center">
  <a href="#how-to-build-manually">Manually</a> •
  <a href="#docker-images">Docker</a> •
  <a href="#how-to-create-a-keypair">Keypair</a> •
  <a href="#packages">Binaries</a> •
  <a href="#env-variables">Variables</a><br>
  [<a href="README-FR.md">French</a>] | [<a href="README-DE.md">Deutsch</a>] | [<a href="README-NL.md">Nederlands</a>] | [<a href="README-TW.md">繁體中文</a>] | [<a href="README-ZH.md">简体中文</a>] | [<a href="README-RU.md">Русский</a>]<br>
</p>

# Programme de serveur SctgDesk

![Docker Pulls](https://img.shields.io/docker/pulls/sctg/sctgdesk-server)
[![build](https://github.com/sctg-development/sctgdesk-server/actions/workflows/multiarch-docker-hub.yml/badge.svg)](https://github.com/sctg-development/sctgdesk-server/actions/workflows/multiarch-docker-hub.yml)
[![build](https://github.com/sctg-development/sctgdesk-server/actions/workflows/macos-intel-build.yml/badge.svg)](https://github.com/sctg-development/sctgdesk-server/actions/workflows/macos-intel-build.yml)
[![build](https://github.com/sctg-development/sctgdesk-server/actions/workflows/windows.yml/badge.svg)](https://github.com/sctg-development/sctgdesk-server/actions/workflows/windows.yml)

[**Téléchargement binaire**](https://github.com/sctg-development/sctgdesk-server/releases)

[**Documentation de l’API**](https://sctg-development.github.io/sctgdesk-api-server/)

Il s’agit d’une version modifiée de RustDesk Server, qui est gratuite et open source.

*   La première différence est que cette version inclut le nouveau *Tcp* mode inclus dans la version RustDesk Server Pro.
*   La deuxième différence est que cette version inclut une implémentation préliminaire du serveur API Rustdesk Server Pro.
    *   Prise en charge du carnet d’adresses personnel
    *   Prise en charge du carnet d’adresses partagé au niveau du groupe
        *   Lecture seule, lecture-écriture, admin
    *   Prise en charge du carnet d’adresses partagé au niveau de l’utilisateur
        *   Lecture seule, lecture-écriture, admin
*   La troisième différence est que cette version inclut une implémentation préliminaire d’une webconsole simple.

La webconsole est accessible à l’adresse `http://<server-ip>:21114/` avec l’identifiant « admin » et le mot de passe « Hello,world ! » .\
Vous pouvez parcourir la documentation de l’API dans le serveur d’API intégré à l’adresse suivante : `http://<server-ip>:21114/api/doc/`.

Une documentation API non interactive est disponible à l’adresse suivante : [sctgdesk-api-server repo](https://sctg-development.github.io/sctgdesk-api-server/).

## Lancez le projet

**Si vous appréciez mon travail, pensez à lui donner une étoile ! 🤩 ou un** [![](https://img.shields.io/static/v1?label=Sponsor\&message=%E2%9D%A4\&logo=GitHub\&color=%23fe8e86)](https://github.com/sponsors/sctg-development)

## TL; DR

Vous pouvez utiliser les éléments suivants `docker-compose.yml` pour démarrer le serveur :

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

et démarrez le serveur avec :

```bash
mkdir -p data
docker-compose up 
```

## Binaires

Les binaires sont disponibles pour les plateformes suivantes :

*   Linux x86\_64 lié statiquement
*   Linux arm64 lié statiquement
*   Linux armv7 lié statiquement
*   MacOS Intel
*   MacOS Apple Silicon
*   Windows x86\_64

### Utilisateur admin par défaut

L’utilisateur admin par défaut est créé avec le nom d’utilisateur `admin` et le mot de passe `Hello,world!`. Vous pouvez modifier le mot de passe après la première connexion sur la webconsole.

## API Version autonome

La version autonome de l’API est une version du serveur qui inclut le serveur API et la webconsole mais pas le serveur de rendez-vous.\
La version autonome est disponible dans son propre dépôt [sctgdesk-api-server](https://github.com/sctg-development/sctgdesk-api-server).\
Pour tout problème lié à l’api ou à la console web, veuillez vous référer à la [sctgdesk-api-server](https://github.com/sctg-development/sctgdesk-api-server) dépôt.

## Captures d’écran

### Console Web

<img width="1085" alt="login" src="https://github.com/sctg-development/sctgdesk-server/assets/165936401/fe72a374-8a98-4606-8632-3d919f9317c9">

<img width="1285" alt="dashboard" src="https://github.com/sctg-development/sctgdesk-api-server/assets/165936401/0bb148d6-8723-491f-88c5-b98331d64f61">

<img width="1085" alt="devices" src="https://github.com/sctg-development/sctgdesk-server/assets/165936401/6ae55861-f65c-4950-a068-f22eef3ad81a">

<img width="1084" alt="users" src="https://github.com/sctg-development/sctgdesk-server/assets/165936401/8d225841-43f5-44f4-8d41-5b6ca3324096">

<img width="1087" alt="groups" src="https://github.com/sctg-development/sctgdesk-server/assets/165936401/d84ce3d3-1d19-4765-883f-001f313a4a1e">

<img width="1089" alt="address books" src="https://github.com/sctg-development/sctgdesk-server/assets/165936401/db13010b-077a-4e14-943b-9d8de3266f82">

<img width="730" alt="rues" src="https://github.com/sctg-development/sctgdesk-api-server/assets/165936401/3a990deb-d8bb-4725-a47d-435ec3667fee">

<img width="621" alt="add rules" src="https://github.com/sctg-development/sctgdesk-api-server/assets/165936401/355f3903-2b54-4b08-abd0-e33c84a260ed">

### Documentation de l’API

<img width="1502" alt="apidoc" src="https://github.com/sctg-development/sctgdesk-server/assets/165936401/88fe7910-fe62-43e5-a16c-70dc1201e040">

### Utilisation dans le client Rustdesk

<img width="913" alt="Capture d’écran 2024-05-24 à 12 14 34" src="https://github.com/sctg-development/sctgdesk-server/assets/165936401/1b253577-dce2-4163-9a49-ba4b3da37812">

<img width="923" alt="Capture d’écran 2024-05-24 à 12 07 21" src="https://github.com/sctg-development/sctgdesk-server/assets/165936401/c49b3aba-b13f-4b15-a69c-d492a90e774a">

<img width="927" alt="Capture d’écran 2024-05-24 à 12 07 32" src="https://github.com/sctg-development/sctgdesk-server/assets/165936401/f447f5fa-bc77-4bc6-858a-c6cadf9b7f6c">

## Génération de liens de mise à jour automatique

Nous avons modifié notre client pour récupérer les liens de mise à jour automatique du serveur d’api plutôt que des versions de Github.\
Pour que les liens de mise à jour automatique fonctionnent, vous devez modifier votre client pour récupérer les liens de mise à jour automatique à partir du serveur d’API. Ceci [Comment vous pouvez le faire](https://github.com/sctg-development/sctgdesk/blob/481d3516fef1daa145d8044594187cb11959f8be/src/common.rs#L953L972):

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

# Sécurité

Le serveur API intégré n’est ni sécurisé ni protégé contre les attaques DDOS. Une bonne pratique consiste à utiliser un proxy inverse devant le serveur API. NGINX est un bon choix à cet effet. HAProxy est également un bon choix.\
Nous utilisons HAProxy devant le serveur API dans notre environnement de production.
Il s’agit de notre fichier de configuration pour HAProxy, il est fourni à titre d’exemple uniquement. Vous devez l’adapter à vos propres besoins.

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

Le serveur hbbs est lancé avec

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

# Limiter les accès indésirables

Pour restreindre l’accès à votre serveur, vous pouvez utiliser l’option `--logged-in-only` ou définir l’option `LOGGED_IN_ONLY=Y` pour la variable `hbbs` serveur. Cela limitera le contrôle aux utilisateurs connectés uniquement.

Même avec cette option activée, les utilisateurs peuvent toujours s’inscrire sur le serveur Rendez-vous, mais ils ne pourront pas contrôler le pair d’un autre utilisateur. Si quelqu’un essaie de contrôler un homologue sans être connecté, il recevra un message d’erreur :

<img width="524" alt="Error message for unauthenticated control attempt" src="https://github.com/user-attachments/assets/cfa46504-39d8-46a7-9072-3ece6818b4a3">

En activant cette fonctionnalité, vous pouvez ajouter une couche de sécurité supplémentaire à votre serveur et empêcher tout accès non autorisé.

**Configuration `LOGGED_IN_ONLY`**

Pour activer cette fonctionnalité :

1.  Réglez l’icône `LOGGED_IN_ONLY=Y` pour la variable `hbbs` serveur.
2.  Vous pouvez également utiliser l’icône `--logged-in-only` lors de l’exécution de l’option `hbbs` serveur.

**Exemple**

Pour définir le `LOGGED_IN_ONLY` , vous pouvez ajouter la ligne suivante à votre `~/.bashrc` fichier ou équivalent :

```bash
export LOGGED_IN_ONLY=Y
```

# Programme de serveur RustDesk

[![build](https://github.com/sctg-development/sctgdesk-server/actions/workflows/multiarch-docker-hub.yml/badge.svg)](https://github.com/sctg-development/sctgdesk-server/actions/workflows/multiarch-docker-hub.yml)
[![build](https://github.com/sctg-development/sctgdesk-server/actions/workflows/macos-intel-build.yml/badge.svg)](https://github.com/sctg-development/sctgdesk-server/actions/workflows/macos-intel-build.yml)
[![build](https://github.com/sctg-development/sctgdesk-server/actions/workflows/windows.yml/badge.svg)](https://github.com/sctg-development/sctgdesk-server/actions/workflows/windows.yml)

[**Télécharger**](https://github.com/sctgdesk/sctgdesk-server/releases)

[**Manuelle**](https://rustdesk.com/docs/en/self-host/)

[**FAQ**](https://github.com/rustdesk/rustdesk/wiki/FAQ)

Auto-hébergez votre propre serveur RustDesk, il est gratuit et open source.

## Comment construire manuellement

Tout d’abord, vous devez disposer d’une chaîne d’outils de développement Rust fonctionnelle et d’une installation fonctionnelle de Node ≥ 20.

*   Unices (Linux, MacOS, etc.) :

```bash
DATABASE_URL=sqlite://$(pwd)/db_v2.sqlite3 cargo build --release
```

*   Fenêtres avec coque cmd.exe :

```cmd
set "DATABASE_URL=sqlite://%CD%/db_v2.sqlite3" && cargo build --release
```

Trois exécutables seront générés dans target/release.

*   hbbs - Serveur RustDesk ID/Rendezvous avec serveur API
*   hbbr - Serveur relais RustDesk
*   rustdesk-utils - Utilitaires CLI RustDesk

Vous pouvez trouver les fichiers binaires mis à jour sur le [Versions](https://github.com/sctg-development/sctgdesk-server/releases) page.

Tous les binaires publiés après la version v1.1.99-40 sont attestés par Github Actions. Vous pouvez vérifier l’attestation en vérifiant la somme sha256 du binaire avec `https://search.sigstore.dev/?hash=<sha256>` par exemple.

Si vous voulez des fonctionnalités supplémentaires [Serveur RustDesk Pro](https://rustdesk.com/pricing.html) pourrait mieux vous convenir.

Si vous souhaitez développer votre propre serveur, [rustdesk-server-demo](https://github.com/rustdesk/rustdesk-server-demo) pourrait être un meilleur et plus simple début pour vous que ce dépôt.

## Images Docker

Les images Docker sont automatiquement générées et publiées sur chaque version de github.

Ces images sont construites contre `ubuntu-22.04` avec le seul ajout des binaires principaux (`hbbr` et `hbbs`). Ils sont disponibles sur [Hub Docker](https://hub.docker.com/r/sctg/sctgdesk-server/) avec ces balises :

| L’architecture | image :balise |
| --- | --- |
| AMD64 | `sctg/sctgdesk-server:latest` |
| ARM64V8 | `sctg/sctgdesk-server:latest` |
| ARM32v7 | `sctg/sctgdesk-server:latest` |

Vous pouvez commencer ces images directement avec `docker run` avec ces commandes :

```bash
docker run --name hbbs --net=host -v "$PWD/data:/usr/local/share/sctgdesk" -d sctg/sctgdesk-server:latest hbbs -r <relay-server-ip[:port]> 
docker run --name hbbr --net=host -v "$PWD/data:/usr/local/share/sctgdesk" -d sctg/sctgdesk-server:latest hbbr 
```

ou sans `--net=host`, mais la connexion directe P2P ne peut pas fonctionner.

Pour les systèmes utilisant SELinux, le remplacement de `/root` par `/root:z` est nécessaire au bon fonctionnement des conteneurs. Alternativement, la séparation des conteneurs SELinux peut être complètement désactivée en ajoutant l’option `--security-opt label=disable`.

```bash
docker run --name hbbs -p 21114:21114 -p 21115:21115 -p 21116:21116 -p 21116:21116/udp -p 21118:21118 -v "$PWD/data:/usr/local/share/sctgdesk" -d sctg/sctgdesk-server:latest hbbs -r <relay-server-ip[:port]> 
docker run --name hbbr -p 21117:21117 -p 21119:21119 -v "$PWD/data:/usr/local/share/sctgdesk" -d sctg/sctgdesk-serverlatest hbbr 
```

Le `relay-server-ip` parameter est l’adresse IP (ou le nom dns) du serveur exécutant ces conteneurs. Le **optionnel** `port` doit être utilisé si vous utilisez un port différent de **21117** pour `hbbr`.

Vous pouvez également utiliser docker-compose, en utilisant cette configuration comme modèle :

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

Éditez la ligne 16 pour pointer vers votre serveur relais (celui qui écoute sur le port 21117). Vous pouvez également modifier les lignes de volume (ligne 18 et ligne 33) si vous le souhaitez.

(crédit docker-compose revient à @lukebarone et @QuiGonLeong)

> Notez qu’ici, le sctg/sctgdesk-server-server :latest en Chine peut être remplacé par le dernier numéro de version sur dockerhub, tel que sctg/sctgdesk-server-server :1.1.99-37. Sinon, l’ancienne version peut être retirée en raison de l’accélération de l’image.

## Comment créer une paire de clés

Une paire de clés est nécessaire pour le chiffrement ; Vous pouvez le fournir, comme expliqué précédemment, mais vous avez besoin d’un moyen d’en créer un.

Vous pouvez utiliser cette commande pour générer une paire de clés :

```bash
/usr/bin/rustdesk-utils genkeypair
```

Si vous n’avez pas (ou ne voulez pas) le `rustdesk-utils` installé sur votre système, vous pouvez invoquer la même commande avec docker :

```bash
docker run --rm --entrypoint /usr/bin/rustdesk-utils  sctg/sctgdesk-server-server:latest genkeypair
```

Le résultat sera quelque chose comme ceci :

```text
Public Key:  8BLLhtzUBU/XKAH4mep3p+IX4DSApe7qbAwNH9nv4yA=
Secret Key:  egAVd44u33ZEUIDTtksGcHeVeAwywarEdHmf99KM5ajwEsuG3NQFT9coAfiZ6nen4hfgNICl7upsDA0f2e/jIA==
```

## Paquets

Des paquets .deb séparés sont disponibles pour chaque binaire, vous pouvez les trouver dans le [Versions](https://github.com/sctg-development/sctgdesk-server/releases).
Ces paquets sont destinés aux distributions suivantes :

*   Ubuntu 22.04 LTS
*   MacOS Intel ou Apple Silicon
*   Windows x86\_64 ou i686

## Variables ENV

hbbs et hbbr peuvent être configurés à l’aide de ces variables ENV.
Vous pouvez spécifier les variables comme d’habitude ou utiliser un `.env` lime.

| variable | binaire | Descriptif |
| --- | --- | --- |
| ALWAYS_USE_RELAY | HBB | s’il est défini sur **« Y »** Interdit la connexion directe entre pairs |
| DOWNGRADE_START_CHECK | HBBR | Délai (en secondes) avant la vérification de la rétrogradation |
| DOWNGRADE_THRESHOLD | HBBR | Seuil de vérification de la rétrogradation (bit/ms) |
| LÉGENDE | hbbs/hbbr | si cette option est définie, force l’utilisation d’une touche spécifique, si elle est définie sur **"\_"** forcer l’utilisation de n’importe quelle touche |
| LIMIT_SPEED | HBBR | Limitation de vitesse (en Mb/s) |
| OAUTH2\_CONFIG_FILE | HBB | chemin d’accès au fichier de configuration OAuth2 |
| OAUTH2\_CREATE_USER | HBB | s’il est défini sur **"1"** Créer un utilisateur s’il n’existe pas |
| LE PORT | hbbs/hbbr | Port d’écoute (21116 pour HBBS - 21117 pour HBBR) |
| RELAIS | HBB | Adresse IP/nom DNS des machines exécutant hbbr (séparé par une virgule) |
| RUST_LOG | Tous | définir le niveau de débogage (error|warn|info|debug|trace) |
| S3CONFIG_FILE | HBB | Chemin d’accès au fichier de configuration S3 |
| SINGLE_BANDWIDTH | HBBR | bande passante maximale pour une seule connexion (en Mb/s) |
| TOTAL_BANDWIDTH | HBBR | bande passante totale maximale (en Mb/s) |
