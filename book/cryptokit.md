# cryptokit更轻松的在python中实现加密解密

> github 地址: https://github.com/istommao/cryptokit

## 安装
> pip install cryptokit

## AES 使用

```python
from cryptokit import AESCrypto

message = "hello cryptokit"
crypto = AESCrypto('WDMG1e38igW53YuxkE0SsKUDeLbULAtL',  'm2VYHdx41zRgvg6f')

data = crypto.encrypt(message, mode='cbc')
# b'\xaa<\x9d\xe9\xde\x0b\xd7\xe9\xfd\xac\xfc\xdd\x9f\xe2V\xd4'
crypto.decrypt(data)
# 'hello cryptokit'
```

## RSA 使用

### 加密解密
```python
from cryptokit import RSACrypto
private_key = RSACrypto.generate_private_key(2048)
public_key = private_key.public_key()

message = 'Hello cryptokit'
ciphertext = RSACrypto.encrypt(message, public_key, algorithm='sha256')
plaintext = RSACrypto.decrypt(ciphertext, private_key, algorithm='sha256')
plaintext == message
# True
```
### 签名验签
```python
from cryptokit import RSACrypto
private_key = RSACrypto.generate_private_key(2048)
public_key = private_key.public_key()

message = 'Hello cryptokit'
signature = RSACrypto.sign(message, private_key, algorithm='sha256')

result = RSACrypto.verify(message, signature, public_key, algorithm='sha256')
# result = True
```

## pkcs12 (PFX文件相关)
```python
from cryptokit import load_pfx, get_pubkey_from_pfx

# 加载pfx文件
pkcs12 = load_pfx(pfx_file, password='password')
# 获取证书
cert = pkcs12.get_certificate()

# 获取公钥
pubkey = get_pubkey_from_pfx(pfx_file, password='password')
# or use cert get pubkey
pubkey = cert.get_pubkey().to_cryptography_key()

# 生成pfx文件
from cryptokit import generate_pfx
pfx_data = generate_pfx(cert, friendly_name, private_key)
```
