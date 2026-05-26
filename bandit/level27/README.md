# Bandit Level 27 → 28 — git clone over SSH

> 密碼不在伺服器上，在一個 git repo 裡——clone 下來就拿到了。

---

## 題目說明

官方原文：

> There is a git repository at ssh://bandit27-git@bandit.labs.overthewire.org/home/bandit27-git/repo via the port 2220. The password for the user bandit27-git is the same as for the user bandit27.

---

## 解題步驟

在本機執行：

```bash
git clone ssh://bandit27-git@bandit.labs.overthewire.org:2220/home/bandit27-git/repo
cd repo
cat README
```

密碼就在 README 裡。

---

## 密碼

<details>
<summary>展開（先自己試過再看）</summary>

```
Yz9IpL0sBcCeuG7m9uQFt8ZNpS4HZRcN
```

</details>

---

## 這關學到什麼

- `git clone ssh://用戶@主機:port/路徑` — SSH 方式 clone repo
- git 不限定 GitHub，任何跑 git server 的主機都可以

---

<div align="center">

**◀ [Level 26 → 27：vim shell](../level26/)** · [🏠 回 Bandit 索引](../README.md) · **[Level 28 → 29：git log ▶](../level28/)**

</div>
