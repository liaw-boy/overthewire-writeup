# Bandit Level 30 → 31

## 目標
Clone git repo，README 是空的，密碼藏在 git tag 裡。

## 解題過程

```bash
git clone ssh://bandit30-git@bandit.labs.overthewire.org:2220/home/bandit30-git/repo
cd repo
cat README.md
# just an epmty file... muahaha
```

查看 tag：
```bash
git tag
# secret
```

查看 tag 內容：
```bash
git show secret
```

## 關鍵概念

- `git tag` 列出所有標籤
- `git show <tag>` 查看標籤內容
- git tag 通常用於版本號，但也可藏資料

## 密碼
`fb5S2xb7bRyFmAvQYQGEqsbhVyJqhnDy`
