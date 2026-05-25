# Bandit Level 22 → 23 — cron + md5 推算檔名

> 腳本用 md5 hash 產生檔名——你看懂邏輯，自己算出來就行。

---

## 題目說明

官方原文：

> A program is running automatically at regular intervals from cron. Look in `/etc/cron.d/` for the configuration and see what command is being executed.

---

## 腳本內容

```bash
#!/bin/bash
myname=$(whoami)
mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)
echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"
cat /etc/bandit_pass/$myname > /tmp/$mytarget
```

腳本用 `whoami` 取得執行者名稱，再把 `I am user <名稱>` 做 md5 hash，結果當作 `/tmp/` 底下的檔名。

---

## 解題思路

腳本是 bandit23 在跑，所以 `myname=bandit23`。

你來模擬腳本的邏輯，算出檔名：

```bash
echo I am user bandit23 | md5sum | cut -d ' ' -f 1
# 8ca319486bfbbc3663ea0fbe81326349
```

直接讀那個檔案：

```bash
cat /tmp/8ca319486bfbbc3663ea0fbe81326349
```

---

## `md5sum | cut -d ' ' -f 1` 是什麼？

`md5sum` 輸出：`8ca319486bfbbc3663ea0fbe81326349  -`

`cut -d ' ' -f 1`：以空格切割，取第一欄 → 只留 hash 值。

---

## 密碼

<details>
<summary>展開（先自己試過再看）</summary>

```
0Zf11ioIjMVN551jX3CmStKLYqjk54Ga
```

</details>

---

<div align="center">

**◀ [Level 21 → 22：cron 基礎](../level21/)** · [🏠 回 Bandit 索引](../README.md) · **[Level 23 → 24：自寫腳本讓 cron 執行 ▶](../level23/)**

</div>
