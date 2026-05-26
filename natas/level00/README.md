# Natas Level 0 → 1

## 目標
密碼藏在頁面裡，但看不到。

## 解題過程

登入後頁面只顯示 "You can find the password for the next level on this page."

用 `Cmd+U` 查看原始碼，找到 HTML 註解：
```html
<!--The password for natas1 is 0nzCigAq7t2iALyvU9xcHlYN4MlkIwlq -->
```

## 關鍵概念

- HTML 註解 `<!-- -->` 在瀏覽器不顯示，但原始碼看得到
- 開發者常把測試資料、密碼留在註解裡忘記刪掉

## 密碼
`0nzCigAq7t2iALyvU9xcHlYN4MlkIwlq`
