# Bandit Level 26 → 27

## 目標
從 vim 裡取得 bash shell，使用 bandit27-do setuid binary 讀取密碼。

## 解題過程

承接 Level 25，已在 vim 裡。在 vim 中設定 shell 為 bash：
```
:set shell=/bin/bash
:shell
```

取得 bash shell 後，使用 setuid binary：
```bash
./bandit27-do cat /etc/bandit_pass/bandit27
```

## 關鍵概念

- vim 的 `:set shell=` 可以指定要用哪個 shell
- `:shell` 從 vim 內部開啟一個 shell
- `bandit27-do` 有 setuid 權限，以 bandit27 身份執行指令

## 密碼
`upsNCc7vzaRDx6oZC6GiR6ERwe1MowGB`
