# Bandit Level 0 → Level 1 — 讀取家目錄的檔案

> 第一次真正解題。重點是熟悉 `ls` 看目錄、`cat` 讀檔，並且**先看清楚再動手**。
> First real puzzle. Goal: get comfortable with `ls` and `cat`, and learn to *look before you leap*.

---

## 🎯 Level Goal

> The password for the next level is stored in a file called `readme` located in the home directory.
> Use this password to log into `bandit1` using SSH. Whenever you find a password for a level,
> use SSH (on port 2220) to log into that level and continue the game.

### 中文翻譯

下一關（`bandit1`）的密碼存在 **home directory 裡一個叫 `readme` 的檔案**。
拿到後，用 SSH（port `2220`）登入 `bandit1`，繼續闖下去。

> 💡 之後每一關的玩法都是：「在這關找到下一關的密碼 → SSH 登入下一關」。

## 🧠 預備知識 / Prerequisites

- **Home directory (`~`)**：使用者登入後預設所在的目錄，路徑是 `/home/<username>`，本關裡就是 `/home/bandit0`。
- **`$HOME` 環境變數**：等同於家目錄路徑，跨 shell 通用。
- **絕對路徑 vs 相對路徑**：`/home/bandit0/readme` 是絕對路徑；`readme` 是相對於目前目錄。
- **`pwd`** 隨時可以確認自己在哪裡。

## 🛠️ 用到的指令 / Commands

| 指令 | 用途 |
|------|------|
| `pwd` | 印出 **p**resent **w**orking **d**irectory（目前所在目錄） |
| `ls` | 列出目錄內容 |
| `ls -la` | 連隱藏檔（`.` 開頭）和檔案 metadata 一起列 |
| `cat <file>` | 把檔案內容印到 stdout |
| `file <file>` | 判斷檔案型別（text / binary / 壓縮檔...） |

man 重點 / Man page essentials:

```bash
man ls
#   -a, --all       do not ignore entries starting with .
#   -l              use a long listing format
#   -h, --human-readable  with -l, sizes like 1K, 234M

man cat
#   -n   number all output lines
#   -A   show all (tabs, line endings, non-printing chars)
```

## 🚀 解題步驟 / Solution

### Step 1 — 用 Level 0 的方法登入

```bash
$ ssh bandit0@bandit.labs.overthewire.org -p 2220
bandit0@bandit.labs.overthewire.org's password: bandit0
```

> 從這關開始每一關都會這樣登入，差別只在 `banditN` 帳號與該關的密碼。

### Step 2 — 確認自己在哪、有什麼東西

```bash
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
```

**關鍵觀察 / Key observations：**
- `readme` 的擁有者是 `bandit1`，group 是 `bandit0` → 所以 `bandit0` 可以讀（group r 權限）。
- 大小 `33` bytes → 大約是 32 字元密碼 + 1 個換行符。
- 這就是為什麼題目能設計成「給你讀但你還沒登入下一關」的權限模式。

### Step 3 — 讀檔

```bash
bandit0@bandit:~$ cat readme
<32 個字元的隨機字串>
```

> 也可以用絕對路徑保險一點：`cat /home/bandit0/readme` 或 `cat ~/readme`。

### Step 4 — 用拿到的密碼登入下一關

```bash
bandit0@bandit:~$ exit
logout

$ ssh bandit1@bandit.labs.overthewire.org -p 2220
bandit1@bandit.labs.overthewire.org's password: <貼上剛剛 cat 出來的密碼>
bandit1@bandit:~$
```

過關 ✅

## 🔓 Password for next level

<details>
<summary>展開 / Expand（請先自己嘗試 / try yourself first）</summary>

OverTheWire 會不定期重置密碼，這裡不放固定值。
請自己 `cat readme` 後把結果填到下面這個 code block 當作個人備忘：

```text
<把你拿到的 32 字元密碼貼這裡>
```

> 推薦：自己手動填這個欄位，可以強迫自己回想流程，而不是一鍵複製。

</details>

---

<div align="center">

**◀ [Level 0：SSH 登入](../level00/)** · [🏠 回 Bandit 索引](../) · **下一關 ▶ _待寫_**

</div>
