# Bandit Level 32 → 33 — UPPERCASE Shell 逃逸

> 所有字母都被轉大寫，指令全部失效——但 `$0` 不是字母。

---

## 題目說明

登入後進入 UPPERCASE SHELL，所有輸入都被轉成大寫：

```
WELCOME TO THE UPPERCASE SHELL
>>
```

`ls` 變成 `LS`，什麼都執行不了。

---

## 解題步驟

輸入 `$0` 逃出 uppercase shell：

```
>> $0
$
```

取得正常 shell 後讀取密碼：

```bash
cat /etc/bandit_pass/bandit33
```

---

## 密碼

<details>
<summary>展開（先自己試過再看）</summary>

```
tQdtbs5D5i2vJwkO8mEyYEyTL8izoeJ0
```

</details>

---

## 這關學到什麼

- `$0` 是 shell 特殊變數，代表目前 shell 的名稱（如 `/bin/sh`）
- `$` 和 `0` 不是字母，不會被大寫轉換
- 輸入 `$0` 等於執行 `/bin/sh`，開啟正常子 shell

---

<div align="center">

**◀ [Level 31 → 32：git push](../level31/)** · [🏠 回 Bandit 索引](../README.md) · **[Level 33：完成 ▶](../level33/)**

</div>
