# Bandit Level 0 → Level 1 — 讀取 home 目錄的檔案

> 第一次真正解題。重點是熟悉 `ls` 看目錄、`cat` 讀檔，並且**先看清楚再動手**。

---

## 題目說明

密碼存在 home 目錄裡一個叫 `readme` 的檔案，拿到後用該密碼 SSH 登入 `bandit1`。

官方原文：

> The password for the next level is stored in a file called `readme` located in the home directory.
> Use this password to log into `bandit1` using SSH. Whenever you find a password for a level,
> use SSH (on port 2220) to log into that level and continue the game.

> 💡 之後每一關的玩法都一樣：在目前這關找到下一關的密碼 → SSH 登入下一關。

## 挑戰點

這關沒有 trick — 純粹練 `ls` 看目錄、`cat` 讀檔。

真正的學習重點是養成**先 `ls -la` 看清楚權限與檔案，再動手**的習慣。

## 解題過程

```text
bandit0@bandit:~$ pwd
/home/bandit0

bandit0@bandit:~$ ls -la
total 24
drwxr-xr-x  3 root    root    4096 ... .
drwxr-xr-x 70 root    root    4096 ... ..
-rw-r--r--  1 root    root     220 ... .bash_logout
-rw-r--r--  1 root    root    3771 ... .bashrc
-rw-r--r--  1 root    root     807 ... .profile
-rw-r-----  1 bandit1 bandit0   33 ... readme

bandit0@bandit:~$ cat readme
<32 字元密碼>
```

**觀察：**

- `readme` 的 owner 是 `bandit1`、group 是 `bandit0`，所以 `bandit0` 可以透過 group `r` 權限讀取。
- 大小 33 bytes = 32 字元密碼 + 1 個換行符。
- 這就是為什麼題目能設計成「給你讀但你還沒登入下一關」的權限模式。

拿到密碼後登入下一關：

```bash
bandit0@bandit:~$ exit
logout

$ ssh bandit1@bandit.labs.overthewire.org -p 2220
bandit1@bandit.labs.overthewire.org's password: <貼上剛剛 cat 出來的密碼>
bandit1@bandit:~$
```

過關 ✅

## 密碼

<details>
<summary>展開（請先自己嘗試）</summary>

OverTheWire 會不定期重置密碼，這裡不放固定值。請自己 `cat readme` 後把結果填到下面這個 code block 當作個人備忘：

```text
<把你拿到的 32 字元密碼貼這裡>
```

</details>

## 指令介紹

| 指令 / 選項 | 說明 |
|--------------|------|
| `pwd` | print working directory，顯示目前所在的絕對路徑 |
| `ls` | 列出目錄內容 |
| `ls -l` | 詳細列出（權限、owner、size、時間）|
| `ls -a` | 連 `.` 開頭的隱藏檔一起列 |
| `ls -la` | 上兩者組合，最常用 |
| `cat <file>` | 把檔案內容印到 stdout |
| `~` / `$HOME` | 目前使用者的 home 目錄路徑 |
| `exit` 或 `Ctrl+D` | 離開目前的 shell |

---

<div align="center">

**◀ [Level 0：SSH 登入](../level00/)** · [🏠 回 Bandit 索引](../) · **下一關 ▶ _待寫_**

</div>
