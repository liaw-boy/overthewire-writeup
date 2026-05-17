# Bandit Level 0 – SSH 登入

> 第一關，學會用 `ssh` 連到遊戲伺服器。

---

## 題目說明

使用 SSH 登入遊戲伺服器。

官方原文：

> The goal of this level is for you to log into the game using SSH.
> The host to which you need to connect is `bandit.labs.overthewire.org`, on port `2220`.
> The username is `bandit0` and the password is `bandit0`.
> Once logged in, go to the [Level 1 page](https://overthewire.org/wargames/bandit/bandit1.html) to find out how to beat Level 1.

## 連線資訊

| 項目 | 內容 |
|------|------|
| Host | `bandit.labs.overthewire.org` |
| Port | `2220` |
| Username | `bandit0` |
| Password | `bandit0` |

## 指令

```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
```

## 解題過程

```text
$ ssh bandit0@bandit.labs.overthewire.org -p 2220
The authenticity of host '[bandit.labs.overthewire.org]:2220 ...' can't be established.
ED25519 key fingerprint is SHA256:...
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
bandit0@bandit.labs.overthewire.org's password: bandit0

                         _                     _ _ _
                        | |__   __ _ _ __   __| (_) |_
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_
                        |_.__/ \__,_|_| |_|\__,_|_|\__|

                       This is an OverTheWire game server.
                ...
bandit0@bandit:~$
```

看到 `bandit0@bandit:~$` prompt 代表登入成功，第一關完成 ✅

## 密碼

<details>
<summary>展開 / Expand（請先自己嘗試 / try yourself first）</summary>

Level 0 的密碼**題目已經告訴你**：`bandit0`。

下一關（`bandit1`）的密碼要登入後從 home 目錄的 `readme` 取得，留到下一篇紀錄。

</details>

## 指令介紹

| 指令 / 選項 | 說明 |
|--------------|------|
| `ssh` | Secure Shell，用於遠端加密連線 |
| `user@host` | 指定登入帳號與目標主機 |
| `-p <port>` | 指定連接埠（SSH 預設為 22，這裡用 2220） |
| `-l <user>` | 另一種指定帳號的寫法（等同 `user@host`） |
| `-i <keyfile>` | 用指定的私鑰登入（未來要免密碼登入會用到） |
| `exit` 或 `Ctrl+D` | 登出遠端 session |

## Helpful Reading Material（官方建議閱讀）

官方頁面下方推薦的延伸閱讀：

- [Secure Shell (SSH) on Wikipedia](https://en.wikipedia.org/wiki/Secure_Shell) — 弄清楚 SSH 的歷史、為什麼要加密、跟 telnet 的差別
- [How to use SSH with a non-standard port on It's FOSS](https://itsfoss.com/ssh-to-port/) — 為什麼這關要 `-p 2220`
- [How to use SSH with ssh-keys on wikiHow](https://www.wikihow.com/Use-SSH) — 公鑰認證入門

---

<div align="right">

**下一關 ▶ [Level 0 → 1：讀取 home 目錄的檔案](../level01/)**

</div>

<div align="center">

[🏠 回 Bandit 索引](../README.md) · [📋 全站首頁](../../README.md)

</div>
