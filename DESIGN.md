# DESIGN SYSTEM — mustafauner.com.tr
> Portfolyo sitesinin bütüncül tasarım sistemi. Yeni bileşen, makale veya araç geliştirirken bu doküman tek kaynak olarak kullanılır.

---

## 1. Tasarım Felsefesi

Site üç prensip üzerine inşa edilmiştir:

- **Teknik Otoriye** — Her görsel karar mühendislik kimliğini yansıtır. Grid arka planlar, terminal simülasyonları, monospaced fontlar tesadüf değil; marka dilidir.
- **Karanlık + Amber** — Koyu zemin üzerinde amber/altın aksanlar; CNC makine arayüzlerinden, enerji ölçerlerden ilham alan bir estetik.
- **Veri Önce** — Animasyon ve dekorasyon, içeriğin önüne geçmez. Tüm süsleme `pointer-events: none` ile işlevselliği engellememek üzere kurgulanmıştır.

---

## 2. Renk Sistemi (CSS Custom Properties)

```css
:root {
  /* Ana Aksanlar */
  --amber:    #f59e0b;   /* Birincil vurgu, CTA, aktif durumlar */
  --amber-dim:#92400e;   /* Hover geri planları, düşük güçlü vurgu */
  --gold:     #fbbf24;   /* Hover'da amber üstü parlaklık */

  /* Zemin Katmanları (Derinlik için 4 ton) */
  --ink:      #080810;   /* En derin arka plan — body */
  --ink-2:    #0f0f1a;   /* İkincil bölümler, stats, terminal */
  --ink-3:    #161625;   /* Kart zeminleri */
  --ink-4:    #1e1e30;   /* Input, sonuç kutuları, iç elementler */

  /* Metin Hiyerarşisi */
  --light:    #e2e8f0;   /* Ana gövde metni */
  --mist:     #94a3b8;   /* İkincil metin, label'lar */
  --white:    #f8fafc;   /* Başlıklar, aktif öğeler */
  --steel:    #334155;   /* Ayırıcılar, devre dışı sınırlar */

  /* Fonksiyonel Renkler */
  --danger:          #ef4444;   /* Hata mesajları, kritik uyarı */
  --teal:            #0d9488;   /* Kullanılmayan (rezerv) */
  --terminal-green:  #22c55e;   /* Başarı durumları, terminal success */
}
```

### Renk Kullanım Kuralları

| Kullanım Amacı | Değişken |
|---|---|
| Birincil buton, aktif nav linki, vurgu çizgisi | `--amber` |
| Section label, badge metin, ikon | `--amber` |
| Hover state (buton) | `--gold` |
| Kart arka planı | `--ink-3` |
| Input / form zemin | `--ink-4` |
| Gövde metni | `--light` |
| Placeholder, label | `--mist` |
| Başlıklar | `--white` |
| Border varsayılan | `rgba(var(--steel), 0.6)` veya `rgba(245,158,11,0.15)` |

> **Kural:** Amber'ı asla düz arka plan olarak kullanma; sadece vurgu, sınır ve metin aksanı olarak uygula.

---

## 3. Tipografi Sistemi

Site üç font ailesine sahiptir ve her birinin kesin rolü vardır:

```css
/* Google Fonts import — HEAD içinde mevcut */
font-family: 'Bebas Neue', sans-serif;   /* Display / Başlık */
font-family: 'DM Sans', sans-serif;      /* Gövde / Genel metin */
font-family: 'JetBrains Mono', monospace; /* Kod / Teknik etiket */
```

### Font Rolleri

| Font | Sınıf | Kullanım Alanı |
|---|---|---|
| **Bebas Neue** | `.display` | H1, H2 başlıklar, nav-logo, stat sayıları, badge büyük metin |
| **DM Sans** | (body default) | Paragraflar, açıklamalar, genel UI metni |
| **JetBrains Mono** | `.mono` | Nav linkler, label'lar, badge tag'ları, formüller, terminal, input değerleri |

### Boyut Skalası

