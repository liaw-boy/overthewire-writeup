# Bandit Level 31 → 32

## 目標
Push 一個檔案到遠端 repo，但 .gitignore 擋住了 .txt 檔案。

## 解題過程

```bash
git clone ssh://bandit31-git@bandit.labs.overthewire.org:2220/home/bandit31-git/repo
cd repo
cat .gitignore
# *.txt
```

建立檔案（注意不能有多餘換行）：
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

## 關鍵概念

- `.gitignore` 讓 git 忽略特定檔案
- `git add -f` 強制加入被 ignore 的檔案
- `echo -n` 不加換行符號

## 密碼
`3O9RfhqyAlVBEZpVb6LYStshZoqoSx5K`
