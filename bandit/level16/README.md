# Bandit Level 16 → 17 — nmap 掃 port + 找 SSL server

> 一千個 port 裡找那一個——先掃哪些有開，再試哪個說 SSL。

---

## 題目說明

官方原文：

> The credentials for the next level can be retrieved by submitting the password of the current level to a port on localhost in the range 31000 to 32000. First find out which of these ports have a server listening on them. Then find out which of those speak SSL/TLS and which don't.

31000~32000 之間只有一個 port 會給你下一關的私鑰，其他是 echo server（把你說的原樣送回來）。

---

## 第一步：nmap 掃 port

`nmap` 是 port 掃描器，去敲每一個 port 的門，看哪些有人應答：

```bash
nmap localhost -p 31000-32000
```

輸出：

```
PORT      STATE SERVICE
31046/tcp open  unknown
31518/tcp open  unknown
31691/tcp open  unknown
31790/tcp open  unknown
31960/tcp open  unknown
```

5 個 port 有開。

---

## 第二步：找 SSL server

用 `openssl s_client` 逐一試——有憑證噴出來 = SSL server；`no peer certificate` = 不是 SSL。

```bash
openssl s_client -connect localhost:31790 -ign_eof
```

看到憑證資訊後，貼上密碼：

```
kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx
Correct!
-----BEGIN RSA PRIVATE KEY-----
...
-----END RSA PRIVATE KEY-----
```

這次拿到的是私鑰，不是密碼——跟 Level 13 一樣，用私鑰登入 bandit17。

---

## 第三步：用私鑰登入

把私鑰存到本地，然後：

```bash
ssh -i bandit17.key bandit17@bandit.labs.overthewire.org -p 2220
cat /etc/bandit_pass/bandit17
```

---

## 密碼

<details>
<summary>展開（先自己試過再看）</summary>

```
EReVavePLFHtFlFsjn3hyzMlvSuSAcRD
```

</details>

---

## 這關學到什麼

- `nmap -p 範圍` 掃描開放的 port
- 有憑證 = SSL；`no peer certificate` = 不是 SSL
- echo server 把你的輸入原樣送回；正確 server 回 `Correct!` + 私鑰

---

<div align="center">

**◀ [Level 15 → 16：SSL 加密](../level15/)** · [🏠 回 Bandit 索引](../README.md) · **[Level 17 → 18：diff 比較檔案 ▶](../level17/)**

</div>
