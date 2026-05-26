# Bandit Level 25 → 26 — more / vim 逃逸

> 登入成功，卻立刻被踢出——因為 shell 根本不是 bash，而是一個會自動退出的程式。縮小視窗是解題關鍵。

---

## 題目說明

官方原文：

> Logging in to bandit26 from bandit25 should be fairly easy… The shell for user bandit26 is not /bin/bash, but something else. Find out what it is, how it works and how to break out of it.

家目錄有 `bandit26.sshkey`，可以 SSH 進 bandit26。但 bandit26 的 shell 不是 bash，登入後立刻退出。

---

## 解題步驟

取得 SSH 金鑰：

```bash
cat bandit26.sshkey
```

存到本機（Mac）：

```bash
nano ~/bandit26.key
chmod 600 ~/bandit26.key
```

**關鍵**：把終端機視窗縮到只剩 2～3 行高，再連線：

```bash
ssh -i ~/bandit26.key bandit26@bandit.labs.overthewire.org -p 2220
```

視窗夠小時，bandit26 的 shell（`more`）無法顯示完整內容，停在 `--More--`。

在 `more` 裡按 `v` 進入 vim，讀取密碼：

```
:e /etc/bandit_pass/bandit26
```

---

## 密碼

<details>
<summary>展開（先自己試過再看）</summary>

```
s0773xxkk0MXfdqOfPRVr9L3jJBUOgCZ
```

</details>

---

## 這關學到什麼

- `/etc/passwd` 記錄每個用戶的 shell，可以是任意程式
- 縮小視窗讓 `more` 暫停，是繞過自動退出 shell 的手段
- `more` 裡按 `v` 可以呼叫 `$VISUAL`（預設 vim）

---

<div align="center">

**◀ [Level 24 → 25：暴力破解 PIN](../level24/)** · [🏠 回 Bandit 索引](../README.md) · **[Level 26 → 27：vim shell ▶](../level26/)**

</div>
