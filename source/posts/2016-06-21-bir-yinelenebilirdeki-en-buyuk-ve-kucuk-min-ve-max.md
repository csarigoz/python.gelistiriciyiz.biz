---
title: "Bir yinelenebilirdeki en büyük ve küçük: `min` ve `max`"
date: Jun 21, 2016 14:08
tags: builtin-functions
author:
  name: Uğur Özyılmazel
  email: ugurozyilmazel@gmail.com
  link: http://ugur.ozyilmazel.com
  bio: Yazılım Geliştiricisi
---

Bir yinelenebilirdeki (*iterable*) en yüksek ve en düşük değeri bulmak için:

```python
a = [1, 2, 3, 4]
max(a) # 4
min(a) # 1
```

Eğer **integer** cinsinden iki tane argüman alırsa;

```python
max(1, 100) # 100
min(1, 100) # 1
```

Eğer yinelenebilirin elemanları `string` cinsindense alfabetik sıralamaya
göre işlem yapılır:

```python
names = ["vigo", "jim", "commodore", "atari"]
max(names) # 'vigo'  -- v harfi ile başlıyor
min(names) # 'atari' -- a harfi ile başlıyor
```

Eğer `string` cinsinden tek bir argüman verilirse bu argüman `byte-array` olarak
yorumlanır, yani karakterlerden oluşan bir liste olur;

```python
max("Merhaba millet, ben vigo") # 'v' -- alfabetik olarak v harfi
min("Merhaba millet, ben vigo") # ' ' -- space karakteri ilk sırada
```

ASCII tablosunun bir kısmına baktığımızda;

    32 -  
    33 - !
    34 - "
    35 - #
    36 - $
    37 - %
    38 - &
    39 - '
    40 - (
    41 - )
    42 - *
    43 - +
    44 - ,
    45 - -
    46 - .
    47 - /
    48 - 0
    49 - 1
    50 - 2
    51 - 3
    52 - 4
    53 - 5
    54 - 6
    55 - 7
    56 - 8
    57 - 9
    58 - :
    59 - ;
    60 - <
    61 - =
    62 - >
    63 - ?
    64 - @
    65 - A
    66 - B
    67 - C
    68 - D
    69 - E
    70 - F
    71 - G
    72 - H
    73 - I
    74 - J
    75 - K
    76 - L
    77 - M
    78 - N
    79 - O
    80 - P
    81 - Q
    82 - R
    83 - S
    84 - T
    85 - U
    86 - V
    87 - W
    88 - X
    89 - Y
    90 - Z
    91 - [
    92 - \
    93 - ]
    94 - ^
    95 - _
    96 - `
    97 - a
    98 - b
    99 - c
    100 - d
    101 - e
    102 - f
    103 - g
    104 - h
    105 - i
    106 - j
    107 - k
    108 - l
    109 - m
    110 - n
    111 - o
    112 - p
    113 - q
    114 - r
    115 - s
    116 - t
    117 - u
    118 - v
    119 - w
    120 - x
    121 - y
    122 - z
    123 - {
    124 - |
    125 - }
    126 - ~

şeklinde bir sıralama görürüz.

Eğer istersek, yapılan `sort` işlemini de kendimize göre değiştirebiliriz. Şimdi,
`mix` ile `max` işlerini tersine çevirelim:

```python
max([1, 2, 3, 4], key=lambda x: -int(x)) # 1 -- 4 yerine
min([1, 2, 3, 4], key=lambda x: -int(x)) # 4 -- 1 yerine
```
