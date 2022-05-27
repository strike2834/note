# 自動化工具

為了簡化各種工作，開發前端也有許多自動化工具可使用，<br />
例如自動化工作流程的 Gulp，整合、打包模組的 Webpack，或是免設定的編譯、打包的 Parcel。

## npm

- `npm` 是 Node.js 的套件管理系統（Package Manager）
- 可在開始開發時使用 `npm init` 指令
  - 會在開發環境底下新增一個 `package.json` 檔案，將所使用的套件名稱與版本等相關資訊儲存在裡面
- 每次追加新的 `xxx` 套件時，執行 `npm install xxx --save` 就會更新 `package.json` 裡面的 `dependencies`，並且新增另一個 `package-lock.json` 檔案
- `xxx` 套件的最新版本為 `1.0.0` 時，`package.json` 的 `dependencies` 會以範圍格式記載 `"xxx": "^1.0.0"`，亦即適用以 1 開頭的最新版本檔案
  - 然而若是已經推播最新版本 `yyy` 含有漏洞亦或問題，直接使用 `npm install` 會難以重現開發環境
- 雖然 `package-lock.json` 存有該次建構時的確切版本，但 `npm install` 會覆寫 `package-lock.json` 裡的版本紀錄
  - 若是需要以建構環境時的套件版本為主，需改用 `npm ci`，便會以 `package-lock.json` 為主要參照來源
