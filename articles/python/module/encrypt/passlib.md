# passlib

## 安装

```
pip install passlib
```

## 加密

```py
from passlib.hash import pbkdf2_sha256

hash = pbkdf2_sha256.hash("123456")
```

## 验证

```py
from passlib.hash import pbkdf2_sha256

hash = pbkdf2_sha256.hash("123456")
print(pbkdf2_sha256.verify("123456"), hash)  # True
print(pbkdf2_sha256.verify("111222"), hash)  # False
```