```css
/* Hero Başlıklar */
font-size: clamp(56px, 8vw, 96px);   /* Ana isim */
font-size: clamp(28px, 4vw, 48px);   /* Alt başlık */
font-size: clamp(36px, 5vw, 56px);   /* Section title */

/* UI Elementler */
font-size: 9px;   /* Bebas Neue ile büyük görünür: badge, label, section-label, nav link */
font-size: 10px;  /* Buton metni, mono etiketler */
font-size: 12px;  /* Card açıklamaları, terminal satırları */
font-size: 14px;  /* Makale gövde metni */
font-size: 15px;  /* Hero açıklaması */

/* Letter-spacing — Mono/Bebas kombinasyonlarında kritik */
letter-spacing: 0.04em;   /* Bebas Neue başlıklar */
letter-spacing: 0.08em;   /* İkincil başlıklar */
letter-spacing: 0.15em;   /* Buton ve nav linkleri */
letter-spacing: 0.2em;    /* Section labelları */
letter-spacing: 0.25em-0.3em; /* Micro badge metin */
```

---

## 4. Spacing & Layout

```
Max Content Width:  1200px   (.section-inner, .nav-inner)
Section Padding:    100px 24px  (her section varsayılan)
Nav Height:         64px (fixed)
Card Gap (grid):    2px  (kasıtlı sıkı — "makine plakası" estetiği)
Card Gap (normal):  24px
```

### Grid Sistemi

Site içinde kullanılan grid şemaları:

```css
/* Hero */
grid-template-columns: 1fr 1fr;
gap: 64px;

/* Stats Bar */
grid-template-columns: repeat(4, 1fr);

/* Portfolio */
grid-template-columns: repeat(3, 1fr);
gap: 2px;

/* Skills */
grid-template-columns: repeat(2, 1fr);

/* TÜBİTAK */
grid-template-columns: 1fr 1fr;
gap: 24px;

/* Blog Layout */
grid-template-columns: 350px 1fr;

/* Tools Layout */
grid-template-columns: 280px 1fr;

/* Input Grid */
grid-template-columns: 1fr 1fr;
gap: 16px;
```

---

## 5. Bileşen Kütüphanesi

### 5.1 Butonlar

```html
<!-- Birincil (CTA) Buton -->
<a href="#" class="btn-primary">
  <i class="fa-solid fa-..."></i> ETİKET
</a>

<!-- Ghost (İkincil) Buton -->
<a href="#" class="btn-ghost">
  <i class="fa-solid fa-..."></i> ETİKET
</a>

<!-- Nav CTA (küçük, sınırlı) -->
<a href="#" class="nav-cta">İletişim</a>
```

**btn-primary:** Amber arka plan, koyu metin. Hover'da gold'a geçer + `translateY(-2px)` + amber box-shadow.
**btn-ghost:** Şeffaf zemin, mist renkli metin, steel border. Hover'da white border + white metin.

### 5.2 Section Başlıkları

Her içerik bölümü aynı 4 katmanlı başlık yapısını kullanır:

```html
<div class="section-label">Kategori Etiketi</div>
<h2 class="section-title">ANA<br><span>BAŞLIK</span></h2>
<p class="section-sub">Alt açıklama metni, maksimum 540px genişlik.</p>
```

- `.section-label` → Amber mono font, sol tarafında `::before` ile 24px çizgi
- `.section-title` → Bebas Neue, `<span>` içi amber renk
- `.section-sub` → DM Sans 300 weight, mist rengi

### 5.3 Kartlar

#### Tubitak / Proje Kartı
```html
<div class="tubitak-card reveal d1">
  <i class="fa-solid fa-[ikon] tubitak-card-bg"></i>  <!-- Dekoratif büyük ikon -->
  <div class="tubitak-logo-wrap">...</div>
  <div class="t-badge-group">
    <span class="t-badge program">Etiket</span>
    <span class="t-badge success"><i class="fa-solid fa-check"></i> Durum</span>
  </div>
  <h3 class="t-project-name">Proje Adı</h3>
  <div class="t-details">
    <div class="t-detail-item">
      <span class="label">ETIKET</span>
      <span class="val">Değer</span>
    </div>
  </div>
</div>
```

