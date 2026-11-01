# Digest v1 planı

Kişisel link ve metin takipçisi. Veriler yalnızca tarayıcıda durur, sunucu ve veritabanı yoktur.

## Durum

**Şu an:** 1. oturum bitti, sırada 2. oturum.

Yayın adresi: `https://bariso1.github.io/digest/`. Bu adres değişmemeli.

Yapıldı:
- [x] 1. oturum: sayfa GitHub Pages'te yayında, iPhone testi kullanıcı tarafından onaylandı.
- [x] Git kimliği bu depoya özel, noreply adresiyle ayarlandı.

Sırada:
- [ ] 2. oturum: link veya metin ve not ekleme, en yenisi üstte liste.

## Kapsam

1. Link ya da metin yapıştırma, isteğe bağlı kısa not.
2. Bir ya da birkaç etiket.
3. En yenisi üstte liste, etikete göre filtre.
4. Okundu işareti.
5. Telefonda düzgün görünüm, iPhone ana ekranına eklenebilme.
6. Tek tuşla JSON dışa aktarma.
7. JSON içe aktarma (sonradan onaylandı).
8. Kayıt silme (sonradan onaylandı).

v1'de yok: giriş, senkronizasyon, AI özeti, çevrimdışı açılış.

## Kararlar

| Konu | Karar | Bedeli |
|---|---|---|
| Teknoloji | Düz HTML, CSS, JavaScript. Framework ve build aracı yok. | Ekran kodu biraz daha uzun olur. |
| Depolama | localStorage. Depoya yalnızca `storage.js` dokunur, kayıt biçimi sürüm numarası taşır. | Yaklaşık 5 MB sınır, kabaca birkaç bin kayıt. Dolunca uygulama hata gösterir. |
| Ana ekran | Web manifest ve ikon. | Ana ekrana elle eklenir. Paylaş menüsünde Digest'in çıkması beklenmiyor (doğrulanmadı). |
| Çevrimdışı | Service worker yok. | İnternet yokken uygulama açılmayabilir. |
| Test | Otomatik test yok, `TESTLER.md` listesi iPhone'da elle denenir. | Her oturum sonunda yaklaşık 5 dakika. |
| Barındırma | GitHub Pages, herkese açık `digest` deposu, git ile yayın. | Kod herkese açık olur (kayıtlar değil). Adres kullanıcı adına bağlıdır. Aynı hesaptaki başka Pages siteleri aynı depolama alanını paylaşır. |
| Filtre | Aynı anda tek etiket. | |
| Okunan kayıtlar | Listede soluk görünür, gizlenmez. | |

## Dosya yapısı

```
index.html             Sayfanın iskeleti: form, liste, düğmeler.
styles.css             Görünüm ve telefon yerleşimi.
storage.js             Veriyi okuyan, yazan, dışa ve içe aktaran tek dosya.
app.js                 Düğmeleri çalıştıran, listeyi çizen ve filtreleyen kod.
manifest.webmanifest   Ana ekran için ad, ikon ve tam ekran ayarı.
icons/                 Ana ekran ve manifest ikonları.
TESTLER.md             Her oturumda iPhone'da denenecek adımlar.
```

Bugün yalnızca `index.html`, `styles.css` ve `TESTLER.md` var. Diğerleri ilgili oturumda eklenir.

## Riskler

Veri, adres ve açılış biçimiyle birlikte saklanır.

| Risk | Durum | Önlem |
|---|---|---|
| Safari ve ana ekran uygulaması ayrı depolama kullanır | Doğrulandı, Apple'a göre tasarım gereği. | Gerçek kullanım ikondan yapılır. Safari'de açılınca uyarı gösterilir. |
| 7 gün kullanılmayınca silinme | Safari'de geçerli. Ana ekran uygulaması resmi olarak muaf, eski bir hata raporu aksini anlatıyor. | Muafiyet tek güvence sayılmaz. |
| Telefonda yer azalınca otomatik silinme | Mümkün. | Açılışta `persist()` istenir, sonuç ekranda gösterilir. Garanti değildir. |
| İkon silinince veri ne olur | Belirsiz. | Silindiği varsayılır, 7. oturumda test edilir. |
| Safari geçmişini temizleme, telefon değişimi, iCloud yedeği | Doğrulanmadı. | Bunlara güvenilmez. |
| Adres değişimi | Veri erişilemez olur. | Adres 1. oturumda sabitlenir, gerekirse dışa ve içe aktarmayla taşınır. |
| Hatalı güncelleme veriyi bozar | Mümkün. | Tanınmayan biçimdeki veri üzerine yazılmaz. |
| Yapıştırılan içeriğin kod gibi çalışması | Önlenebilir. | İçerik düz metin gösterilir, yalnızca `http` ve `https` bağlantıları tıklanabilir. |

Asıl güvence telefon dışındaki yedektir: dışa aktarılan dosya iCloud Drive'a kaydedilir ve ekranda son yedek tarihi görünür.

## Oturumlar (her biri 45 dakika)

| # | Yapılacak | Sonunda test |
|---|---|---|
| 1 | GitHub kurulumu, boş sayfa, ilk yayın | Adres iPhone'da açılıyor. |
| 2 | Link veya metin ve not ekleme, en yenisi üstte liste | 3 kayıt ekle, sayfayı yenile: kayıtlar duruyor, sıra doğru. |
| 3 | Etiket ekleme, etikete göre filtre | Birden çok etiketli kayıtlar doğru etiketlerde çıkıyor, filtre temizleniyor. |
| 4 | Okundu işareti, silme, telefon düzeni | Çok uzun link ve metin taşmıyor, düğmeler parmakla rahat basılıyor, okundu işareti geri alınabiliyor. |
| 5 | Manifest, ikon, tam ekran, `persist()`, Safari uyarısı | İkondan tam ekran açılıyor. Safari'deki kayıtlar uygulamada görünmüyor. |
| 6 | JSON dışa aktarma (paylaş menüsü ve yedek indirme yöntemi), son yedek bilgisi | Dosya iCloud Drive'a gidiyor, açılıyor, tüm kayıtlar içinde. |
| 7 | JSON içe aktarma, kayıp tatbikatı, son kontrol | Yedek al, ikonu sil, yeniden ekle, sonucu not et, yedekten geri yükle. Ardından gerçek kullanım başlar. |

7. oturuma kadar girilen kayıtlar deneme verisi sayılır.
