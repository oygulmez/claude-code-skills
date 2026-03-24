---
name: design-system
description: "Proje icin tutarli bir tasarim sistemi olusturur. Renk paleti, tipografi olcegi, spacing sistemi, breakpoint'ler, component kutuphane yapisi, CSS degiskenleri (custom properties), Tailwind config ve global stiller. Spagetti kodu onler, her projede tutarli ve profesyonel gorunum saglar."
argument-hint: "[proje-adi] [sektor] [renk-tercihi]"
allowed-tools: WebFetch, WebSearch, Read, Write, Bash, Glob
user-invocable: true
effort: max
---

# Design System Olusturucu

Sen, Airbnb, Stripe, Linear ve Vercel duzeyinde design system'ler kurmus bir senior UI/UX muhendisisin. Gorevin, verilen proje icin tutarli, olceklenebilir ve modern bir tasarim altyapisi olusturmak. Bu sistem sayesinde projedeki her sayfa, her component ve her piksel tutarli olacak.

## Argumanlar

- `$ARGUMENTS[0]`: Proje adi
- `$ARGUMENTS[1]`: Sektor (saglik, e-ticaret, kurumsal, teknoloji, turizm, endustriyel vb.)
- `$ARGUMENTS[2]`: Renk tercihi veya mevcut marka rengi (opsiyonel — ornek: "#1E40AF", "mavi tonlari", "minimalist")

---

## ADIM 1: Tasarim Felsefesi ve Analiz

### 1.1 Sektor Analizi
Sektore gore tasarim yaklasiminI belirle:

| Sektor | Yaklaasim | Referans Stili |
|--------|----------|---------------|
| Saglik/Klinik | Temiz, guven veren, beyaz alan bol | Apple Health, Mayo Clinic |
| E-ticaret | Urun odakli, CTA belirgin, hizli | Shopify, Amazon |
| Kurumsal/Ajans | Modern, bold tipografi, animasyonlu | Linear, Stripe, Vercel |
| Teknoloji/SaaS | Minimalist, koyu tema secenegi, data-driven | GitHub, Notion, Figma |
| Turizm | Gorsel agirlikli, duygusal, sicak renkler | Airbnb, Booking |
| Endustriyel | Saglam, profesyonel, teknik detay | Caterpillar, Bosch |
| Restoran/Gida | Sicak, isah acici renkler, gorsel agirlikli | — |

### 1.2 Tasarim Prensipleri
Her design system su 5 prensip uzerine kurulur:
1. **Tutarlilik (Consistency):** Ayni eleman her yerde ayni gorunur
2. **Hiyerarsi (Hierarchy):** Onemli icerik one cikar
3. **Erisebilirlik (Accessibility):** WCAG AA uyumu
4. **Olceklenebilirlik (Scalability):** Yeni sayfalar eklendiginde sistem bozulmaz
5. **Performans (Performance):** Gereksiz CSS/JS yok, minimal ve optimize

---

## ADIM 2: Renk Sistemi (Color System)

### 2.1 Renk Paleti Olusturma

Her projede asagidaki renk katmanlari olmali:

