# Bandit Level 29 → 30 — git branch

> master 沒有，dev 有——密碼藏在另一條分支裡。

---

## 題目說明

官方原文：

> There is a git repository at ssh://bandit29-git@bandit.labs.overthewire.org/home/bandit29-git/repo via the port 2220.

---

## 解題步驟

```bash
git clone ssh://bandit29-git@bandit.labs.overthewire.org:2220/home/bandit29-git/repo
cd repo
cat README.md
# 顯示 <no passwords in production!>
```

查看所有分支：

```bash
git branch -a
# remotes/origin/dev
# remotes/origin/master
# remotes/origin/sploits-dev
```

切換到 dev 分支：

```bash
git checkout dev
cat README.md
```

密碼就在 dev 分支的 README.md 裡。

---

## 密碼

<details>
<summary>展開（先自己試過再看）</summary>

```
qp30ex3VLz5MDG1n91YowTv4Q8l7CDZL
```

</details>

---

## 這關學到什麼

- `git branch -a` 列出所有本地與遠端分支
- `git checkout <branch>` 切換分支
- dev 分支不代表比 master 安全，有 repo 存取權就能看所有分支

---

<div align="center">

**◀ [Level 28 → 29：git log](../level28/)** · [🏠 回 Bandit 索引](../README.md) · **[Level 30 → 31：git tag ▶](../level30/)**

</div>
