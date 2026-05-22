# Bandit Level 10 → 11 — base64 解碼

> 密碼被 base64 編碼存起來，`base64 -d` 一行還原，認識這個網路上最常見的編碼格式。

---

## 題目說明

官方原文：

> The password for the next level is stored in the file `data.txt`, which contains base64 encoded data.

也就是說 — `data.txt` 裡的內容不是明文，是經過 base64 編碼的字串，需要解碼才能讀到密碼。

## 挑戰點

1. **base64 不是加密** — 看起來像亂碼，但沒有金鑰，任何人都能解；常被誤以為有安全性。
2. **結尾的 `=` 是 padding** — base64 以 3 bytes 為單位編碼，不足時補 `=`，是正常現象。

## 用到的指令

| 指令 | 用途 |
|------|------|
| `base64 -d` | 把 base64 字串解碼回原始內容 |
| `base64` | 把檔案或標準輸入編碼成 base64 |

### base64 重點

```bash
base64 -d FILE          # 解碼檔案
base64 FILE             # 編碼檔案（輸出到 stdout）
echo "hello" | base64   # 編碼字串 → aGVsbG8K
echo "aGVsbG8K" | base64 -d   # 解碼 → hello
```

> **base64 字符集**：A-Z、a-z、0-9、`+`、`/`，結尾補 `=` 對齊。看到只含這些字元的長字串，基本上就是 base64。

## 解題步驟

登入：

```bash
ssh bandit10@bandit.labs.overthewire.org -p 2220
# password: FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey
```

看一下 `data.txt`：

```bash
bandit10@bandit:~$ cat data.txt
VGhlIHBhc3N3b3JkIGlzIGR0UjE3M2ZaS2IwUlJzREZTR3NnMlJXbnBOVmozcVJyCg==
```

典型的 base64：只有英數字 + `=` 結尾。直接解碼：

```bash
bandit10@bandit:~$ base64 -d data.txt
The password is dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr
```

`dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr` 就是 bandit11 的密碼。

驗證登入：

```bash
ssh bandit11@bandit.labs.overthewire.org -p 2220
```

## 密碼

<details>
<summary>展開（先自己試過再看）</summary>

```
dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr
```

</details>

## base64 是什麼？

base64 把每 3 個 bytes（24 bits）轉成 4 個可印字元（每個 6 bits）：

```
原始：      M       a       n
ASCII：    77      97     110
二進位：  01001101 01100001 01101110
重新分組： 010011  010110  000101  101110
十進位：    19      22       5      46
base64：    T       W       F      u
```

結果 `Man` → `TWFu`，長度膨脹 4/3 倍。

**常見用途**：
- HTTP Basic Auth 的帳密傳輸
- Email 附件（MIME encoding）
- JWT 的 header 和 payload
- 在 JSON / XML 裡嵌入二進位資料（圖片、檔案）

**不是加密**：base64 是 encoding（編碼），目的是「讓 binary 能在文字通道傳輸」，不提供任何機密性。

## 一句話記法

> 「**`base64 -d` 解碼，`base64` 編碼**」——`-d` 是 decode，沒有 `-d` 就是 encode。

## 延伸閱讀（官方建議）

- `man base64`

---

<div align="center">

**◀ [Level 9 → 10：strings 從 binary 撈密碼](../level10/)** · [🏠 回 Bandit 索引](../README.md) · **下一關 Level 11 → 12 ▶ _待寫_**

</div>
