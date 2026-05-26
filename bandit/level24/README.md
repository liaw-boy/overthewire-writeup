# Bandit Level 24 → 25

## 目標
Port 30002 上的 daemon 需要你傳入 bandit24 的密碼加上一個 4 位數 PIN（0000～9999），暴力破解找出正確 PIN。

## 解題過程

建立工作目錄：
```bash
mkdir /tmp/mywork25 && cd /tmp/mywork25
```

寫一個 script 產生所有 10000 種組合：
```bash
nano gen.sh
```

內容：
```bash
#!/bin/bash
for i in $(seq -w 0000 9999); do
    echo "gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8 $i"
done
```

```bash
chmod +x gen.sh
```

一次把所有組合 pipe 進 nc，過濾掉錯誤回應：
```bash
./gen.sh | nc localhost 30002 | grep -v "Wrong"
```

## 關鍵概念

- `seq -w 0000 9999`：產生帶前導零的 4 位數序列
- 單一連線傳送所有組合，比開 10000 次連線快很多
- `grep -v "Wrong"`：反向過濾，只留下正確答案

## 密碼
`iCi86ttT4KSNe1armKiwbQNmB3YJP3q4`
