# Bandit Level 4 → Level 5 — 找出 human-readable 的檔案

> 第五關。重點是用 `file` 指令判斷檔案類型，搭配 wildcard 一次掃整個目錄。

---

## 題目說明

`inhere/` 目錄底下有 10 個檔案（`-file00` 到 `-file09`），其中只有**一個是 human-readable** 純文字檔，密碼就在裡面。其他 9 個是 binary data。

官方原文：

> The password for the next level is stored in the only human-readable file in the `inhere` directory. Tip: if your terminal is messed up, try the `reset` command.

## 挑戰點

兩個重點：

1. **怎麼判斷檔案是文字還是 binary？** 不能直接 `cat` 每個檔案（10 個太多，而且 `cat` binary 還會把你 terminal 弄花）→ 用 `file` 指令。
2. **檔名 `-` 開頭** — 跟 Level 1→2 同個狀況，必須 `./` 前綴避免被 `file` 當成 option。

## 解題過程

```text
bandit4@bandit:~$ ls -al
total 12
drwxr-xr-x  3 root    root    4096 ... .
drwxr-xr-x 70 root    root   4096 ... ..
drwxr-xr-x  2 root    root    4096 ... inhere

bandit4@bandit:~$ cd inhere/

bandit4@bandit:~/inhere$ ls -al
total 48
drwxr-xr-x 2 root    root    4096 ... .
drwxr-xr-x 3 root    root    4096 ... ..
-rw-r----- 1 bandit5 bandit4   33 ... -file00
-rw-r----- 1 bandit5 bandit4   33 ... -file01
-rw-r----- 1 bandit5 bandit4   33 ... -file02
-rw-r----- 1 bandit5 bandit4   33 ... -file03
-rw-r----- 1 bandit5 bandit4   33 ... -file04
-rw-r----- 1 bandit5 bandit4   33 ... -file05
-rw-r----- 1 bandit5 bandit4   33 ... -file06
-rw-r----- 1 bandit5 bandit4   33 ... -file07
-rw-r----- 1 bandit5 bandit4   33 ... -file08
-rw-r----- 1 bandit5 bandit4   33 ... -file09

bandit4@bandit:~/inhere$ file ./-file*
./-file00: data
./-file01: data
./-file02: data
./-file03: data
./-file04: data
./-file05: data
./-file06: data
./-file07: ASCII text
./-file08: data
./-file09: data

bandit4@bandit:~/inhere$ cat ./-file07
4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw
```

**關鍵觀察：**

- `data` = `file` 判斷不出是哪種具體格式的 binary（也包含一些 random bytes 的文字檔）
- `ASCII text` = 可讀的純文字 → 就是它
- 萬用字元 `-file*` 一次比對所有匹配的檔名，省去逐個檢查

拿到密碼後登入下一關：

```bash
$ ssh bandit5@bandit.labs.overthewire.org -p 2220
```

過關 ✅

## 密碼

<details>
<summary>展開（請先自己嘗試）</summary>

```text
4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw
```

</details>

## 指令介紹

| 指令 / 寫法 | 說明 |
|--------------|------|
| `file <file>` | 判斷檔案類型，會讀檔頭的 magic bytes + 內容啟發式判斷 |
| `file ./*` | 一次判斷當前目錄所有檔案 |
| `*` | shell **glob wildcard**：比對「任意字元（含 0 個）」 |
| `?` | glob wildcard：比對「**剛好一個**字元」 |
| `[abc]` | glob wildcard：比對 a / b / c 其中之一 |
| `./` | 相對路徑前綴，避免檔名被當成 option |
| `reset` | 如果不小心 `cat` 了 binary 把 terminal 弄花，這個指令會重置 terminal |

### `file` 常見輸出

| 輸出 | 意思 |
|------|------|
| `ASCII text` | 純 ASCII 文字檔 |
| `UTF-8 Unicode text` | UTF-8 文字檔 |
| `data` | 判斷不出來，通常是 binary |
| `ELF 64-bit LSB executable` | Linux 執行檔 |
| `gzip compressed data` | gzip 壓縮檔 |
| `PNG image data` | PNG 圖片 |

---

<div align="center">

**◀ [Level 3 → 4：隱藏檔](../level04/)** · [🏠 回 Bandit 索引](../) · **下一關 ▶ [Level 5 → 6：條件式 find](../level06/)**

</div>