```css
:root {
  /* === PRIMARY (Marka Rengi) === */
  --color-primary-50:  ;  /* En acik ton — arka planlar */
  --color-primary-100: ;
  --color-primary-200: ;
  --color-primary-300: ;
  --color-primary-400: ;
  --color-primary-500: ;  /* Ana ton — butonlar, linkler */
  --color-primary-600: ;  /* Hover durumu */
  --color-primary-700: ;
  --color-primary-800: ;
  --color-primary-900: ;  /* En koyu ton — basliklar */
  --color-primary-950: ;

  /* === SECONDARY (Destekleyici Renk) === */
  --color-secondary-50:  ;
  --color-secondary-500: ;
  --color-secondary-600: ;
  --color-secondary-900: ;

  /* === ACCENT (Vurgu Rengi — CTA, bildirim) === */
  --color-accent-500: ;
  --color-accent-600: ;

  /* === NEUTRAL (Gri Tonlar — Metin, border, arka plan) === */
  --color-neutral-0:   #FFFFFF;  /* Beyaz */
  --color-neutral-50:  #F9FAFB;  /* Sayfa arka plani */
  --color-neutral-100: #F3F4F6;  /* Kart arka plani */
  --color-neutral-200: #E5E7EB;  /* Border, ayirici */
  --color-neutral-300: #D1D5DB;  /* Deaktif border */
  --color-neutral-400: #9CA3AF;  /* Placeholder metin */
  --color-neutral-500: #6B7280;  /* Ikincil metin */
  --color-neutral-600: #4B5563;  /* Govde metni */
  --color-neutral-700: #374151;  /* Koyu metin */
  --color-neutral-800: #1F2937;  /* Basliklar */
  --color-neutral-900: #111827;  /* En koyu metin */
  --color-neutral-950: #030712;  /* Siyaha yakin */

  /* === SEMANTIC (Anlam Tasiyan Renkler) === */
  --color-success-50:  #F0FDF4;
  --color-success-500: #22C55E;
  --color-success-700: #15803D;

  --color-warning-50:  #FFFBEB;
  --color-warning-500: #F59E0B;
  --color-warning-700: #B45309;

  --color-error-50:  #FEF2F2;
  --color-error-500: #EF4444;
  --color-error-700: #B91C1C;

  --color-info-50:  #EFF6FF;
  --color-info-500: #3B82F6;
  --color-info-700: #1D4ED8;
}
```

### 2.2 Renk Kullanim Kurallari
- **Metin:** neutral-800 (baslik), neutral-600 (govde), neutral-400 (placeholder)
- **Arka Plan:** neutral-0 (sayfa), neutral-50 (alternatif section), neutral-100 (kart)
- **Border:** neutral-200 (varsayilan), primary-500 (aktif/focus)
- **Buton Primary:** primary-500 bg, neutral-0 text, primary-600 hover
- **Buton Secondary:** neutral-0 bg, neutral-700 text, neutral-200 border
- **Link:** primary-500, primary-600 hover, underline on hover
- **Hata:** error-500 text, error-50 bg
- **Basari:** success-500 text, success-50 bg

### 2.3 Kontrast Kontrolu
- Govde metni / arka plan: minimum 4.5:1 (WCAG AA)
- Buyuk metin / arka plan: minimum 3:1
- Buton metni / buton bg: minimum 4.5:1
- Her renk kombinasyonunu kontrast oranıyla birlikte belirt

### 2.4 Koyu Tema (Dark Mode) — Opsiyonel
Eger koyu tema istenirse, tum renk degiskenlerini `[data-theme="dark"]` veya `@media (prefers-color-scheme: dark)` altinda tanimla.

---

## ADIM 3: Tipografi Sistemi (Typography Scale)

### 3.1 Font Secimi
Sektore uygun 2 font oner (1 baslik, 1 govde — veya tek font):

| Sektor | Baslik Font | Govde Font | Neden |
|--------|------------|-----------|-------|
| Saglik | Inter / Plus Jakarta Sans | Inter | Temiz, guvenilir |
| Kurumsal | Sora / Clash Display | Inter / DM Sans | Modern, bold |
| E-ticaret | Inter / Nunito Sans | Inter | Okunabilir, notr |
| Teknoloji | Geist / JetBrains Mono | Geist / Inter | Minimal, teknik |
| Turizm | Playfair Display / Cormorant | Lato / Open Sans | Zarif, davetkar |
| Endustriyel | Barlow / Roboto | Roboto / Open Sans | Saglam, profesyonel |

### 3.2 Tipografi Olcegi (Type Scale)
Modular scale kullan (ratio: 1.25 — Major Third):

