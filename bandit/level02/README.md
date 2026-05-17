# Bandit Level 1 → Level 2 — 特殊檔名 `-`

> 第二關。重點是搞懂為什麼 `cat -` 不會讀檔，以及怎麼正確處理檔名為 `-` 的檔。

---

## 題目說明

密碼存在 home 目錄裡一個檔名為 `-` 的檔案中。

官方原文：

> The password for the next level is stored in a file called `-` located in the home directory.

## 挑戰點

檔名是 `-`（破折號）。在 Linux 大多數工具裡，`-` 代表「從 standard input 讀取」（讀檔場景）或「寫到 standard output」（輸出場景），所以直接 `cat -` 並不會讀到這個檔，而是會卡住等你打字。

要讓 `cat` 把 `-` 當成「真實檔名」而非 stdin，必須加上**路徑前綴**或用 `--` 結束選項解析。

## 解題過程

```text
bandit1@bandit:~$ ls -al
total 24
drwxr-xr-x  2 root    root    4096 ... .
drwxr-xr-x 70 root    root    4096 ... ..
-rw-r--r--  1 root    root     220 ... .bash_logout
-rw-r--r--  1 root    root    3771 ... .bashrc
-rw-r--r--  1 root    root     807 ... .profile
-rw-r-----  1 bandit2 bandit1   33 ... -

bandit1@bandit:~$ cat -
（卡住，等 stdin 輸入 → 按 Ctrl+C 中止）

bandit1@bandit:~$ cat ./-
263JGJPfgU6LtdEvgfWU1XP5yac29mFx
```

**三種等價寫法：**

```bash
cat ./-               # 相對路徑前綴
cat /home/bandit1/-   # 絕對路徑
cat -- -              # -- 結束 options，之後的 token 都當成檔名
```

拿到密碼後登入下一關：

```bash
bandit1@bandit:~$ exit
$ ssh bandit2@bandit.labs.overthewire.org -p 2220
bandit2@bandit.labs.overthewire.org's password: <貼上密碼>
bandit2@bandit:~$
```

過關 ✅

## 密碼

<details>
<summary>展開（請先自己嘗試）</summary>

```text
263JGJPfgU6LtdEvgfWU1XP5yac29mFx
```

</details>

## 指令介紹

| 指令 / 寫法 | 說明 |
|--------------|------|
| `cat -` | `-` 在 `cat` 裡代表 stdin，**不會**讀檔 |
| `cat ./-` | 加 `./` 前綴讓 `-` 明確是檔名（相對路徑） |
| `cat /home/bandit1/-` | 絕對路徑寫法，最沒歧義 |
| `cat -- -` | `--` 是 GNU 工具的標準「end of options」標記 |
| `./` | 「當前目錄」的相對路徑前綴 |
| `--` | 多數 GNU 工具用來結束選項解析的分隔符，之後的 token 全部當成 positional 參數（檔名）處理 |

---

<div align="center">

**◀ [Level 0 → 1：讀取 home 目錄的檔案](../level01/)** · [🏠 回 Bandit 索引](../) · **下一關 ▶ [Level 2 → 3：含空白的檔名](../level03/)**

</div>
