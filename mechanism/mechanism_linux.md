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
| `ps            | 顯示使用者所有執行中的程式   |      |
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
