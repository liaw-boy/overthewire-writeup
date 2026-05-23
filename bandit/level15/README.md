# Bandit Level 15 → 16 — openssl s_client SSL 加密傳輸

> `nc` 傳明文，`openssl s_client` 傳加密——就像 http 和 https 的差別。

---

## 題目說明

官方原文：

> The password for the next level can be retrieved by submitting the password of the current level to port 30001 on localhost using SSL/TLS encryption.

跟上一關一樣，但這次要用 SSL/TLS 加密。

---

## nc vs openssl s_client

| | nc | openssl s_client |
|--|--|--|
| 傳輸 | 明文 | SSL 加密 |
| 中間被攔截 | 看得到內容 | 只看到亂碼 |
| 用途 | 一般 port | HTTPS、加密服務 |

---

## 解題步驟

```bash
openssl s_client -connect localhost:30001
```

連上後會噴一大堆憑證資訊（SSL 握手過程），等游標停住看到 `read R BLOCK`，貼上密碼按 Enter：

```
kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx
Correct!
kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx
```

---

## 遇到 KEYUPDATE 怎麼辦

加上 `-ign_eof` 參數：

```bash
openssl s_client -connect localhost:30001 -ign_eof
```

---

## 密碼

<details>
<summary>展開（先自己試過再看）</summary>

```
kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx
```

</details>

---

## 這關學到什麼

- `openssl s_client -connect host:port` = SSL 加密連線
- SSL 握手完成後才能輸入，`read R BLOCK` 是「我準備好了」的提示
- `-ign_eof` 防止遇到 KEYUPDATE 時自動斷線

---

<div align="center">

**◀ [Level 14 → 15：nc 傳密碼](../level14/)** · [🏠 回 Bandit 索引](../README.md) · **[Level 16 → 17：nmap 掃 port ▶](../level16/)**

</div>
