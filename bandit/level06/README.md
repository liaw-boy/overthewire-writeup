# Bandit Level 5 → Level 6 — 條件式 find

> 第六關。重點是學會 `find` 加多個條件（檔案大小、可執行、檔案類型）做精準篩選。

---

## 題目說明

`inhere/` 目錄底下有 20 個子目錄（`maybehere00` 到 `maybehere19`），裡面散落很多檔案。密碼藏在其中一個檔，滿足以下**三個條件**：

- human-readable（純文字檔）
- 1033 bytes 大小
- not executable（不可執行）

官方原文：

> The password for the next level is stored in a file somewhere under the `inhere` directory and has all of the following properties:
> - human-readable
> - 1033 bytes in size
> - not executable

## 挑戰點

20 個子目錄、每個裡面又有一堆檔案 — 人肉一個個 `file` + `ls -l` 看 size 是不可能的。

需要 `find` 一次把三個條件 AND 起來。

## 解題過程

```text
bandit5@bandit:~$ ls
inhere

bandit5@bandit:~$ cd inhere/

bandit5@bandit:~/inhere$ ls
maybehere00  maybehere02  maybehere04  maybehere06  maybehere08  maybehere10  maybehere12  maybehere14  maybehere16  maybehere18
maybehere01  maybehere03  maybehere05  maybehere07  maybehere09  maybehere11  maybehere13  maybehere15  maybehere17  maybehere19

bandit5@bandit:~/inhere$ find . -type f -size 1033c ! -executable
./maybehere07/.file2

bandit5@bandit:~/inhere$ cat ./maybehere07/.file2
HWasnPhtq9AVKe0dmk45nxy20cvUa6EG
```

**逐條件拆解：**

| 條件 | find 寫法 |
|------|-----------|
| 從當前目錄遞迴搜尋 | `.` |
| 只要檔案，不要目錄 | `-type f` |
| 大小剛好 1033 bytes | `-size 1033c` |
| 不可執行 | `! -executable` |

> 三個條件之間 `find` 預設用 AND 串接（每個都要滿足）。`!` 是 NOT。

拿到密碼後登入下一關：

```bash
$ ssh bandit6@bandit.labs.overthewire.org -p 2220
```

過關 ✅

## 密碼

<details>
<summary>展開（請先自己嘗試）</summary>

```text
HWasnPhtq9AVKe0dmk45nxy20cvUa6EG
```

</details>

## 指令介紹

| 指令 / 選項 | 說明 |
|--------------|------|
| `find <path>` | 從 `<path>` 開始遞迴搜尋 |
| `-type f` | 只找一般檔案（f=file） |
| `-type d` | 只找目錄（d=directory） |
| `-type l` | 只找 symlink |
| `-size <N>c` | 大小剛好 N bytes（單位 `c`） |
| `-size +<N>c` | 大小**大於** N bytes |
| `-size -<N>c` | 大小**小於** N bytes |
| `-executable` | 可執行（owner 或 group 或 others 任一有 x） |
| `! <test>` | 邏輯 NOT，反轉條件 |
| `-readable` | 當前 user 可讀 |
| `-writable` | 當前 user 可寫 |
| `-user <name>` | owner 是 `<name>` |
| `-group <name>` | group 是 `<name>` |
| `-name <pattern>` | 檔名比對（支援 glob） |

### `-size` 單位速記

| 單位 | 意思 |
|------|------|
| `c` | bytes（character） |
| `k` | KiB（1024 bytes） |
| `M` | MiB |
| `G` | GiB |
| `b` | 512-byte blocks（預設，最容易踩雷）|

> 用 `c` 才是 bytes，沒寫單位 = 512-byte blocks，很容易誤算。

---

<div align="center">

**◀ [Level 4 → 5：找 human-readable 檔](../level05/)** · [🏠 回 Bandit 索引](../) · **下一關 ▶ _待寫_**

</div>