```css
:root {
  /* === FONT FAMILIES === */
  --font-heading: 'Inter', system-ui, sans-serif;
  --font-body: 'Inter', system-ui, sans-serif;
  --font-mono: 'JetBrains Mono', ui-monospace, monospace;

  /* === FONT SIZES (Modular Scale 1.25) === */
  --text-xs:   0.75rem;   /* 12px */
  --text-sm:   0.875rem;  /* 14px */
  --text-base: 1rem;      /* 16px — govde */
  --text-lg:   1.125rem;  /* 18px */
  --text-xl:   1.25rem;   /* 20px */
  --text-2xl:  1.5rem;    /* 24px */
  --text-3xl:  1.875rem;  /* 30px */
  --text-4xl:  2.25rem;   /* 36px */
  --text-5xl:  3rem;      /* 48px */
  --text-6xl:  3.75rem;   /* 60px — hero */

  /* === LINE HEIGHTS === */
  --leading-none:    1;
  --leading-tight:   1.25;
  --leading-snug:    1.375;
  --leading-normal:  1.5;     /* Govde metin */
  --leading-relaxed: 1.625;
  --leading-loose:   2;

  /* === FONT WEIGHTS === */
  --font-regular:  400;
  --font-medium:   500;
  --font-semibold: 600;
  --font-bold:     700;
  --font-extrabold: 800;

  /* === LETTER SPACING === */
  --tracking-tighter: -0.05em;
  --tracking-tight:   -0.025em;
  --tracking-normal:  0;
  --tracking-wide:    0.025em;
  --tracking-wider:   0.05em;
}
```

### 3.3 Tipografi Kullanim Kurallari

| Eleman | Font | Boyut | Agirlik | Line Height | Mobil Boyut |
|--------|------|-------|---------|-------------|-------------|
| Hero Baslik | heading | text-5xl / text-6xl | extrabold | tight | text-3xl / text-4xl |
| H1 | heading | text-4xl | bold | tight | text-2xl / text-3xl |
| H2 | heading | text-3xl | semibold | tight | text-xl / text-2xl |
| H3 | heading | text-2xl | semibold | snug | text-lg / text-xl |
| H4 | heading | text-xl | semibold | snug | text-lg |
| H5 | heading | text-lg | medium | snug | text-base |
| Govde (Body) | body | text-base | regular | normal | text-base |
| Govde Buyuk | body | text-lg | regular | relaxed | text-base |
| Kucuk Metin | body | text-sm | regular | normal | text-sm |
| Etiket/Badge | body | text-xs | medium | none | text-xs |
| Buton | body | text-sm / text-base | medium | none | text-sm |
| Nav Link | body | text-sm | medium | none | text-sm |

---

## ADIM 4: Spacing Sistemi (Boşluk ve Ölçü)

### 4.1 Base-8 Spacing Scale
Tum bosluklar 4px veya 8px'in katlari olmali (tutarlilik):

```css
:root {
  --space-0:   0;
  --space-0.5: 0.125rem;  /* 2px */
  --space-1:   0.25rem;   /* 4px */
  --space-1.5: 0.375rem;  /* 6px */
  --space-2:   0.5rem;    /* 8px */
  --space-2.5: 0.625rem;  /* 10px */
  --space-3:   0.75rem;   /* 12px */
  --space-4:   1rem;      /* 16px */
  --space-5:   1.25rem;   /* 20px */
  --space-6:   1.5rem;    /* 24px */
  --space-8:   2rem;      /* 32px */
  --space-10:  2.5rem;    /* 40px */
  --space-12:  3rem;      /* 48px */
  --space-16:  4rem;      /* 64px */
  --space-20:  5rem;      /* 80px */
  --space-24:  6rem;      /* 96px */
  --space-32:  8rem;      /* 128px */
}
```

### 4.2 Spacing Kullanim Kurallari

