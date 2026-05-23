# Bandit Level 11 → 12 — ROT13 凱撒密碼

> 字母換了位置就不算加密——ROT13 是最入門的「移位密碼」，`tr` 一行搞定。

---

## 題目說明

官方原文：

> The password for the next level is stored in the file `data.txt`, where all lowercase (a-z) and all uppercase (A-Z) letters have been rotated by 13 positions.

---

## 先登入，看看檔案長什麼樣

```bash
ssh bandit11@bandit.labs.overthewire.org -p 2220
# password: dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr
```

登入後，先讀一下 `data.txt`：

```bash
cat data.txt
```

你會看到類似這樣的輸出：

```
Gur cnffjbeq vf 7k16JArUVv5LxVuJfsSVdbbtaHGlw9D4
```

---

## 停一下，先觀察

**問自己**：這串文字有什麼特徵？

- 它有空格，有大小寫字母，結構上看起來像一個英文句子。
- 但意思完全不通——`Gur`、`cnffjbeq` 是什麼字？
- 數字和符號（`7k16J...`）看起來沒有被動過。

這個特徵給你什麼提示？

<details>
<summary>想想看，再展開</summary>

> 「只有字母被動過，數字和空格沒有」——這是移位密碼的典型行為。
> 題目說「rotated by 13 positions」，這個操作叫 **ROT13**。

</details>

---

## ROT13 是什麼？

字母表有 26 個字母。ROT13 就是把每個字母往後移 13 格：

```
A → N
B → O
C → P
...
M → Z
N → A   ← 到 Z 之後，從 A 繞回來
...
Z → M
```

**問自己**：如果 A 移 13 格變成 N，那 N 移 13 格會變成什麼？

<details>
<summary>算一下再展開</summary>

> N 再移 13 格 = N + 13 = 第 27 格 = 繞回第 1 格 = **A**。
>
> 所以 ROT13 **加密和解密是同一個操作**——對同一串文字做兩次 ROT13，會回到原文。

</details>

---

## 用什麼工具還原？

Linux 有個指令叫 `tr`（transliterate），可以做逐字元替換。

先試試看一個簡單的例子——把所有大寫轉小寫：

```bash
echo "HELLO" | tr 'A-Z' 'a-z'
```

輸出：`hello`

`tr 'SET1' 'SET2'` 的邏輯是：**SET1 裡的第 N 個字元，換成 SET2 裡的第 N 個字元**。

---

## 動手設計 ROT13 的對應表

ROT13 的大寫對應是：

```
原始： A B C D E F G H I J K L M  N O P Q R S T U V W X Y Z
替換： N O P Q R S T U V W X Y Z  A B C D E F G H I J K L M
```

用 `tr` 的範圍語法來表達：

- 原始：`A-Z`（A 到 Z）
- 替換：`N-ZA-M`（N 到 Z，然後接 A 到 M）

**問自己**：小寫的部分要怎麼寫？

<details>
<summary>試著自己填，再展開</summary>

```
原始小寫： a-z
替換小寫： n-za-m
```

所以完整的 `tr` 指令是：

```bash
tr 'A-Za-z' 'N-ZA-Mn-za-m'
```

</details>

---

## 執行解密

把 `cat data.txt` 的輸出接進 `tr`：

```bash
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```

你應該看到：

```
The password is 7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4
```

驗證登入：

```bash
ssh bandit12@bandit.labs.overthewire.org -p 2220
```

---

## 密碼

<details>
<summary>展開（先自己試過再看）</summary>

```
7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4
```

</details>

---

## 這關學到什麼？

| 概念 | 要點 |
|------|------|
| ROT13 | 字母移 13 位，加解密同一操作，不是真正的加密 |
| `tr 'SET1' 'SET2'` | 逐字元替換，支援範圍語法 `A-Z` |
| 範圍拼接 | `N-ZA-M` = N 到 Z 再接 A 到 M，處理繞回的問題 |
| pipe `\|` | 把一個指令的輸出接到下一個指令的輸入 |

**延伸練習**：

1. 試著把 `The password is ...` 再 ROT13 一次，應該會回到 `Gur cnffjbeq vf ...`
2. 試試 `echo "Hello World" | tr 'A-Za-z' 'N-ZA-Mn-za-m'`，觀察空格和大小寫的行為

---

## 延伸閱讀

- `man tr`

---

<div align="center">

**◀ [Level 10 → 11：base64 解碼](../level10/)** · [🏠 回 Bandit 索引](../README.md) · **下一關 Level 12 → 13 ▶ _待寫_**

</div>
