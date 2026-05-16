# Bandit Level 3 → Level 4 — 隱藏檔

> 第四關。重點是知道 `.` 開頭的檔案預設不會被 `ls` 列出來，要用 `-a` 才看得到。

---

## 題目說明

密碼存在 `inhere/` 目錄底下的**隱藏檔**裡。

官方原文：

> The password for the next level is stored in a hidden file in the `inhere` directory.

## 挑戰點

Linux 把 `.` 開頭的檔案視為**隱藏檔**（從原始 Unix 時代的習慣繼承下來）。`ls` 預設不會列出來，必須加 `-a` (all) flag。

這關的隱藏檔名是 `...Hiding-From-You`（**三個點**開頭），不只一個 dot，第一眼可能會誤以為是 `.` 或 `..` 這種目錄參照符。

## 解題過程

```text
bandit3@bandit:~$ ls -la
total 12
drwxr-xr-x 3 root    root    4096 ... .
drwxr-xr-x 70 root    root   4096 ... ..
drwxr-xr-x 2 root    root    4096 ... inhere

bandit3@bandit:~$ cd inhere/

bandit3@bandit:~/inhere$ ls
（空的，沒東西？）

bandit3@bandit:~/inhere$ ls -la
total 12
drwxr-xr-x 2 root    root    4096 ... .
drwxr-xr-x 3 root    root    4096 ... ..
-rw-r----- 1 bandit4 bandit3   33 ... ...Hiding-From-You

bandit3@bandit:~/inhere$ cat ...Hiding-From-You
2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ
```

> 保險寫法：`cat ./...Hiding-From-You`，明確告訴 shell「這是當前目錄的檔名」，避免被誤判（**對齊 Level 1→2 的抓手**）。

拿到密碼後登入下一關：

```bash
bandit3@bandit:~/inhere$ exit
$ ssh bandit4@bandit.labs.overthewire.org -p 2220
bandit4@bandit.labs.overthewire.org's password: <貼上密碼>
bandit4@bandit:~$
```

過關 ✅

## 密碼

<details>
<summary>展開（請先自己嘗試）</summary>

```text
2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ
```

</details>

## 指令介紹

| 指令 / 選項 | 說明 |
|--------------|------|
| `cd <dir>` | change directory，切換到指定目錄 |
| `cd` | 不接參數 = 回 home 目錄 |
| `cd -` | 回上次所在的目錄 |
| `ls -a` | **all**：連 `.` 開頭的隱藏檔（含 `.` 與 `..` 本身）一起列 |
| `ls -A` | almost all：同 `-a` 但**不**列 `.` 和 `..` |
| `ls -l` | long format：權限、owner、size、時間 |
| `ls -la` | 上兩個組合，最常用 |
| `cat ./<file>` | 加 `./` 前綴避免檔名被誤判（特別是 `-` 或多個 `.` 開頭）|

### Unix 隱藏檔的由來

> 1970 年代 Unix 工程師寫 `ls` 時，本來只想跳過 `.`（當前目錄）和 `..`（上層目錄）這兩個特殊條目，但圖快用了「以 `.` 開頭就跳過」的判斷。後來大家發現「不想被列出的 config 檔可以用 `.` 起頭」，就將錯就錯沿用至今。— 沒有「隱藏」的本意，就是個延續 50 年的歷史 bug。

---

<div align="center">

**◀ [Level 2 → 3：含空白的檔名](../level03/)** · [🏠 回 Bandit 索引](../) · **下一關 ▶ _待寫_**

</div>
