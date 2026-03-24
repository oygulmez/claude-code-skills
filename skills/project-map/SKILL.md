---
name: project-map
description: "Proje haritasini olusturur ve gunceller. Dosya yapisi, component haritasi, sayfa listesi, API endpoint'leri, bagimlilklar, yapilan isler ve kalan gorevleri tek bir dosyada tutar. Claude Code bu dosyayi okuyarak projeye hakim olur, tum dosyalari tekrar tekrar okumak zorunda kalmaz. Token tasarrufu saglar."
argument-hint: "[olustur|guncelle|durum]"
allowed-tools: Read, Write, Bash, Glob, Grep
user-invocable: true
effort: high
---

# Proje Haritasi Yonetim Skili

Gorevin, projenin tam bir haritasini olusturmak ve guncel tutmak. Bu harita sayesinde Claude Code projeye hakim olur, her seferinde tum dosyalari okumak zorunda kalmaz.

## Argumanlar

- `$ARGUMENTS[0]`: Islem turu
  - `olustur` veya `create` — Ilk kez proje haritasi olustur (projeyi tara)
  - `guncelle` veya `update` — Mevcut haritayi guncelle (degisiklikleri yansit)
  - `durum` veya `status` — Proje durumunu goster (ilerleme ozeti)
  - Bos birakilirsa: harita varsa guncelle, yoksa olustur

---

## PROJE HARITASI DOSYASI: PROJECT-MAP.md

Bu dosya projenin kok dizininde olusturulur ve asagidaki bolumleri icerir:

### Dosya Konumu
```
projem/
├── CLAUDE.md          ← Proje kurallari (Claude bunu zaten okur)
├── PROJECT-MAP.md     ← PROJE HARITASI (bu dosya)
├── src/
└── ...
```

### PROJECT-MAP.md Sablonu

```markdown
# PROJECT MAP — {Proje Adi}
> Son guncelleme: {tarih ve saat}
> Toplam dosya: {sayi} | Degisen dosya (son guncelleme): {sayi}

---

## 1. MIMARI OZET
[Projenin 3-5 cumlelik teknik ozeti. Teknoloji stack, mimari yaklasim, temel akis.]

## 2. DIZIN YAPISI
[Sadece onemli dizinler ve dosyalar — her dosya degil, yapinin iskeleti]
```
src/
├── components/     # UI componentleri (Button, Card, Header, Footer)
├── pages/          # Sayfa dosyalari (index, about, contact, blog/[slug])
├── layouts/        # Layout sablonlari (BaseLayout, BlogLayout)
├── styles/         # Global stiller (global.css, variables.css)
├── lib/            # Yardimci fonksiyonlar (api.ts, utils.ts, sanity.ts)
├── content/        # Icerik dosyalari (blog/, services/)
└── assets/         # Gorseller, fontlar
```

## 3. SAYFA HARITASI
| Sayfa | Dosya Yolu | Layout | Durum | Notlar |
|-------|-----------|--------|-------|--------|
| Anasayfa | src/pages/index.astro | BaseLayout | Tamamlandi | Hero + Services + CTA |
| Hakkimizda | src/pages/about.astro | BaseLayout | Devam ediyor | Takim bolumu eksik |
| Blog | src/pages/blog/[slug].astro | BlogLayout | Planlanıyor | Sanity CMS entegrasyonu |

## 4. COMPONENT HARITASI
| Component | Dosya Yolu | Kullanildigi Yerler | Props | Notlar |
|-----------|-----------|-------------------|-------|--------|
| Header | src/components/Header.astro | Tum sayfalar (BaseLayout) | - | Sticky, responsive |
| ServiceCard | src/components/ServiceCard.astro | index, services | title, desc, icon, href | 3'lu grid |

## 5. VERI KAYNAKLARI
| Kaynak | Tur | Dosya/URL | Aciklama |
|--------|-----|----------|----------|
| Blog yazilar | Sanity CMS | lib/sanity.ts | GROQ ile cekiliyor |
| Hizmetler | Statik | content/services.json | JSON dosyasindan |
| Iletisim formu | API | /api/contact | Resend ile mail |

## 6. STIL SISTEMI
| Degisken | Deger | Kullanim |
|----------|-------|---------|
| --color-primary | #1E40AF | Butonlar, linkler |
| --color-text | #1F2937 | Govde metni |
| --font-heading | Inter | Basliklar |
| --font-body | Inter | Govde |
| Container max | 1440px | Sayfa genisligi |

## 7. UCUNCU PARTI BAGIMLILIKLAR
| Paket | Versiyon | Ne Icin |
|-------|---------|---------|
| astro | 5.x | Framework |
| tailwindcss | 4.x | CSS |
| @sanity/client | 6.x | CMS |

## 8. ORTAM DEGISKENLERI
| Degisken | Nerede | Aciklama |
|----------|--------|----------|
| SANITY_PROJECT_ID | .env | Sanity proje ID |
| SANITY_DATASET | .env | production |
| RESEND_API_KEY | .env | Mail servisi |

## 9. YAPILAN ISLER (TAMAMLANAN)
- [x] Proje kurulumu ve yapilandirma (2026-03-24)
- [x] Design system olusturma (2026-03-24)
- [x] Header ve Footer componentleri (2026-03-25)
- [x] Anasayfa Hero section (2026-03-25)

## 10. DEVAM EDEN ISLER
- [ ] Hakkimizda sayfasi — takim bolumu eksik
- [ ] Blog sayfa sablonu — Sanity entegrasyonu bekliyor

## 11. KALAN ISLER (YAPILACAK)
- [ ] Iletisim sayfasi ve form
- [ ] SEO: meta etiketler, schema, sitemap
- [ ] Performans optimizasyonu
- [ ] KVKK/Gizlilik sayfasi
- [ ] Deploy ve yayina cikis kontrolu

## 12. SON DEGISIKLIKLER
| Tarih | Dosya | Degisiklik |
|-------|-------|-----------|
| 2026-03-25 | src/components/Header.astro | Mobil menu eklendi |
| 2026-03-25 | src/pages/index.astro | CTA section eklendi |

## 13. BILINEN SORUNLAR / NOTLAR
- Sanity webhook henuz yapilandirilmadi
- Mobil menude gecis animasyonu eksik
- OG gorselleri henuz olusturulmadi
```