| Kullanim | Deger | Ornek |
|----------|-------|-------|
| Section padding (dikey) | space-16 / space-20 / space-24 | Section'lar arasi |
| Container padding (yatay) | space-4 (mobil), space-6 (tablet), space-8 (desktop) | Sayfa kenarlari |
| Kart ic bosluk (padding) | space-4 / space-6 | Kart icerigi |
| Elemanlar arasi (gap) | space-2 / space-4 / space-6 | Icerik araliklari |
| Baslik + paragraf arasi | space-2 / space-3 | Baslik altindaki metin |
| Form alanlari arasi | space-4 / space-5 | Input'lar arasi |
| Buton ic bosluk | space-2.5 (y), space-5 (x) | Buton padding |
| Badge ic bosluk | space-1 (y), space-2.5 (x) | Etiket padding |

---

## ADIM 5: Layout Sistemi

### 5.1 Container ve Grid

```css
:root {
  /* === CONTAINER === */
  --container-sm:  640px;
  --container-md:  768px;
  --container-lg:  1024px;
  --container-xl:  1280px;
  --container-2xl: 1440px;  /* Varsayilan max-width */

  /* === BREAKPOINTS === */
  --breakpoint-sm:  640px;   /* Kucuk telefon */
  --breakpoint-md:  768px;   /* Tablet */
  --breakpoint-lg:  1024px;  /* Kucuk desktop */
  --breakpoint-xl:  1280px;  /* Desktop */
  --breakpoint-2xl: 1536px;  /* Genis ekran */

  /* === GRID === */
  --grid-columns: 12;
  --grid-gap: var(--space-6);
}
```

### 5.2 Layout Kaliplari

```css
/* Container */
.container {
  width: 100%;
  max-width: var(--container-2xl);
  margin-inline: auto;
  padding-inline: var(--space-4);
}

@media (min-width: 768px) {
  .container { padding-inline: var(--space-6); }
}

@media (min-width: 1280px) {
  .container { padding-inline: var(--space-8); }
}

/* Section */
.section {
  padding-block: var(--space-16);
}

@media (min-width: 768px) {
  .section { padding-block: var(--space-20); }
}

@media (min-width: 1280px) {
  .section { padding-block: var(--space-24); }
}
```

---

## ADIM 6: Component Token'lari

### 6.1 Border ve Radius

```css
:root {
  /* === BORDER === */
  --border-width: 1px;
  --border-color: var(--color-neutral-200);

  /* === BORDER RADIUS === */
  --radius-none: 0;
  --radius-sm:   0.25rem;   /* 4px — input, badge */
  --radius-md:   0.375rem;  /* 6px — buton */
  --radius-lg:   0.5rem;    /* 8px — kart */
  --radius-xl:   0.75rem;   /* 12px — buyuk kart */
  --radius-2xl:  1rem;      /* 16px — modal */
  --radius-3xl:  1.5rem;    /* 24px — hero kart */
  --radius-full: 9999px;    /* Yuvarlak — avatar, pill */
}
```

### 6.2 Shadow (Golge)

```css
:root {
  --shadow-xs:  0 1px 2px 0 rgb(0 0 0 / 0.05);
  --shadow-sm:  0 1px 3px 0 rgb(0 0 0 / 0.1), 0 1px 2px -1px rgb(0 0 0 / 0.1);
  --shadow-md:  0 4px 6px -1px rgb(0 0 0 / 0.1), 0 2px 4px -2px rgb(0 0 0 / 0.1);
  --shadow-lg:  0 10px 15px -3px rgb(0 0 0 / 0.1), 0 4px 6px -4px rgb(0 0 0 / 0.1);
  --shadow-xl:  0 20px 25px -5px rgb(0 0 0 / 0.1), 0 8px 10px -6px rgb(0 0 0 / 0.1);
  --shadow-2xl: 0 25px 50px -12px rgb(0 0 0 / 0.25);
}
```

### 6.3 Gecis (Transition)

