---
name: project-init
description: "Yeni proje baslatir. CLAUDE.md, .cursorrules, git init, dizin yapisi ve temel yapilandirma dosyalarini olusturur. WordPress, AstroJS, Next.js ve statik HTML projeleri icin kullan."
argument-hint: "[proje-adi] [proje-turu] [musteri-adi]"
allowed-tools: Read, Write, Bash, Glob
user-invocable: true
effort: high
---

# Yeni Proje Baslatma Skili

Gorevin, yeni bir web projesi icin gelistirme ortamini hizli ve standart bir sekilde kurmak. CLAUDE.md, .cursorrules, git ve dizin yapisi dahil.

## Argumanlar

- `$ARGUMENTS[0]`: Proje adi (ornek: lavitadoor, mutfak304, eyeglow)
- `$ARGUMENTS[1]`: Proje turu (wordpress, astro, nextjs, html — varsayilan: wordpress)
- `$ARGUMENTS[2]`: Musteri/firma adi (opsiyonel)

---

## ADIM 1: Dizin Yapisi Olusturma

### WordPress Projesi
```
{proje-adi}/
├── CLAUDE.md
├── .cursorrules
├── .gitignore
├── wp-content/
│   ├── themes/
│   │   └── {proje-adi}-theme/
│   │       ├── style.css
│   │       ├── functions.php
│   │       ├── header.php
│   │       ├── footer.php
│   │       ├── index.php
│   │       ├── assets/
│   │       │   ├── css/
│   │       │   ├── js/
│   │       │   ├── images/
│   │       │   └── fonts/
│   │       └── template-parts/
│   └── plugins/
└── docs/
    └── notes.md
```

### AstroJS Projesi
```
{proje-adi}/
├── CLAUDE.md
├── .cursorrules
├── .gitignore
├── astro.config.mjs
├── tailwind.config.mjs
├── tsconfig.json
├── package.json
├── src/
│   ├── layouts/
│   │   └── BaseLayout.astro
│   ├── pages/
│   │   └── index.astro
│   ├── components/
│   ├── styles/
│   │   └── global.css
│   ├── content/
│   ├── utils/
│   └── assets/
│       └── images/
├── public/
│   ├── favicon.svg
│   └── robots.txt
└── docs/
    └── notes.md
```

### Next.js Projesi
```
{proje-adi}/
├── CLAUDE.md
├── .cursorrules
├── .gitignore
├── next.config.js
├── tailwind.config.js
├── tsconfig.json
├── package.json
├── src/
│   ├── app/
│   │   ├── layout.tsx
│   │   ├── page.tsx
│   │   └── globals.css
│   ├── components/
│   │   ├── ui/
│   │   └── shared/
│   ├── lib/
│   ├── hooks/
│   ├── types/
│   └── assets/
├── public/
│   ├── favicon.ico
│   └── robots.txt
└── docs/
    └── notes.md
```

### Statik HTML Projesi
```
{proje-adi}/
├── CLAUDE.md
├── .cursorrules
├── .gitignore
├── index.html
├── assets/
│   ├── css/
│   │   └── style.css
│   ├── js/
│   │   └── main.js
│   ├── images/
│   └── fonts/
├── pages/
└── docs/
    └── notes.md
```

---

## ADIM 2: CLAUDE.md Olusturma

Proje turune gore ozellestirilmis CLAUDE.md olustur:

```markdown
# {Proje Adi}

## Proje Bilgileri
- **Musteri:** {musteri adi}
- **Proje Turu:** {wordpress/astro/nextjs/html}
- **Baslangic Tarihi:** {tarih}
- **Durum:** Gelistirme asamasinda

## Teknoloji Stack
{proje turune gore otomatik doldur}

## Proje Yapisi
{dizin agaci}

## Gelistirme Kurallari
{proje turune gore kurallar — asagidaki sablonlardan sec}

## SEO Gereksinimleri
- Tum sayfalarda benzersiz title ve meta description olmali
- Schema.org JSON-LD her sayfada olmali
- Gorsellerde alt text zorunlu
- Semantic HTML kullan (header, nav, main, article, footer)
- Core Web Vitals hedefleri: LCP < 2.5s, CLS < 0.1, INP < 200ms

## Deployment
{proje turune gore deployment bilgileri}
```

### WordPress CLAUDE.md Kurallar Sablonu
```
## Gelistirme Kurallari
- PHP 8.2+ uyumlu kod yaz
- WordPress Coding Standards'a uy
- Elementor kullaniliyorsa: ozel widget'lar icin PHP class yapisi kullan
- functions.php'yi temiz tut, buyuk islevleri ayri dosyalara bol
- Enqueue ile CSS/JS yukle (inline yazma)
- Veritabani islemlerinde $wpdb->prepare() kullan (SQL injection onleme)
- Nonce dogrulama kullan (CSRF onleme)
- esc_html(), esc_attr(), esc_url() ile cikti temizle (XSS onleme)
- wp_kses_post() ile HTML icerigi temizle
- Yonetici paneli ozellestirmelerinde admin_menu ve admin_init hook'larini kullan
- ACF kullaniliyorsa: get_field() ile veri cek, the_field() ile goster
- WooCommerce hook'lari: woocommerce_before/after_* sablonunu takip et
- Coklu dil destegi gerekiyorsa: WPML/Polylang uyumlu string ceviri kullan
```