---

## OLUSTURMA ISLEMI (create)

Proje haritasini sifirdan olusturmak icin:

### Adim 1: Proje Taramasi
1. Glob ile tum dosyalari tara (src/**, pages/**, components/** vb.)
2. package.json veya composer.json'dan bagimliliklari cek
3. .env.example veya .env'den ortam degiskenlerini listele (DEGERLERI GOSTERME)
4. Git log'dan son degisiklikleri cek
5. CLAUDE.md'den proje kurallarini oku

### Adim 2: Yapiyi Analiz Et
1. Sayfa dosyalarini tespit et (pages/, routes/)
2. Component dosyalarini tespit et (components/)
3. Layout dosyalarini tespit et (layouts/)
4. API endpoint'lerini tespit et (api/, routes/)
5. Stil dosyalarini tespit et (styles/, css/)
6. Icerik dosyalarini tespit et (content/, data/)

### Adim 3: PROJECT-MAP.md Olustur
Yukaridaki sablonu kullanarak dosyayi olustur ve projenin kok dizinine kaydet.

---

## GUNCELLEME ISLEMI (update)

Mevcut haritayi guncellemek icin:

### Adim 1: Degisiklikleri Tespit Et
1. Git diff ile son degisiklikleri bul
2. Yeni eklenen dosyalari tespit et
3. Silinen dosyalari tespit et
4. Degistirilen dosyalari not et

### Adim 2: Haritayi Guncelle
1. Mevcut PROJECT-MAP.md'yi oku
2. Degisen bolumleri guncelle (yeni dosyalar, silinen dosyalar)
3. "Son Degisiklikler" bolumunu guncelle
4. "Yapilan Isler" ve "Kalan Isler" bolumlerini guncelle
5. Tarih ve sayilari guncelle

### Adim 3: Kaydet
PROJECT-MAP.md'yi guncellenmis icerikiyle kaydet.

---

## DURUM ISLEMI (status)

Hizli proje durumu ozeti:
1. PROJECT-MAP.md'yi oku
2. Tamamlanan / devam eden / kalan is sayilarini goster
3. Son degisiklikleri goster
4. Bilinen sorunlari goster

---

## ONEMLI KURALLAR

1. **Hassas bilgi YAZMA**: .env degerlerini, API key'leri, sifreleri PROJECT-MAP.md'ye YAZMA. Sadece degisken adlarini listele.
2. **Kisa tut**: Her bolum ozetlenmeli. Dosya iceriklerini kopyalama, sadece ne oldugunu yaz.
3. **Guncelle tutma**: Her onemli degisiklikten sonra haritayi guncelle.
4. **Sayfa/component durumu**: Her ogemin durumunu belirt (tamamlandi, devam ediyor, planlanıyor).
5. **.gitignore'a EKLEME**: PROJECT-MAP.md git'e dahil olmali, takim arkadaslarin da gorsun.
6. **Token tasarrufu**: Bu dosyanin amaci Claude'un tum dosyalari okumadan projeye hakim olmasini saglamak. Gereksiz detaydan kacin.
