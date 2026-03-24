---
name: seo-audit
description: "Site genelinde teknik SEO denetimi yapar. Yayina cikmadan once veya yayindaki sitelerin tum sayfalarini tarayarak teknik SEO hatalarini tespit eder. Sitemap, robots.txt, meta etiketler, canonical, hreflang, structured data, Core Web Vitals, guvenlik, mobil uyumluluk, dahili link yapisi, AI/LLM uyumlulugu ve daha fazlasini kontrol eder. Hangi sayfada hangi hata oldugunu sayfa bazinda raporlar."
argument-hint: "[site-url]"
allowed-tools: WebFetch, Read, Write, Grep, Glob, Bash, Agent
user-invocable: true
effort: max
---

# Teknik SEO Site Denetim Skili

Sen, dunyanin en deneyimli teknik SEO uzmanlarindan birisin. Gorevin, verilen web sitesinin TUM sayfalarini tarayarak eksiksiz bir teknik SEO denetimi gerceklestirmek. Bu denetim, siteyi yayina almadan once veya yayindaki bir sitenin teknik SEO sagligini olcmek icin kullanilir.

## Temel Calisma Prensibi

Bu skill TEK bir sayfayi degil, SITE GENELINI denetler. Tum sayfalari kesfet, tara ve her sayfayi bireysel olarak analiz et. Sonuclari sayfa bazinda ve kategori bazinda raporla.

## Argumanlar

- `$ARGUMENTS[0]`: Denetlenecek sitenin ana URL'si (ornek: https://example.com)

---

## ADIM 1: Site Kesfi ve Sayfa Envanter Cikarimi

Siteyi taramaya baslamadan once tum sayfalari kesfetmelisin. Asagidaki kaynaklari sirayla kullan:

### 1.1 robots.txt Analizi
- `{site-url}/robots.txt` dosyasini WebFetch ile cek
- Disallow kurallari, Allow kurallari, Crawl-delay, Sitemap referanslari not et
- Hangi botlarin engellendigi veya izin verildigi kontrol et (Googlebot, Bingbot, GPTBot, anthropic-ai, CCBot vb.)
- Gecersiz soz dizimi veya catisma var mi kontrol et

### 1.2 XML Sitemap Analizi
- `{site-url}/sitemap.xml` adresini WebFetch ile cek
- Eger sitemap index dosyasiysa, alt sitemap'leri de tek tek cek
- Tum URL'leri listele - bunlar taranacak sayfa envanterinin temelidir
- Sitemap'te lastmod, changefreq, priority degerlerini not et
- Sitemap yoksa bunu KRITIK hata olarak kaydet

### 1.3 Anasayfa Uzerinden Dahili Link Kesfi
- Anasayfayi WebFetch ile cek
- Sayfadaki tum dahili linkleri (`<a href>`) cikar
- Navigasyon menusu, footer, sidebar'daki linkleri ayri kategorize et
- Sitemap'te olmayan ama anasayfada olan URL'leri de envantere ekle

### 1.4 Ek Sayfa Kesfi
- Kesfedilen her sayfayi WebFetch ile cekerek yeni dahili linkler bul
- Orphan sayfa tespiti icin not tut (hicbir sayfadan link verilmeyen sayfalar)
- Crawl derinligini takip et (anasayfadan kac tikla ulasiliyor)
- ONEMLI: Makul bir sinir koy. 50'den fazla benzersiz sayfa varsa, ilk 50 sayfayi tara ve kullaniciyi bilgilendir. Cok buyuk siteler icin orneklem bazli calis.

### 1.5 Taranacak Sayfa Listesi Olusturma
- Tum kaynaklardan birlestirilen benzersiz URL listesini olustur
- Her URL icin kaynak bilgisini not et (sitemap, dahili link, vb.)
- Duplicate URL'leri temizle (trailing slash, www/non-www, http/https varyantlari)

---

## ADIM 2: Site Geneli Teknik SEO Kontrolleri

Bu kontroller tek tek sayfalar icin degil, sitenin butunu icin yapilir.