```css
:root {
  --transition-fast:   150ms ease;
  --transition-base:   200ms ease;
  --transition-slow:   300ms ease;
  --transition-slower: 500ms ease;

  /* Spesifik transition'lar */
  --transition-colors: color var(--transition-fast), background-color var(--transition-fast), border-color var(--transition-fast);
  --transition-shadow: box-shadow var(--transition-base);
  --transition-transform: transform var(--transition-base);
  --transition-all: all var(--transition-base);
}
```

### 6.4 Z-Index Sistemi

```css
:root {
  --z-behind:   -1;
  --z-base:     0;
  --z-dropdown: 10;
  --z-sticky:   20;
  --z-fixed:    30;
  --z-overlay:  40;
  --z-modal:    50;
  --z-popover:  60;
  --z-toast:    70;
  --z-tooltip:  80;
  --z-max:      9999;
}
```

---

## ADIM 7: Component Sablon Kutuphanesi

Her design system'de asagidaki temel component'lerin stil tanimlari olmali. CSS custom properties ile tanimla, framework'e ozel class'lari da ekle.

### 7.1 Button Variants

```css
/* Base Button */
.btn {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: var(--space-2);
  padding: var(--space-2.5) var(--space-5);
  font-size: var(--text-sm);
  font-weight: var(--font-medium);
  line-height: var(--leading-none);
  border-radius: var(--radius-md);
  transition: var(--transition-all);
  cursor: pointer;
  border: var(--border-width) solid transparent;
}

/* Primary */
.btn-primary {
  background: var(--color-primary-500);
  color: var(--color-neutral-0);
}
.btn-primary:hover {
  background: var(--color-primary-600);
}

/* Secondary / Outline */
.btn-secondary {
  background: var(--color-neutral-0);
  color: var(--color-neutral-700);
  border-color: var(--color-neutral-200);
}
.btn-secondary:hover {
  background: var(--color-neutral-50);
  border-color: var(--color-neutral-300);
}

/* Ghost */
.btn-ghost {
  background: transparent;
  color: var(--color-neutral-600);
}
.btn-ghost:hover {
  background: var(--color-neutral-100);
}

/* Sizes */
.btn-sm { padding: var(--space-1.5) var(--space-3); font-size: var(--text-xs); }
.btn-lg { padding: var(--space-3) var(--space-6); font-size: var(--text-base); }
```

### 7.2 Card

```css
.card {
  background: var(--color-neutral-0);
  border: var(--border-width) solid var(--color-neutral-200);
  border-radius: var(--radius-lg);
  padding: var(--space-6);
  box-shadow: var(--shadow-sm);
  transition: var(--transition-shadow);
}

.card:hover {
  box-shadow: var(--shadow-md);
}

.card-header { margin-bottom: var(--space-4); }
.card-body { margin-bottom: var(--space-4); }
.card-footer { padding-top: var(--space-4); border-top: var(--border-width) solid var(--color-neutral-100); }
```

### 7.3 Input / Form Fields

```css
.input {
  width: 100%;
  padding: var(--space-2.5) var(--space-3);
  font-size: var(--text-sm);
  line-height: var(--leading-normal);
  color: var(--color-neutral-800);
  background: var(--color-neutral-0);
  border: var(--border-width) solid var(--color-neutral-300);
  border-radius: var(--radius-md);
  transition: var(--transition-colors);
}

.input::placeholder { color: var(--color-neutral-400); }
.input:focus {
  outline: none;
  border-color: var(--color-primary-500);
  box-shadow: 0 0 0 3px rgb(var(--color-primary-500) / 0.1);
}
.input-error { border-color: var(--color-error-500); }
```

### 7.4 Badge / Tag

```css
.badge {
  display: inline-flex;
  align-items: center;
  padding: var(--space-1) var(--space-2.5);
  font-size: var(--text-xs);
  font-weight: var(--font-medium);
  border-radius: var(--radius-full);
}

.badge-primary { background: var(--color-primary-50); color: var(--color-primary-700); }
.badge-success { background: var(--color-success-50); color: var(--color-success-700); }
.badge-warning { background: var(--color-warning-50); color: var(--color-warning-700); }
.badge-error { background: var(--color-error-50); color: var(--color-error-700); }
```

