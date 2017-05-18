# 分组密码

`密码算法分为 分组密码和流密码 两种`

> 分组密码每次只处理特定长度的一块数据

## 分组密码的模式

> 由于分组密码每次只加密特定长度的数据，而明文长度很可能超过分组的长度，这时就需要对分组密码
算法进行迭代，而迭代的方法就称为分组密码的模式

**主要模式**

- ECB模式: Electronic CodeBook mode (电子密码本模式)
- CBC模式: Cipher Block Chaining mode (密码分组链接模式)
- CFB模式: Cipher FeedBack mode (密文反馈模式)
- OFB模式: Output FeedBack mode (输出反馈模式)
- CTR模式: CounTeR mode (计时器模式)
