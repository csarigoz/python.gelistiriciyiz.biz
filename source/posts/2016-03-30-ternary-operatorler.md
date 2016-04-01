---
title: Ternary Operatörler
date: Mar 30, 2016 10:51
tags: ternary,conditional operator
author:
  name: "Ali GÖREN"
  email: "goren.ali@yandex.com"
  link: "https://aligoren.com"
  bio: "Python Sevicisi"
---
Tek satırda `if` kullanma işlemini **ternary** operatör ile yaparız.

    True if KOŞUL else False

Örnek vermek gerekirse;

```python
status = True
"True" if status else "False" # 'True'
```

Bu işlemin haricinde `Tuple`’ları kullanarak da ternary operatörler 
gerçekleştirebiliriz. Burada bilmemiz gereken **Tuple** içindeki sol 
değer `False`, sağ değer ise `True`’ya karşılık gelmektedir.

    (False, True)[KOŞUL]

Bunu daha da açık olarak şöyle gösterebiliriz;

```python
from __future__ import unicode_literals
is_alive = True
print u"%s" % (u"Ölmüş", u"Yaşıyor")[is_alive] # Yaşıyor
```

