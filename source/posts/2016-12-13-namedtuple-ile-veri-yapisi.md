---
title: "namedtuple ile veri yapısı"
date: Dec 13, 2016 10:22
tags: py2.6+,collections
subtitle: Yüksek performanslı veri taşıyıcılar
# published: false
# cover: 
author:
  name: Uğur Özyılmazel
  email: ugurozyilmazel@gmail.com
  link: http://ugur.ozyilmazel.com
  bio: Yazılım Geliştiricisi
  twitter: vigobronx
---

Basit veri yapılarına ihtiyacınız olduğunda kullanabileceğiniz bir fonksiyondan
bahsetmek istiyorum.READ_MORE

`namedtuple` Python 2.6’dan itibaren, `collections` modulünün içinde bulunan bir
fonksiyon:

```python
from collections import namedtuple

User = namedtuple('MyCustomUserStruct', ['first_name', 'last_name'])

user_1 = User(u"Uğur", u"Özyılmazel")
user_1.__doc__    # MyCustomUserStruct(first_name, last_name)
user_1.first_name # Uğur
user_1.last_name  # Özyılmazel

# user_1’e ait public method’lar:
[m for m in dir(user_1) if not m.startswith("_")]
# ['count', 'first_name', 'index', 'last_name']
```

Aslında perde arkasında ne olduğunu görmek için `verbose` durumunda üretelim
nesneyi:

```python
User = namedtuple('MyCustomUserStruct', ['first_name', 'last_name'], verbose=True)

class MyCustomUserStruct(tuple):
    'MyCustomUserStruct(first_name, last_name)'

    __slots__ = ()

    _fields = ('first_name', 'last_name')

    def __new__(_cls, first_name, last_name):
        'Create new instance of MyCustomUserStruct(first_name, last_name)'
        return _tuple.__new__(_cls, (first_name, last_name))

    @classmethod
    def _make(cls, iterable, new=tuple.__new__, len=len):
        'Make a new MyCustomUserStruct object from a sequence or iterable'
        result = new(cls, iterable)
        if len(result) != 2:
            raise TypeError('Expected 2 arguments, got %d' % len(result))
        return result

    def __repr__(self):
        'Return a nicely formatted representation string'
        return 'MyCustomUserStruct(first_name=%r, last_name=%r)' % self

    def _asdict(self):
        'Return a new OrderedDict which maps field names to their values'
        return OrderedDict(zip(self._fields, self))

    def _replace(_self, **kwds):
        'Return a new MyCustomUserStruct object replacing specified fields with new values'
        result = _self._make(map(kwds.pop, ('first_name', 'last_name'), _self))
        if kwds:
            raise ValueError('Got unexpected field names: %r' % kwds.keys())
        return result

    def __getnewargs__(self):
        'Return self as a plain tuple.  Used by copy and pickle.'
        return tuple(self)

    __dict__ = _property(_asdict)

    def __getstate__(self):
        'Exclude the OrderedDict from pickling'
        pass

    first_name = _property(_itemgetter(0), doc='Alias for field number 0')

    last_name = _property(_itemgetter(1), doc='Alias for field number 1')
```

`namedtuple`’ı çağırırken geçtiğimiz ilk parametre ile aslında birazdan
üreteceğimiz `Class`’ın adını vermiş oluyoruz. İkinci parametre ile, bu
oluşacak sınıfın `property`’lerinin listesini vermiş oluyoruz.

```python
namedtuple(typename, field_names, verbose=False, rename=False)
```

Dikkat ettiyseniz bu oluşan sınıf, `tuple`’dan türedi:

```python
class MyCustomUserStruct(tuple):
```

`count` ve `index` method’ları da direk olarak `tuple`’dan geldi:

```python
[m for m in dir(tuple) if not m.startswith("_")] # ['count', 'index']
```

`user_1.first_name` ya da `user_1.last_name` aslında birer **alias** (*rumuz*).
Neticede elimizde bir `tuple` olduğu için index kullanarak da işlem yapabilirdik:

```python
user_1[0] # Uğur
user_1[1] # Özyılmazel
```

Nokta yazım şekli (*dot notation*) kodun okunabilirliği açısından çok rahatlatıcı.
Bu bakımdan kullanımı da çok kolay. Index ezberlemek yerine property adını
çağırıyorsunuz. Sınıfın method’larına bakarsanız:

```python
user_1._fields  # ('first_name', 'last_name')
user_1.__dict__
# OrderedDict([('first_name', u'U\u011fur'), 
#              ('last_name', u'\xd6zy\u0131lmazel')])

user_1.__repr__()
# "MyCustomUserStruct(first_name=u'U\\u011fur', last_name=u'\\xd6zy\\u0131lmazel')"

user_2 = user_1._replace(first_name=u"Vigo", last_name=u"Kadriyani")
user_2.first_name # u'Vigo'
user_2.last_name  # u'Kadriyani'

# farklı yöntemler
user_1 = User(first_name=u"Uğur", last_name=u"Özyılmazel")
# MyCustomUserStruct(first_name=u'U\u011fur', last_name=u'\xd6zy\u0131lmazel')

user_2_data = {
    'first_name': u"Tony",
    'last_name': u"Hawk",
}

# dict’den kwargs şeklinde
user_2 = User(**user_2_data)
# MyCustomUserStruct(first_name=u'Tony', last_name=u'Hawk')
```

`collections` modülü içinde başka güzel özellikler de bulunmakta. İleriki
yazılarda yeri geldikçe değinmeyi düşünüyorum.