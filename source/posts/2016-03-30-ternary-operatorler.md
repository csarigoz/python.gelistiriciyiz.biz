---
title: Ternary Operatörler
date: Mar 30, 2016 10:51
tags: ternary, ternary operator, conditional, conditional operator
author:
  name: "Ali GÖREN"
  email: "goren.ali@yandex.com"
  link: "https://aligoren.com"
  bio: "Python Sevicisi"
---
Tek satırda if kullanma işlemini ternary operatör ile yaparız.

**Açıklama**

  kosul_dogru_ise_yapilacak if kosul else kosul_yanlis_ise_yapilacak

Örnek vermek gerekirse

```python
durum = True
"Şu an True" if durum else "Şu an False" # 'Şu an True'
```

Bu işlemin haricinde tuple'ları kullanarak da ternary operatörler gerçekleştirebiliriz.
Burada bilmemiz gereken tuple içindeki sol değer, False, sağ değer ise True'ya karşılık gelmektedir.

**Açıklama**

  (kosul_yanlis_ise, kosul_dogru_ise)[kosul]

Bunu daha da açık olarak şöyle gösterebiliriz:

```python
is_alive = True
("Ölmüş", "Yaşıyor")[is_alive]
'Yaşıyor'
```

Tek satırda for iterasyonu da yapabiliriz:

```python
hayvanlar = ["kedi", "kopek", "fare", "panda", "kuş", "keçi"]
hayvan = [hyv for hyv in hayvanlar]
hayvan[0] # "kedi"

"".join(str(i) for i in range(10)) # 123456789
```
