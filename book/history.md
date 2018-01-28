# 密码学简史

## 凯撒密码（Caesar cipher）

> 凯撒密码的加密：通过将明文中所使用的字母表按照一定的字数"平移"来进行加密
> 用凯撒密码进行加密，密钥为3

![](./_image/CaesarCipher.png)

![](./_image/CaesarCipherEncrypt.png)

`简单示例`
```python
def caesar_cipher(sentence, step=3):
    return ''.join([chr(ord(c) + (step)) if c != ' ' else ' ' for c in sentence])

ciphertext = caesar_cipher('Hello Caesar cipher')
print(ciphertext)
```

## Enigma (二战德国使用)
