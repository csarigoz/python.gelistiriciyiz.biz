---
title: "Dictionary'i güzel yazdırmak"
date: Apr 28, 2016 14:39
tags: dict,pprint
subtitle: PrettyPrinter’dan daha pretty!
# cover: 
---

Dictionary’i daha düzgün görüntülemek için `json` desteği;

```python
import json

def pp(hash, indent=4, sort_keys=True):
    print json.dumps(dict(hash), indent=indent, sort_keys=sort_keys)
```

Yapmanız gereken `pp(BURAYA_DICTIONARY_GELSIN)`