**Hover efekti:** `translateY(-4px)` + amber sınır opaklığı artar + sol kenardaki amber çizgi gözükür (her zaman `::before` ile).

#### Machine Card (Portfolyo)
```html
<div class="machine-card reveal d1" onclick="openModal('YOUTUBE_ID')">
  <div class="machine-card-bg" style="background-image: url('...');"></div>
  <div class="machine-card-inner">
    <div class="machine-num">01</div>
    <div>
      <div class="machine-title">MAKİNE ADI</div>
      <div class="machine-desc">Kısa açıklama</div>
    </div>
  </div>
  <div class="machine-play">
    <div class="play-btn"><i class="fa-solid fa-play" style="margin-left:3px"></i></div>
  </div>
</div>
```

`machine-card.featured` → `grid-column: span 2` ile iki sütun kaplar.

### 5.4 Badge'ler

```html
<!-- Section etiketi (mono, amber) -->
<div class="hero-badge">Senior R&D Project Leader</div>

<!-- Proje durum badge'leri -->
<span class="t-badge program">1501 Sanayi Ar-Ge Programı</span>
<span class="t-badge success"><i class="fa-solid fa-check"></i> Tamamlandı</span>

<!-- Timeline tag -->
<span class="tl-tag">B.Sc. Mech. Eng.</span>
```

### 5.5 Timeline Öğesi

```html
<div class="tl-item">
  <div class="tl-left reveal-right d1">   <!-- Sol içerik (sağa hizalı) -->
    <div class="tl-year">2013</div>
    <div class="tl-heading">BAŞLIK</div>
    <div class="tl-desc">Açıklama metni.</div>
    <span class="tl-tag">Etiket</span>
  </div>
  <div class="tl-center"><div class="tl-dot"></div></div>
  <div class="tl-right"></div>  <!-- Boş sağ (sadece sol doluysa) -->
</div>
```

Aktif (günümüz) dot için: `<div class="tl-dot active"></div>` — amber dolgu + pulse animasyonu.

### 5.6 Skill Bar

```html
<div class="skill-bar-wrap">
  <div class="skill-bar-top">
    <span class="skill-name">Beceri Adı</span>
    <span class="skill-pct">85%</span>
  </div>
  <div class="skill-bar-bg">
    <div class="skill-bar-fill" data-width="0.85"></div>
  </div>
</div>
```

Bar animasyonu JS ile `IntersectionObserver` aracılığıyla tetiklenir; `data-width` 0.0–1.0 arası değer alır.

### 5.7 Tool Panel (Hesaplama Aracı)

Her araç paneli aynı şemayı izler:

```html
<div id="t-[isim]" class="tool-panel [active?]">
  <svg class="tool-watermark" ...></svg>  <!-- Dekoratif arka plan SVG -->
  
  <div class="tool-panel-title">Araç Adı</div>
  <div class="tool-panel-formula">F = m × a | Birim: N</div>
  
  <!-- Tek Sonuç Kutusu (opsiyonel) -->
  <div class="result-box">
    <div class="result-value" id="[id]-result">0.00</div>
    <div class="result-unit">Birim Açıklaması</div>
  </div>
  
  <!-- Giriş Izgarası -->
  <div class="input-grid">
    <div class="input-field">
      <label>Girdi Adı (Birim)</label>
      <input type="number" id="[id]-param" class="tool-input">
      <!-- veya range slider -->
      <input type="range" id="[id]-param" min="1" max="100" value="50">
      <div class="input-row">
        <span class="input-label">P =</span>
        <span class="input-val" id="[id]-val">50</span>
      </div>
    </div>
  </div>
  
  <!-- Çoklu Sonuç Izgarası (opsiyonel) -->
  <div class="result-grid">
    <div class="result-card"><span class="result-card-label">Etiket</span><div class="result-card-value" id="res">—</div></div>
    <div class="result-card highlight"><span class="result-card-label">Ana Sonuç</span><div class="result-card-value" id="res2">—</div></div>
  </div>
</div>
```

