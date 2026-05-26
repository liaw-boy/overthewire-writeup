# Bandit Level 28 → 29

## 目標
Clone git repo，密碼在 README 裡被遮掉了，要從歷史 commit 找回來。

## 解題過程

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

找到 "fix info leak" 的前一個 commit，查看差異：
```bash
git show a3437bddd447f2d496731658e86b98cbea9d3c98
```

## 關鍵概念

- git 保留所有歷史，即使刪除或遮掩過的資料仍可找回
- `git log` 查看提交歷史
- `git show <hash>` 查看特定 commit 的變更內容
- 現實啟示：不小心 commit 了密碼，即使後來刪除也要立刻輪換

## 密碼
`4pT1t5DENaYuqnqvadYs1oE4QLCdjmJ7`
