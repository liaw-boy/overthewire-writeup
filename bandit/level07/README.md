# Bandit Level 6 → 7 — 全機搜尋（owner / group / size 三條件 find）

> 上一關只在當前目錄找；這一關密碼藏在**整台伺服器**任何角落。

---

## 題目說明

官方原文：

> The password for the next level is stored **somewhere on the server** and has all of the following properties:
> - owned by user `bandit7`
> - owned by group `bandit6`
> - 33 bytes in size

也就是 — 不再限制在 home 目錄，要對整個檔案系統 `/` 下手，過濾出滿足這三個條件的檔案。

## 挑戰點

1. **搜尋範圍從 `.` 變成 `/`** — 整台機器很多目錄你沒權限讀（`/root`、`/proc/<pid>`、其他玩家的 home），`find` 會噴一堆 `Permission denied`。要把錯誤訊息丟掉，只留有效結果。
2. **三個條件要同時成立** — 之前學的 `-size` 之外，多了 `-user` 跟 `-group`。
3. **stderr 與 stdout 的差別** — 第一次遇到必須把 `stderr` 重新導向到 `/dev/null` 的場景。

## 解題過程

登入：

```bash
ssh bandit6@bandit.labs.overthewire.org -p 2220
# password: HWasnPhtq9AVKe0dmk45nxy20cvUa6EG
```

從根目錄 `/` 開始找，同時把 stderr 丟掉避免被 `Permission denied` 洗版：

```bash
bandit6@bandit:~$ find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null
/var/lib/dpkg/info/bandit7.password
```

只有一個結果，直接讀：

```bash
bandit6@bandit:~$ cat /var/lib/dpkg/info/bandit7.password
morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj
```

拿到密碼，登入下一關驗證：

```bash
ssh bandit7@bandit.labs.overthewire.org -p 2220
```

## 密碼

<details>
<summary>展開（先自己試過再看）</summary>

```
morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj
```

</details>

## 指令介紹

### find 條件補完

| 選項 | 說明 |
|------|------|
| `-user <name>` | 檔案 owner 是 `<name>` |
| `-group <name>` | 檔案 group 是 `<name>` |
| `-size 33c` | 大小剛好 33 bytes（`c` = bytes，沿用上一關） |
| `-type f` | 只要一般檔案，跳過目錄、symlink |

三個條件並列預設就是 **AND**，不需要寫 `-a`。

### stdin / stdout / stderr 速記

Linux 每個 process 開機就有三個檔案描述符（file descriptor，簡稱 fd）：

| fd | 名稱 | 預設指向 | 中文 |
|----|------|----------|------|
| `0` | stdin | 鍵盤 | 標準輸入 |
| `1` | stdout | 螢幕 | 標準輸出（正常結果） |
| `2` | stderr | 螢幕 | 標準錯誤（錯誤訊息） |

`find` 正常結果走 `1`、`Permission denied` 走 `2`，所以同一個畫面上看起來混在一起，但其實是兩條獨立的水管。

### 導向（redirection）

| 寫法 | 意思 |
|------|------|
| `> file` | 把 stdout（1）覆寫到 `file` |
| `>> file` | 把 stdout 附加到 `file` |
| `2> file` | 把 stderr（2）覆寫到 `file` |
| `2>/dev/null` | 把 stderr 丟掉（`/dev/null` 是黑洞，寫進去什麼都不剩） |
| `2>&1` | 把 stderr 併進 stdout（合流到同一條水管） |
| `&> file` 或 `> file 2>&1` | stdout + stderr 全部導到 `file` |

> 為什麼是 `2>/dev/null` 而不是 `2 > /dev/null`？
> 因為 `2>` 是一個 token，中間**不能有空白**，否則 shell 會把 `2` 當成普通字串傳給指令。

### `/dev/null` 是什麼

特殊裝置檔，**讀**它永遠是空、**寫**它的內容直接消失。在 Linux 哲學裡專門拿來當「垃圾桶」用。

## 延伸閱讀（官方建議）

- `man find`
- `man bash`（看 REDIRECTION 那一節）

---

<div align="center">

**◀ [Level 5 → 6：條件式 find](../level06/)** · [🏠 回 Bandit 索引](../README.md) · **下一關 ▶ [Level 7 → 8：grep 撈關鍵字](../level08/)**

</div>
