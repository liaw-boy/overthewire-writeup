# Bandit

> Bandit 是 OverTheWire 給初學者的關卡，重點放在 Linux 指令列基礎。

## 🔌 連線資訊

- Host: `bandit.labs.overthewire.org`
- Port: `2220`
- Protocol: SSH
- 帳號格式：`banditN`（N 為關卡編號，例如 `bandit0`、`bandit1` ⋯）

連線範本：

```bash
ssh bandit<N>@bandit.labs.overthewire.org -p 2220
```

## 🎮 過關方式

每一關都是登入該關卡的帳號，在伺服器上想辦法找出下一關的密碼。取得 `banditN+1` 的密碼後，用該密碼 SSH 登入 `banditN+1`，依此類推。

## 📋 關卡進度（對應官方 35 關）

| Level | 主題 | 重點指令 | Writeup |
|-------|------|----------|---------|
| 0 | SSH 登入 | `ssh` | [→ level00](./level00/) |
| 0 → 1 | 讀取 home 目錄檔案 | `ls`, `cat` | [→ level01](./level01/) |
| 1 → 2 | 特殊檔名 `-` | `cat ./-` | [→ level02](./level02/) |
| 2 → 3 | 含空白的檔名 | quoting, `\` escape | [→ level03](./level03/) |
| 3 → 4 | 隱藏檔 | `ls -a` | [→ level04](./level04/) |
| 4 → 5 | 找 human-readable 檔 | `file`, `find` | [→ level05](./level05/) |
| 5 → 6 | 條件式 find（size, executable） | `find -size -executable` | [→ level06](./level06/) |
| 6 → 7 | 全系統搜尋（user / group） | `find / -user -group` | [→ level07](./level07/) |
| 7 → 8 | grep 字串 | `grep` | [→ level08](./level08/) |
| 8 → 9 | 找唯一行 | `sort`, `uniq -u` | [→ level09](./level09/) |
| 9 → 10 | 二進位中找字串 | `strings`, `grep` | [→ level10](./level10/) |
| 10 → 11 | base64 解碼 | `base64 -d` | [→ level11](./level11/) |
| 11 → 12 | ROT13 | `tr` | [→ level12](./level12/) |
| 12 → 13 | 多重壓縮 hexdump | `xxd -r`, `file`, `gzip`, `bzip2`, `tar` | [→ level13](./level13/) |
| 13 → 14 | SSH 私鑰登入 | `ssh -i` | [→ level14](./level14/) |
| 14 → 15 | netcat 連 localhost port | `nc localhost 30000` | [→ level15](./level15/) |
| 15 → 16 | openssl s_client（SSL）| `openssl s_client` | [→ level16](./level16/) |
| 16 → 17 | nmap + openssl | `nmap`, `openssl s_client` | [→ level17](./level17/) |
| 17 → 18 | diff 比對兩檔 | `diff` | [→ level18](./level18/) |
| 18 → 19 | SSH 帶遠端指令 | `ssh ... 'cmd'` | [→ level19](./level19/) |
| 19 → 20 | setuid binary | `./bandit20-do` | [→ level20](./level20/) |
| 20 → 21 | nc listener + setuid | `nc -l`, `suconnect` | [→ level21](./level21/) |
| 21 → 22 | cron 任務分析 | `/etc/cron.d/`, `cat` | [→ level22](./level22/) |
| 22 → 23 | cron + md5sum | `md5sum`, `mktemp` | [→ level23](./level23/) |
| 23 → 24 | 可寫 cron 目錄 | scripting cron job | [→ level24](./level24/) |
| 24 → 25 | brute force pincode + nc | shell loop, `nc` | [→ level25](./level25/) |
| 25 → 26 | `more` / vi 逃逸 | `more`, `vim` | [→ level26](./level26/) |
| 26 → 27 | vim shell + setuid | `:set shell`, `:shell` | [→ level27](./level27/) |
| 27 → 28 | git clone over SSH | `git clone` | [→ level28](./level28/) |
| 28 → 29 | git log 找歷史 | `git log`, `git show` | [→ level29](./level29/) |
| 29 → 30 | git branches | `git branch -a`, `git checkout` | [→ level30](./level30/) |
| 30 → 31 | git tags | `git tag`, `git show` | [→ level31](./level31/) |
| 31 → 32 | git push + .gitignore 繞過 | `git add -f`, `git push` | [→ level32](./level32/) |
| 32 → 33 | shell escape `$0` | `$0` | [→ level33](./level33/) |
| 33 | 完成！ | — | [→ level34](./level34/) |

> Writeup 會隨闖關進度持續更新。

## 🔒 關於密碼

每一關的密碼都用 `<details>` 摺疊。請先自己試，真的卡住或要驗證再展開。

## 🧰 範本

新關卡 writeup 範本放在 [`_template/`](./_template/)，方便快速複製。
