# RSA加密

`什么是RSA`
> 1977年，三位数学家Rivest、Shamir 和 Adleman 设计了一种算法，可以实现非对称加密。这种算法用他们三个人的名字命名，叫做RSA算法。
> RSA算法基于一个十分简单的数论事实：将两个大质数相乘十分容易，但是想要对其乘积进行因式分解却极其困难，因此可以将乘积公开作为加密密钥。
>

`阮一峰的RSA算法笔记`
- [RSA算法原理（一）](http://www.ruanyifeng.com/blog/2013/06/rsa_algorithm_part_one.html)
- [RSA算法原理（二）](http://www.ruanyifeng.com/blog/2013/07/rsa_algorithm_part_two.html)

> RSA是公钥加密的一种(也叫非对称加密)

 `1976年以前，所有的加密方法都是同一种模式`
> 那就是加密与解密用同样的规则(密钥)
> 而公钥加密的出现改变了这样的模式

## 非对称加密
> 公钥加密的信息只有私钥解得开，那么只要私钥不泄漏，通信就是安全的

- 小明生成两把钥匙(公钥和私钥), 公钥可以公开，任何人都可以获得，而私钥必须保密
- 小强获得了小明的公钥，使用它加密信息
- 小明获得加密信息后，用私钥解密

## 使用cryptography进行简单的RSA实践

`https://github.com/pyca/cryptography`

```python
from cryptography.hazmat.primitives.asymmetric import rsa, padding
from cryptography.hazmat.primitives import hashes
from cryptography.hazmat.backends import default_backend

# 生成私钥
key_size = 2048
private_key = rsa.generate_private_key(
    public_exponent=65537,
    key_size=key_size,
    backend=default_backend()
)
# 根据私钥获取公钥
public_key = private_key.public_key()

# 公钥加密
algorithm = hashes.SHA256()
oaep_padding = padding.OAEP(
     mgf=padding.MGF1(algorithm=algorithm),
     algorithm=algorithm,
     label=None
 )

message = 'Hello RSA'
ciphertext = public_key.encrypt(message.encode(), oaep_padding)

# 私钥解密
data = private_key.decrypt(ciphertext, padding_data)

# 私钥签名
pss_padding = padding.PSS(
    mgf=padding.MGF1(algorithm),
    salt_length=padding.PSS.MAX_LENGTH
)
sign_data = private_key.sign(message.encode(), pss_padding, hashes.SHA256())

# 公钥验签
public_key.verify(sign_data, message.encode(), pss_padding, hashes.SHA256())
```
