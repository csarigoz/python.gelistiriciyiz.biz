---
title: "Bir Python projesinde gizli veya sabit değerleri saklama"
published: false
date: Jan 19, 2017 21:25
tags: pickle, import
author:
  name: Çağrı Sarıgöz
  email: cagri.sarigoz@gmail.com
  link: http://cagrisarigoz.com
  bio: Data Science Heveslisi
  twitter: cagrisarigoz
---

Onedio.com bünyesinde birçok farklı kaynaktan çektiğimiz verileri toparlayıp raporlama işlemlerini otomatikleştirmek için geliştirdiğim küçük bir Python projem var. Bu projeyi şirketin GitHub hesabında yer alan bir repository üzerinden de sürekli olarak güncelliyorum.

Projede kullandığım gizli ve/veya sabit değerleri saklama ihtiyacını karşılamak için denediğim / kullandığım yöntemleri aktaracağım bu yazıda.READ_MORE

Öncelikle projeyi nasıl yönettiğimi aktarayım, projeyi 3 farklı yerde tutuyorum:
- Kendi bilgisayarımda bir Git repository içinde
- GitHub şirket hesabımızda bir repository içinde
- Projede yazdığım raporlama script'lerini bir crontab üzerinden yönettiğim raporlama server'ı üzerinden

Kendi bilgisayarımda yazdığım script'leri test ettikten sonra hem kendi bilgisayarımdaki hem de GitHub'daki repository'ye commit göndererek projenin güncelliğini sağlıyorum. Eğer yazdığım script'i periyodik olarak çalıştırmam gerekecekse diğer script'lerin de çalıştığı server'a rsync ile bu yeni script'i de gönderiyorum.

Veri kaynaklarından verileri alabilmek için kullandığım access token gibi gizli / sabit değerleri GitHub repository üzerine göndermeden, kendi bilgisayarım ve raporlama server'ı üzerinde tutmak istiyordum.

Bunu sağlayabilmek için ilk denediğim yöntem Python'un environment variable'larını kullanarak GitHub repository'sinden tamamen bağımsız şekilde tutmak oldu. Stackoverflow senin Ubuntu forumları benim dolaşmaktan bir süre yorulduktan sonra bu değerleri hem kendi bilgisayarımda hem de raporlama server'ında her seferinde güncellemekle uğraşmaktan vazgeçtim.

Bunun yerine kendi bilgisayarımdaki proje içerisinde `constants` isimli bir klasör oluşturup gizli / sabit değerleri bu klasör içerisinde tutup, bu klasörü `.gitignore` dosyasını kullanarak ile GitHub repository'sinden gizlemeye karar verdim.

`constants` klasörü içine `p.12`, `.json` gibi halihazırda formatlanmış gizli bilgilerin olduğu dosyaları olduğu gibi koydum. Bunun dışında access token, cookie bilgileri gibi veri kaynaklarına erişimde kullandığım diğer sabit değerleri de tek bir dosyada tutmak istedim.

İlk bulduğum yöntem pickle oldu.

buraya klasörün mimarisi

pickle kullanarak şu şekilde bu bilgileri yazdım

buraya kod gelecek

sonra da ilgili raporlama script dosyalarından şu şekilde ihtiyacım olan bilgileri aldım

buraya kod gelecek

github'da dolaşırken .py python dosyası içinde direkt kullanan birkaç örneği görünce bunun daha kolay olacağına kanaat getirdim.

.py dosyasının içindeki kod

raporlama script'lerinde tek bir satır ile ihtiyacım olan değerleri alabildim böylece

from .py import bla bla
