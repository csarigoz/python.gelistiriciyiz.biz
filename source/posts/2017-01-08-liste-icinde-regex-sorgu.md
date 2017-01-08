---
title: "Listede Regular Expression sorgusu yapmak"
date: Jan 08, 2017 21:25
tags: regex, unicode
author:
  name: Çağrı Sarıgöz
  email: cagri.sarigoz@gmail.com
  link: http://cagrisarigoz.com
  bio: Data Science Heveslisi
  twitter: cagrisarigoz
---

Bir liste içerisinde yer alan string’ler üzerinde Python’un `re` modülü 
ile regular expression sorgu döndürebiliriz.READ_MORE
Aşağıdaki örnekte `mumlar` listesinde çift sayıda mum barındıran string’leri 
filtreleyeceğiz:

```python
# -*- coding: utf-8 -*-

import re

mumlar = [
    u'bir mumdur', u'iki mumdur',
    u'üç mumdur', u'dört mumdur',
    u'ondört mumdur',
]

regex = re.compile(u'iki|dört', re.UNICODE)
cevap = [mum for mum in mumlar if regex.search(mum)]
```

Elde ettiğimiz `cevap` listesi aşağıdaki gibi olacaktır:

```python
>>> cevap
['iki mumdur', 'dört mumdur', 'ondört mumdur']
```
