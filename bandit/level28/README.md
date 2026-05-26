# Bandit Level 28 → 29 — git log 找歷史

> 密碼被遮掉了，但 git 記住了一切——`git log` 翻出過去的版本。

---

## 題目說明

官方原文：

> There is a git repository at ssh://bandit28-git@bandit.labs.overthewire.org/home/bandit28-git/repo via the port 2220.

---

## 解題步驟

```bash
git clone ssh://bandit28-git@bandit.labs.overthewire.org:2220/home/bandit28-git/repo
cd repo
cat README.md
# 密碼欄位顯示 xxxxxxxxxx
```

查看 git 歷史：

```bash
git log
```

找到 "fix info leak" 的前一個 commit，查看變更：

```bash
git show a3437bddd447f2d496731658e86b98cbea9d3c98
```

輸出顯示密碼從真實值被改成了 `xxxxxxxxxx`。

---

## 密碼

<details>
<summary>展開（先自己試過再看）</summary>

```
4pT1t5DENaYuqnqvadYs1oE4QLCdjmJ7
```

</details>

---

## 這關學到什麼

- git 保留所有歷史，刪除或遮掩的資料仍可從舊 commit 找回
- `git log` 查看提交歷史，`git show <hash>` 查看特定 commit 內容
- 不小心 commit 了密碼，即使後來刪除也要立刻輪換

---

<div align="center">

**◀ [Level 27 → 28：git clone](../level27/)** · [🏠 回 Bandit 索引](../README.md) · **[Level 29 → 30：git branch ▶](../level29/)**

</div>