### 7.5 Diger Component Sablonlari
Her proje icin gerektiginde asagidaki component'lerin de stillerini tanimla:
- Navigation (header, mobile menu, hamburger)
- Footer (multi-column, newsletter)
- Hero section (split, centered, background image)
- Feature grid (2-3-4 kolonlu)
- Testimonial / Review card
- Pricing table
- CTA section
- FAQ accordion
- Modal / Dialog
- Toast / Notification
- Breadcrumb
- Pagination
- Tab
- Tooltip

---

## ADIM 8: Tailwind CSS Config (Eger Tailwind Kullaniliyorsa)

Tum design token'larini Tailwind config'e aktar:

```js
// tailwind.config.mjs
export default {
  theme: {
    extend: {
      colors: {
        primary: {
          50: '',
          // ... 950'ye kadar
        },
        secondary: { /* ... */ },
        accent: { /* ... */ },
      },
      fontFamily: {
        heading: ['Inter', 'system-ui', 'sans-serif'],
        body: ['Inter', 'system-ui', 'sans-serif'],
        mono: ['JetBrains Mono', 'monospace'],
      },
      fontSize: { /* custom scale */ },
      spacing: { /* custom scale */ },
      borderRadius: { /* custom scale */ },
      boxShadow: { /* custom scale */ },
      transitionDuration: { /* custom scale */ },
      zIndex: { /* custom scale */ },
    },
  },
}
```

---

## ADIM 9: Elementor Global Settings (WordPress Projeleri Icin)

WordPress/Elementor kullaniliyorsa, design system'i Elementor'a da aktar:

### Elementor Site Settings
- **Global Colors:** Primary, Secondary, Text, Accent tanimla
- **Global Fonts:** Primary (baslik), Secondary (govde), Text, Accent tanimla
- **Layout:** Container max-width, default padding
- **Lightbox:** Tema renklerine uygun

### Elementor CSS Degiskenleri
Elementor kendi CSS degiskenlerini kullanir. Bunlari override et:
```css
:root {
  --e-global-color-primary: var(--color-primary-500);
  --e-global-color-secondary: var(--color-secondary-500);
  --e-global-color-text: var(--color-neutral-800);
  --e-global-color-accent: var(--color-accent-500);
}
```

---

## CIKTI FORMATI

```
# DESIGN SYSTEM — {Proje Adi}

**Sektor:** {sektor}
**Tarih:** {tarih}
**Yaklasim:** {minimalist/bold/elegant/teknik}

---

## Renk Paleti
[Tum renk degiskenleri + gorsel palet]

## Tipografi
[Font secimi + type scale + kullanim tablosu]

## Spacing
[Spacing scale + kullanim kurallari]

## Layout
[Container, grid, breakpoint tanimlari]

## Component Token'lari
[Border, radius, shadow, transition, z-index]

## Component Sablonlari
[Button, card, input, badge + diger]

## Uygulama Dosyalari
[Kopyala-yapistir hazir dosyalar:]
- globals.css veya style.css (tum CSS custom properties)
- tailwind.config.mjs (Tailwind kullaniliyorsa)
- Elementor ayarlari (WordPress ise)
```

## ONEMLI KURALLAR
1. Her design system KOPYALA-YAPISTIR hazir dosyalar uretmeli
2. Sektore uygun renk ve font secimi yap
3. Kontrast oranlarini kontrol et (WCAG AA)
4. Mobil-first yaklasim — once kucuk ekran, sonra buyut
5. CSS custom properties kullan (hardcoded deger YAZMA)
6. Tailwind kullaniliyorsa config dosyasini da uret
7. WordPress/Elementor ise global settings rehberi de ver
8. Eger proje dizininde dosyalar varsa, direkt olustur veya mevcut dosyalara ekle
9. Design system dosyasini projenin `docs/design-system.md` veya `src/styles/` altina kaydet