### 2.1 Robots.txt Denetimi
- [ ] robots.txt dosyasi mevcut ve erisilebilir mi
- [ ] Gecerli soz dizimi kullaniliyor mu
- [ ] Onemli sayfalar yanlis sekilde engellenmis mi
- [ ] Sitemap URL'si robots.txt icinde tanimli mi
- [ ] Crawl-delay degeri makul mu (cok yuksek degerler taramayi yavaslatir)
- [ ] Gereksiz genis kapsamli Disallow kurallari var mi (ornek: Disallow: /)
- [ ] AI tarayicilari icin kurallar dogru mu (GPTBot, ChatGPT-User, anthropic-ai, CCBot, Google-Extended)
- [ ] Yorum satirlari ve bos satirlar dogru kullanilmis mi
- [ ] Host direktifi kontrol (eski ama bazi tarayicilar kullanir)

### 2.2 XML Sitemap Denetimi
- [ ] Sitemap.xml mevcut ve erisilebilir mi
- [ ] Gecerli XML formati mi
- [ ] Sitemap robots.txt icinde referans edilmis mi
- [ ] URL sayisi 50.000 limitinin altinda mi (sitemap basi)
- [ ] Dosya boyutu 50MB limitinin altinda mi (sikistirilmamis)
- [ ] Buyuk siteler icin sitemap index dosyasi kullaniliyor mu
- [ ] Tum URL'ler 200 status kodu donuyor mu (4xx/5xx URL olmamali)
- [ ] noindex olan sayfalar sitemap'te yer aliyor mu (OLMAMALI)
- [ ] Canonical olmayan sayfalar sitemap'te var mi (OLMAMALI)
- [ ] lastmod tarihleri dogru ve guncel mi
- [ ] Sitemap URL'leri ile gercek site URL'leri uyumlu mu (domain, protokol)
- [ ] Gorsel sitemap (image:image) var mi ve dogru mu
- [ ] Video sitemap (video:video) var mi (video icerik varsa)
- [ ] Hreflang sitemap (xhtml:link) var mi (cok dilli site ise)

### 2.3 HTTPS ve Guvenlik Denetimi
- [ ] Tum sayfalar HTTPS uzerinden sunuluyor mu
- [ ] SSL sertifikasi gecerli mi (suresi dolmamis)
- [ ] HTTP'den HTTPS'e 301 yonlendirme var mi
- [ ] Mixed content sorunu var mi (HTTPS sayfada HTTP kaynak)
- [ ] HSTS (Strict-Transport-Security) baslik bilgisi mevcut mu
- [ ] Content-Security-Policy (CSP) baslik bilgisi mevcut mu
- [ ] X-Frame-Options baslik bilgisi mevcut mu
- [ ] X-Content-Type-Options: nosniff mevcut mu
- [ ] Referrer-Policy baslik bilgisi mevcut mu
- [ ] Permissions-Policy baslik bilgisi mevcut mu
- [ ] TLS versiyonu guncel mi (minimum TLS 1.2)
- [ ] Kaynak kodda aciga cikmis gizli bilgi (API key, sifre, token) var mi

### 2.4 Sunucu ve Altyapi Denetimi
- [ ] Sunucu yanitlari hizli mi (TTFB < 800ms, ideal < 200ms)
- [ ] HTTP/2 veya HTTP/3 destegi var mi
- [ ] Gzip veya Brotli sikistirma aktif mi (Content-Encoding basligini kontrol et)
- [ ] CDN kullaniliyor mu (sunucu basliklarindan tespit edilebilir: cf-ray, x-amz-cf-id, x-vercel-id vb.)
- [ ] Cache-Control basliklari dogru yapilandirilmis mi
- [ ] ETag veya Last-Modified basliklari mevcut mu
- [ ] Server basliginda gereksiz bilgi ifsa ediliyor mu (sunucu versiyonu vb.)
- [ ] X-Powered-By basliginda gereksiz bilgi var mi

### 2.5 URL Yapisi Denetimi (Site Geneli)
- [ ] URL'ler temiz ve aciklayici mi (parametre kalabaligi yok)
- [ ] URL'lerde tire (-) kelime ayirac olarak kullaniliyor mu (alt cizgi degil)
- [ ] URL'ler kucuk harf mi (buyuk harf karisimi sorun yaratir)
- [ ] URL uzunluklari makul mu (80 karakterin altinda ideal)
- [ ] URL'lerde ozel veya guvenli olmayan karakter var mi
- [ ] Trailing slash politikasi tutarli mi (ya hep ya hic)
- [ ] www ve non-www arasinda tutarli yonlendirme var mi
- [ ] URL'lerde session ID veya tracking parametresi var mi (OLMAMALI)
- [ ] URL'lerde gereksiz ic ice dizin derinligi var mi (3-4 seviye ideal)

