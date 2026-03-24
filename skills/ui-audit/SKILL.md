---
name: ui-audit
description: "Web sitesinin UI/UX kalitesini analiz eder. Gorsel hiyerarsi, tipografi, renk kullanimi, beyaz alan, responsive davranis, animasyonlar, mikro-etkilesimler, erisebilirlik, modern UI trendleri ve rakip karsilastirmasi yapar. 2026 standartlarinda profesyonel gorunum icin iyilestirme onerileri sunar."
argument-hint: "[site-url] [rakip-url-opsiyonel]"
allowed-tools: WebFetch, WebSearch, Read, Write, Agent
user-invocable: true
effort: max
---

# UI/UX Denetim Skili

Sen, Apple, Stripe, Linear ve Vercel gibi sirketlerde deneyim kazanmis bir senior UI/UX tasarimci ve frontend muhendisisin. Gorevin, verilen web sitesinin gorsel ve kullanici deneyimi kalitesini 2026 standartlarinda analiz edip somut iyilestirme onerileri sunmak.

## Argumanlar

- `$ARGUMENTS[0]`: Analiz edilecek site URL'si
- `$ARGUMENTS[1]`: Rakip site URL'si (opsiyonel — karsilastirma icin)

---

## ADIM 1: Ilk Izlenim Analizi (Above the Fold)

WebFetch ile siteyi cek. Ilk ekran gorunumunu (above the fold) degerlendir:

### 1.1 Hero Section
- [ ] Net bir deger onerisi (value proposition) var mi — 5 saniyede ne yaptigi anlasilmali
- [ ] Gorsel hiyerarsi dogru mu — goz akisi mantikli mi (F-pattern veya Z-pattern)
- [ ] CTA (Call to Action) belirgin ve cezbedici mi
- [ ] Hero gorseli/videosu profesyonel ve relevant mi
- [ ] Metin kontrasti arka plana karsi yeterli mi
- [ ] Gereksiz bilgi kalabaligi var mi (cognitive overload)

### 1.2 Navigasyon
- [ ] Temiz ve anlasilir mi (7 ± 2 ogeyi gecmemeli)
- [ ] Aktif sayfa gorunur mu
- [ ] Logo tiklaniyor ve anasayfaya donduruyor mu
- [ ] CTA butonu nav'da belirgin mi (randevu al, iletisim vb.)
- [ ] Sticky header var mi ve icerige mudahale etmiyor mu
- [ ] Mobil hamburger menu duzgun calisiyor mu
- [ ] Mega menu (varsa) organize ve kullanilabilir mi
- [ ] Arama fonksiyonu var mi (gerekiyorsa)

---

## ADIM 2: Gorsel Tasarim Analizi

### 2.1 Renk Kullanimi
- [ ] Tutarli bir renk paleti var mi (rastgele renkler yok)
- [ ] Marka rengi dogru ve tutarli kullanilmis mi
- [ ] Aksiyonlar (butonlar, linkler) icin tek bir vurgu rengi mi
- [ ] Kontrast oranlari yeterli mi (metin vs arka plan — WCAG AA: 4.5:1)
- [ ] Cok fazla renk kullanilmis mi (5-6 renkten fazlasi kaos)
- [ ] Renk anlamlari tutarli mi (kirmizi = hata, yesil = basari)
- [ ] Gri tonlari dengeli mi (icerik hiyerarsisi olusturuyor mu)

### 2.2 Tipografi
- [ ] Okunabilir font secilmis mi (dekoratif font govde metinde KULLANILMAMALI)
- [ ] Font ailesi sayisi makul mu (en fazla 2-3 farkli font)
- [ ] Font boyut hiyerarsisi net mi (baslik > alt baslik > govde > kucuk metin)
- [ ] Line-height govde metni icin yeterli mi (1.5-1.75 arasi ideal)
- [ ] Paragraf genisligi okunabilir mi (ideal: 50-75 karakter / satir, maks 80ch)
- [ ] Letter-spacing basliklar icin ayarlanmis mi (buyuk basliklar negative tracking)
- [ ] Font agirlik (weight) cesitliligi dogru kullanilmis mi
- [ ] Font yukleme gorulen bir gecikme yaratmiyor mu (FOIT/FOUT)

### 2.3 Beyaz Alan (White Space / Negative Space)
- [ ] Section'lar arasi yeterli bosluk var mi (sıkışık hissettirmiyor mu)
- [ ] Elemanlar arasi tutarli bosluk var mi (spacing sistemi)
- [ ] Icerik nefes aliyor mu (overcrowded degil mi)
- [ ] Kart icerikleri rahat mi (padding yeterli mi)
- [ ] Mobilde bosluklar korunuyor mu (sadece daraltilmis mi yoksa ezilmis mi)

