# Natas Level 2 → 3

## 目標
頁面原始碼有圖片連結，發現可瀏覽的目錄。

## 解題過程

原始碼找到：
```html
<img src="files/pixel.png">
```

直接瀏覽目錄：
```
http://natas2.natas.labs.overthewire.org/files/
```

看到 `users.txt`，打開後：
```
natas3:3gqisGdR0pjm6tpkDKdIWO2hSvchLeYH
```

## 關鍵概念

- 伺服器未禁止目錄列表（Directory Listing）
- 任何人都能瀏覽目錄內容
- 應設定 `Options -Indexes` 關閉目錄列表

## 密碼
`3gqisGdR0pjm6tpkDKdIWO2hSvchLeYH`