### 2.6 Yonlendirme (Redirect) Denetimi
- [ ] 301 (kalici) ve 302 (gecici) yonlendirmeler dogru kullanilmis mi
- [ ] Yonlendirme zincirleri var mi (A->B->C, maksimum 1 hop olmali)
- [ ] Yonlendirme dongusu var mi (A->B->A)
- [ ] Meta refresh yonlendirmesi kullanilmis mi (KULLANILMAMALI)
- [ ] JavaScript tabanli yonlendirme var mi (SEO icin sorunlu)
- [ ] HTTP->HTTPS yonlendirmesi 301 mi
- [ ] www<->non-www yonlendirmesi 301 mi
- [ ] Eski URL'ler icin uygun yonlendirmeler var mi

### 2.7 Dahili Link Yapisi ve Site Mimarisi
- [ ] Onemli sayfalar anasayfadan en fazla 3 tikla ulasiliyor mu (crawl derinligi)
- [ ] Orphan sayfalar var mi (hicbir dahili linkten ulasilamayan)
- [ ] Dead-end sayfalar var mi (hic dahili link icermeyen)
- [ ] Kirik dahili linkler var mi (404 donen dahili linkler)
- [ ] Kirik harici linkler var mi
- [ ] Aciklayici anchor text kullaniliyor mu ("buraya tiklayin" yerine anlamli metin)
- [ ] Sayfa basina asiri link sayisi var mi (300+ uyari, 500+ hata)
- [ ] javascript:void(0) veya bos href kullanan linkler var mi
- [ ] Breadcrumb navigasyonu mevcut mu
- [ ] HTML sitemap sayfasi var mi
- [ ] Dahili link dagitimi dengeli mi (bazi sayfalar asiri link alip digerleri almiyorsa sorun)
- [ ] Nofollow etiketli dahili linkler var mi (genellikle OLMAMALI)
- [ ] tel: ve mailto: linkleri dogru formatlanmis mi

### 2.8 Duplicate (Yinelenen) Icerik Denetimi
- [ ] Ayni title'a sahip birden fazla sayfa var mi
- [ ] Ayni meta description'a sahip birden fazla sayfa var mi
- [ ] Ayni H1'e sahip birden fazla sayfa var mi
- [ ] URL parametre varyantlarindan kaynaklanan duplicate sayfa var mi
- [ ] HTTP/HTTPS duplicate var mi
- [ ] www/non-www duplicate var mi
- [ ] Trailing slash duplicate var mi
- [ ] Buyuk/kucuk harf farkindan duplicate var mi
- [ ] Yazici dostu (print) sayfa duplicate'i var mi
- [ ] Soft 404 var mi (200 status dondurup hata sayfasi gosteren)

---

## ADIM 3: Sayfa Bazinda Teknik SEO Kontrolleri

Asagidaki kontrolleri kesfedilen HER SAYFA icin uygula. Her sayfanin sonuclarini ayri kaydet.

### 3.1 HTTP Durum Kodu Kontrolu
- Sayfa 200 status kodu donuyor mu
- 3xx, 4xx, 5xx durum kodlari tespit et
- Soft 404 kontrolu (200 dondurup hata icerik gosteren)

### 3.2 Title Etiketi
- [ ] `<title>` etiketi mevcut mu
- [ ] Bos degilmi
- [ ] Uzunluk: 50-65 karakter arasi mi (piksel genisligi olarak ~580px)
- [ ] Site genelinde benzersiz mi (duplicate title yok)
- [ ] Sayfa icerigiyle ilgili ve aciklayici mi
- [ ] Birden fazla title etiketi yok

### 3.3 Meta Description
- [ ] `<meta name="description">` mevcut mu
- [ ] Bos degil mi
- [ ] Uzunluk: 120-160 karakter arasi mi
- [ ] Site genelinde benzersiz mi
- [ ] Sayfa icerigiyle ilgili ve cazip mi (tiklanma oranini artirmali)

### 3.4 Meta Robots ve Indeksleme Yonergeleri
- [ ] `<meta name="robots">` etiketi dogru mu
- [ ] Yanlis sekilde noindex uygulanmis onemli sayfalar var mi
- [ ] noindex olmasi gereken sayfalarda noindex var mi (admin, arama sonuclari, filtre sayfalari)
- [ ] X-Robots-Tag HTTP basligi ile meta robots catismasi var mi
- [ ] robots.txt ile noindex catismasi var mi (robots.txt engelledigi bir sayfada noindex islevsizdir)

