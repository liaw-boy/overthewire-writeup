# Bandit Level 29 → 30

## 目標
Clone git repo，密碼藏在其他分支裡。

## 解題過程

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

## 關鍵概念

- `git branch -a` 列出所有本地與遠端分支
- `git checkout <branch>` 切換分支
- dev 分支常放有密碼的開發設定，不代表比 master 安全

## 密碼
`qp30ex3VLz5MDG1n91YowTv4Q8l7CDZL`
