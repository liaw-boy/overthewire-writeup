# Bandit Level 7 → 8 — grep 在大檔裡撈關鍵字

> 第一次處理「幾千行的純文字檔」，學 `grep` 怎麼當你的 Ctrl+F。

---

## 題目說明

官方原文：

> The password for the next level is stored in the file `data.txt` next to the word `millionth`.

也就是 — `data.txt` 裡有一堆「英文單字 + 隨機字串」的配對，找到 `millionth` 那行，旁邊就是密碼。

## 挑戰點

1. **`data.txt` 很大** — 幾千行，直接 `cat` 會把你 terminal 洗到看不到頂。
2. **要學會用關鍵字過濾** — 第一次出場的 `grep`，是後面很多關卡的基本工具。
3. **欄位分隔是 tab** — 輸出長得像 `millionth	<密碼>`，中間是 tab 不是空白，複製密碼時要小心。

## 解題過程

登入：

```bash
ssh bandit7@bandit.labs.overthewire.org -p 2220
# password: morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj
```

先看看 home 目錄有什麼：

```bash
bandit7@bandit:~$ ls -al
-rw-r----- 1 bandit8 bandit7 4.0K ... data.txt
```

確認檔案在了，直接 `grep` 撈關鍵字：

```bash
bandit7@bandit:~$ grep millionth data.txt
millionth	4CKMh1JI91bUIZZPXDqGanal4xvAg0JM
```

只有一行命中，tab 之後那一串就是 `bandit8` 的密碼。

登入下一關驗證：

```bash
ssh bandit8@bandit.labs.overthewire.org -p 2220
```

## 密碼

<details>
<summary>展開（先自己試過再看）</summary>

```
4CKMh1JI91bUIZZPXDqGanal4xvAg0JM
```

</details>

## 指令介紹

### grep 基本用法

```text
grep [選項] PATTERN FILE
```

| 寫法 | 說明 |
|------|------|
| `grep millionth data.txt` | 印出含 `millionth` 的所有行 |
| `grep -i Hello f.txt` | 忽略大小寫 |
| `grep -n word f.txt` | 同時印出行號 |
| `grep -v word f.txt` | 反向：印出**不含**關鍵字的行 |
| `grep -c word f.txt` | 只回報命中幾行（count） |
| `grep -r word .` | 從當前目錄遞迴搜所有檔 |
| `grep -E 'a\|b' f.txt` | 啟用 ERE 正則（支援 `\|` 等） |
| `grep -F 'a.b.c' f.txt` | 關閉正則，當純字串比對（fixed string） |

### 後續常配的工具（先有印象就好）

| 工具 | 用途 |
|------|------|
| `cut -f2` | 用 tab 切欄位，只取第 N 欄 |
| `awk '{print $2}'` | 比 `cut` 更彈性，用空白/tab 分欄 + 條件判斷 |
| `wc -l` | 算行數，常拿來確認過濾結果 |
| `sort` / `uniq` | 排序、去重，下一關（Level 8→9）會用 |

### 一條龍寫法示範

只切出密碼（不要 `millionth` 那欄）：

```bash
grep millionth data.txt | cut -f2
# 4CKMh1JI91bUIZZPXDqGanal4xvAg0JM
```

用 `awk` 一步搞定（不用 pipe）：

```bash
awk '/millionth/ {print $2}' data.txt
# 4CKMh1JI91bUIZZPXDqGanal4xvAg0JM
```

### 為什麼不用 `cat data.txt | grep millionth`

很多新手會這樣寫，能跑但**多餘**，會被資深工程師笑「Useless Use Of Cat」（UUOC）。`grep` 本身就吃檔案參數，不需要先 `cat` 再 pipe 進去。

```bash
# 多此一舉
cat data.txt | grep millionth

# 正確
grep millionth data.txt
```

## 延伸閱讀（官方建議）

- `man grep`
- `man cut`

---

<div align="center">

**◀ [Level 6 → 7：全機 find（owner/group/size）](../level07/)** · [🏠 回 Bandit 索引](../README.md) · **[Level 8 → 9：sort + uniq 找唯一行](../level09/) ▶**

</div>