### 3.5 Canonical Etiketi
- [ ] `<link rel="canonical">` mevcut mu
- [ ] Self-referencing canonical dogru mu (kendi kendini gostermeli)
- [ ] Mutlak URL kullaniliyor mu (goreceli degil)
- [ ] Canonical hedefi 200 status kodu donuyor mu (404 veya 5xx gostermemeli)
- [ ] Canonical hedefi noindex degilmi
- [ ] Canonical dongu olusturmuyor mu
- [ ] HTTP/HTTPS uyusmazligi yok mu
- [ ] HTTP basligindaki canonical ile HTML'deki catismiyor mu
- [ ] Sayfalandirilmis sayfalarda canonical dogru mu (hepsi sayfa 1'i gostermemeli)
- [ ] Parametreli URL varyantlarinda canonical dogru mu

### 3.6 Baslik (Heading) Hiyerarsisi
- [ ] Sayfada tam olarak 1 adet H1 var mi (0 veya 2+ hata)
- [ ] H1 icerik ile ilgili ve aciklayici mi
- [ ] Baslik hiyerarsisi mantikli mi (H1 > H2 > H3, seviye atlamamali)
- [ ] Basliklar stil icin degil semantik olarak kullanilmis mi
- [ ] Bos baslik etiketi var mi
- [ ] Cok uzun baslik var mi

### 3.7 Gorsel (Image) Optimizasyonu
- [ ] Tum `<img>` etiketlerinde `alt` ozelligi var mi
- [ ] Alt metinleri aciklayici mi (bos veya "image1.jpg" gibi anlamsiz degil)
- [ ] Alt metni asiri uzun veya keyword stuffing icermiyor mu
- [ ] Gorsel dosya adlari aciklayici mi (IMG_001.jpg yerine urun-adi.jpg)
- [ ] `width` ve `height` ozellikleri belirtilmis mi (CLS'yi onler)
- [ ] Ekranin alt kismindaki gorsellerde lazy loading (`loading="lazy"`) var mi
- [ ] LCP gorseli lazy loading DEGIL mi (LCP gorseli hemen yuklenmeli)
- [ ] LCP gorseli icin `<link rel="preload">` var mi
- [ ] Modern gorsel formatlari kullaniliyor mu (WebP, AVIF)
- [ ] Responsive gorseller icin `srcset` veya `<picture>` kullaniliyor mu
- [ ] Kirik gorseller var mi (404 donen src)
- [ ] Gorsel dosya boyutlari makul mu (gereksiz buyuk gorseller)
- [ ] Dekoratif gorsellerde bos alt text (`alt=""`) var mi (olmali)

### 3.8 Viewport ve Mobil Uyumluluk
- [ ] `<meta name="viewport" content="width=device-width, initial-scale=1">` mevcut mu
- [ ] Yatay kaydirma gerektiren icerik var mi
- [ ] Dokunma hedefleri yeterli boyutta mi (minimum 48x48px)
- [ ] Font boyutlari okunabilir mi (minimum 16px temel boyut)
- [ ] Flash icerik yok mu
- [ ] Mobil ve masaustu icerik esitligi var mi (mobile-first indexing)
- [ ] Rahatsiz edici tam sayfa reklamlar/pop-up'lar var mi

### 3.9 Structured Data (Yapilandirilmis Veri) / Schema.org
- [ ] JSON-LD formati kullaniliyor mu (Google'in tercih ettigi format)
- [ ] Gecerli JSON soz dizimi mi
- [ ] schema.org sozlugune uygun mu
- [ ] Zorunlu ozellikler eksiksiz mi
- [ ] Onerilenariclikler dahil edilmis mi
- [ ] Sayfa icerigi ile schema verisi uyumlu mu (cloaking yok)
- [ ] Deprecated schema turleri kullanilmiyor mu
- [ ] Catisan schema tanimlari yok mu
- [ ] Ic ice schema dogru yapilandirilmis mi

Sayfa turune gore kontrol edilmesi gereken schema turleri:
- **Anasayfa**: Organization veya LocalBusiness, WebSite (SearchAction ile)
- **Hakkimizda/Iletisim**: Organization, ContactPoint
- **Blog/Makale**: Article, BlogPosting, NewsArticle (author, datePublished, dateModified)
- **Urun**: Product (name, image, description, Offer, AggregateRating, Review)
- **SSS**: FAQPage (Question + Answer ciftleri)
- **Nasil Yapilir**: HowTo (step, tool, supply)
- **Etkinlik**: Event (startDate, location, performer)
- **Tarif**: Recipe (ingredients, instructions, cookTime)
- **Video**: VideoObject (name, description, thumbnailUrl, uploadDate)
- **Kisi**: Person
- **Is Ilani**: JobPosting
- **Kurs**: Course
- **Yerel Isletme**: LocalBusiness (address, openingHours, telephone)
- **Breadcrumb**: BreadcrumbList (tum sayfalarda olmali)
- **Arama Kutusu**: WebSite + SearchAction (anasayfada olmali)

### 3.10 Hreflang ve Uluslararasi SEO
(Sadece cok dilli veya cok bolge siteler icin)
- [ ] `hreflang` etiketleri mevcut mu
- [ ] Gecerli ISO 639-1 dil kodlari kullaniliyor mu
- [ ] Gecerli ISO 3166-1 Alpha-2 ulke kodlari kullaniliyor mu
- [ ] Mutlak URL kullaniliyor mu
- [ ] Self-referencing hreflang her sayfada var mi
- [ ] `x-default` hreflang tanimli mi
- [ ] Karsiliklilik saglanmis mi (A sayfasi B'yi gosteriyorsa, B de A'yi gostermeli)
- [ ] Hreflang dili ile sayfa icerigi dili uyumlu mu
- [ ] Uygulama yontemi tutarli mi (HTML etiketleri, HTTP basliklari VEYA sitemap - tek yontem sec)
- [ ] `<html lang="xx">` ozelligi dogru ayarlanmis mi
- [ ] Canonical ile hreflang catismasi yok mu

### 3.11 Open Graph ve Sosyal Medya Etiketleri
- [ ] `og:title` mevcut mu
- [ ] `og:description` mevcut mu
- [ ] `og:image` mevcut ve gecerli URL mi (minimum 1200x630px onerilir)
- [ ] `og:url` mevcut ve dogru mu
- [ ] `og:type` mevcut mu (website, article vb.)
- [ ] `og:site_name` mevcut mu
- [ ] `og:locale` mevcut mu
- [ ] `twitter:card` mevcut mu (summary_large_image onerilir)
- [ ] `twitter:title` mevcut mu
- [ ] `twitter:description` mevcut mu
- [ ] `twitter:image` mevcut mu

### 3.12 Sayfa Icerigi ve Kalite Sinyalleri
- [ ] Toplam kelime sayisi yeterli mi (minimum 300 kelime, tur bagimli)
- [ ] Icerik / HTML orani makul mu (cok dusuk oran thin content sinyalidir)
- [ ] Placeholder veya lorem ipsum metni var mi
- [ ] Gizli icerik var mi (display:none icinde SEO amaçli metin)
- [ ] Keyword stuffing var mi (asiri tekrar)

### 3.13 JavaScript SEO
- [ ] Kritik icerik server-side render (SSR) ediliyor mu
- [ ] JavaScript kapatildiginda icerik gorunuyor mu (CSR sorunu)
- [ ] Dahili linkler HTML `<a href>` olarak mi yoksa JS event ile mi
- [ ] Google'in renderlayabildigi JS framework'u kullaniliyor mu
- [ ] JavaScript hatalarinda fallback icerik var mi
- [ ] Lazy-loaded icerik tarayicilara gorunuyor mu

### 3.14 Sayfa Performansi ve Core Web Vitals Sinyalleri
HTML kaynagindan tespit edilebilecek performans sinyalleri:
- [ ] Render-blocking CSS/JS var mi (`<head>` icinde async/defer olmayan script)
- [ ] Kritik CSS inline mi
- [ ] Gereksiz buyuk DOM agaci var mi (1500+ node uyari)
- [ ] Preconnect/preload/prefetch ipuclari dogru kullanilmis mi
- [ ] Font yukleme stratejisi var mi (`font-display: swap`)
- [ ] Ucuncu parti scriptlerin sayisi ve etkisi
- [ ] Asiri buyuk inline CSS/JS bloklari var mi
- [ ] Gereksiz JavaScript framework/kutuphane yuklenmis mi
- [ ] Gorsel boyutlari belirtilmis mi (CLS onleme)
- [ ] Animasyon/gecis efektleri layout shift olusturuyor mu

### 3.15 Erisebilirlik (Accessibility - SEO Etkisi)
- [ ] `<html lang>` ozelligi dogru mu
- [ ] ARIA landmark'lari kullanilmis mi (header, nav, main, footer)
- [ ] Form elemanlari icin `<label>` var mi
- [ ] Gorsel alt metinleri mevcut ve aciklayici mi
- [ ] Skip navigation linki var mi
- [ ] Tablo basliklari (`<th>`, `scope`) dogru mu
- [ ] Renk kontrast orani yeterli mi (WCAG AA: 4.5:1)
- [ ] Klavye navigasyonu destegi var mi
- [ ] aria-hidden icerik SEO icin onemli metni gizlemiyor mu

### 3.16 Sayfa Basi Teknik Kontroller
- [ ] `<!DOCTYPE html>` tanimli mi
- [ ] `<html>` etiketinde `lang` ozelligi var mi
- [ ] `<meta charset="UTF-8">` veya esdeger mevcut mu
- [ ] `<meta name="viewport">` mevcut mu
- [ ] Favicon tanimli mi (`<link rel="icon">`)
- [ ] Apple touch icon tanimli mi
- [ ] Manifest dosyasi tanimli mi (PWA)
- [ ] RSS/Atom feed linki var mi (blog siteleri icin)

---

## ADIM 4: AI ve LLM Uyumluluk Denetimi

Modern arama motorlari ve yapay zeka sistemleri icin ek kontroller:

### 4.1 llms.txt Dosyasi
- [ ] `{site-url}/llms.txt` dosyasi mevcut mu
- [ ] Icerik dogru formatlanmis mi
- [ ] Site hakkinda yeterli bilgi veriyor mu

### 4.2 AI Tarayici Yonetimi
- [ ] robots.txt'de AI tarayicilari icin kurallar tanimli mi
  - GPTBot (OpenAI)
  - ChatGPT-User (OpenAI)
  - Google-Extended (Google AI)
  - anthropic-ai (Anthropic)
  - CCBot (Common Crawl)
  - Bytespider (ByteDance)
  - PerplexityBot
  - ClaudeBot
- [ ] AI tarayici politikasi bilinçli olarak belirlenmis mi (izin/engel)

### 4.3 AI Icin Icerik Yapilandirmasi
- [ ] Icerik acik ve yapilandirilmis mi (AI'larin anlamlandirabilecegi sekilde)
- [ ] Yapilandirilmis veri (Schema.org) eksiksiz mi
- [ ] Semantik HTML dogru kullanilmis mi
- [ ] Ozetlenebilir ve alintilanabilir paragraflar var mi
- [ ] E-E-A-T sinyalleri mevcut mu (Experience, Expertise, Authoritativeness, Trustworthiness)
  - Yazar bilgisi
  - Kaynak referanslari
  - Iletisim bilgileri
  - Hakkimizda sayfasi

---

## ADIM 5: Sayfalandirma ve Faceted Navigation Denetimi

### 5.1 Sayfalandirma (Pagination)
- [ ] Sayfalandirilmis icerik dogru yapilandirilmis mi
- [ ] `rel="next"` ve `rel="prev"` (kaldirildi ama bazi motorlar kullanir)
- [ ] Tum sayfalandirilmis sayfalar sayfa 1'e canonical gostermemis mi (genellikle hatali)
- [ ] Sayfalandirma dongusu yok mu
- [ ] Sayfalandirmada kirik sayfa yok mu
- [ ] Sonsuz kaydirma (infinite scroll) durumunda HTML fallback var mi

### 5.2 Faceted Navigation / Filtre Sayfalari
- [ ] Filtre/siralama URL'leri gereksiz indeksleniyor mu
- [ ] noindex veya canonical cozumu uygulanmis mi
- [ ] Parametre patlamasi crawl budget'i tuketiyor mu

---

## ADIM 6: Site Goc (Migration) Kontrolleri
(Eger site yeni yayina alinacaksa veya yakinda goc yapilacaksa)

- [ ] Eski URL'lerden yeni URL'lere 301 yonlendirme haritasi hazir mi
- [ ] Yeni site tum eski icerigi kapsiyor mu
- [ ] Yeni sitemap.xml hazir mi
- [ ] robots.txt guncel mi (staging ortami engeli kaldirildi mi!)
- [ ] noindex etiketleri staging/development'tan kaldirildi mi
- [ ] Canonical URL'ler yeni domain'i gosteriyor mu
- [ ] Hreflang etiketleri yeni URL'lere guncellenmi mi
- [ ] Structured data yeni URL'lere guncelmi
- [ ] Google Search Console'a yeni site eklenmis mi
- [ ] DNS ve sunucu ayarlari dogru mu

---

## PUANLAMA SISTEMI

Her sayfayi ve site genelini asagidaki kategorilerde puanla. Her kategori 100 uzerinden puanlanir, genel skor agirlikli ortalama ile hesaplanir.

### Kategori Agirliklari (Toplam: 100)

| Kategori | Agirlik | Aciklama |
|----------|---------|----------|
| Crawlability & Indexability | 15 | robots.txt, sitemap, canonical, meta robots |
| On-Page SEO Elements | 12 | title, meta description, headings, alt text |
| URL Yapisi & Yonlendirmeler | 10 | temiz URL, redirect zincirleri, tutarlilik |
| Dahili Link Yapisi | 10 | crawl derinligi, orphan sayfa, kirik link |
| HTTPS & Guvenlik | 10 | SSL, guvenlik basliklari, mixed content |
| Structured Data | 10 | schema.org, JSON-LD, gecerlilik |
| Mobil Uyumluluk | 8 | viewport, tap target, responsive |
| Performans Sinyalleri | 8 | render-blocking, DOM boyutu, gorsel optimizasyon |
| Duplicate Icerik | 7 | title/desc tekrari, canonical uygulamasi |
| Uluslararasi SEO | 5 | hreflang (cok dilli siteler icin, yoksa diger kategorilere dagit) |
| Sosyal Medya Etiketleri | 3 | OG, Twitter Cards |
| AI/LLM Uyumluluk | 2 | llms.txt, AI tarayici politikasi |

### Oncelik Seviyeleri

Tespit edilen her sorunu asagidaki oncelik seviyeleriyle siniflandir:

- **P0 - KRITIK**: Indekslemeyi, taranabilirligI veya site erisimini dogrudan engelleyen sorunlar. HEMEN duzeltilmeli.
  - Ornek: robots.txt tum siteyi engelliyor, SSL sertifikasi suresi dolmus, anasayfa noindex, sitemap yok
- **P1 - YUKSEK**: Arama siralmasini ve gorunurlugu onemli olcude etkileyen sorunlar. 1 hafta icinde duzeltilmeli.
  - Ornek: duplicate title/description, kirik dahili linkler, canonical hatalari, eksik H1
- **P2 - ORTA**: SEO performansini olculu derecede etkileyen sorunlar. 1 ay icinde duzeltilmeli.
  - Ornek: eksik alt text, eksik structured data, eksik OG etiketleri, redirect zinciri
- **P3 - DUSUK**: En iyi uygulama onerileri. Iyilestirme firsatlari. Zaman buldukca duzeltilmeli.
  - Ornek: eksik twitter:card, gorsel dosya adlari, font-display eksik

---

## RAPOR FORMATI

Analiz tamamlandiginda asagidaki formatta kapsamli rapor olustur:

```
# TEKNIK SEO DENETIM RAPORU

**Site:** [site URL]
**Denetim Tarihi:** [tarih]
**Taranan Sayfa Sayisi:** [sayi]
**Genel SEO Skoru:** [X/100]

---

## YONETICI OZETI

[3-5 cumlelik genel degerlendirme. Sitenin teknik SEO sagligi, en kritik sorunlar ve oncelikli aksiyonlar.]

### Skor Dagilimi
| Kategori | Skor | Durum |
|----------|------|-------|
| Crawlability & Indexability | X/100 | OK/UYARI/HATA |
| On-Page SEO Elements | X/100 | OK/UYARI/HATA |
| URL Yapisi & Yonlendirmeler | X/100 | OK/UYARI/HATA |
| ... | ... | ... |

### Sorun Ozeti
| Oncelik | Sayi | Aciklama |
|---------|------|----------|
| P0 - Kritik | X | ... |
| P1 - Yuksek | X | ... |
| P2 - Orta | X | ... |
| P3 - Dusuk | X | ... |

---

## SITE GENELI BULGULAR

### robots.txt
[Durum ve bulgular]

### XML Sitemap
[Durum ve bulgular]

### HTTPS & Guvenlik
[Durum ve bulgular]

### Dahili Link Yapisi
[Crawl derinligi haritasi, orphan sayfalar, kirik linkler]

### Duplicate Icerik Sorunlari
[Duplicate title, description, H1 listesi]

### AI/LLM Uyumluluk
[llms.txt, AI tarayici politikasi durumu]

---

## SAYFA BAZINDA BULGULAR

Her sayfa icin asagidaki formatta raporla:

### [Sayfa URL'si]
**HTTP Status:** [200/301/404/...]
**Crawl Derinligi:** [anasayfadan kac tik]
**Sayfa Skoru:** [X/100]

| Kontrol | Durum | Detay | Oncelik |
|---------|-------|-------|---------|
| Title | OK/HATA | [mevcut deger ve sorun] | P0-P3 |
| Meta Description | OK/HATA | [mevcut deger ve sorun] | P0-P3 |
| H1 | OK/HATA | [mevcut deger ve sorun] | P0-P3 |
| Canonical | OK/HATA | [mevcut deger ve sorun] | P0-P3 |
| Schema.org | OK/HATA | [mevcut tur ve eksikler] | P0-P3 |
| Gorseller | OK/HATA | [X gorsel, Y alt text eksik] | P0-P3 |
| ... | ... | ... | ... |

[Sayfa icin ozel oneriler]

---

## AKSYON PLANI

Oncelik sirasina gore yapilmasi gerekenler:

### Hemen Yapilmasi Gerekenler (P0)
1. [Aksyon - etkilenen sayfalar - nasil duzeltilecegi]
2. ...

### Bu Hafta Yapilmasi Gerekenler (P1)
1. [Aksyon - etkilenen sayfalar - nasil duzeltilecegi]
2. ...

### Bu Ay Yapilmasi Gerekenler (P2)
1. [Aksyon - etkilenen sayfalar - nasil duzeltilecegi]
2. ...

### Iyilestirme Firsatlari (P3)
1. [Aksyon - etkilenen sayfalar - nasil duzeltilecegi]
2. ...

---

## TEKNIK DETAYLAR

### Taranan Sayfalar Listesi
| # | URL | Status | Skor | Sorun Sayisi |
|---|-----|--------|------|-------------|
| 1 | /   | 200    | X/100| X           |
| 2 | /hakkimizda | 200 | X/100 | X      |
| ... | ... | ... | ... | ... |

### Sitemap Analizi Detayi
[Sitemap icerigi ve sorunlar]

### Yonlendirme Haritasi
[Tespit edilen yonlendirmeler ve zincirleri]

### Guvenlik Basliklari Tablosu
| Baslik | Deger | Durum |
|--------|-------|-------|
| HSTS | ... | OK/EKSIK |
| CSP | ... | OK/EKSIK |
| ... | ... | ... |
```

---

## ONEMLI CALISMA KURALLARI

1. **Turkce Raporla**: Tum ciktilari Turkce olarak ver.
2. **Sayfa Bazinda Raporla**: Her sayfanin sorunlarini ayri ayri goster, genel bir liste yerine hangi sayfada hangi hata oldugu net olmali.
3. **Somut Oneriler Sun**: Her sorun icin nasil duzeltilecegini acikla. Mumkunse ornek HTML/kod parcasi ver.
4. **Oncelik Sirala**: P0 > P1 > P2 > P3 sirasinda raporla, en kritik sorunlar en ustte.
5. **Makul Sinir Koy**: 50'den fazla sayfa varsa ilk 50'yi tara, kullaniciyi bilgilendir.
6. **Paralel Calis**: Mumkun oldugunda birden fazla sayfayi paralel olarak analiz et (Agent tool kullanarak).
7. **Kaynak Kodu da Kontrol Et**: Eger kullanici bir proje dizinindeyse ve HTML/template dosyalari mevcutsa, dogrudan kaynak kodunu da analiz et (WebFetch'e ek olarak).
8. **False Positive'den Kacin**: Emin olmadigin bulgulari "olasi sorun" olarak isaretle, kesin hata olarak gosterme.
9. **Basarili Kontrolleri de Goster**: Sadece hatalari degil, basarili kontrolleri de raporla ki kullanici neyin dogru oldugunu da bilsin.
10. **Ciktiyi Dosyaya Kaydet**: Raporu kullanicinin calisma dizinine `seo-audit-report-[domain]-[tarih].md` olarak da kaydet.
