<p align="center">
  <a href="#how-to-build-manually">Manually</a> •
  <a href="#docker-images">Docker</a> •
  <a href="#how-to-create-a-keypair">Keypair</a> •
  <a href="#packages">Binaries</a> •
  <a href="#env-variables">Variables</a><br>
  [<a href="README-FR.md">French</a>] | [<a href="README-DE.md">Deutsch</a>] | [<a href="README-NL.md">Nederlands</a>] | [<a href="README-TW.md">繁體中文</a>] | [<a href="README-ZH.md">简体中文</a>] | [<a href="README-RU.md">Русский</a>]<br>
</p>

# SctgDesk Server Program

![Docker Pulls](https://img.shields.io/docker/pulls/sctg/sctgdesk-server)页。[![build](https://github.com/sctg-development/sctgdesk-server/actions/workflows/multiarch-docker-hub.yml/badge.svg)](https://github.com/sctg-development/sctgdesk-server/actions/workflows/multiarch-docker-hub.yml)版本 v1.1.99-40 之后发布的所有二进制文件都使用 Github Actions 进行证明。您可以通过使用[![build](https://github.com/sctg-development/sctgdesk-server/actions/workflows/macos-intel-build.yml/badge.svg)](https://github.com/sctg-development/sctgdesk-server/actions/workflows/macos-intel-build.yml)例如。[![build](https://github.com/sctg-development/sctgdesk-server/actions/workflows/windows.yml/badge.svg)](https://github.com/sctg-development/sctgdesk-server/actions/workflows/windows.yml)

[**如果您想要额外的功能**](https://github.com/sctg-development/sctgdesk-server/releases)

[**RustDesk 服务器专业版**](https://sctg-development.github.io/sctgdesk-api-server/)

可能更适合您。

*   如果你想开发自己的服务器，*rustdesk-server-demo*对您来说，可能比此 repo 更好、更简单的开始。
*   Docker 镜像
    *   Docker 镜像是自动生成的，并在每个 github 版本上发布。
    *   这些映像是针对
        *   唯一添加的主二进制文件 （
    *   和
        *   ).它们可在
*   Docker 中心

替换为这些标签：`http://<server-ip>:21114/`|建筑 |图片：标签 |
|--- |--- |
|AMD64 系列 |\
|
|ARM64V8 |`http://<server-ip>:21114/api/doc/`|
|ARM32V7 |

|[您可以直接使用](https://sctg-development.github.io/sctgdesk-api-server/)使用以下命令：

## 或没有

**，但 P2P 直连无法使用。**对于使用 SELinux 的系统，将[![](https://img.shields.io/static/v1?label=Sponsor\&message=%E2%9D%A4\&logo=GitHub\&color=%23fe8e86)](https://github.com/sponsors/sctg-development)

## 由

是容器正常运行所必需的。或者，可以完全禁用 SELinux 容器分离，并添加选项`docker-compose.yml`.

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

这

```bash
mkdir -p data
docker-compose up 
```

## parameter 是运行这些容器的服务器的 IP 地址（或 DNS 名称）。这

自选

*
*   参数，如果使用的端口不同于
*   21117
*   为
*   .
*   您还可以使用 docker-compose，使用此配置作为模板：

### 编辑第 16 行以指向您的中继服务器（侦听端口 21117 的服务器）。如果需要，您还可以编辑体积行（第 18 行和第 33 行）。

（docker-compose 功劳归于 @lukebarone 和 @QuiGonLeong）`admin`注意，这里中国的 sctg/sctgdesk-server-server：latest 可能会替换为 dockerhub 上的最新版本号，例如 sctg/sctgdesk-server-server：1.1.99-37。否则，可能会因镜像加速而拉取旧版本。`Hello,world!`如何创建密钥对

## 加密需要密钥对;如前所述，您可以提供它，但您需要一种方法来创建一个。

您可以使用此命令生成密钥对：\
如果您没有（或不想要）[软件包，您可以使用 Docker 调用相同的命令：](https://github.com/sctg-development/sctgdesk-api-server)输出将如下所示：\
包[每个二进制文件都有单独的 .deb 包，您可以在](https://github.com/sctg-development/sctgdesk-api-server)释放

## .&#xA;这些软件包适用于以下发行版：

### Ubuntu 22.04 LTS

<img width="1085" alt="login" src="https://github.com/sctg-development/sctgdesk-server/assets/165936401/fe72a374-8a98-4606-8632-3d919f9317c9">

<img width="1285" alt="dashboard" src="https://github.com/sctg-development/sctgdesk-api-server/assets/165936401/0bb148d6-8723-491f-88c5-b98331d64f61">

<img width="1085" alt="devices" src="https://github.com/sctg-development/sctgdesk-server/assets/165936401/6ae55861-f65c-4950-a068-f22eef3ad81a">

<img width="1084" alt="users" src="https://github.com/sctg-development/sctgdesk-server/assets/165936401/8d225841-43f5-44f4-8d41-5b6ca3324096">

<img width="1087" alt="groups" src="https://github.com/sctg-development/sctgdesk-server/assets/165936401/d84ce3d3-1d19-4765-883f-001f313a4a1e">

<img width="1089" alt="address books" src="https://github.com/sctg-development/sctgdesk-server/assets/165936401/db13010b-077a-4e14-943b-9d8de3266f82">

<img width="730" alt="rues" src="https://github.com/sctg-development/sctgdesk-api-server/assets/165936401/3a990deb-d8bb-4725-a47d-435ec3667fee">

<img width="621" alt="add rules" src="https://github.com/sctg-development/sctgdesk-api-server/assets/165936401/355f3903-2b54-4b08-abd0-e33c84a260ed">

### MacOS Intel 或 Apple Silicon

<img width="1502" alt="apidoc" src="https://github.com/sctg-development/sctgdesk-server/assets/165936401/88fe7910-fe62-43e5-a16c-70dc1201e040">

### Windows x86\_64 或 i686

<img width="913" alt="Capture d’écran 2024-05-24 à 12 14 34" src="https://github.com/sctg-development/sctgdesk-server/assets/165936401/1b253577-dce2-4163-9a49-ba4b3da37812">

<img width="923" alt="Capture d’écran 2024-05-24 à 12 07 21" src="https://github.com/sctg-development/sctgdesk-server/assets/165936401/c49b3aba-b13f-4b15-a69c-d492a90e774a">

<img width="927" alt="Capture d’écran 2024-05-24 à 12 07 32" src="https://github.com/sctg-development/sctgdesk-server/assets/165936401/f447f5fa-bc77-4bc6-858a-c6cadf9b7f6c">

## ENV 变量

hbbs 和 hbbr 可以使用这些 ENV 变量进行配置。
您可以像往常一样指定变量，也可以使用\
文件。[|变量 |二进制 |描述 |
|--- |--- |--- |
|ALWAYS_USE_RELAY |HBBS |如果设置为](https://github.com/sctg-development/sctgdesk/blob/481d3516fef1daa145d8044594187cb11959f8be/src/common.rs#L953L972)“Y”

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

# 不允许直接对等连接 |&#xA;|DOWNGRADE_START_CHECK |HBBBR |降级检查前的延迟（以秒为单位） |&#xA;|DOWNGRADE_THRESHOLD |HBBBR |降级检查阈值 （bit/ms） |&#xA;|密钥 |HBBS/HBBR |如果设置为 ，则强制使用特定密钥，如果设置为

"\_"\
强制使用任意键 |
|LIMIT_SPEED |HBBBR |速度限制（Mb/s） |
|OAUTH2\_CONFIG_FILE |HBBS |OAuth2 配置文件的路径 |
|OAUTH2\_CREATE_USER |HBBS |如果设置为

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

"1"

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

# 创建不存在的用户 |&#xA;|端口 |HBBS/HBBR |侦听端口（HBB 为 21116 - HBBR 为 21117）|&#xA;|继电器 |HBBS |运行 hbbr 的计算机的 IP 地址/DNS 名称（以逗号分隔） |&#xA;|RUST_LOG |全部 |设置调试级别 （error|warn|info|debug|trace） |&#xA;|S3CONFIG_FILE |HBBS |S3 配置文件的路径 |&#xA;|SINGLE_BANDWIDTH |HBBBR |单个连接的最大带宽（以 Mb/s 为单位） |&#xA;|TOTAL_BANDWIDTH |HBBBR |最大总带宽（以 Mb/s 为单位） |

To restrict access to your server, you can use the `--logged-in-only` option or set the `LOGGED_IN_ONLY=Y` environment variable for the `hbbs` server. This will limit control to logged-in users only.

Even with this option enabled, users can still register on the Rendez-vous server, but they won't be able to control another user's peer. If someone tries to control a peer without being logged in, they'll receive an error message:

<img width="524" alt="Error message for unauthenticated control attempt" src="https://github.com/user-attachments/assets/cfa46504-39d8-46a7-9072-3ece6818b4a3">

By enabling this feature, you can add an extra layer of security to your server and prevent unauthorized access.

**Configuring `LOGGED_IN_ONLY`**

To enable this feature:

1.  Set the `LOGGED_IN_ONLY=Y` environment variable for the `hbbs` server.
2.  Alternatively, you can use the `--logged-in-only` option when running the `hbbs` server.

**Example**

To set the `LOGGED_IN_ONLY` environment variable, you can add the following line to your `~/.bashrc` file or equivalent:

```bash
export LOGGED_IN_ONLY=Y
```

# RustDesk Server Program

[![build](https://github.com/sctg-development/sctgdesk-server/actions/workflows/multiarch-docker-hub.yml/badge.svg)](https://github.com/sctg-development/sctgdesk-server/actions/workflows/multiarch-docker-hub.yml)
[![build](https://github.com/sctg-development/sctgdesk-server/actions/workflows/macos-intel-build.yml/badge.svg)](https://github.com/sctg-development/sctgdesk-server/actions/workflows/macos-intel-build.yml)
[![build](https://github.com/sctg-development/sctgdesk-server/actions/workflows/windows.yml/badge.svg)](https://github.com/sctg-development/sctgdesk-server/actions/workflows/windows.yml)

[**Download**](https://github.com/sctgdesk/sctgdesk-server/releases)

[**Manual**](https://rustdesk.com/docs/en/self-host/)

[**FAQ**](https://github.com/rustdesk/rustdesk/wiki/FAQ)

Self-host your own RustDesk server, it is free and open source.

## How to build manually

First you need to have a working Rust development toolchain and a Node ≥ 20 working installation.

*   Unices (Linux, MacOS, etc.):

```bash
DATABASE_URL=sqlite://$(pwd)/db_v2.sqlite3 cargo build --release
```

*   Windows with cmd.exe shell:

```cmd
set "DATABASE_URL=sqlite://%CD%/db_v2.sqlite3" && cargo build --release
```

Three executables will be generated in target/release.

*   hbbs - RustDesk ID/Rendezvous server with API server
*   hbbr - RustDesk relay server
*   rustdesk-utils - RustDesk CLI utilities

You can find updated binaries on the [releases](https://github.com/sctg-development/sctgdesk-server/releases) page.

All released binaries after release v1.1.99-40 are attestated with Github Actions. You can check the attestation by checking the sha256sum of the binary with `https://search.sigstore.dev/?hash=<sha256>` for example.

If you want extra features [RustDesk Server Pro](https://rustdesk.com/pricing.html) might suit you better.

If you want to develop your own server, [rustdesk-server-demo](https://github.com/rustdesk/rustdesk-server-demo) might be a better and simpler start for you than this repo.

## Docker images

Docker images are automatically generated and published on every github release.

These images are build against `ubuntu-22.04` with the only addition of the main binaries (`hbbr` and `hbbs`). They're available on [Docker hub](https://hub.docker.com/r/sctg/sctgdesk-server/) with these tags:

| architecture | image:tag |
| --- | --- |
| amd64 | `sctg/sctgdesk-server:latest` |
| arm64v8 | `sctg/sctgdesk-server:latest` |
| arm32v7 | `sctg/sctgdesk-server:latest` |

You can start these images directly with `docker run` with these commands:

```bash
docker run --name hbbs --net=host -v "$PWD/data:/usr/local/share/sctgdesk" -d sctg/sctgdesk-server:latest hbbs -r <relay-server-ip[:port]> 
docker run --name hbbr --net=host -v "$PWD/data:/usr/local/share/sctgdesk" -d sctg/sctgdesk-server:latest hbbr 
```

or without `--net=host`, but P2P direct connection can not work.

For systems using SELinux, replacing `/root` by `/root:z` is required for the containers to run correctly. Alternatively, SELinux container separation can be disabled completely adding the option `--security-opt label=disable`.

```bash
docker run --name hbbs -p 21114:21114 -p 21115:21115 -p 21116:21116 -p 21116:21116/udp -p 21118:21118 -v "$PWD/data:/usr/local/share/sctgdesk" -d sctg/sctgdesk-server:latest hbbs -r <relay-server-ip[:port]> 
docker run --name hbbr -p 21117:21117 -p 21119:21119 -v "$PWD/data:/usr/local/share/sctgdesk" -d sctg/sctgdesk-serverlatest hbbr 
```

The `relay-server-ip` parameter is the IP address (or dns name) of the server running these containers. The **optional** `port` parameter has to be used if you use a port different than **21117** for `hbbr`.

You can also use docker-compose, using this configuration as a template:

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

Edit line 16 to point to your relay server (the one listening on port 21117). You can also edit the volume lines (line 18 and line 33) if you need.

(docker-compose credit goes to @lukebarone and @QuiGonLeong)

> Note that here, the sctg/sctgdesk-server-server:latest in China may be replaced with the latest version number on dockerhub, such as sctg/sctgdesk-server-server:1.1.99-37. Otherwise, the old version may be pulled due to image acceleration.

## How to create a keypair

A keypair is needed for encryption; you can provide it, as explained before, but you need a way to create one.

You can use this command to generate a keypair:

```bash
/usr/bin/rustdesk-utils genkeypair
```

If you don't have (or don't want) the `rustdesk-utils` package installed on your system, you can invoke the same command with docker:

```bash
docker run --rm --entrypoint /usr/bin/rustdesk-utils  sctg/sctgdesk-server-server:latest genkeypair
```

The output will be something like this:

```text
Public Key:  8BLLhtzUBU/XKAH4mep3p+IX4DSApe7qbAwNH9nv4yA=
Secret Key:  egAVd44u33ZEUIDTtksGcHeVeAwywarEdHmf99KM5ajwEsuG3NQFT9coAfiZ6nen4hfgNICl7upsDA0f2e/jIA==
```

## Packages

Separate .deb packages are available for each binary, you can find them in the [releases](https://github.com/sctg-development/sctgdesk-server/releases).
These packages are meant for the following distributions:

*   Ubuntu 22.04 LTS
*   MacOS Intel or Apple Silicon
*   Windows x86\_64 or i686

## ENV variables

hbbs and hbbr can be configured using these ENV variables.
You can specify the variables as usual or use an `.env` file.

| variable | binary | description |
| --- | --- | --- |
| ALWAYS_USE_RELAY | hbbs | if set to **"Y"** disallows direct peer connection |
| DOWNGRADE_START_CHECK | hbbr | delay (in seconds) before downgrade check |
| DOWNGRADE_THRESHOLD | hbbr | threshold of downgrade check (bit/ms) |
| KEY | hbbs/hbbr | if set force the use of a specific key, if set to **"\_"** force the use of any key |
| LIMIT_SPEED | hbbr | speed limit (in Mb/s) |
| OAUTH2\_CONFIG_FILE | hbbs | path for oauth2 config file |
| OAUTH2\_CREATE_USER | hbbs | if set to **"1"** create a user if it doesn't exist |
| PORT | hbbs/hbbr | listening port (21116 for hbbs - 21117 for hbbr) |
| RELAY | hbbs | IP address/DNS name of the machines running hbbr (separated by comma) |
| RUST_LOG | all | set debug level (error|warn|info|debug|trace) |
| S3CONFIG_FILE | hbbs | path for s3 config file |
| SINGLE_BANDWIDTH | hbbr | max bandwidth for a single connection (in Mb/s) |
| TOTAL_BANDWIDTH | hbbr | max total bandwidth (in Mb/s) |