### 5.8 Blog / Makale Bileşenleri

Makale içindeki zengin içerik elementleri:

```html
<!-- Teknik Callout Kutusu -->
<div class="tech-callout">
  <h4>Başlık</h4>
  <p>İçerik metni.</p>
</div>

<!-- Diyagram Sarmalayıcı -->
<div class="tech-diagram-wrap">
  <svg width="400" height="160" viewBox="0 0 400 160">...</svg>
</div>

<!-- Tablo -->
<div class="table-wrap">
  <table>
    <thead><tr><th>Başlık</th></tr></thead>
    <tbody><tr><td>Veri</td></tr></tbody>
  </table>
</div>

<!-- Inline kod -->
<code>fonksiyon_adi(param)</code>

<!-- Kod bloğu -->
<pre><code>Python kodu buraya</code></pre>
```

---

## 6. Animasyon Sistemi

### Scroll Reveal Sınıfları

```html
<!-- Aşağıdan yukarı -->
<div class="reveal">...</div>

<!-- Soldan sağa -->
<div class="reveal-left">...</div>

<!-- Sağdan sola -->
<div class="reveal-right">...</div>

<!-- Gecikme modifikatörleri (d1–d5) -->
<div class="reveal d1">  <!-- 0.1s gecikme -->
<div class="reveal d2">  <!-- 0.2s gecikme -->
<div class="reveal d3">  <!-- 0.3s gecikme -->
```

`IntersectionObserver` eleman görünür alana girince `.visible` sınıfı ekler ve CSS transition çalışır.

### Sayaç Animasyonu

```html
<div class="stat-num counter" data-target="15">0</div>
```

`data-target` değerine kadar sayarak çıkar. `IntersectionObserver` tetikler.

### Pulse Dot (Hero Badge)

```css
.hero-badge::before {
  animation: pulse-dot 2s ease-in-out infinite;
}
```

### Terminal Cursor Blink

```css
.term-cursor { animation: blink 1s step-end infinite; }
```

### Timeline Active Dot

```css
.tl-dot.active { animation: tl-pulse 2s ease-in-out infinite; }
```

---

## 7. SPA Yönlendirme Mimarisi

Site tek sayfa üçgen mimarisinde çalışır:

```
URL Hash      → Görünen View
#/ (default)  → #view-home
#/blog        → #view-blog
#/blog?id=X   → #view-blog + makale X yüklenir
#/tools       → #view-tools
```

Yeni view eklemek için:

1. HTML'e `<div id="view-[isim]" class="spa-view">...</div>` ekle
2. `router()` fonksiyonuna `else if (hash.startsWith('#/[isim]'))` bloğu ekle
3. Nav'a link ekle (hem `.nav-links` hem `.mobile-menu-content`)

---

## 8. Blog Makale Veri Şeması

```javascript
const articles = [
  {
    id: "art-benzersiz-id",       // URL'de kullanılır: #/blog?id=art-...
    date: "15 OCAK 2026",         // Türkçe büyük harf format
    tags: ["TAG1", "TAG2", "TAG3"], // İlk tag sidebar'da gösterilir
    title: "Makale Başlığı",
    readTime: "8 Dk",
    content: `                     // HTML string — prose class içine render edilir
      <h2>Bölüm</h2>
      <p>İçerik...</p>
      <div class="tech-callout">...</div>
      <div class="tech-diagram-wrap"><svg>...</svg></div>
      <div class="table-wrap"><table>...</table></div>
    `
  }
];
```

---

## 9. Yeni Hesaplama Aracı Ekleme

### Adım 1: Sidebar'a tab ekle
```html
<div class="tool-tab" data-target="t-yeni-arac">
  <i class="fa-solid fa-[ikon]"></i>
  <div class="tool-tab-text">
    <span class="tool-tab-name">Araç Adı</span>
    <span class="tool-tab-sub">Alt Başlık / Formül</span>
  </div>
</div>
```

