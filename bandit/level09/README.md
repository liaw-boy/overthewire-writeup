# Bandit Level 8 → 9 — sort + uniq 找「只出現一次」的那行

> 幾千行幾乎一樣的資料，密碼藏在唯一一行沒有重複的文字裡——用 `sort` 整理 + `uniq` 過濾一行解決。

---

## 題目說明

官方原文：

> The password for the next level is stored in the file `data.txt` and is the only line of text that occurs only once.

也就是說 — `data.txt` 裡大多數行都有重複出現，只有**一行**是唯一的，那一行就是密碼。

## 挑戰點

1. **`uniq` 有個大陷阱** — 它只去除「相鄰」的重複行；如果相同的行散落在不同地方，`uniq` 不會認出來。
2. **解法是組合技** — 先 `sort` 把相同的行排在一起，再 `uniq -u` 只印出出現一次的行。
3. **`-u` vs 不加旗標的差異** — 不加旗標的 `uniq` 只是去重，`-u` 才是「只保留唯一行」，行為完全不同。

## 用到的指令

| 指令 | 用途 |
|------|------|
| `sort` | 對文字行做排序，讓相同的行相鄰 |
| `uniq -u` | 只輸出「在輸入裡只出現過一次」的行 |

### sort 重點

```bash
sort data.txt        # 預設：依字典序升冪排列
sort -r data.txt     # 降冪
sort -n data.txt     # 數字排序（10 > 9，不是字典序）
sort -u data.txt     # 排序後同時去重（等同 sort | uniq）
```

### uniq 重點

```bash
uniq file            # 去除「相鄰」重複行（要先 sort 才有意義）
uniq -u file         # 只印出唯一行（整份輸入裡只出現 1 次）
uniq -d file         # 只印出有重複的行（至少出現 2 次）
uniq -c file         # 每行前加上出現次數，方便肉眼 debug
```

> **關鍵概念**：`uniq` 只比對「當前行」和「前一行」是否相同。所以一定要先 `sort` 讓相同的行連在一起，`uniq` 才能正確計數。

## 解題步驟

登入：

```bash
ssh bandit8@bandit.labs.overthewire.org -p 2220
# password: 4CKMh1JI91bUIZZPXDqGanal4xvAg0JM
```

看一下 `data.txt` 的規模，建立直覺：

```bash
bandit8@bandit:~$ wc -l data.txt
1001 data.txt
```

1001 行。先用 `uniq -c` 確認重複分佈（前幾行示意）：

```bash
bandit8@bandit:~$ sort data.txt | uniq -c | head -5
     10 07KC3ukwX7kswbgqs5WKjDobQMQCGEXv
     10 0efnqHJ7TKNxaF8bkCRJsCbHrRAG5PeK
     10 0N65GBAssK3IyYHqBCMBJZGBMzPiBOsH
     10 1fuU3Pf8bvRK0GBvhFqYHSX3p3aFJKjF
     10 ...
```

幾乎每行都出現 10 次，找那個出現 1 次的：

```bash
bandit8@bandit:~$ sort data.txt | uniq -u
4CKMh1JI91bUIZZPXDqGanal4xvAg0JM
```

只有一行輸出，就是密碼。

驗證登入下一關：

```bash
ssh bandit9@bandit.labs.overthewire.org -p 2220
```

## 密碼

<details>
<summary>展開（先自己試過再看）</summary>

```
4CKMh1JI91bUIZZPXDqGanal4xvAg0JM
```

</details>

## 常見錯誤

### 直接 `uniq -u` 而不先 `sort`

```bash
# 錯誤示範
bandit8@bandit:~$ uniq -u data.txt
# 輸出一大堆行，因為相同的行沒有相鄰
```

`uniq` 只看「與前一行是否相同」，沒先排序就用，等於沒用。

### 用 `sort -u` 想一步解決

```bash
# 結果是去重後的所有唯一值，不是「只出現一次」的行
bandit8@bandit:~$ sort -u data.txt
# 把每種行各留一條，1001 行變成 100 多行——仍然不對
```

`sort -u` 是「去重」（deduplicate），不是「找唯一」（find unique）。

## 一句話記法

> 「**先 sort，再 uniq -u**」— sort 讓相同的手牽手，uniq -u 只留落單的那張牌。

## 延伸閱讀（官方建議）

- `man sort`
- `man uniq`

---

<div align="center">

**◀ [Level 7 → 8：grep 在大檔裡撈關鍵字](../level08/)** · [🏠 回 Bandit 索引](../README.md) · **[Level 9 → 10：strings 從 binary 撈密碼](../level10/) ▶**

</div>
