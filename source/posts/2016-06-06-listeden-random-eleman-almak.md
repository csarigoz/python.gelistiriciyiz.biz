---
title: "Liste’den random eleman almak"
date: Jun 06, 2016 12:02
tags: random
author:
  name: Uğur Özyılmazel
  email: ugurozyilmazel@gmail.com
  link: http://ugur.ozyilmazel.com
  bio: Yazılım Geliştiricisi
---

Bir liste (*dizi*) içinden random (*rastgele*) eleman almak:

```python
import random

users = ["vigo", "lego", "mego", "fugo"]
print random.choice(users) # python 2.7+
```