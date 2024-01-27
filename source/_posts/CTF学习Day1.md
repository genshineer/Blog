---
title: CTF学习Day1
date: 2023-11-25 22:00:07
tags: "技术类"
katex: true
---

尝试两个例题：

## 将 $16$ 进制编码转化为 `Base64` 编码（[Convert hex to base64](https://cryptopals.com/sets/1/challenges/1)）。

##### Input

`49276d206b696c6c696e6720796f757220627261696e206c696b65206120706f69736f6e6f7573206d757368726f6f6d`

##### Output

`SSdtIGtpbGxpbmcgeW91ciBicmFpbiBsaWtlIGEgcG9pc29ub3VzIG11c2hyb29t`

`Python` 居然有可以直接用的函数，甚至可以直接解码成明文。。。

```python
import base64
msg = '49276d206b696c6c696e6720796f757220627261696e206c696b65206120706f69736f6e6f7573206d757368726f6f6d'
s = bytes.fromhex(msg)
ans = base64.b64encode(s)
print(ans)
```

其中 `s` 为明文，`ans` 为 `Base64` 加密结果。

## $16$ 进制下的异或（[Fixed XOR](https://cryptopals.com/sets/1/challenges/2)）

##### Input

```
1c0111001f010100061a024b53535009181c
686974207468652062756c6c277320657965
```

##### Output

```
746865206b696420646f6e277420706c6179
```

直接映射到十进制下进行异或，这样的代码还是 `c++` 好使。

```cpp
#include <bits/stdc++.h>
using namespace std;

string s1, s2;
map<char, int> m;
map<int, char> M;

signed main() {
    cin >> s1 >> s2;
    for (int i = 0; i < 10; i++) m[i + '0'] = i, M[i] = i + '0';
    for (int i = 0; i < 6; i++) m[i + 'a'] = i + 10, M[i + 10] = i + 'a';
    for (int i = 0; i < s1.size(); i++) cout << M[m[s1[i]] ^ m[s2[i]]];
}
```

这两个 `RuoZhi`（~~神仙~~）题目还能用掉我一小时，

果然是我太 `RuoZhi` 了。
