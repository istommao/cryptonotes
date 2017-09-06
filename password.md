# django 的密码方案


```python
def make_password(raw_password, salt=None, hasher='default'):
    hasher = get_hasher(hasher)
    if not salt:
        salt = hasher.salt()
    return hasher.encode(raw_password, salt)


def get_hashers():
    hashers = []
    for hasher_path in settings.PASSWORD_HASHERS:
        hasher_cls = import_string(hasher_path)
        hasher = hasher_cls()
        if not getattr(hasher, 'algorithm'):
            raise ImproperlyConfigured("hasher doesn't specify an "
                                       "algorithm name: %s" % hasher_path)
        hashers.append(hasher)
    return hashers


# global_settings.py
PASSWORD_HASHERS = [
    'django.contrib.auth.hashers.PBKDF2PasswordHasher',
    'django.contrib.auth.hashers.PBKDF2SHA1PasswordHasher',
    'django.contrib.auth.hashers.Argon2PasswordHasher',
    'django.contrib.auth.hashers.BCryptSHA256PasswordHasher',
    'django.contrib.auth.hashers.BCryptPasswordHasher',
]

```
