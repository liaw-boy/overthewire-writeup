# Bandit Level 17 → 18 — diff 找出兩檔案的差異

> 兩個檔案只有一行不同——`diff` 一秒找出來。

---

## 題目說明

官方原文：

> There are 2 files in the homedirectory: passwords.old and passwords.new. The password for the next level is in passwords.new and is the only line that has been changed between passwords.old and passwords.new.

`passwords.new` 裡唯一被改過的那行就是密碼。

---

## 解題步驟

```bash
diff passwords.old passwords.new
```

輸出：

```
42c42
< KxOU4IzbXM8j8HeAWPAXTd1eC77mp1qV
---
> x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO
```

解讀：
- `<` = passwords.old 的第 42 行（舊的）
- `>` = passwords.new 的第 42 行（新的）
- 密碼在 `passwords.new`，所以取 `>` 那行

---

## 密碼

<details>
<summary>展開（先自己試過再看）</summary>

```
x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO
```

</details>

---

## 這關學到什麼

- `diff 檔案1 檔案2` 比較兩個檔案的差異
- `<` 是第一個檔案的內容，`>` 是第二個檔案的內容
- `42c42` 意思是「第 42 行被改了」（c = change）

---

<div align="center">

**◀ [Level 16 → 17：nmap 掃 port](../level16/)** · [🏠 回 Bandit 索引](../README.md) · **[Level 18 → 19：繞過 bashrc ▶](../level18/)**

</div>
