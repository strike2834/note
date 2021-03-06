# Git

## Git 簡介

- Git 是由 Linus Torvalds 為了管理 Linux 原始碼所寫的分散式版控系統
- 有三種檔案區域，並透過指令將檔案移至不同的區域

1. 「工作目錄（Working Directory）」
2. 「暫存區（Staging Area）」
3. 「儲存庫（Repository）」

- 有四種 File State 檔案狀態

1. `Untracked` 新增檔案
2. `New`: 加入暫存區後
3. `Modified`: 修改後
4. `Deleted`: 刪除後

## How does Git works？

- [たぶんもう怖くない Git ～ Git 内部の仕組み～](https://qiita.com/marchin_1989/items/2ec01553e907f3a9e6bb)
- Git 的 Repo 由 Git 物件構成，透過有向無環圖與標籤管理履歷。
- 提交 commit 並不是儲存差異，而是**快照（Snapshot）**。
- Git 的指令實質上是在處理有向無環圖上的 Git 物件增減，以及標籤的移動。

## What is GitHub？

與 Git 一同很常聽到的，還有 GitHub 與 GitLab，這兩者則是提供 Git 服務的網路平台，除了可將程式碼儲存於上頭外，也有獨自額外的輔助功能，例如 Pull Request（後述）或是 GitHub Actions 等等。

## 工具安裝

- [Git Client](https://git-scm.com/downloads)
- [gitignore.io](https://www.gitignore.io/)

### VSCode 插件

- [GitLens](https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens)
- [Git History](https://marketplace.visualstudio.com/items?itemName=donjayamanne.githistory)
- [Github Pull Request](https://marketplace.visualstudio.com/items?itemName=GitHub.vscode-pull-request-github)
- [gitignore](https://marketplace.visualstudio.com/items?itemName=codezombiech.gitignore)
- [Git Project Manager](https://marketplace.visualstudio.com/items?itemName=felipecaputo.git-project-manager)

### 平台服務

- [GitHub](https://github.com/)
- [GitLab](https://gitlab.com/)

### 指令速見表

- [Git でよく使われるコマンドにイラストによる説明を加えて 1 枚のチートシートにまとめてみた](https://qiita.com/kozzy/items/b42ba59a8bac190a16ab)
- [Git Cheatsheet Cht](http://scars377.github.io/git-cheatsheet-cht/)

## 指令

- [Learn Git Branching](https://learngitbranching.js.org/?locale=zh_TW)
- [Git でのバージョン コントロールの概要](https://docs.microsoft.com/ja-jp/learn/paths/intro-to-vc-git/)
- [GitHub の基礎 - 管理の基本と製品の機能。](https://docs.microsoft.com/ja-jp/learn/paths/github-administration-products/)
- [Git 的奇技淫巧](https://github.com/521xueweihan/git-tips)

### 初始

#### 1. `git config`

- 建構 Git 相關設定
  - `git config --global user.name ""`<br/>
    設定使用者名稱
  - `git config --global user.email ""`<br/>
    設定使用者帳號
  - `git config --global -l`<br/>
    查看目前的設定內容
    - `-l` 為 `--list` 的簡碼
    - 亦可參照根目錄底下的 `.gitconfig` 檔
  - `--local` 參數套用於單獨 project 上時會優於 `--global`
  - `git config --global --edit`<br/>
    編輯全域設定

#### 2. `git init`

- 建立 local repository
- 在該工作目錄建立 `.git` 資料夾，開始使用 Git 做版控

#### 3. `git remote`

- 查看／註冊遠端數據庫 remote repository 的設定
  - `git remote -v`
    <br/>顯示遠端 repo 連結
  - `git remote add [remote_name] [git_url]`
    <br/>新增遠端 repo
    <br/>e.g. `git remote add origin http://github.com/f6bfb5/Sample.git`
  - `origin`、`upstream` 為常見的遠端數據庫名稱別名，亦可更改為其它名稱
    <br/>遠端 repo 會以 `[remote_name]/[branch]` 的格式顯示
    <br/>此例下 Remote Repository 的 master 分支就會是 `origin/master`
  - `git remote set-url origin git://new.url.here`
    <br/>修改 remote 位置
  - `git remote remove origin`
    <br/>刪除 remote
  - `git push -u origin master`
    <br/>更新資料至遠端 master 分支
    <br/>`-u` 等同於 `--set-upstream`
    <br/>意為將此遠端數據庫服務設為追蹤指定的遠端分支

### 設定

#### 1. `git config`

- 建構 Git 相關設定
- proxy 設定
  - `git config --global http.proxy http://[FQDN]:[PORT]`
  - `git config --global https.proxy http://proxy.example.com:8080`
  - e.g.
    <br/>`git config --global http.proxy http://[ID]:[Password]@[FQDN]:[PORT]`
    <br/>`git config --global https.proxy http://[ID]:[Password]@[FQDN]:[PORT]`
  - `git config --global url."https://".insteadOf git://`
- 內容設定
  - `git config --global core.autocrlf false`
    <br/>將 Windows 環境的換行代碼轉換為 CR+LF
  - `git config --global alias.[alias_command] [git_command]`
    <br/>設定指令快捷
    - e.g. `git config --global alias.co checkout`
    - co=checkout, br=branch, ci=commit, st=status
    - 若想執行外部指令，而非 git 底下的指令，
      <br/>需要在指令的開頭加上 `!` 字元
      <br/>e.g. `git config --global alias.visual '!gitk'`
- [Git productivity with aliasing and multiple commands](https://bardoloi.com/blog/2015/10/29/git-aliases/)
- [[git] gitconfig で会社用アカウントと個人用アカウントを楽に使い分けする](https://qiita.com/SugarShootingStar/items/64f239f89d25a3b9f520)

### 提交

#### 1. `git add`

- 將 Working Repository 的檔案變更儲存至 Staging Area
  - `git add .`
    <br/>將該目錄及其子目錄下所有異動放入暫存區
  - `git add --all`
    <br/>將整個 Git 版控範圍異動放入暫存區

#### 2. `git commit`

- 將檔案從 Staging Area（暫存區） commit 到 Local Repository（本地儲存庫）
  <br>需要使用 `-m` 參數記述備註，並會分配一個 commit ID
  - `git commit -m "Commit 說明"`
  - `git commit --amend -m "修改後的 Commit 訊息"`
    <br/>修改最後一次 Commit 訊息
    <br/>（實則是撤掉前一次 Commit 重發一次，SHA1 不同）
  - `git commit -am "commit message"`
    <br/>commit 已跟蹤過的文件

#### 3. `git push`

- 將 Local Repository 本地儲存庫的異動 commit 到 Remote Repository 遠端儲存庫
  - `git push [remote_repo] [local_branch]`
    <br/>e.g. `git push origin master`
  - `git push [remote_repo] [source_branch]:[destination_branch]`
    <br/>推送至不同的 branch

#### 4. `git rm [filename] --cached`

- 將檔案轉為 untracked，即 stop tracking

### 狀態

#### 1. `git status`

- 查看目前的變更狀態
  - `Untracked files:`
    <br/>不存在 Local Repository 和 Staging Area，
    <br/>只存在 Working Directory 裡的檔案
  - `Changes not staged for commit:`
    <br/>之前已存在於 Local Repository 和 Staging Area 裡的檔案
  - `Changes to be commited`

#### 2. `git diff [file_name]`

- 比較 Staging Area 和 Local Repository 的檔案內容差異
  - `git diff [branch_name] [branch_name]`
    <br/>比較兩者 branch 之間的差異
  - `git diff master origin/master`

#### 3. `git log`

- 檢視提交歷史紀錄，從上至下由新到舊
  - `git log --all --decorate --oneline --graph`
    <br/>圖形化展示歷史紀錄
  - `git config --global alias.dog log --all --decorate --oneline --graph`

#### 4. `git reflog`

- 檢視詳細提交紀錄
- 可以查看 reset 歷程，找到（可能因為失誤）被拆掉的 commit
- [Git を使ってやらかした時、git reflog さえ使えればわりかしなんとかなる](https://qiita.com/getty104/items/cfd98f5f0ea89ef07bf0)

#### 5. `git show [commit_id]`

- 檢視提交紀錄內容

#### 6. `git tag [tag_name] [commit_id]`

- 設定錨定點

#### 7. `git describe [ref]`

- `ref` 可為 `branch` 或 `commit-id`
- 尋找 `ref` 最近的錨定點
- 若未指定 `ref` 會以當前位置（`HEAD`）為準

### 分支

#### 1. `git branch`

- 顯示分支一覽，當前分支的前方會有 `*`
  - `git branch [branch_name]`
    <br/>建立新的分支
  - `git branch -d [branch_name]`
    <br/>刪除本地端的分支
  - `git branch -r`
    <br/>查看遠端 repo 的分支
  - `git branch -a`
    <br/>查看所有分支
  - `git branch [branch_name]/[revision]`
    <br/>切換至指定分支的特定版本
  - `git branch -f main HEAD^3`
  - `git branch -u [remote_branch] [local_branch]`
    <br/>`git branch -u o/main foo`
    <br/>已經位於該本地分支則可省略 `[local_branch]`

#### 2. `git push [remote_repo] :[branch_name]`

- 刪除遠端的分支
- ※在欲刪除的遠端分支名稱前有個 `:`、使用的指令是 `push`

#### 3. `git checkout [branch_name]`

- 切換至指定的分支
  <br>Working Directory 也會變更成指定的分支狀態
  - `git checkout -b [branch_name]`
    <br/>建立新的分支，並切換至該分支
  - `git checkout [branch_name] .`
    <br/>將當前分支的所有檔案複製至指定分支（※在最後方有一個 `.`）
- `checkout` 也可以用於切換至不同的 HEAD
  - HEAD：指向當前 checkout 的 commit 的 reference，即目前所在的 commit
  - `git checkout [commit SHA-1]`
    <br/>由於 SHA-1 通常很長，也可以只輸入前幾個字元
  - `git checkout main^`
    <br/>切換至 main 的上個版本
    - `^` 代表前一個版本，`~5` 則代表 5 個之前的版本
    - 如果有多個母分支（如 merge 過後），可用 `^2` 指定
    - `^` 和 `~` 可以組合使用，如 `git checkout HEAD~^2~2`
  - `git checkout HEAD^`
    <br/>也可將 `HEAD` 用於相對引用
- 兩者也可組合，建立新的分支並將分支指向某個 HEAD
  - `git checkout -b [branch_name] [commit SHA-1]`
    <br/>e.g. `git checkout -b feature C2`
    <br/>建立 feature 分支並切換至該分支，之後再將分支 HEAD 指向 C2
  - `git checkout -b [local_branch] [remote_branch]`
    <br/>也可以用來指向不同的 remote branch
    <br/>e.g. `git checkout -b totallyNotMain o/main`

#### 4. `git stash [save ['message]]`

- 暫時儲存目前變更的內容，但不進行 commit
- 預設省略 `save`，亦可加上以註記 `stash` 的內容為何
- 通常用於需跳至其他 branch 時
  - `git stash apply [stash@{n}]`
  - `git stash pop [stash@{n}]`
    <br/>復原保存於 `stash` 的作業內容
- 可於參數指定想回復何次的 `stash`，省略時預設為最新的 `stash@{0}`
- `apply` 復原後不會取消 `stash`，`pop` 復原後會取消 `stash`
  - `git stash show [stash@{n}]`
    <br/>顯示指定的 `stash` 內容
  - `git stash list`
    <br/>顯示目前儲存的 `stash` 一覽
  - `git stash drop [stash@{n}]`
    <br/>刪除指定的 `stash`
  - `git stash clear`
    <br/>刪除所有 `stash`

### 合併

#### 1. `git merge [branch_name]`

- 將 `指定分支` 的檔案修改合併至 `當前分支`
  <br>合併兩個分支操作，紀錄兩者之間的實際操作
  <br>預設時使用 `fast-forward` 方式合併，不會產生新的 commit
  - `git merge [branch] --no-ff`
    <br/>合併時產生新的 commit，用以確保主要分支線圖乾淨
  - `git merge [branch] --squash`
    <br/>合併後僅保留一次 commit 紀錄
  - `git merge [remote_resository]/[branch_name]`
    <br>將從 `git fetch` 取得的 Remote Repository 的變更
    <br>反應至 Local Repository 裡目前的 branch

#### 2. `git rebase [target_branch]`

- 複製當前分支做的修改，到目標分支的最後一次提交上面
  <br>會將指定分支的歷史紀錄併進 master 的線圖上，用以確保整體分支線圖乾淨
- 即把當前 branch 的 HEAD 修改為指定 branch 的（無參數的情況下）最後一個 commit
- 由於這個動作過程會再做一次 commit，也會改變目標分支的 commit id，需謹慎使用
- `git rebase -i HEAD~4`
  - 開啟互動式編輯視窗（Interactive 模式）
- `git rebase caption main`
  - 等同於 `git checkout main` -> `git rebase caption`？
- [git merge 與 rebase 的觀念與實務應用](https://www.slideshare.net/WillHuangTW/git-merge-rebase)
- [rebase をちゃんと理解して使えるようになろう！](https://qiita.com/shira-shun/items/29c7f36179117022cb6d)
- [Git Rebase: Don't be Afraid of the Force (Push) - Gerald Versluis](https://blog.verslu.is/git/git-rebase/)
  - `git rebase -i origin/master`
  - `git rebase --abort`

#### 3. `git cherry-pick [commit_id]`

- 任意挑選一個或多個 commit 複製並接到目前位置（`HEAD`）的下面
- 可以避免 rebase 操作過多時可能的 rebase conflict

#### 4. `git clone [git_url]`

- 複製 `遠端 repo` 至本地端
  - `git clone --mirror`
  - `cd C:\Git\GitHub`
  - `git clone https://github.com/f6bfb5/Sample.git`
    <br/>clone 遠端工作目錄至本地端

#### 5. `git fetch`

- 將 `遠端 repo` 的最新變更加入至 `本地 repo`
  - `git fetch --prune`
    <br/>執行 fetch 之前，刪除遠端庫裡不存在的 repo
  - 但 `fetch` 不會更動本地的 commit
- `fetch` 也可以指定抓取特定 branch 的變更
  - `git fetch origin foo`
  - 同樣的，`fetch` 不會更動本地的 commit
  - 也可與 `pull` 同樣透過 `:` 指定特定本地 branch
    - `git fetch [remote_repo] [remote_branch]:[local_branch]`
      <br/>e.g. `git fetch origin foo~1:bar`
      <br/>將遠端 foo branch 到前一次的 commit 內容 fetch 至 bar branch
- `git push [remote_repo] :[branch_name]` 會刪除遠端 branch
  - 同樣地，`git fetch [remote_repo] :[branch_name]` 則會增加一個本地 branch

#### 6. `git pull`

- 將 `遠端 repo` 的最新變更加入至 `本地 repo` 後，合併本地 commit
- 等同 `git fetch` + `git merge origin/master`
- `git pull --rebase`<br/>
  加上 `--rebase` 則等同 `git fetch` + `git rebase`
- `git pull [remote_repo] [branch_name]`
  - = `git fetch [remote_repo] [branch_name]: git merge o/[branch_name]`

#### 衝突

- `git mergetool`<br/>
  開啟編輯工具，介面左邊為當前分支，右邊為目標分支，中間為原始檔案

### 撤銷

#### 1. `git clean`

#### 2. `git rm [file_name]`

#### 3. `git commit --amend -m "commit message"`

- 撤掉前一次 commit 重發一次，SHA1 會不同
  - `git commit --amend --no-edit`<br/>
    沿用原 commit 訊息

#### 4. `git reset [commit_id]`

- 完全撤銷修改至某次 commit<br/>
  若省略 `[commit_id]` 則會自動指定為 `HEAD`
  - `git reset --hard HEAD^`<br/>
    還原至前個版本
  - `^` 代表前一個版本，`~5` 則代表 5 個之前的版本<br/>
    `--soft`：保留暫存區和工作區的檔案<br/>
    `--mixed`：捨棄所有暫存區的檔案，但不影響工作區的檔案<br/>
    `--hard`：捨棄暫存區和工作區的檔案
- 對 remote branch 無效，需使用 `revert`

#### 5. `git revert [commit_id]`

- 撤銷某次 commit，但保留此次之前和之後的 commit 與紀錄
- 此次撤銷會成為一次最新的 commit，以修改 remote branch

## 不想版控的項目

建立／編輯 `.gitignore` 檔案列舉排除不要納入版控的路徑（支援萬用字元 `*`）

```.gitignore
# 不加入副檔名為 .exe 的檔案
*.exe
# 不加入 .settings 資料夾與其中的檔案
.settings/
# 不加入 Bin/bin 資料夾與其中的檔案
[Bb]in/
# 不加入特定資料夾裡的特定副檔名檔案
out/*.log

*.sh
```

在修改 .gitignore 前就加入的項目可用 `git rm --cached` 清除，
或用 `git clean -fx` 一口氣清理所有應忽略的檔案

## GitHub

### Pull Request（PR）

`Pull Request` 和 `fork` 同樣是 Github／Bitbucket 上新增的整合功能
<br>而 `fork` 是將**他人的**遠端 repo 複製至自己的**遠端 repo**
<br>以便做出個人版本的內容修改
<br>不同於 `clone` 是將**自己的**遠端 repo 複製至**本地端**

- PR 指發出一個請求他人 `merge` 自己在 `fork` 後做的相關修改內容
- 過程為：

1. `fork` 專案到自己帳號
2. `clone` 到本地修改
3. `push` 回自己帳號專案
4. 發出 PR 給原作者
5. 原作者收下 PR

- [與其它開發者的互動 - 使用 Pull Request（PR） - 為你自己學 Git | 高見龍](https://gitbook.tw/chapters/github/pull-request.html)

### 切換多個帳號 - VSCode 插件法

- [I have 2 GitHub accounts. How can I use both when I am working in VS Code?](https://stackoverflow.com/questions/62625513/i-have-2-github-accounts-how-can-i-use-both-when-i-am-working-in-vs-code)

#### 1. 安裝插件

- [GitHub Pull Requests and Issues](https://marketplace.visualstudio.com/items?itemName=GitHub.vscode-pull-request-github)
  - 自動化登入 GitHub
- [git-autoconfig](https://marketplace.visualstudio.com/items?itemName=shyykoserhiy.git-autoconfig)

  - 依據開啟專案自動詢問並設定 Git
  - 也可以 `F1` -> `Set Config` 手動更改
  - 於 `settings.json` 裡可以新增預設設定

  ```json
    /**
     * @file "settings.json"
     * @desc "This is what my configuration looks like" */

    "git-autoconfig.configList": [
      {
        "user.email": "ex1@example.com",
        "user.name": "example1"
      },
      {
        "user.email": "ex2@example.com",
        "user.name": "example2"
      }
    ]
  ```

### 切換多個帳號 - 系統認證法

- [Windows で会社用と個人用の GitHub アカウントを Https を使って簡単に切り替える方法を丁寧に説明する。](https://zenn.dev/longbridge/articles/a91089c30851ff)

#### 1. 申請 personal access token

由於 GitHub 已經不再支援使用密碼認證，需改為申請 [personal access token](https://github.com/settings/tokens) 完成認證，勾選 `repo` 與其餘需要的功能。

#### 2. 確認目前設定狀況

1. 檢查目前設定
  - `git config --global --list`
2. 設定主要帳號
  - `git config --global user.name "用戶名"`
  - `git config --global user.email email` 
3. 設定以系統認證管理員儲存認證
  - `git config --global credential.helper wincred`
4. （可跳過？）開啟「認證管理員（Credential Manager）」
  - 選擇「Windows 認證」，刪除之前的 GitHub 認證資料（`git:https://github.com`）
5. 嘗試 push 會彈出帳號密碼登入視窗，跳過該視窗
  - 於之後 VSCode 上方出現的密碼輸入框內，貼上申請的主帳號 personal access token

#### 3. 設定副帳號

1. 移動錨點至副帳號管理用的 git 資料夾
2. 初始化及設定遠端 repo 
  - `git init`
  - `git remote add origin https://github.com/[subusername]/[subuserrepo].git`（可跳過？）
3. 檢查目前設定
  - `git config --local --list` 
4. 設定次要帳號
  - `git config --local user.name "用戶名"`
  - `git config --local user.email email` 
5. 設定以系統認證管理員儲存認證
  - `git config --local credential.helper wincred`
6. 修改遠端 repo
  -  `git remote set-url origin https://[subusername]@github.com/[subusername]/[subuserrepo].git`
7. 嘗試 push 會彈出帳號密碼登入視窗，跳過該視窗
  - 於之後 VSCode 上方出現的密碼輸入框內，貼上申請的副帳號 personal access token

#### 4. 如果失敗…

如果 push 後失敗且沒有再跳出密碼輸入框，直接開啟「認證管理員」，選擇「Windows 認證」並「新增一般認證」，主帳號的「網際網路或網路位址」輸入 `git:https://github.com`，密碼輸入主帳號的 personal access token，副帳號的「網際網路或網路位址」輸入 `git:https://[subusername]@github.com`，其餘同文。

### 切換多個帳號 - Access Token 法

#### 1. 申請 personal access token

由於 GitHub 已經不再支援使用密碼認證，需改為申請 [personal access token](https://github.com/settings/tokens) 完成認證，勾選 `repo` 與其餘需要的功能。

#### 2. 於 remote url 加上 access token

`git remote set-url origin https://username:token@github.com/username/repository.git`

### 移除 GitHub 上的敏感資料

- [GitHub 上の sensitive data を削除するための手順と道のり](https://engineering.mercari.com/blog/entry/20211207-removing-sensitive-data-from-github/)

### GitHub Actions

- [Check! GitHub Actions で導入しておきたい自動化 5 つ（GitHub ブログ要約）](https://zenn.dev/dzeyelid/articles/77541fe1336951)
- [GitHub Actions における Step/Job/Workflow 設計論](https://zenn.dev/hsaki/articles/github-actions-component)
- [GitHub Actions 逆引きリファレンス](https://gkzz.dev/posts/github-actions-tips/)

## Branch Model

### git-flow

由 Driessen 所[發表](http://keijinsonyaban.blogspot.com/2010/10/a-successful-git-branching-model.html)的一種 git 開發手法，亦或指遵循這套手法所開發的工具
<br>將專案分為 5 種分支：`master`、`develop`、`release`、`feature`、`hotfix`

#### 主要分支：`master`、`develop`

- `master` 分支
  - 品質穩定保證可上線的產品主線，多會加上版號 `release/1.0`
  - 從 `release` 分支 merge 而來，不可於此分支直接進行作業或 commit
- `develop` 分支
  - 最新進度的開發主線
  - 自 `master` 分支而來，`feature` 由此分支出去，改好再 merge 進來

#### 輔助分支：`feature`、`release`、`hotfix`

- `release` 分支
  - 開發進度成熟時，分支到 `release` 做上線前的最後測試
  - 測試沒問題後 merge 至 `master` 及 `develop`，merge 完畢後會刪除該 `release` 分支
- `feature` 分支
  - 進行功能追加或修正作業用的分支
  - 自 `develop` 分支而來
  - 通常會將實作功能寫在 `feature/` 的後方明確化內容，例如 `feature/news_feed`
  - 作業完成後再 merge（可再加上 [`--no-ff`](https://medium.com/@fcamel/%E4%BD%95%E6%99%82%E8%A9%B2%E7%94%A8-git-merge-no-ff-d765c3a6bef5) option 明確化結構）回 `develop` 分支
- `Hotfix` 分支
  - 緊急修正內容用
  - 從 `master` 分支出來，改完合併回 `master` 及 `develop`

#### 相關文章

- [Git Workflows and Tutorials](https://github.com/xirong/my-git/blob/master/git-workflow-tutorial.md)
- [Git 怎麼這麼難用？Git Flow + 好習慣 = 不再苦惱](https://medium.com/kuma%E8%80%81%E5%B8%AB%E7%9A%84%E8%BB%9F%E9%AB%94%E5%B7%A5%E7%A8%8B%E6%95%99%E5%AE%A4/%E5%9F%BA%E7%A4%8E-git-flow-%E5%B7%A5%E4%BD%9C%E6%B3%95-fa50b1dddc4f)
- [git flow 實戰經驗談 part1 - 別再讓 gitflow 拖累團隊的開發速度](https://blog.hellojcc.tw/2017/12/14/the-flaw-of-git-flow/)
- [git-flow 図解](https://qiita.com/ohnaka0410/items/7c7fa20710dfd72b7d7a)

### GitHub Flow

簡略化過後的 Branch Model
<br>將專案分為 2 種分支：`master`、`topic`

#### `master` 分支

- 品質穩定保證可上線的產品主線
- 等同於 git-flow 中的 `master` + `develop`
- 不可於此分支直接進行作業或 commit

#### `topic` 分支

- 進行功能追加或修正作業用的分支
- 自 `master` 唯一分支出來的 branch
- 等同於 git-flow 中的 `feature` + `hotfix`
- merge 回 `master` 後會刪除該 `topic` 分支

## commit message

- 風格：Markup syntax、wrap margins、文法、大寫習慣、符號慣例
- 內容：**需要**的資訊
- Metadata：可參照的 issue tracking IDs、pull request 號碼

### 七條規則

1. 用一行空白分隔標題與內容
2. 限制標題最多只有 50 字元
3. 標題開頭要大寫
4. 標題不以句點結尾
5. 以祈使句撰寫標題
6. 內文每行最多 72 字
7. 用內文解釋 what 以及 why vs. how

### template

```
Header: <type>(<scope>): <subject>
 - type: 代表 commit 的類別：feat, fix, docs, style, refactor, test, chore，必要欄位
 - scope 代表 commit 影響的範圍，例如資料庫、控制層、模板層等等，視專案不同決定，可選欄位
 - subject 代表此 commit 的簡短描述，不要超過 50 個字元，結尾不要加句號，必要欄位

Body: 72-character wrapped. This should answer:
 - Body 部份是對本次 Commit 的詳細描述，可以分成多行，每一行不要超過 72 個字元
 - 說明程式碼變動的項目與原因，還有與先前行為的對比

Footer:
 - 填寫任務編號（如果有的話）.
 - BREAKING CHANGE（可忽略），記錄不兼容的變動，
   以 BREAKING CHANGE: 開頭，後面是對變動的描述、以及變動原因和遷移方法
```

#### type

- Feat: 新增／修改功能（feature）
- Fix: 修補 bug（bug fix）
- Docs: 文件（documentation）
- Style: 格式（不影響程式碼運行的變動 white-space, formatting, missing semt colons, etc）
- Refactor: 重構（非新增功能，亦不是修補 bug 的程式碼變動）
- Perf: 改善效能（A code change that improves performance）
- Test: 增加測試（Adding missing tests or correcting existing tests）
- chore: 程式建構或輔助工具變動（maintain）
- revert: 撤銷回覆先前的 commit，例如：`revert: type(scope): subject (回覆版本:xxxx)`

### 工具

- [commitizen/cz-cli: The commitizen command line utility.](https://github.com/commitizen/cz-cli)
- `yarn global add commitizen` or `npm install -g commitizen`

### 相關文章

- [Write your commit messages in the right way](https://medium.com/@kevin940726/write-your-commit-messages-in-the-right-way-65c8e1dfc8a3)
- [如何寫一個 Git Commit Message](https://blog.louie.lu/2017/03/21/%E5%A6%82%E4%BD%95%E5%AF%AB%E4%B8%80%E5%80%8B-git-commit-message/)
- [Git Commit Message 這樣寫會更好，替專案引入規範與範例](https://wadehuanglearning.blogspot.com/2019/05/commit-commit-commit-why-what-commit.html)
- [撰寫有效的 Git Commit Message](http://blog.fourdesire.com/2018/07/03/%E6%92%B0%E5%AF%AB%E6%9C%89%E6%95%88%E7%9A%84-git-commit-message/)
- [レビュー前に直して欲しい日本語の問題点８つ](https://qiita.com/tonluqclml/items/bc63c294dda6010b63e9)
- [Git のコミットメッセージの書き方](https://qiita.com/itosho/items/9565c6ad2ffc24c09364)
- [如何維護更新日誌](https://keepachangelog.com/zh-TW/1.0.0/)

## 參考文章

- [Git でやりたいこと、ここで見つかる](https://qiita.com/shimotaroo/items/b73d896ace10894fd290)
- [Git 入門](https://pepese.github.io/blog/git-basics/)
- [Git コマンド整理](https://pepese.github.io/blog/git-commands/)
- [zlargon - Git](https://zlargon.gitbooks.io/git-tutorial/content/)
- [30 天精通 Git 版本控管](https://github.com/doggy8088/Learn-Git-in-30-days/tree/master/zh-tw)
- [我的 Git 指令小抄](https://blog.darkthread.net/blog/my-git-cheatsheet/)
- [[筆記]learning-Git-2019](https://medium.com/ashes-note/%E3%84%85-learning-git-2019-cd0a71e061ff)
- [いまさらだけど Git を基本から分かりやすくまとめてみた](https://qiita.com/gold-kou/items/7f6a3b46e2781b0dd4a0)
- [新人ではないが Git 初心者であるエンジニアが「このリポジトリをフォークしてローカルで開発できるようにしておいて！」と言われた時にやること](https://qiita.com/sky0621/items/8b6e88f4327b42ade5d7)
- [入門書を終えた人に捧げる、社会人のための Git 中級編](https://qiita.com/yamamoto7/items/fe15a1e7e360b4015fae)
- [実務でどんな git コマンドを使っているか振り返ってみる](https://qiita.com/west-hiroaki/items/74cccbc22b2cc7a4aacb)
- [Git でやらかした時に使える 19 個の奥義](https://qiita.com/muran001/items/dea2bbbaea1260098051)
- [【狀況題】怎麼刪除遠端的分支？](https://gitbook.tw/chapters/github/delete-remote-branch.html)
- [【狀況題】剛才的 Commit 後悔了，想要拆掉重做…](https://gitbook.tw/chapters/using-git/reset-commit.html)
- [git 操作は GUI ツール派な自分も CUI に乗り換えた便利 git 拡張まとめ](https://qiita.com/yukiarrr/items/9c21d97f6c8ac31de157)
- [GitHub でセキュリティ脆弱性のアラートが来てビビりながら対応した話](https://qiita.com/Nash-BETA/items/0d4e876cf9460778b985)
- [Git の使い方(応用編) · kaityo256/github](https://github.com/kaityo256/github/blob/main/advanced/README.md)
