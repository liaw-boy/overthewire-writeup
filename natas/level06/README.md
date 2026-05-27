# Natas Level 6 → 7

## 目標
輸入正確 secret 才能取得密碼，secret 從外部檔案 include 進來。

## 解題過程

原始碼顯示：
```php
include "includes/secret.inc";
if($secret == $_POST['secret']) { ... }
```

直接瀏覽 include 的檔案：
```
http://natas6.natas.labs.overthewire.org/includes/secret.inc
```

取得：
```php
$secret = "FOEIUWGHFEEUHOFUOIU";
```

把 `FOEIUWGHFEEUHOFUOIU` 輸入表單，取得密碼。

## 關鍵概念

- PHP `include` 檔案放在 web root 可公開存取的目錄裡
- 機密設定檔應放在 web root 之外，或設定伺服器拒絕直接存取

## 密碼
`bmg8SvU1LizuWjx3y7xkNERkHxGre0GS`
