---
title: "Listede Regular Expression Sorgusu Yapmak"
date: Jan 08, 2017 18:05
tags: regex
author:
  name: Çağrı Sarıgöz
  email: cagri.sarigoz@gmail.com
  link: https://cagrisarigoz.com
  bio: Data Science Heveslisi
  twitter: cagrisarigoz
---

Bir liste içerisinde yer alan string'ler üzerinde Python'un `re` modülü ile regular expression sorgu döndürebiliriz.READ_MORE

Aşağıdaki örnekte mumlar listesinde çift sayıda mum barındıran string'leri filtreleyeceğiz.

```python
import re

mumlar = ['bir mumdur', 'iki mumdur', 'uc mumdur', 'dort mumdur', 'on dort mumdur']
regex = re.compile('iki|dort')
ciftMumlar = [i for i in mumlar if regex.search(i)]
```

Elde ettiğimiz `ciftMumlar` listesi aşağıdaki gibi olacaktır.

```python
>>> ciftMumlar
['iki mumdur', 'dört mumdur', 'on dört mumdur']
```
