# Bandit Level 20 → 21 — setuid + 自建 server + 背景執行

> 這關要你同時扮演 server 和 client——`&` 把一個程式丟背景，讓兩件事同時發生。

---

## 題目說明

官方原文：

> There is a setuid binary `suconnect` that makes a connection to localhost on the port you specify. It reads a line of text and compares it to the password in the previous level. If the password is correct, it will transmit the password for the next level.

`suconnect` 有 setuid（bandit21 身份），它連到你指定的 port，收到 bandit20 的密碼後，回傳 bandit21 的密碼。

---

## 這關的架構

```
你開一個 server（nc）在背景等待
    ↓
suconnect 連進來
    ↓
nc 自動送出 bandit20 的密碼
    ↓
suconnect 驗證正確 → 送回 bandit21 的密碼
```

任何網路連線都有兩端——**server 等待，client 主動連**。這關要你同時扮演兩個角色。

---

## 解題步驟

**第一步**：背景開 nc server，連線進來時自動送出密碼：

```bash
echo "0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO" | nc -l -p 59999 &
```

| 部分 | 意思 |
|------|------|
| `echo "密碼"` | 準備要送出的內容 |
| `\|` | 把 echo 輸出接到 nc 的輸入 |
| `nc -l -p 59999` | 開 server 監聽 port 59999 |
| `&` | 丟到背景，不卡住終端機 |

**第二步**：執行 suconnect 連到那個 port：

```bash
./suconnect 59999
```

輸出：

```
Read: 0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO
Password matches, sending next password
EeoULMCra2q0dSkYj561DX7s1CpBuOBt
```

---

## 密碼

<details>
<summary>展開（先自己試過再看）</summary>

```
EeoULMCra2q0dSkYj561DX7s1CpBuOBt
```

</details>

---

## 這關學到什麼

- `&` 把指令丟到背景，讓你繼續在同一個 terminal 操作
- `nc -l -p PORT` 開 server 監聽
- server/client 模型是所有網路通訊的基礎

---

<div align="center">

**◀ [Level 19 → 20：setuid](../level19/)** · [🏠 回 Bandit 索引](../README.md) · **[Level 21 → 22：cron 基礎 ▶](../level21/)**

</div>
