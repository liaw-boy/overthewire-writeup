# Bandit Level 21 → 22 — cron 排程追蹤

> cron 定時跑腳本，腳本把密碼寫到 /tmp——追蹤路徑就能拿到。

---

## 題目說明

官方原文：

> A program is running automatically at regular intervals from cron. Look in `/etc/cron.d/` for the configuration and see what command is being executed.

---

## 追蹤路徑

**步驟 1**：看 cron 設定
```bash
cat /etc/cron.d/cronjob_bandit22
# * * * * * bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
```

每分鐘用 bandit22 身份執行腳本。

**步驟 2**：看腳本內容
```bash
cat /usr/bin/cronjob_bandit22.sh
```

```bash
#!/bin/bash
chmod 644 /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
cat /etc/bandit_pass/bandit22 > /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
```

腳本把 bandit22 密碼寫到 `/tmp/` 底下，權限 644（所有人可讀）。

**步驟 3**：直接讀
```bash
cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
```

---

## 密碼

<details>
<summary>展開（先自己試過再看）</summary>

```
tRae0UfB9v0UzbCdn9cY0gQnds9GF58Q
```

</details>

---

## cron 語法速查

```
* * * * * 使用者 指令
│ │ │ │ └── 星期幾 (0-7)
│ │ │ └──── 月份 (1-12)
│ │ └────── 日 (1-31)
│ └──────── 時 (0-23)
└────────── 分 (0-59)
```

`* * * * *` = 每分鐘執行一次。

---

<div align="center">

**◀ [Level 20 → 21：背景執行](../level20/)** · [🏠 回 Bandit 索引](../README.md) · **[Level 22 → 23：cron + md5 ▶](../level22/)**

</div>
