# Bandit Level 14 → 15 — nc 送密碼到指定 port

> `localhost` 是自己，port 是門牌號碼——`nc` 讓你敲任何一扇門說話。

---

## 題目說明

官方原文：

> The password for the next level can be retrieved by submitting the password of the current level to port 30000 on localhost.

把目前的密碼送到 `localhost:30000`，就能拿到下一關的密碼。

---

## 觀念：localhost 和 port

- **localhost** = 自己這台機器（127.0.0.1）
- **port** = 同一台機器上不同服務的入口，就像大樓裡不同房間的門牌號碼

---

## 工具：nc（netcat）

`nc` 是網路界的瑞士刀，可以連到任何 host:port 傳送文字：

```bash
nc 主機 port
```

連上後游標停住，等你輸入，輸入什麼就送什麼過去。

---

## 解題步驟

登入 bandit14，取得自己的密碼：

```bash
cat /etc/bandit_pass/bandit14
# MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS
```

連到 port 30000：

```bash
nc localhost 30000
```

游標停住後貼上密碼按 Enter：

```
MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS
Correct!
8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo
```

---

## 密碼

<details>
<summary>展開（先自己試過再看）</summary>

```
8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo
```

</details>

---

## 這關學到什麼

- `nc host port` 連線後就像打電話，你說什麼對方收到什麼
- localhost = 自己，port = 服務入口
- 明文傳輸——網路上任何人都能看到你傳的內容（下一關會解決這個問題）

---

<div align="center">

**◀ [Level 13 → 14：SSH 私鑰](../level13/)** · [🏠 回 Bandit 索引](../README.md) · **[Level 15 → 16：SSL 加密傳輸 ▶](../level15/)**

</div>
