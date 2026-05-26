# Bandit Level 30 → 31 — git tag

> README 空空的，commit 也沒料——但 tag 裡藏了東西。

---

## 題目說明

官方原文：

> There is a git repository at ssh://bandit30-git@bandit.labs.overthewire.org/home/bandit30-git/repo via the port 2220.

---

## 解題步驟

```bash
git clone ssh://bandit30-git@bandit.labs.overthewire.org:2220/home/bandit30-git/repo
cd repo
cat README.md
# just an epmty file... muahaha
```

查看 tag：

```bash
git tag
# secret
```

查看 tag 內容：

```bash
git show secret
# fb5S2xb7bRyFmAvQYQGEqsbhVyJqhnDy
```

---

## 密碼

<details>
<summary>展開（先自己試過再看）</summary>

```
fb5S2xb7bRyFmAvQYQGEqsbhVyJqhnDy
```

</details>

---

## 這關學到什麼

- `git tag` 列出所有標籤，通常用於版本號（`v1.0`）
- `git show <tag>` 查看標籤內容
- git 物件（commit、tag、blob）都可以用 `git show` 查看

---

<div align="center">

**◀ [Level 29 → 30：git branch](../level29/)** · [🏠 回 Bandit 索引](../README.md) · **[Level 31 → 32：git push ▶](../level31/)**

</div>