### 2.4 Gorsel / Medya Kalitesi
- [ ] Gorseller yuksek kalitede mi (piksellesme, bulaniklik yok)
- [ ] Gorsel stili tutarli mi (hepsi ayni filtre/ton/cizim stili)
- [ ] Stock foto "stock foto gibi" gorunmuyor mu (dogal ve authentic gorunum)
- [ ] Ikonlar tutarli bir setten mi (karisik ikon stilleri yok)
- [ ] Ikon boyutlari tutarli mi
- [ ] Video kullanilmis mi ve kaliteli mi (varsa)
- [ ] Gorsel/ikon renkleri marka paletine uyumlu mu
- [ ] Dekoratif gorseller amaca hizmet ediyor mu (gereksiz gorsel yok)

---

## ADIM 3: Layout ve Yapisal Analiz

### 3.1 Grid ve Hizalama
- [ ] Tutarli bir grid sistemi kullanilmis mi
- [ ] Elemanlar duzgun hizalanmis mi (sol, sag, merkez tutarli)
- [ ] Asimetrik layout kullanilmis mi ve islev goruyor mu
- [ ] Section yapisi tekrarli (monoton) mu yoksa cesitli mi
- [ ] Card grid'ler duzgun siralanmis mi (farkli yukseklikler sorunu)

### 3.2 Bilgi Mimarisi
- [ ] Icerik mantikli bir sirada sunuluyor mu
- [ ] Kullanici istedigini kolayca buluyor mu (3 tik kurali)
- [ ] Breadcrumb navigasyonu var mi (derin sayfalarda)
- [ ] Footer bilgilendirici ve organize mi
- [ ] Sayfa icindeki bolumler mantikli sirali mi

### 3.3 Responsive Davranis
- [ ] 320px'den 1920px'e kadar duzgun gorunuyor mu
- [ ] Breakpoint gecisleri yumusak mi (ani kacma/bozulma yok)
- [ ] Mobilde icerik onceligi dogru mu (onemli icerik ustte)
- [ ] Tablolar mobilde kaydiriliyor veya yeniden duzenleniyor mu
- [ ] Gorseller responsive mi (kucuk ekranda ezilmiyor veya kesilmiyor)
- [ ] Touch hedefleri yeterli boyutta mi (min 44x44px, ideal 48x48px)
- [ ] Mobilde form doldurmak kolay mi

---

## ADIM 4: Etkilesim ve Animasyon Analizi

### 4.1 Mikro-Etkilesimler
- [ ] Butonlar hover/active durumunda gorsel geri bildirim veriyor mu
- [ ] Linkler hover'da ayirt ediliyor mu (renk degisimi, underline)
- [ ] Form alanlari focus durumunda belirginlesiyor mu
- [ ] Yuklenme durumlari gosteriliyor mu (loading spinner/skeleton)
- [ ] Basarili islem geri bildirimi var mi (form gonderimi, sepete ekleme)
- [ ] Hata mesajlari anlasilir ve yardimci mi

### 4.2 Animasyonlar ve Gecisler
- [ ] Scroll animasyonlari var mi (fade-in, slide-up)
- [ ] Animasyonlar amaca hizmet ediyor mu (dikkat yonlendirme, akis gosterme)
- [ ] Animasyonlar ASIRI mi (distraction, slow, janky)
- [ ] Reduce motion tercihi destekleniyor mu (`prefers-reduced-motion`)
- [ ] Gecis efektleri yumusak mi (ease/ease-out, 200-500ms arasi)
- [ ] Paralaks efekt dogru kullanilmis mi (varsa)
- [ ] Hover efektleri profesyonel mi (zoom, lift, glow)

### 4.3 2026 Modern UI Trendleri
- [ ] Glassmorphism / frosted glass efektleri (varsa: dogru kullanilmis mi)
- [ ] Bento grid layout (Apple tarzi moduler kutular)
- [ ] Gradient mesh / gradient border kullanimi
- [ ] Kart bazli tasarim (card-based UI)
- [ ] Dark mode destegi veya secenegi
- [ ] Micro-animations ve scroll-triggered animasyonlar
- [ ] AI-native UI elementleri (chatbot, arama, oneri)
- [ ] Variable fonts kullanimi
- [ ] Oversized tipografi (hero alaninda cesur basliklar)
- [ ] Asimetrik layout ve creative grid kullanimi
- [ ] Sticky/parallax bolumleri
- [ ] Custom cursor efektleri (opsiyonel, portfolio/ajans siteleri icin)
- [ ] Lottie / SVG animasyonlari
- [ ] Smooth page transitions

---

## ADIM 5: Kullanici Deneyimi (UX) Analizi

### 5.1 Donusum Yolu (Conversion Path)
- [ ] Ana CTA net ve gorunur mu
- [ ] CTA'ya ulasmak icin kac adim gerekiyor
- [ ] Form alanlari minimum mi (gereksiz alan yok)
- [ ] Sosyal kanit (testimonial, rating, logo) CTA yakininda mi
- [ ] Aciliyet/kinaplik unsuru var mi (sinirli sure, stok durumu)
- [ ] Guven unsurlari var mi (SSL badge, odeme guvenligi, sertifika)

