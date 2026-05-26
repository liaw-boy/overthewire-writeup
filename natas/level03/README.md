# Natas Level 3 → 4

## 目標
原始碼暗示「連 Google 都找不到」，密碼藏在 robots.txt 指向的目錄。

## 解題過程

原始碼找到：
```html
<!-- No more information leaks!! Not even Google will find it this time... -->
```

查看 robots.txt：
```
http://natas3.natas.labs.overthewire.org/robots.txt
```

內容：
```
User-agent: *
Disallow: /s3cr3t/
```

瀏覽隱藏目錄：
```
http://natas3.natas.labs.overthewire.org/s3cr3t/
```

找到 `users.txt`，內含密碼。

## 關鍵概念

- `robots.txt` 是給搜尋引擎的「請勿爬取」清單，但本身是公開的
- `Disallow` 不是存取控制，只是請求，任何人都能直接訪問被 Disallow 的路徑
- robots.txt 反而暴露了隱藏目錄的位置

## 密碼
`QryZXc2e0zahULdHrtHxzyYkj59kUxLQ`
