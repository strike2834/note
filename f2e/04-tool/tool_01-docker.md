# Docker

Docker 的出現，是為了解決在 deploy 作業途中時會出現的各種問題。

## Deploy 的歷史

早前的網路環境（約莫至 1990 年左右）是以一台大型電腦做為伺服器，處理所有的 request，但是這樣的設計會受限於製造商的品牌硬體，造成高成本、欠缺柔軟性和擴充性的問題。

之後技術進步，隨著小型電腦的性能提升與價格下降，出現了串接多台小型電腦，設置分散系統與功能的構築手法，這種手法稱為 Engine downsizing，成為了當時的主流作法，但這波變化又帶來了新的問題。

### 虛擬化

首先不難想像的是，隨著電腦增加造成管理與使用上的困難，有 100 台電腦，就需要進行 100 次的環境設定，若之後有更新，也要 100 台電腦全部都裝過一遍，並且這些電腦不會經常保持滿載處理，而是總會有閒置中的電腦。

在安全性與維護性上也有所疑慮，當其中一台電腦受到攻擊，就會影響到所有在上面執行的程式。

以及隨著作業系統的多樣化，會有程式無法在不相容的伺服器上執行，這時出現了「虛擬化」，透過軟體來整合多種硬體，能夠自由模擬各種規格的電腦環境。

雖然虛擬化以及虛擬機器的登場，解決了許多 deploy 時會遇到的問題，但虛擬機器也有其弱點，那就是在系統背後執行的，其它與程式無關的系統服務，會造成大量的系統開銷與資源浪費。

### 容器（Container）虛擬化

於是「容器虛擬化」誕生了。容器虛擬化指的是，把執行的程式從開發與執行環境隔離開來，如此能夠安全並且快速地執行多個程式。並且這套技術不需要安裝新的作業系統，而是透過系統裡的多個功能，讓應用程式在同一個作業系統上，但執行於不同的容器隔離空間中。

### Docker 的出現

Docker 就是使用了容器虛擬化概念的應用程式之一，另外也有許多其它使用容器虛擬化的應用程式。

Docker 以名為 `dockerfile` 的檔案為基礎來建立鏡像，以及產生容器（執行程式），Docker 會依照檔案內所記載的指令依序執行。因此擁有 1. 能夠簡單多次產生容器 2. 能夠將容器帶著走 3. 能夠簡便管理應用程式的版本 等優點。

原本 Docker 是 LinuxOS 專用的功能，之後 macOS 和 Windows 上面也有了如 `Docker Desktop for Mac` 或 `Docker for Windows` 這類先於電腦上執行 Linux 環境的虛擬機器，再於其中執行 Docker 的應用程式。

### tl;dr

- Docker 成立於既有的 Linux Kernal
- 透過分享鏡像可讓多人於不同環境簡單啟動容器
- 容器透過 Docker 指令逐一命令
- dockerfile 可以簡化 docker 指令輸入作業
- docker-compose 可以於同一 host OS 上管理複數容器

## 安裝

