# Bandit Level 25 → 26

## 目標
使用 bandit26.sshkey 登入 bandit26，但 bandit26 的 shell 不是 bash，會立刻退出。

## 解題過程

取得 SSH 金鑰：
```bash
cat bandit26.sshkey
```

將金鑰存到本機 `~/bandit26.key`，設定權限：
```bash
chmod 600 ~/bandit26.key
```

**關鍵**：把終端機視窗縮到只剩 2～3 行高，再 SSH 連線：
```bash
ssh -i ~/bandit26.key bandit26@bandit.labs.overthewire.org -p 2220
```

視窗夠小時，bandit26 的 shell（`more`）無法一次顯示完整內容，會停在 `--More--`。

在 `more` 裡按 `v` 進入 vim，然後讀取密碼：
```
:e /etc/bandit_pass/bandit26
```

## 關鍵概念

- bandit26 的 shell 是自訂程式，用 `more` 顯示文字後立刻退出
- 縮小視窗讓 `more` 暫停，再從 `more` 跳進 vim
- vim 可以用 `:e` 直接開啟任何有權限的檔案

## 密碼
`s0773xxkk0MXfdqOfPRVr9L3jJBUOgCZ`
