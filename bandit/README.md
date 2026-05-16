# Bandit Writeup

> Bandit 是 OverTheWire 給初學者的關卡，重點放在 **Linux 指令列基礎**。
> Bandit is OverTheWire's beginner wargame, focused on basic Linux command-line skills.

## 🔌 連線資訊 / Connection

- Host: `bandit.labs.overthewire.org`
- Port: `2220`
- Protocol: `SSH`
- 帳號格式：`banditN`（N 為關卡編號，例如 `bandit0`、`bandit1`...）

連線範本 / Template:

```bash
ssh bandit<N>@bandit.labs.overthewire.org -p 2220
```

## 🎮 過關方式 / How it works

每一關都是登入該關卡的帳號，**在伺服器上想辦法找出下一關的密碼**。
取得 `banditN+1` 的密碼後，用該密碼 SSH 登入 `banditN+1`，依此類推。

> Each level: log in as `banditN`, hunt for the password of `banditN+1` on the server,
> then SSH in as the next user.

## 📋 關卡進度 / Level Progress

| Level | 主題 / Topic | 重點指令 / Key commands | Writeup |
|-------|--------------|--------------------------|---------|
| 0 | SSH 連線入門 | `ssh` | [→ level00](./level00/) |
| 0 → 1 | 讀取檔案 | `ls`, `cat` | [→ level01](./level01/) |
| 1 → 2 | 特殊檔名 | `cat ./-`, `cat < -` | _coming_ |
| 2 → 3 | 含空白的檔名 | quoting, `\` escape | _coming_ |
| 3 → 4 | 隱藏檔案 | `ls -a` | _coming_ |
| 4 → 5 | 找文字檔 | `file`, `find` | _coming_ |
| 5 → 6 | 條件式 find | `find -size`, `-readable` | _coming_ |
| 6 → 7 | 全系統搜尋 | `find / -user -group` | _coming_ |

> Writeup 會隨我自己過關進度持續更新。
> Writeups update as I progress.

## 🔒 關於密碼 / About passwords

每一關的密碼都用 `<details>` 摺疊。**請先自己試**，真的卡住或要驗證再展開。
Passwords are wrapped in `<details>` blocks. Please try first; expand only to verify.

## 🧰 Template

新關卡 writeup 模板放在 [`_template/`](./_template/)，方便快速複製。
