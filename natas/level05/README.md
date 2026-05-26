# Natas Level 5 → 6

## 目標
伺服器用 cookie `loggedin` 判斷登入狀態，預設值為 0。

## 解題過程

登入後顯示 "Access disallowed. You are not logged in"

F12 → Application → Cookies，找到：
```
loggedin = 0
```

直接雙擊改成：
```
loggedin = 1
```

重新整理頁面，取得密碼。

## 關鍵概念

- Cookie 存在瀏覽器，可以用 F12 直接修改
- 用 `loggedin=0/1` 做認證完全不安全
- 伺服器應該用 session token 驗證，而非信任客戶端 cookie 的值

## 密碼
`0RoJwHdSKWFTYR5WuiAewauSuNaBXned`