- [30 天與鯨魚先生做好朋友](https://ithelp.ithome.com.tw/users/20102562/ironman/3746?page=1)

### A. MAC、Windows

目前在 MAC 和 Windows 上面也可以使用 docker，從官方網站 [Docker Desktop for Mac and Windows](https://www.docker.com/products/docker-desktop) 裡下載並安裝之後，在 terminal 裡輸入 `docker --version` 和 `docker-compose --version` 有出現版本號，就代表安裝成功。

Windows 版會推薦先安裝 WSL2（Windows Subsystem for Linux，於 Windows 上執行的 Linux 子系統），之後再安裝 docker，可以參照下列流程。

#### 1. 啟用虛擬機器平台

1. 開啟控制台（control panel）
2. 開啟「程式集」
3. 開啟「開啟或關閉 Windows 功能」
4. 勾選「虛擬機器平台」

#### 2. 安裝 WSL2

1. 以管理者權限開啟 PowerShell
2. 執行指令 `dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart`
3. 從微軟官方網站[下載 WSL2 Linux 核心更新套件](https://docs.microsoft.com/zh-tw/windows/wsl/wsl2-kernel)
4. 從 MicrosoftStore 安裝 Ubuntu 18.04LTS

#### 3. 安裝 Docker Desktop

從官方網站 [Docker Desktop for Mac and Windows](https://www.docker.com/products/docker-desktop) 裡下載並安裝 Docker Desktop。

### B. Linux

- 移除舊版本：`sudo apt-get remove docker docker-engine docker.io`
- 使用腳本安裝：`curl -fsSL https://get.docker.com -o get-docker.sh`<br/>
  `sudo sh get-docker.sh`
- 若想使用非 root 使用者執行 docker，可將此使用者加至 `docker` 身份組中
- `sudo usermod -aG docker your-user`

## 使用

- `docker images`：查看 images
- `docker run`：執行 images
- `docker ps`：查看執行中的 container
- `top`、`htop`、`ctop`、`gtop`、`conky`：監看工具

### 撰寫 Dockerfile

- [あなたの Dockerfile はベストプラクティスに従っていますか？(ベストプラクティスとチェックツール)](https://qiita.com/yoshii0110/items/0accb7f21fa1c375e0d7)

```dockerfile
# fetch node v4 LTS codename argon
FROM node:argon

# Request samplename build argument
ARG samplename

# Create app directory
RUN mkdir -p /usr/src/spfx-samples
WORKDIR /usr/src/spfx-samples

# Install app dependencies
RUN git clone https://github.com/SharePoint/sp-dev-fx-webparts.git .
WORKDIR /usr/src/spfx-samples/samples/$samplename

# Install gulp on a global scope
RUN npm install gulp -g

# RUN ["npm", "install", "gulp"]
RUN npm install
RUN npm cache clean

# Expose required ports
EXPOSE 4321 35729 5432

# Run Sample
CMD ["gulp", "serve"]
```

### VS Code Remote - Containers

- [Remote - Containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)
- `Remote-Containers: Try a Development Container Sample...`

### devcontainers/cli

- [Dev Container が VSCode から CLI にもやって来た](https://zenn.dev/hankei6km/articles/devcontainers-in-cli-ci)

### Docker deploy

- [Container Registry および Runtime (Docker デプロイ)](https://devcenter.heroku.com/ja/articles/container-registry-and-runtime)

## 參考資料

### 2018

- [「Docker」を全く知らない人のために「Docker」の魅力を伝えるための「Docker」入門](https://qiita.com/bremen/items/4604f530fe25786240db)

### 2019

- [Docker で立ち上げた開発環境を VS Code で開く!](https://qiita.com/yoskeoka/items/01c52c069123e0298660)

### 2020

- [いまさらだけど Docker に入門したので分かりやすくまとめてみた](https://qiita.com/gold-kou/items/44860fbda1a34a001fc1)
- [【図解】Docker の全体像を理解する -前編-](https://qiita.com/etaroid/items/b1024c7d200a75b992fc)
- [Docker を体系的に学び直してみた(導入編)](https://qiita.com/takuya_tsurumi/items/182d2de3f3ce7bb63edb)
- [Docker のことが多分わかるハンズオン](https://speakerdeck.com/yoshi0202/dockerfalsekotogaduo-fen-wakaruhanzuon)

### 2022

- [Docker を体系的に学べる公式チュートリアル和訳](https://qiita.com/Michinosuke/items/5778e0d9e9c04038903c)
- [初心者が絵で理解する Docker](https://zenn.dev/suzuki_hoge/books/2021-04-docker-picture-60fbe950136be9c7ad85)
- [Docker 完全に理解した](https://eng-blog.iij.ad.jp/archives/12414)
- [Mark Volkmann's blog - Containers](https://mvolkmann.github.io/blog/topics/#/blog/containers/)
- [作業環境を Dockerfile にまとめて、macOS でも Linux でも WSL2 でも快適に過ごせるようになった話](https://zenn.dev/hinoshiba/articles/workstation-on-docker)
- [VSCode のリモートコンテナ機能を用いて、あるリポジトリ専用の環境を開発者間で統一する](https://zenn.dev/yuchiki/articles/vscode-remote-container)
- [Docker Compose な開発環境にちょい足し 3 分で作る VSCode devcontainer](https://zenn.dev/saboyutaka/articles/9cffc8d14c6684)
