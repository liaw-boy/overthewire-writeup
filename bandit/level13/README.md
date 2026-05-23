# Bandit Level 13 → 14 — SSH 私鑰登入

> 不需要密碼也能登入——SSH 金鑰認證用數學證明你是你。

---

## 題目說明

官方原文：

> You don't get the next password, but you get a private SSH key that can be used to log into the next level.

這關給你一把私鑰，用它直接登入 bandit14，不需要密碼。

---

## 什麼是 SSH 金鑰認證？

平常登入：你輸入密碼 → 伺服器驗證。

金鑰認證：

```
你持有「私鑰」 ←配對→ 伺服器持有「公鑰」
```

伺服器出一道只有對應私鑰才能解的數學題，你解出來就證明你是你，完全不需要傳密碼。就像家裡的鑰匙——公鑰是鎖，私鑰是鑰匙。

---

## 登入 bandit13

```bash
ssh bandit13@bandit.labs.overthewire.org -p 2220
# password: FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn
```

```bash
ls
# sshkey.private
```

---

## 用私鑰登入

`ssh` 的 `-i` 參數（identity file）指定私鑰：

```bash
ssh -i 私鑰路徑 使用者@主機 -p 埠號
```

**注意**：不能從 bandit 伺服器內部 SSH 回自己（被封鎖）。要從本地機器執行。

### Windows 步驟

1. `cat ~/sshkey.private` 複製全部內容
2. 在 PowerShell 存成本地檔案：

```powershell
@"
（貼上私鑰內容）
"@ | Set-Content -Encoding ASCII C:\Users\你的名字\bandit14.key
```

3. SSH 登入：

```powershell
ssh -i C:\Users\你的名字\bandit14.key bandit14@bandit.labs.overthewire.org -p 2220
```

### Linux/macOS 步驟

```bash
# 存私鑰
cat > ~/bandit14.key << 'EOF'
（貼上私鑰內容）
EOF
chmod 600 ~/bandit14.key

# 登入
ssh -i ~/bandit14.key bandit14@bandit.labs.overthewire.org -p 2220
```

登入後：

```bash
cat /etc/bandit_pass/bandit14
```

---

## 密碼

<details>
<summary>展開（先自己試過再看）</summary>

```
MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS
```

</details>

---

## 這關學到什麼

- **`-i`**：SSH 指定私鑰的參數
- **`chmod 600`**：私鑰權限必須設為只有自己能讀，SSH 會拒絕太開放的私鑰
- **Windows 換行問題**：記事本存的檔案有 `\r\n`，SSH 只認 `\n`，要用 `Set-Content -Encoding ASCII`

---

<div align="center">

**◀ [Level 12 → 13：hexdump 解壓縮](../level12/)** · [🏠 回 Bandit 索引](../README.md) · **[Level 14 → 15：nc 傳送密碼 ▶](../level14/)**

</div>
