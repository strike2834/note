# Linux note

## Windows Subsystem

### Basic setup

- Installation:
  - `wsl --install`
  - [安裝 WSL | Microsoft Docs](https://docs.microsoft.com/zh-tw/windows/wsl/install)
  - [Ubuntu - Microsoft Store 應用程式](https://apps.microsoft.com/store/detail/ubuntu/9PDXGNCFSCZV?hl=zh-tw&gl=TW)
- Launch:
  - `bash`
  - `wsl`
- Update System:
  - `sudo apt-get update -y`
  - `sudo apt-get upgrade -y`
- List installed shell: `cat /etc/shells`
- List installed pkg:

### Change config of shell

#### zsh

- Install zsh: `sudo apt-get install zsh -y`
- Install zsh framework:
  - zim: `curl -fsSL https://raw.githubusercontent.com/zimfw/install/master/install.zsh | zsh`
  - oh-my-zsh: `sh -c "$(wget https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"`
  - uninstall oh-my-zsh: `uninstall_oh_my_zsh`
- Set zsh as default shell: `chsh -s $(which zsh)`
  - or: `chsh -s /bin/zsh`
- Set zsh theme:
  - [romkatv/powerlevel10k: A Zsh theme](https://github.com/romkatv/powerlevel10k)
- Zim: add `zmodule romkatv/powerlevel10k` in `~/.zimrc`
- Zsh plugins:
- Restart zsh: `exec zsh -l`
  - [Option -l of exec shell command](https://stackoverflow.com/questions/39972978/option-l-of-exec-shell-command)

#### fish

- [fish shell](https://fishshell.com/)

## TinyCore Linux

- [Contents](https://dywang.csie.cyut.edu.tw/dywang/linuxSystem/node1.html)
- [GNU/Linux Command-Line Tools Summary](https://tldp.org/LDP/GNU-Linux-Tools-Summary/html/index.html)
- [BASH Programming - Introduction HOW-TO](https://tldp.org/HOWTO/Bash-Prog-Intro-HOWTO.html)

### Default Settings

- acc: tc
- pwd: piCore
- [Chris Mccormick - Tiny Core Linux on Raspberry Pi](https://mccormick.cx/news/entries/tiny-core-linux-on-raspberry-pi)

### 基礎資料夾結構

| 資料夾   | 內容                                              |
| -------- | ------------------------------------------------- |
| `/`      | 根目錄                                            |
| `/bin`   | 基礎可執行的檔案與指令                            |
| `/boot`  | 啟動 OS 需要的檔案                                |
| `/dev`   | 裝置檔案                                          |
| `/etc`   | 系統設定檔案                                      |
| `/home`  | 各個使用者的根目錄                                |
| `/lib`   | 通用 library                                      |
| `/mnt`   | 檔案系統 mount point                              |
| `/media` | CD 或 DVD 的 mount point                          |
| `/opt`   | Addon app and data                                |
| `/proc`  | Information of kernal and process                 |
| `/root`  | root 使用者的根目錄                               |
| `/sbin`  | 系統管理者用的可執行檔案                          |
| `/srv`   | 系統關聯檔案                                      |
| `/tmp`   | 暫存檔案｜                                        |
| `/usr`   | 與使用者相關的檔案、library、文件與 kernal source |
| `/var`   | 郵件或紀錄等等的變動資料                          |

### 確認空間使用狀況

- `df`
- `fdisk -l`

#### 重新分割使用空間

- [Setting up TinyCore Linux on Raspberry Pi](https://chipnetics.com/tutorials/tinycore-raspberry-pi/)

```bash
sudo fdisk -u /dev/mmcblk0
# p -> 記下第二個分割區的起始與結束位置
# d -> 刪除第二個分割區
# n -> 選擇主要分割區，重新分配分割區大小
# w -> 儲存變更並離開

sudo reboot

resize2fs /dev/mmcblk0p2
```

### 儲存變更

- TinyCore 將檔案都 mount 於 RAM 上，且重開機就會清除檔案
- `filetool -b` 會儲存變更過的設定
- `sudo vi /opt/.filetool.lst` 可新增其他儲存路徑

### Install Repo

- `tce`
- [TCE Repository - Tiny Core Linux](http://distro.ibiblio.org/tinycorelinux/tce.html)

## Basic instruction

| 指令             | 內容         | 補充           |
| ---------------- | ------------ | -------------- |
| `mv`             | 移動檔案     | move           |
| `cp`             | 複製檔案     | copy           |
| `rm`             | 移除檔案     | remove         |
| `mkdir`          | 建立資料夾   | make directory |
| `rm -f [file]`   | 強制移除檔案 | force          |
| `rm -r [folder]` | 移除資料夾   | recursive      |

### System instruction

| 指令           | 內容                         | 補充 |
| -------------- | ---------------------------- | ---- |
| `top`          | 顯示系統所有執行中的程式     |      |
| `ps`           | 顯示使用者所有執行中的程式   |      |
| `ps -a`        | 顯示系統所有執行中的程式     |      |
| `kill [id]`    | 關閉執行中的程式             |      |
| `pkill [name]` | 關閉名稱包含 `[name]` 的程式 |      |
| `clear`        | 清除畫面                     |      |
| `history`      | 顯示執行過的指令             |      |

- `ip`
- `ss`
- `scp`
- `sshfs`
- `curl`
- `tail`
- `split`
- `sed`
- `grep`
- `pgrep`
- `awk`
- `xargs`
- `wget [url] \ -O [file]`

### set file as excutable

- `chmod u+x [file]`

### 50 個常用指令

- [写代码怎能不会这些 Linux 命令？](https://blog.hellokaton.com/2017/08/write-code-must-linux-command.html)
- tar
  - 建立新的 tar 檔案
    - `tar cvf archive_name.tar dirname/`
  - 解壓縮 tar 檔案
    - `tar xvf archive_name.tar`
  - 開啟 tar 檔案
    - `tar tvf archive_name.tar`
- grep
  - 於檔案搜尋字串（不分大小寫）
    - `grep -i "the" demo_file`
  - 顯示搜尋結果，與結果後三行
    - `grep -A 3 -i "example" demo_text`
  - 遞迴搜尋資料夾裡的檔案
    - `grep -r "ramesh" *`
- find
  - 搜尋指定名稱之檔案（不分大小寫）
    - `find -iname "MyProgram.c"
  - 以搜尋結果之檔案執行命令
    - `find -iname "MyProgram.c" -exec md5sum {} \;`
  - 搜尋 home 目錄底下的所有空檔案
    - `find ~ -empty`
- ssh
  - 加入遠端主機
    - `ssh -l jsmith remotehost.example.com`
  - 與 ssh 終端互動
    - `ssh -v -l jsmith remotehost.example.com`
  - 顯示 ssh 終端版本
    - `ssh -V`
- sed
  - 將 dos 文件（`\r\n` 結尾）轉換為 unix 格式（`\n` 結尾）文件
    - `sed 's/.$//' filename`
  - 反轉文件內容後儲存
    - `sed -n '1!G; h; p' filename`
  - 替非空行加上行數
    - `sed '/./=' thegeekstuff.txt | sed 'N; s/\n/ /'`
- awk
  - 刪除重複行內容
    - `awk '!($0 in array) { array[$0]; print}' temp`
  - 輸出 `/etc/passwd/ 裡所有包含相同 `uid`與`gid` 的行內容
    - `awk -F ':' '$3=$4' /etc/passwd`
  - 輸出文件指定段落的文字
    - `awk '{print $2,$5;}' employee.txt`
- vim
  - 開啟檔案並跳至第 10 行
    - `vim +10 filename.txt`
  - 開啟檔案並跳至第一個符合內容的位置
    - `vim +/search-term filename.txt`
  - 以唯獨模式開始檔案
    - `vim -R /etc/passwd`
- diff
  - 比較時忽略空白
    - `diff -w name_list.txt name_list_new.txt`
- sort
  - 以遞增排序文件內容
    - `sort names.txt`
  - 以遞減排序文件內容
    - `sort -r names.txt`
  - 根據第三個單字排序 `/etc/passwd` 的內容
    - `sort -t: -k 3n /etc/passwd | more`
- export
  - 顯示含有字串 `oracle` 的環境變數
    - `$ export | grep ORACLE`
    - `declare -x ORACLE_BASE="/u01/app/oracle"`
    - `declare -x ORACLE_HOME="/u01/app/oracle/product/10.2.0"`
    - `declare -x ORACLE_SID="med"`
    - `declare -x ORACLE_TERM="xterm"`
  - 設定全域環境變數
    - `$ export ORACLE_HOME=/u01/app/oracle/product/10.2.0`
- xargs
  - 複製所有 jpg 檔案到外接硬碟
    - `ls *.jpg | xargs -n1 -i cp {} /external-hard-drive/directory`
  - 壓縮所有 jpg 檔案
    - `find / -name *.jpg -type f -print | xargs tar -cvzf images.tar.gz`
  - 下載文件檔案中的所有網址內容
    - `cat url-list.txt | xargs wget -c`
- ls
  - 更換檔案大小顯示方式
    - `ls -lh`
  - 以最後修改時間遞增排序顯示檔案
    - `ls -ltr`
  - 於檔案名稱後方顯示副檔名
    - `ls -F`
- pwd
  - 顯示目前所在目錄
- cd
- gzip
  - 建立 `.gz` 壓縮檔
    - `gzip test.txt`
  - 解壓縮 `.gz` 檔案
    - `gzip -d test.txt.gz`
  - 顯示壓縮比例
    - `gzip -l *.gz`
- bzip2
  - 建立 `.bz2` 壓縮檔
    - `bzip2 test.txt`
  - 解壓縮 `.bz2` 檔案
    - `bzip2 -d test.txt.bz2`
- unzip
  - 解壓縮 `.zip` 檔案
    - `unzip test.zip`
  - 顯示 `.zip` 檔案內容
    - `unzip -l jasper.zip`
- shutdown
  - 立即關機
    - `shutdown -h now`
  - 10 分鐘後關機
    - `shutdown -h +10`
  - 重新啟動
    - `shutdown -r now`
  - 重新啟動並進行系統檢查
    - `shutdown -Fr now`
- ftp
  - 連接至 ftp 伺服器並下載多個檔案
    - `ftp IP/hostname`
    - `ftp> mget *.html`
  - 顯示遠端主機檔案一覽
    - `ftp> mls *.html -`
- crontab
  - 顯示使用者的 `crontab`
    - `crontab -u john -l`
  - 建立一個每十分鐘執行一次的任務
    - `*/10 * * * * /home/ramesh/check-disk-space`
- service
  - 從腳本執行系統服務
  - 腳本檔案通常位於 `/etc/init.d` 資料夾裡
  - 查詢服務狀態
    - `service ssh status`
  - 查詢所有服務狀態
    - `service --status-all`
  - 重新啟動服務
    - `service ssh restart`
- ps
  - 輸出執行中的程序資訊
  - 顯示所有執行中的程序
    - `ps -ef | more`
  - 以樹狀結構顯示執行中的程序
    - `ps -efH | more`
- free
  - 顯示目前系統的記憶體使用狀況
  - 預設單位為 byte
  - 更改為其他單位
    - `free -g`
    - `-g` 為 GB，`-m` 為 MB，`-k` 為 KB，`-b` 為 bytea
  - 顯示記憶體總量
    - `free -t`
- top
  - 顯示目前使用系統最多資源的程序
  - 預設為以 CPU 使用率排序，可再按下 `O` 選擇其他標準
  - 只使用某個用戶的程序
    - `top -u oracle`
- df
  - 顯示硬碟使用狀況
  - 預設單位為 byte
    - `df -k`
  - 也可使用更符合閱讀習慣的格式
    - `df -h`
  - 亦可顯示硬碟格式類型
    - `df -T`
- kill
  - 結束某個程序
  - 通常會搭配 `ps -ef` 先找到該程序的編號
    - `ps -ef | grep vim`
    - `kill -9 7243`
  - 其他類似指令還有 `killall`、`pkill`、`xkill`
- cp
  - 複製檔案 1 至檔案 2，並維持檔案的權限、擁有者與時間標記
    - `cp -p file1 file2`
  - 複製檔案 1 至檔案 2，若檔案 2 存在會詢問是否覆蓋
    - `cp -i file1 file2`
- mv
  - 重新命名檔案 1 為檔案 2，若檔案 2 存在會詢問是否覆蓋
    - `mv -i file1 file2`
  - 加上 `-f` 則會直接覆蓋
  - 加上 `-v` 會顯示重新命名過程
- cat
  - 一次輸出多個檔案內容
    - `cat file1 file2`
  - 加上 `-n` 會於前方顯示行號
- mount
  - 如果想要加載檔案系統，需先建立一個目錄，再將系統加載至該目錄上
    - `mkdir /u01`
    - `mount /dev/sdb1 /u01`
- chmod
  - 修改檔案與目錄的權限
  - 賦予檔案擁有者與身份組所有權限
    - `chmod ug+rwx file.txt`
  - 刪除指定檔案身份組的所有權限
    - `chmod g-rwx file.txt`
  - 修改目錄權限，並遞迴修改目錄底下所有檔案與子目錄的權限
    - `chmod -R ug+rwx file.txt`
- chown
  - 修改檔案的擁有者與身份組
  - 修改檔案擁有者為 oracle、身份組為 db
    - `chown oracle:dba dbora.sh`
  - 遞迴修改目錄與目錄底下的所有檔案
    - `chown -R oracle:dba /home/oracle`
- passwd
  - 修改使用者密碼，執行指令後會先詢問舊密碼，之後輸入新密碼
  - 超級使用者可以使用此指令修改其他使用者的密碼，並且不必輸入舊密碼
    - `passwd USERNAME`
  - root 使用者亦可使用此指令刪除其他使用者的密碼，刪除後不需密碼即可登入
    - `passwd -d USERNAME`
- mkdir
  - 於 home 目錄底下建立名為 home 的資料夾
    - `mkdir ~/temp`
  - 加上 `-p` 可一同建立路徑中不存在的資料夾
    - `mkdir -p dir1/dir2/dir3/dir4/`
- ifconfig
  - 檢視系統網路狀況
  - 檢視所有網路狀況
    - `ifconfig -a`
  - 可使用 `up` 與  `down` 啟動或停用某個網路
    - `ifconfig eth0 up`
    - `ifconfig eth0 down`
- uname
  - 顯示重要系統訊息，例如 kernal 名稱、主機名稱、CPU 類型等等
  - `uname -a`
- `whereis`
  - 搜尋某個指令的執行檔位置
    - `whereis ls`
  - 也可加上 `-B` 與目錄位置搜尋位於 `whereis` 預設路徑之外的執行檔
    - `whereis -u -B /tmp -f lsmk`
- whatis
  - 顯示某個指令的內容敘述
    - `whatis ls`
    - `whatis ifconfig`
- locate
  - 輸出某個指定檔案（或一群檔案）的路徑，由 `updatedb` 所建立
    - `locate crontab`
- man
  - 顯示某個指令的說明頁面
    - `man crontab`
- tail
  - 顯示檔案尾端內容，預設為最後 10 行
  - 可使用 `-n` 指定要顯示的行數
    - `tail -n N filename.txt`
  - 可使用 `-f` 持續監聽更新內容
    - `tail -f log-file`
- less
  - 在不載入檔案的前提下顯示檔案內容
    - `less huge-log-file.log`
- su
  - 切換使用帳號
    - `su - USERNAME`
  - 以某個帳號使用指定指令後切換回原本帳號
    - `su -raj -c 'ls'`
  - 使用指定 shell 登入
    - `su -s 'SHELLNAME' USERNAME`
- mysql
  - 登入遠端資料庫
    - `mysql -u root -p -h 192.168.1.2`
  - 登入本地資料庫
    - `mysql -u root -p`
- yum
  - 安裝 Apache
    - `yum install httpd`
  - 更新 Apache
    - `yum update httpd`
  - 移除 Apache
    - `yum remove httpd`
- rpm
  - 安裝 Apache
    - `rpm -ivh httpd-2.2.3-22.0.1.el5.i386.rpm`
  - 更新 Apache
    - `rpm -uvh httpd-2.2.3-22.0.1.el5.i386.rpm`
  - 移除 Apache
    - `rpm -ev httpd`
- ping
  - 發送 5 次封包詢問遠端主機
    - `ping -c 5 gmail.com`
- date
  - 設定系統日期
    - `date -s "01/31/2010 23:59:53"`
  - 同步硬體時間
    - `hwclock -systohc`
    - `hwclock --systohc -utc`
- wget
  - 下載網路內容
    - `wget URL`
  - 下載網路內容並以指定名稱儲存
    - `wget -O FILENAME URL`

### fish

- read command parameter
  - `$argv`
- display last line of text file
  - `tail -n 1 [file]`

### File manager

- [gokcehan/lf](https://github.com/gokcehan/lf/releases)

### libc-bin error

- [dpkg: error processing package libc-bin (-configure) | setokynet Blog (WordPress.com)](https://setokynet.wordpress.com/2021/12/12/dpkg-error-processing-package-libc-bin-configure/)

```bash
sudo mv /var/lib/dpkg/info/libc-bin.* /tmp/
sudo dpkg --remove --force-remove-reinstreq libc-bin
sudo dpkg --purge libc-bin
sudo apt install --reinstall libc-bin
sudo mv /tmp/libc-bin.* /var/lib/dpkg/info/
```

## Bash

- [Bash-Oneliner](https://github.com/onceupon/Bash-Oneliner)
- [名著「入門UNIXシェルプログラミング」の超詳細なレビューをしてみた（古い内容の訂正）](https://qiita.com/ko1nksm/items/0fa2f73dd6d9822518a3)
- [UNIX プログラミングの基礎知識](https://gadgety.net/shin/lang/c/programming.html)
- [Bash: わかるとほんのちょっとうれしくなること５選](https://qiita.com/akauma16/items/c01e12f559a1231ae003)
