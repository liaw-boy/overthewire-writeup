# Bandit Level 31 → 32 — git push + .gitignore 繞過

> .gitignore 擋掉了 .txt，但 `git add -f` 強制加進去。

---

## 題目說明

官方原文：

> There is a git repository at ssh://bandit31-git@bandit.labs.overthewire.org/home/bandit31-git/repo via the port 2220. Push a file to the remote repository.

需要 push 一個指定內容的檔案：
- 檔名：`key.txt`
- 內容：`May I come in?`
- 分支：`master`

---

## 解題步驟

```bash
git clone ssh://bandit31-git@bandit.labs.overthewire.org:2220/home/bandit31-git/repo
cd repo
cat .gitignore
# *.txt
```

建立檔案（用 `-n` 避免多餘換行）：

```bash
echo -n 'May I come in?' > key.txt
```

強制加入被 ignore 的檔案：

```bash
git add -f key.txt
git commit -m "add key.txt"
git push origin master
```

伺服器驗證後在 remote 訊息回傳密碼。

---

## 密碼

<details>
<summary>展開（先自己試過再看）</summary>

```
3O9RfhqyAlVBEZpVb6LYStshZoqoSx5K
```

</details>

---

## 這關學到什麼

- `.gitignore` 讓 git 忽略特定檔案，但 `git add -f` 可強制加入
- `echo -n` 不加換行符號
- `.gitignore` 是保護，不是存取控制，任何有 repo 寫入權的人都能繞過

---

<div align="center">

**◀ [Level 30 → 31：git tag](../level30/)** · [🏠 回 Bandit 索引](../README.md) · **[Level 32 → 33：UPPERCASE shell ▶](../level32/)**

</div>