### AstroJS CLAUDE.md Kurallar Sablonu
```
## Gelistirme Kurallari
- Astro component'leri (.astro) tercih et, React/Vue sadece interaktif UI icin
- Tailwind CSS kullan, ozel CSS minimum tut
- Content Collections ile icerik yonet
- TypeScript kullan (strict mode)
- Gorselleri src/assets/ altinda tut (Astro Image ile optimize edilir)
- SSG (Static Site Generation) varsayilan, SSR sadece gerektiginde
- Sayfa bazli SEO: title, description, og etiketleri her sayfada olmali
- Semantic HTML kullan
- Component prop'larinda TypeScript interface tanimla
- Sanity CMS kullaniliyorsa: GROQ sorgularini lib/ altinda topla
```

### Next.js CLAUDE.md Kurallar Sablonu
```
## Gelistirme Kurallari
- App Router kullan (pages degil)
- Server Components varsayilan, 'use client' sadece gerektiginde
- TypeScript strict mode
- Tailwind CSS kullan
- Supabase kullaniliyorsa: server-side client ve client-side client ayir
- API route'lari app/api/ altinda
- Metadata API ile SEO (generateMetadata)
- next/image ile gorsel optimizasyon
- next/font ile font yukleme
- Loading.tsx ve error.tsx dosyalari ekle
- Environment variable'lari .env.local'da tut
```

---

## ADIM 3: .cursorrules Olusturma

Proje turune gore .cursorrules dosyasi olustur:

```
# {Proje Adi} - Cursor Rules

## Proje Bağlamı
{proje aciklamasi}

## Teknoloji Stack
{teknoloji listesi}

## Kod Stili
{proje turune gore kurallar}

## Dosya Organizasyonu
{dizin kurallari}

## Onemli Notlar
- Her degisiklikte SEO etkisini dusun
- Mobile-first yaklasim kullan
- Turkce yorum yaz
- Performans oncelikli calis
```

---

## ADIM 4: Git Baslat

```bash
cd {proje-dizini}
git init
git add .
git commit -m "Initial project setup: {proje-adi} ({proje-turu})"
```

### .gitignore (proje turune gore)

**WordPress:**
```
node_modules/
.env
*.log
wp-config-local.php
/wp-content/uploads/
/wp-content/cache/
/wp-content/upgrade/
.DS_Store
Thumbs.db
```

**AstroJS / Next.js:**
```
node_modules/
dist/
.next/
.env
.env.local
*.log
.DS_Store
Thumbs.db
.vercel
```

---

## ADIM 5: Temel Dosyalari Olustur

Proje turune gore baslangic dosyalarini icerikleriyle birlikte olustur. Bos dosya birakma — minimum calisir bir baslangic noktasi sagla.

### WordPress: Minimum Tema Dosyalari
- style.css (tema bilgileri)
- functions.php (temel enqueue, tema destekleri)
- header.php (DOCTYPE, head, nav)
- footer.php (footer, wp_footer)
- index.php (temel loop)

### AstroJS: Minimum Dosyalar
- BaseLayout.astro (HTML shell, head, slot)
- index.astro (anasayfa)
- global.css (Tailwind directives)
- astro.config.mjs (Tailwind, sitemap entegrasyonu)

### Next.js: Minimum Dosyalar
- layout.tsx (RootLayout, metadata)
- page.tsx (anasayfa)
- globals.css (Tailwind directives)

---

## CIKTI

Proje olusturuldugunda kullaniciya asagidaki ozeti goster:

```
# PROJE KURULUMU TAMAMLANDI

**Proje:** {proje-adi}
**Tur:** {proje-turu}
**Dizin:** {tam yol}

## Olusturulan Dosyalar
- CLAUDE.md
- .cursorrules
- .gitignore
- {proje turune ozel dosyalar listesi}

## Sonraki Adimlar
1. {proje turune gore ilk adim}
2. {proje turune gore ikinci adim}
3. ...
```

## ONEMLI KURALLAR
1. Proje dizinini kullanicinin calisma dizininde olustur
2. Mevcut bir dizin varsa USTUNE YAZMA — kullaniciyi uyar
3. CLAUDE.md'yi projeye ozel yapilandir, generic birakma
4. Git commit mesaji aciklayici olsun
5. Baslangic dosyalari CALISIR durumda olsun (bos dosya birakma)
6. SEO temellerini en basindan kur (semantic HTML, meta etiketler)
