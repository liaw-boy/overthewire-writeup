# Bandit Level 2 → Level 3 — 含空白的檔名

> 第三關。重點是搞懂 shell 怎麼切 token，學會三種「告訴 shell 這個空白是檔名的一部分」的寫法。

---

## 題目說明

密碼存在 home 目錄裡一個檔名是 `spaces in this filename` 的檔案中。

官方原文：

> The password for the next level is stored in a file called `spaces in this filename` located in the home directory.

## 挑戰點

檔名含空白。Shell 預設把**空白**當成 token 分隔符，所以：

```bash
cat spaces in this filename
# shell 解讀成「cat 4 個檔名」：spaces、in、this、filename
# 結果：四個都不存在，全部 No such file or directory
```

要讓 shell 把整串 `spaces in this filename` 視為**一個** token，必須**引號包住**或**逐個跳脫空白**。

## 解題過程

```text
bandit2@bandit:~$ ls -la
total 24
drwxr-xr-x  2 root    root    4096 ... .
drwxr-xr-x 70 root    root    4096 ... ..
-rw-r--r--  1 root    root     220 ... .bash_logout
-rw-r--r--  1 root    root    3771 ... .bashrc
-rw-r--r--  1 root    root     807 ... .profile
-rw-r-----  1 bandit3 bandit2   33 ... spaces in this filename

bandit2@bandit:~$ cat "spaces in this filename"
MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx
```

**三種等價寫法：**

```bash
cat "spaces in this filename"        # 雙引號包整串
cat 'spaces in this filename'        # 單引號包整串
cat spaces\ in\ this\ filename       # 用 \ 跳脫每個空白
# 或者：輸入 cat sp 然後按 Tab，shell 會自動補全並加好跳脫
```

拿到密碼後登入下一關：

```bash
bandit2@bandit:~$ exit
$ ssh bandit3@bandit.labs.overthewire.org -p 2220
bandit3@bandit.labs.overthewire.org's password: <貼上密碼>
bandit3@bandit:~$
```

過關 ✅

## 密碼

<details>
<summary>展開（請先自己嘗試）</summary>

```text
MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx
```

</details>

## 指令介紹

| 寫法 | 說明 |
|------|------|
| `"..."` | 雙引號：包住的內容當作一個 token，但 `$變數` 和 `` `指令` `` 仍會展開 |
| `'...'` | 單引號：包住的內容**完全字面化**，連 `$` 都不展開 |
| `\<char>` | 反斜線跳脫：把下一個字元當成字面字元（如 `\ ` 代表空白本身） |
| Tab 補全 | 輸入檔名前綴後按 Tab，shell 會自動補上剩餘字元並正確跳脫空白 |
| `cat <file>` | 印出檔案內容 |

### 引號差別速記

| | 保留空白 | 展開 `$變數` | 展開 `` `指令` `` |
|---|---|---|---|
| `"..."` | ✅ | ✅ | ✅ |
| `'...'` | ✅ | ❌ | ❌ |
| `\` | ✅（單字元） | — | — |

> Bandit 這關用三種都行，但寫 shell script 時要分清楚：要展開變數用 `"`、純字面字串用 `'`。

---

<div align="center">

**◀ [Level 1 → 2：特殊檔名 `-`](../level02/)** · [🏠 回 Bandit 索引](../) · **下一關 ▶ [Level 3 → 4：隱藏檔](../level04/)**

</div>
