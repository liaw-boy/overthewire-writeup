# Bandit Level 32 → 33

## 目標
登入後進入 UPPERCASE SHELL，所有輸入都被轉成大寫，無法執行一般指令。

## 解題過程

登入後看到：
```
WELCOME TO THE UPPERCASE SHELL
>>
```

輸入 `$0` 逃出 uppercase shell：
```
>> $0
$
```

取得正常 shell 後讀取密碼：
```bash
cat /etc/bandit_pass/bandit33
```

## 關鍵概念

- UPPERCASE shell 把所有字母輸入轉大寫，`ls` → `LS`
- `$0` 是 shell 特殊變數，代表目前 shell 的名稱（如 `/bin/sh`）
- `$` 和 `0` 不是字母，不會被大寫轉換
- 輸入 `$0` 等於執行 `/bin/sh`，開啟新的正常 shell

## 密碼
`tQdtbs5D5i2vJwkO8mEyYEyTL8izoeJ0`