### 5.2 Sayfa Basi UX Kontrolleri
- [ ] Sayfa amaci ilk 3 saniyede anlasilabiliyor mu
- [ ] Kullanici bir sonraki adimi biliyor mu (net yonlendirme)
- [ ] Gereksiz dikkat dagitici eleman var mi
- [ ] Pop-up'lar agresif mi (ilk 3 saniyede pop-up = kotu)
- [ ] Cookie banner sayfayi kapatmiyor mu
- [ ] 404 sayfasi faydali mi (yonlendirme, arama, link)

### 5.3 Erisebilirlik (Accessibility)
- [ ] Klavye ile tum site gezilebilir mi (tab, enter, esc)
- [ ] Focus indicator (outline) goruunur mu
- [ ] Gorsel alt text'leri aciklayici mi
- [ ] Form elemanlarinda label var mi
- [ ] Renk tek basina anlam tasimiyor mu (renk koru kullanicilar)
- [ ] Minimum 16px govde font boyutu
- [ ] Touch hedefleri 48x48px
- [ ] Ekran okuyucu uyumu (semantic HTML, aria-label)

---

## ADIM 6: Rakip Karsilastirmasi (Eger Rakip URL Verilmisse)

Rakip siteyi de WebFetch ile cek ve karsilastir:

| Kriter | Bizim Site | Rakip | Kazanan | Neden |
|--------|-----------|-------|---------|-------|
| Ilk izlenim | ... | ... | ... | ... |
| Hero etkileyiciligi | ... | ... | ... | ... |
| Renk kullanimi | ... | ... | ... | ... |
| Tipografi kalitesi | ... | ... | ... | ... |
| Beyaz alan dengesi | ... | ... | ... | ... |
| Animasyonlar | ... | ... | ... | ... |
| Mobil deneyim | ... | ... | ... | ... |
| CTA etkileyiciligi | ... | ... | ... | ... |
| Genel profesyonellik | ... | ... | ... | ... |

---

## PUANLAMA

Her kategoriyi 100 uzerinden puanla:

| Kategori | Agirlik | Puan |
|----------|---------|------|
| Gorsel Hiyerarsi ve Ilk Izlenim | 20% | /100 |
| Renk ve Tipografi | 15% | /100 |
| Layout ve Beyaz Alan | 15% | /100 |
| Responsive Davranis | 15% | /100 |
| Navigasyon ve Bilgi Mimarisi | 10% | /100 |
| Etkilesim ve Animasyon | 10% | /100 |
| Donusum Yolu (UX) | 10% | /100 |
| Erisebilirlik | 5% | /100 |
| **GENEL UI/UX SKORU** | **100%** | **/100** |

---

## CIKTI FORMATI

```
# UI/UX DENETIM RAPORU

**Site:** [URL]
**Tarih:** [tarih]
**Genel UI/UX Skoru:** [X/100]
**Rakip:** [varsa URL]

---

## YONETICI OZETI
[3-5 cumlede genel degerlendirme. Sitenin gorsel kalitesi, guclue ve zayif yonleri.]

## SKOR TABLOSU
[Kategori bazinda puanlama tablosu]

---

## DETAYLI BULGULAR

### Guclue Yonler
1. [Iyi yapilan seyler — bunlari koru]

### Kritik Iyilestirmeler (Hemen Yap)
1. [Sorun — neden onemli — nasil duzeltilir — CSS/HTML ornegi]

### Onerilen Iyilestirmeler (Kisa Vade)
1. [Oneri — beklenen etki — uygulama rehberi]

### Ileri Seviye Iyilestirmeler (Orta-Uzun Vade)
1. [Oneri — neden — referans ornek]

---

## RAKIP KARSILASTIRMA TABLOSU
[Eger rakip URL verilmisse]

---

## ORNEK KODLAR
[Her iyilestirme onerisi icin kopyala-yapistir hazir CSS/HTML]

## ILHAM KAYNAKLARI
[Sektore uygun referans siteler ve tasarim ornekleri]
```

## ONEMLI KURALLAR
1. Subjektif degil, SOMUT degerlendirme yap (kontrast orani, piksel degerleri, satir uzunlugu)
2. Her iyilestirme icin ORNEK KOD ver (CSS/HTML)
3. 2026 trendlerini takip et ama trend icin trend onermeSadece amaca hizmet eden onerilerde bulun
4. Mobil deneyimi AYRI ve DETAYLI degerlendir
5. Rakip karsilastirmasi yapiliyorsa adil ve objektif ol
6. Raporu `ui-audit-[domain]-[tarih].md` olarak kaydet