### Adım 2: Panel HTML'i ekle
```html
<div id="t-yeni-arac" class="tool-panel">
  <!-- Watermark SVG, title, formula, input-grid, result-grid -->
</div>
```

### Adım 3: JS hesaplama fonksiyonu
```javascript
function calcYeniArac() {
  const param1 = parseFloat(document.getElementById('ya-param1').value);
  if (!param1 || isNaN(param1)) return;
  
  const sonuc = /* formül */;
  document.getElementById('ya-result').textContent = sonuc.toFixed(2);
}

document.getElementById('ya-param1').addEventListener('input', calcYeniArac);
// Sayfa yüklenince çalıştır:
calcYeniArac();
```

---

## 10. Responsive Kırılma Noktaları

```css
@media (max-width: 768px) {
  /* Tüm 2-sütun grid'ler → 1 sütun */
  /* Hero → tek sütun, fotoğraf üste */
  /* Stats → 2x2 grid */
  /* Desktop nav → display:none !important */
  /* mobile-menu-btn → görünür */
  /* Tools sidebar → yatay scroll (flex row) */
  /* Blog layout → tek sütun */
}
```

---

## 11. İkon Sistemi

**Font Awesome 6.4.0** kullanılır. Yaygın kullanılan ikonlar:

```
fa-solid fa-drafting-compass   → Makine Tasarımı
fa-brands fa-python            → Python / Hesaplamalı
fa-solid fa-industry           → Üretim
fa-solid fa-chart-line         → Ar-Ge / Liderlik
fa-solid fa-rotate             → Kesme Hızı
fa-solid fa-compress           → Piston
fa-solid fa-gear               → Dişli
fa-solid fa-bolt               → Tork
fa-solid fa-screwdriver        → Vidalı Mil
fa-solid fa-layer-group        → Tolerans
fa-solid fa-ruler-horizontal   → Sehim
fa-solid fa-book-open          → Blog
fa-solid fa-calculator         → Hesaplama Araçları
fa-solid fa-briefcase          → Portfolyo
fa-solid fa-check              → Başarı
fa-solid fa-microchip          → Elektronik/Yazılım
fa-solid fa-gears              → Mekanik Sistem
```

---

## 12. Arka Plan Dekorasyon Katmanları

Site görsel derinliği 4 katmanla sağlar (performans açısından `pointer-events: none`):

1. **Noise overlay** — `body::before` SVG feTurbulence, `opacity: 0.025`
2. **Hero grid** — `.hero-grid-bg` amber çizgi ızgarası + radial mask
3. **Hero glow** — `.hero-glow` amber radial gradient, `opacity: 0.07`
4. **Mouse glow** — `#mouse-glow` cursor takip eden ambient ışık, sadece desktop

---

## 13. Modal Kullanımı

```javascript
// YouTube videosunu aç
openModal('YOUTUBE_VIDEO_ID');

// Belirli saniyeden başlat
openModal('YOUTUBE_VIDEO_ID', 13);  // 13. saniyeden başlat

// Kapat
closeModal();
```

ESC tuşu ve modal dışı tıklama ile de kapanır.

---

## 14. Sorumluluk Reddi Bileşeni

Her araç panelinin altında standart uyarı bloğu kullanılır:

```html
<div class="disclaimer">
  <i class="fa-solid fa-shield-halved"></i>
  <div>
    <strong>Mühendislik Sorumluluk Reddi</strong>
    <p>Bu platformdaki algoritmalar ön tasarım süreçlerini hızlandırmak amacıyla hazırlanmıştır...</p>
  </div>
</div>
```

---

## 15. SEO & Meta Standartları

```html
<meta name="description" content="...">
<meta property="og:title" content="Mustafa Üner | Senior R&D Project Leader">
<meta property="og:description" content="...">
<meta property="og:image" content="https://mustafauner.com.tr/cv2.jpeg">
<meta property="og:url" content="https://mustafauner.com.tr">
<meta property="og:type" content="website">
```

Sitemap'te tüm hash rotaları kayıtlıdır (`sitemap.xml`).

---

*Son güncelleme: Mayıs 2026 — mustafauner.com.tr*
