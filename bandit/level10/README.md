# Bandit Level 9 → 10 — strings 從二進位檔裡撈可讀文字

> `cat` 噴亂碼不是壞掉——是檔案本來就是二進位的。`strings` 幫你把人類看得懂的部分挖出來。

---

## 題目說明

官方原文：

> The password for the next level is stored in the file `data.txt` in one of the few human-readable strings, preceded by several '=' characters.

也就是說 — `data.txt` 是個混合了大量 binary 垃圾資料的檔案，密碼就藏在少數幾條可讀字串裡，而且那行前面有好幾個 `=` 號。

## 挑戰點

1. **`cat` 直接噴亂碼** — 檔案是 binary，終端機會被奇怪字元洗版，甚至讓 shell 顯示異常。
2. **`grep` 對 binary 檔預設只回報「Binary file matches」** — 要加 `-a` 才會把 binary 當純文字處理。
3. **密碼不在第一行** — 需要過濾出「前面有 `=` 號」的行才能快速定位。

## 用到的指令

| 指令 | 用途 |
|------|------|
| `strings` | 從任何檔案（含 binary）抽出長度 ≥ 4 的可印字元序列 |
| `grep` | 再過濾含 `=` 的行，縮小範圍 |

### strings 重點

```bash
strings FILE          # 預設：抽出長度 ≥ 4 的可讀字串，每行一條
strings -n 6 FILE     # 調整最短長度為 6（過濾掉更短的雜訊）
strings -t x FILE     # 同時印出每條字串在檔案裡的 hex offset（分析 binary 時很有用）
```

> **原理**：`strings` 掃描檔案的每個 byte，把連續 N 個以上的可印 ASCII 字元（0x20–0x7E）當作一條字串輸出，其餘 binary 全部忽略。

## 解題步驟

登入（用上一關拿到的密碼）：

```bash
ssh bandit9@bandit.labs.overthewire.org -p 2220
# password: <level08 解出的密碼>
```

先確認 `data.txt` 是什麼性質：

```bash
bandit9@bandit:~$ file data.txt
data.txt: data
```

`file` 回報 `data`（不是 `ASCII text`），確認是 binary。直接 `cat` 會亂碼，改用 `strings`：

```bash
bandit9@bandit:~$ strings data.txt
# 輸出很多雜訊字串...
```

再用 `grep` 過濾有 `=` 的行：

```bash
bandit9@bandit:~$ strings data.txt | grep '='
========== theG)
========== password
=ke
========== is
========== FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey
```

含多個 `=` 的那幾行就是密碼提示，最後一條 `FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey` 就是密碼。

驗證登入下一關：

```bash
ssh bandit10@bandit.labs.overthewire.org -p 2220
```

## 密碼

<details>
<summary>展開（先自己試過再看）</summary>

```
FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey
```

</details>

## 為什麼不能直接 `grep = data.txt`

```bash
bandit9@bandit:~$ grep '=' data.txt
Binary file data.txt matches
```

`grep` 偵測到 binary 內容，預設只回報「有沒有命中」，不印出實際內容。解法：

```bash
# 方法一（推薦）：先用 strings 轉成純文字再 grep
strings data.txt | grep '='

# 方法二：強迫 grep 把 binary 當文字（可能有亂碼）
grep -a '=' data.txt
```

## file 指令補充

`file` 會根據檔案內容的 magic bytes 判斷類型，是快速確認「這是什麼東西」的好工具：

```bash
file data.txt          # data（binary）
file /bin/ls           # ELF 64-bit LSB executable...
file README.md         # ASCII text
file image.png         # PNG image data, 800 x 600...
```

遇到不知道是什麼的檔案，`file` 先跑一下是好習慣。

## 一句話記法

> 「**binary 檔先 `strings`，再 `grep` 關鍵字**」——`strings` 是 binary 世界的翻譯官。

## 延伸閱讀（官方建議）

- `man strings`
- `man grep`

---

<div align="center">

**◀ [Level 8 → 9：sort + uniq 找唯一行](../level09/)** · [🏠 回 Bandit 索引](../README.md) · **[Level 10 → 11：base64 解碼](../level11/) ▶**

</div>