- 想更新 `package-lock.json` 時則直接使用 `npm install` 或 `npm update`
- [Composer 與 NPM 指令 install 與 update 的差異｜ SoarLin's blog](https://soarlin.github.io/2017/04/21/Composer-NPM-install-update/)

## Gulp

- [Gulp](https://gulpjs.com/) 是一套任務管理工具（Task Manager）
- 可將工作流程自動化，例如自動重新整理網頁、編譯 SASS、檢查程式碼、壓縮 CSS 與 JavaScript 或圖片檔案等等
- 亦可自訂所需的處理內容

### 安裝

Gulp 運行於 node.js 底下，因此需先安裝 node.js 與 npm。

1. `npm install --global gulp-cli`：安裝 gulp-cli
2. 開啟需使用 gulp 的專案資料夾
3. `npm init`：初始化專案資料夾
4. `npm install --save-dev gulp`：安裝 gulp package
5. `gulp --version`：確認安裝的 gulp 版本

## Webpack

- [Webpack](https://webpack.js.org/) 是一套模組整合工具（Bundler）
- 可以打包零散的 JavaScript 模組，以及解決舊瀏覽器不支援新語法的問題，以利於後續管理與維護
- 亦可將各種靜態資源，例如 JavaScript 、CSS、SASS、圖片檔案視為模組，透過各種 loader 轉換與載入資源，最後由 webpack 打包、最佳化成為 JavaScript 檔

### 安裝

1. 開啟需使用 webpack 的專案資料夾
2. `npm init`：初始化專案資料夾
3. `npm install --save-dev webpack webpack-cli`：安裝 webpack package

- [いちばんやさしい webpack 入門](https://zenn.dev/sprout2000/articles/9d026d3d9e0e8f)
- [やっぱり webpack がわからない（エピソード 1）](https://zenn.dev/antez/articles/58307946cf4f3e)

## Docker

Docker 的出現，是為了解決在 deploy 作業途中時會出現的各種問題。

### Deploy 的歷史

早前的網路環境（約莫至 1990 年左右）是以一台大型電腦做為伺服器，處理所有的 request，但是這樣的設計會受限於製造商的品牌硬體，造成高成本、欠缺柔軟性和擴充性的問題。

之後技術進步，隨著小型電腦的性能提升與價格下降，出現了串接多台小型電腦，設置分散系統與功能的構築手法，這種手法稱為 Engine downsizing，成為了當時的主流作法，但這波變化又帶來了新的問題。

#### 虛擬化

首先不難想像的是，隨著電腦增加造成管理與使用上的困難，有 100 台電腦，就需要進行 100 次的環境設定，若之後有更新，也要 100 台電腦全部都裝過一遍，並且這些電腦不會經常保持滿載處理，而是總會有閒置中的電腦。

在安全性與維護性上也有所疑慮，當其中一台電腦受到攻擊，就會影響到所有在上面執行的程式。

以及隨著作業系統的多樣化，會有程式無法在不相容的伺服器上執行，這時出現了「虛擬化」，透過軟體來整合多種硬體，能夠自由模擬各種規格的電腦環境。

雖然虛擬化以及虛擬機器的登場，解決了許多 deploy 時會遇到的問題，但虛擬機器也有其弱點，那就是在系統背後執行的，其它與程式無關的系統服務，會造成大量的系統開銷與資源浪費。

#### 容器（Container）虛擬化

於是「容器虛擬化」誕生了。容器虛擬化指的是，把執行的程式從開發與執行環境隔離開來，如此能夠安全並且快速地執行多個程式。並且這套技術不需要安裝新的作業系統，而是透過系統裡的多個功能，讓應用程式在同一個作業系統上，但執行於不同的容器隔離空間中。

#### Docker 的出現

Docker 就是使用了容器虛擬化概念的應用程式之一，另外也有許多其它使用容器虛擬化的應用程式。

Docker 以名為 `Dockerfile` 的檔案為基礎來產生容器（執行程式），Docker 會依照檔案內所記載的，依序執行指令。因此擁有 1. 能夠簡單多次產生容器 2. 能夠將容器帶著走 3. 能夠簡便管理應用程式的版本 等等許多優點。

原本 Docker 是 LinuxOS 專用的功能，之後 macOS 和 Windows 上面也有了如 `Docker Desktop for Mac` 或 `Docker for Windows` 這類先於電腦上執行 Linux 環境的虛擬機器，再於其中執行 Docker 的應用程式。

### 安裝

#### A. MAC、Windows

目前在 MAC 和 Windows 上面也可以使用 docker，從官方網站 [Docker Desktop for Mac and Windows](https://www.docker.com/products/docker-desktop) 裡下載並安裝之後，在 terminal 裡輸入 `docker --version` 和 `docker-compose --version` 有出現版本號，就代表安裝成功。

Windows 版會推薦先安裝 WSL2（Windows Subsystem for Linux，於 Windows 上執行的 Linux 子系統），之後再安裝 docker，可以參照下列流程。

##### 1. 啟用虛擬機器平台

1. 開啟控制台（control panel）
2. 開啟「程式集」
3. 開啟「開啟或關閉 Windows 功能」
4. 勾選「虛擬機器平台」

##### 2. 安裝 WSL2

1. 以管理者權限開啟 PowerShell
2. 執行指令 `dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart`
3. 從微軟官方網站[下載 WSL2 Linux 核心更新套件](https://docs.microsoft.com/zh-tw/windows/wsl/wsl2-kernel)
4. 從 MicrosoftStore 安裝 Ubuntu 18.04LTS

##### 3. 安裝 Docker Desktop

從官方網站 [Docker Desktop for Mac and Windows](https://www.docker.com/products/docker-desktop) 裡下載並安裝 Docker Desktop。

#### B. Linux

- 移除舊版本：`sudo apt-get remove docker docker-engine docker.io`
- 使用腳本安裝：`curl -fsSL https://get.docker.com -o get-docker.sh`
  <br>`sudo sh get-docker.sh`
- 若想使用非 root 使用者執行 docker，可將此使用者加至 `docker` 身份組中
- `sudo usermod -aG docker your-user`

### 使用

- `docker images`：查看 images
- `docker run`：執行 images
- `docker ps`：查看執行中的 container
- `top`、`htop`、`ctop`、`gtop`、`conky`：監看工具

#### 撰寫 Dockerfile

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

- Image
- Dockerfile
- Docker Compose

### 參考資料

- [いまさらだけど Docker に入門したので分かりやすくまとめてみた - Qiita](https://qiita.com/gold-kou/items/44860fbda1a34a001fc1)
- [Docker を体系的に学べる公式チュートリアル和訳 - Qiita](https://qiita.com/Michinosuke/items/5778e0d9e9c04038903c)
- [【図解】Docker の全体像を理解する -前編-](https://qiita.com/etaroid/items/b1024c7d200a75b992fc)
- [「Docker」を全く知らない人のために「Docker」の魅力を伝えるための「Docker」入門](https://qiita.com/bremen/items/4604f530fe25786240db)
- [Docker を体系的に学び直してみた(導入編)](https://qiita.com/takuya_tsurumi/items/182d2de3f3ce7bb63edb)
- [Docker で立ち上げた開発環境を VS Code で開く!](https://qiita.com/yoskeoka/items/01c52c069123e0298660)
- [VPN と Docker を併用する - flyhigh](https://shinpei.github.io/blog/2014/11/11/how-to-vpn-and-docker-live-along)
- [GitHub - jim60105/docker-V2Ray: V2Ray on Docker (Docker Compose)](https://github.com/jim60105/docker-V2Ray)
- [軽量 Docker イメージに安易に Alpine を使うのはやめたほうがいいという話 - inductor's blog](https://blog.inductor.me/entry/alpine-not-recommended)
- [初心者が絵で理解する Docker](https://zenn.dev/suzuki_hoge/books/2021-04-docker-picture-60fbe950136be9c7ad85)
- [Docker 完全に理解した | IIJ Engineers Blog](https://eng-blog.iij.ad.jp/archives/12414)

## Parcel

Compiler／Bundler

## Vite
