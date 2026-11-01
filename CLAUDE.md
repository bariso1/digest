# Digest

Kişisel link ve metin takipçisi, statik web uygulaması. Kapsam, kararlar ve oturum durumu `PLAN.md` içinde. Her oturuma oradaki "Durum" bölümünü okuyarak başla ve oturum sonunda güncelle.

## Çalışma biçimi

- Kullanıcı web geliştirici değil. Türkçe yaz, terimleri kısaca ama yüzeysel kalmadan açıkla.
- Kapsam dışına çıkma. Gerekli gördüğün bir eklemeyi önce öner, onay almadan yapma.
- Her oturumun sonunda iPhone'da test edilebilir bir şey olsun, adımlarını `TESTLER.md` dosyasına ekle.
- Token ve şifre gibi bilgileri sohbete yazdırma.

## Kod kuralları

- Düz HTML, CSS, JavaScript. Framework, build aracı ve npm paketi ekleme.
- Klasik `<script>` etiketleri kullan. `type="module"` kullanma, sayfa Mac'te dosyaya çift tıklayınca da açılabilmeli.
- `localStorage` erişimi yalnızca `storage.js` içinde olsun.
- Kayıt biçimi sürüm numarası taşısın. Tanınmayan biçimdeki veriyi asla üzerine yazma, depo dolu hatasını kullanıcıya göster.
- Kullanıcı içeriğini `textContent` ile göster, `innerHTML` kullanma. Yalnızca `http` ve `https` bağlantılarını tıklanabilir yap.
- Service worker ekleme.
- Yolları göreli yaz (`styles.css`, `/styles.css` değil), çünkü site `kullaniciadi.github.io/digest/` altında yayınlanacak.

## Yayın

- GitHub Pages, herkese açık `digest` deposu, `main` dalının kökü.
- Git kimliği bu depoya özel ayarlanır ve GitHub noreply adresini kullanır. Depo herkese açık olduğu için kişisel e-posta commit'lere girmemeli.
- Yayın adresini değiştirme: veri adrese bağlıdır, adres değişirse kayıtlara erişilemez.

## Yerelde deneme

`python3 -m http.server 8765` ile aç, işin bitince kapat. Depolama ve ana ekran davranışının son sözü iPhone'daki testtir.
