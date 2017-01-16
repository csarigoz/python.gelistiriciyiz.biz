---
title: "Python 3.6.0 ve underscore"
date: Jan 16, 2017 16:31
tags: py360,underscore
# subtitle:
# published: false
# cover: 
author:
  name: Uğur Özyılmazel
  email: ugurozyilmazel@gmail.com
  link: https://github.com/vigo
  bio: Pilavüstü Döner
  twitter: vigobronx
---

Tek altçizgi yani `_` (*underscore*) Python 3.6.0 ile çok kullanışlı bir araç
haline geldi.READ_MORE

Daha önce Ruby’de gördüğüm yöntem, artık Python 3.6.0’da da geçerli. `_` sayılarda
ayraç / separatör olarak kullanılabiliyor. [PEP 515: Underscores in Numeric Literals](https://www.python.org/dev/peps/pep-0515)

```python
decimal_number = 1_000_000     # 1000000
hexadecimal_number = 0xfff_fff # 16777215
binary = 0b_1111_1111          # 255
```

Buna ek olarak, bazı değerleri görmezden gelmek için de kullanılabiliyor:

```python
a, _, b = ("a", "ignore", "b") # a="a", b="b"
a, *_, b = ("a", 1, 2, 3, "b") # a="a", b="b"
```

Döngü esnasında da işe yarıyor:

```python
for _ in range(5):
    print("Merhaba")

# Merhaba
# Merhaba
# Merhaba
# Merhaba
# Merhaba
```

Eğer elimizde 2 elemanlı `tuple` listesi varsa:

```python
for _, second in [(1, 2), ("a", "b")]:
    print(second)

# 2
# b
```

şeklinde de kullanabiliyoruz.
