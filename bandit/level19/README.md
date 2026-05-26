# Bandit Level 19 → 20 — setuid 借用其他使用者身份

> 權限不夠？借一把有 setuid 的程式，暫時變成它的擁有者。

---

## 題目說明

官方原文：

> To gain access to the next level, you should use the setuid binary in the homedirectory.

home 目錄有一個 setuid 程式，用它來讀只有 bandit20 能讀的密碼。

---

## 什麼是 setuid？

看 `bandit20-do` 的權限：

```
-rwsr-x---   1 bandit20 bandit19
```

正常的 `x` 變成了 `s`——這叫 **setuid**。

**意思**：執行這個程式時，身份變成**檔案擁有者**（bandit20），而不是執行者（你 bandit19）。

---

## 解題步驟

先看看怎麼用：

```bash
./bandit20-do
# Run a command as another user.
# Example: ./bandit20-do whoami
```

驗證確實是 bandit20：

```bash
./bandit20-do whoami
# bandit20
```

用 bandit20 的身份讀密碼：

```bash
./bandit20-do cat /etc/bandit_pass/bandit20
# 0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO
```

---

## 密碼

<details>
<summary>展開（先自己試過再看）</summary>

```
0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO
```

</details>

---

## 權限格式複習

```
r w s  r - x  - - -
擁有者  群組  其他人
```

- `r` = 可讀，`w` = 可寫，`x` = 可執行，`-` = 無
- `s` 取代 `x` 的位置 = setuid 開啟且可執行

---

## 這關學到什麼

- setuid 讓你「借用」檔案擁有者的身份執行程式
- 這是 Linux 權限提升的基本概念
- 很多安全漏洞就是濫用 setuid——如果 setuid 程式有漏洞，攻擊者可以用更高權限執行任意指令

---

<div align="center">

**◀ [Level 18 → 19：繞過 bashrc](../level18/)** · [🏠 回 Bandit 索引](../README.md) · **[Level 20 → 21：nc listener + setuid ▶](../level20/)**

</div>
