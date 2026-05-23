# Bandit Level 18 → 19 — 繞過 .bashrc 的 exit

> 登入就被踢出去——`.bashrc` 在搞鬼，但 ssh 可以在被踢前先做一件事。

---

## 題目說明

官方原文：

> The password for the next level is stored in a file readme in the homedirectory. Unfortunately, someone has modified .bashrc to log you out when you log in with SSH.

`.bashrc` 裡被加了 `exit`，登入後馬上被踢出。

---

## 為什麼會被踢出去？

`.bashrc` 是 bash **登入時自動執行的腳本**。有人在裡面加了 `exit`，所以：

```
你登入 → bash 執行 .bashrc → 遇到 exit → 連線關閉
```

在你輸入任何指令之前就結束了。

---

## 解法：ssh 直接執行指令

`ssh` 可以在最後加上指令，連線後直接執行，不開互動 shell：

```bash
ssh bandit18@bandit.labs.overthewire.org -p 2220 "cat readme"
```

這樣 `.bashrc` 的 `exit` 來不及作怪，指令就跑完了。

輸出：

```
cGWpMaKXVwDUNgPAVJbWYuGHVn9zl3j8
```

---

## 密碼

<details>
<summary>展開（先自己試過再看）</summary>

```
cGWpMaKXVwDUNgPAVJbWYuGHVn9zl3j8
```

</details>

---

## 這關學到什麼

- `.bashrc` 是登入時自動執行的腳本，可以被用來搞破壞
- `ssh user@host "指令"` 跳過互動 shell，直接執行單一指令
- 這個技巧常用在自動化腳本裡（不需要互動就能遠端執行指令）

---

<div align="center">

**◀ [Level 17 → 18：diff](../level17/)** · [🏠 回 Bandit 索引](../README.md) · **[Level 19 → 20：setuid ▶](../level19/)**

</div>
