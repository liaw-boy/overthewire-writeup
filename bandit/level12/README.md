# Bandit Level 12 → 13 — hexdump 還原 + 反覆解壓縮

> 一個檔案可以被壓縮很多層——`file` 指令告訴你現在是什麼格式，剝一層再剝一層。

---

## 題目說明

官方原文：

> The password for the next level is stored in the file `data.txt`, which is a hexdump of a file that has been repeatedly compressed.

`data.txt` 是一個二進位檔案的 hexdump，而那個二進位檔案被反覆壓縮了很多層。

---

## 先登入，看看檔案

```bash
ssh bandit12@bandit.labs.overthewire.org -p 2220
# password: 7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4
```

```bash
head data.txt
```

輸出長這樣：

```
00000000: 1f8b 0808 ...
```

左欄是位址，中間是 hex，右邊是 ASCII——這是 hexdump 格式，不是文字。

---

## 第一步：認出格式

前兩個 byte 是 `1f 8b`——這是 **gzip** 的 magic number。

每種檔案格式開頭都有固定 bytes，`file` 指令就是靠這個判斷格式，跟副檔名無關。

---

## 第二步：建暫存目錄

home 目錄沒有寫入權限，先建工作區：

```bash
TMPDIR=$(mktemp -d)
cp ~/data.txt $TMPDIR/
cd $TMPDIR
```

---

## 第三步：hexdump 還原成二進位

```bash
xxd -r data.txt > data.bin
file data.bin
# data.bin: gzip compressed data
```

`xxd -r` 把 hexdump 反向轉回二進位。

---

## 第四步：剝洋蔥

固定步驟：`file` 看格式 → 對應工具解壓 → 重複。

| 格式 | 解壓指令 | 注意 |
|------|---------|------|
| gzip | `mv x x.gz && gunzip x.gz` | 需要 `.gz` 副檔名 |
| bzip2 | `mv x x.bz2 && bunzip2 x.bz2` | 需要 `.bz2` 副檔名 |
| tar | `tar xf x` | 直接解，不需改名 |

完整過程：

```
data.bin (gzip) → gunzip → data.bin (bzip2)
→ bunzip2 → data.bin (gzip) → gunzip → data.bin (tar)
→ tar xf → data5.bin (tar) → tar xf → data6.bin (bzip2)
→ bunzip2 → data6.bin (tar) → tar xf → data8.bin (gzip)
→ gunzip → data8.bin (ASCII text) ✓
```

```bash
cat data8.bin
# The password is FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn
```

---

## 密碼

<details>
<summary>展開（先自己試過再看）</summary>

```
FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn
```

</details>

---

## 這關學到什麼

- **Magic number**：每種格式開頭有固定 bytes，`file` 靠這判斷，跟副檔名無關
- **`xxd -r`**：hexdump 還原成二進位
- **剝洋蔥法則**：`file` → 看格式 → 解壓 → 重複，直到 ASCII text

---

<div align="center">

**◀ [Level 11 → 12：ROT13](../level11/)** · [🏠 回 Bandit 索引](../README.md) · **[Level 13 → 14：SSH 私鑰 ▶](../level13/)**

</div>
