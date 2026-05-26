# Bandit Level 27 → 28

## 目標
從 git repository clone 下來，找到密碼。

## 解題過程

在本機執行：
```bash
git clone ssh://bandit27-git@bandit.labs.overthewire.org:2220/home/bandit27-git/repo
cd repo
cat README
```

密碼就在 README 裡。

## 關鍵概念

- `git clone ssh://用戶@主機:port/路徑` — SSH 方式 clone repo
- 密碼直接放在 README，最基本的 git 操作

## 密碼
`Yz9IpL0sBcCeuG7m9uQFt8ZNpS4HZRcN`
