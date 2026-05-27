# Natas Level 8 → 9

## 目標
原始碼有編碼後的 secret，需要逆向還原原始值。

## 解題過程

原始碼顯示編碼函式：
```php
$encodedSecret = "3d3d516343746d4d6d6c315669563362";

function encodeSecret($secret) {
    return bin2hex(strrev(base64_encode($secret)));
}
```

編碼步驟：`secret → base64_encode → strrev → bin2hex`

逆向還原（步驟相反）：
```bash
echo "3d3d516343746d4d6d6c315669563362" | xxd -r -p | rev | base64 -d
# 輸出：oubWYf2kBq
```

把 `oubWYf2kBq` 輸入表單，取得密碼。

## 關鍵概念

- 編碼（encoding）≠ 加密（encryption），完全可逆推
- `xxd -r -p`：hex 轉 binary；`rev`：字串反轉；`base64 -d`：base64 解碼
- 知道編碼步驟，反向操作即可還原

## 密碼
`ZE1ck82lmdGIoErlhQgWND6j2Wzz6b6t`
