# Product Requirements Document (PRD): Fadd Graphics Professional Link Tree

## 1. Executive Summary

**Project Name:** Fadd Graphics Professional Link Directory
**Document Status:** Final
**Target Platform:** Web (Mobile-First, Responsive Desktop)
**Core Tech Stack:** HTML5 (Semantic), Tailwind CSS 4 (via CDN), Vanilla JavaScript, Custom CSS.
**Design Language:** Apple Human Interface Guidelines (Light Theme), Minimalist, High Contrast, Glassmorphism.

**Objective:**
Membangun *landing page* mini (alternatif Linktree) yang sangat ringan (*super lightweight*), elegan, dan responsif. Halaman ini berfungsi sebagai sentralisasi tautan eksternal untuk Fadd Graphics, dirancang khusus untuk memaksimalkan *user experience* (UX) pada perangkat seluler tanpa mengorbankan estetika visual, dengan memprioritaskan performa rendering tinggi dan interaksi mikro yang sangat mulus (*smooth*).

---

## 2. Product Goals & Success Metrics

**Core Goals:**

* **Performa Maksimal:** Waktu muat halaman (*page load time*) di bawah 1 detik.
* **UX Tanpa Friksi:** Menyediakan navigasi yang intuitif dan cepat tanpa teks deskriptif yang bertele-tele.
* **Desain Premium:** Mengomunikasikan profesionalisme kelas dunia melalui estetika setingkat Apple (Light mode, tipografi bersih, ikonografi tegas).
* **Efisiensi Kode (*Clean Code*):** Struktur kode murni tanpa *bloatware*, tidak ada komentar dalam kode, serta menggunakan Vanilla JS dan SVG *in-line*.

**Success Metrics:**

* Lighthouse Score: 100/100 untuk *Performance*, *Accessibility*, *Best Practices*, dan *SEO*.
* *Cumulative Layout Shift* (CLS): 0 (Tidak ada lonjakan elemen saat dimuat).
* *Time to Interactive* (TTI): < 1.5 detik pada jaringan seluler menengah.

---

## 3. Design System & UI/UX Guidelines

*(Mengacu pada standar Apple Design Guidelines & DESIGN.md)*

### 3.1. Visual Language & Color Psychology

* **Tema Utama:** Terang (*Light Mode Only*). Menghasilkan kesan bersih, terbuka, dan profesional.
* **Palet Warna:**
* *Background Utama:* Netral sangat terang (`#f5f5f7` - *Zinc-100/50*).
* *Text Primary:* Hitam tajam/gelap pekat (`#18181b` - *Zinc-900*) untuk kontras maksimal.
* *Text Secondary:* Abu-abu menengah (`#71717a` - *Zinc-500*) untuk elemen non-kritis.
* *Ambient Backdrop:* Aksentuasi pendaran cahaya (*radial-gradient*) super halus di latar belakang untuk menghindari kesan datar.


* **Tipografi:**
* *Font Family:* Native OS Font Stack (`-apple-system, BlinkMacSystemFont, "SF Pro Display", "SF Pro Text", "Inter", "Helvetica Neue", sans-serif`).
* *Hierarchy:* Menggunakan kombinasi ukuran dan ketebalan huruf (bold/semibold untuk judul utama, medium untuk badan teks) daripada memperbesar ukuran font secara berlebihan.


* **Material (Glassmorphism Light):**
* *Kartu (*Cards*):* Latar belakang transparan tinggi (`rgba(255, 255, 255, 0.7)`).
* *Backdrop Filter:* Blur ekstrem (`blur(20px)`) untuk menangkap ambient latar belakang.
* *Border:* Sangat tipis (*hairline*) dengan tingkat transparansi tinggi (`rgba(0,0,0,0.05)`).
* *Shadow:* Bayangan sebar (*diffused drop shadow*) sangat halus (`0 4px 24px -1px rgba(0, 0, 0, 0.08)`).



### 3.2. User Experience (UX) Principles

* **Minimalis & Semantik:** Dilarang menggunakan deskripsi panjang. Komunikasi sepenuhnya bergantung pada kombinasi Ikon + *Headline* + Label mikro.
* **Mobile-First Approach:** Lebar kontainer utama dibatasi ketat (`max-w-md`), memusatkan fokus ke tengah area pandang pada semua perangkat. Area sentuh (*tap target*) dipastikan minimal 44x44pt.
* **Micro-interactions:**
* *Hover State:* Kartu membesar halus (`scale(1.01)`), bayangan menebal secara organik, dan latar menjadi lebih solid putih (`rgba(255,255,255,0.95)`).
* *Ikon Hover:* Ikonografi statis di sisi kanan (*chevron/arrow*) bergeser mulus ke kanan saat berinteraksi (*translate-x*).
* *Animasi Berbasis Transform:* Hanya memanipulasi properti komposit (opacity, transform) untuk memastikan animasi berjalan pada 60 FPS tanpa *layout recalculation*.



### 3.3. Ikonografi

* **Format:** Vektor murni (*SVG In-line*) di dalam HTML.
* **Styling:** Ikon memiliki *bounding box* membulat (`rounded-[12px]`) yang mewakili warna inti setiap *brand* atau tindakan (misal: Hijau Emerald untuk WhatsApp, Biru Indigo untuk Download Aplikasi), berpadu harmonis dengan estetika terang. Ikon itu sendiri menggunakan kontras tegas di dalam kotaknya.

---

## 4. Content Hierarchy & Feature Specifications

*(Mengacu pada struktur LINKS.md)*

Halaman distrukturkan dalam tiga zona vertikal: **Header (Identitas)**, **Main Navigation (Komersial & Portofolio)**, dan **Footer (Sosial Pribadi & Hak Cipta)**.

### 4.1. Header (Identity Area)

* **Logo/Avatar:** Bentuk lingkaran sempurna, *background* putih dengan teks *bold* "FG" hitam di tengah. Dikelilingi *border* abu-abu super halus.
* **Status Indicator:** Lingkaran hijau (*Emerald-500*) dengan garis luar putih tebal, ditempatkan memotong tepi bawah kanan avatar, menandakan status *Available*.
* **Brand Name (H1):** "Fadd Graphics" disandingkan dengan SVG lencana verifikasi biru berukuran kecil (sekelas UI Twitter/Instagram).
* **Tagline:** "Design & Digital Innovation" (Font kecil, *uppercase*, jarak antar huruf direnggangkan/*tracking-wide*, warna sekunder).

### 4.2. Main Navigation (Actionable Link Cards)

Setiap kartu harus terstruktur sebagai tag jangkar `<a>` mandiri yang membungkus seluruh area kartu (`display: flex`).

**Struktur Universal Kartu:**

1. **Kiri:** Ikon di dalam kotak melengkung (*rounded-box*).
2. **Tengah:** Teks Utama (atas) dan Teks Sekunder/URL (bawah), dibatasi properti *truncate* untuk keamanan *layout* layar kecil.
3. **Kanan:** Ikon panah interaktif (`chevron-right` statis beranimasi saat digulir).

**Hierarki Urutan Tautan (Wajib Dipatuhi):**

1. **Selected Portfolio:** (URL: `/portfolio`) -> *Highlighted styling* (gradasi latar biru sangat halus, teks utama disertai *badge* "Featured"). Warna ikon: Biru.
2. **Official Website:** (URL: `/`) -> Warna ikon: Abu-abu Netral (*Zinc*).
3. **Chat via WhatsApp:** (URL: `wa.me/...`) -> Warna ikon: Hijau (*Emerald*).
4. **Email Collaboration:** (URL: `mailto:...`) -> Warna ikon: Abu-abu Netral (*Zinc*).
5. **FaddDompet App v1.3.0:** (URL: `GitHub Release`) -> Teks utama disertai *badge* versi "v1.3.0". Warna ikon: Biru Nila (*Indigo*).
6. **Instagram:** (URL: `@fadd.graphics`) -> Warna ikon: Merah Muda (*Rose*).
7. **TikTok:** (URL: `@fadd.graphics`) -> Warna ikon: Gelap Pekat (*Zinc-800*).
8. **YouTube:** (URL: `@faddgraphics`) -> Warna ikon: Merah (*Red*).
9. **LinkedIn:** (URL: `/in/mufaddhol...`) -> Warna ikon: Biru Muda (*Sky*).
10. **GitHub:** (URL: `@fadd3079-prog`) -> Warna ikon: Gelap Pekat (*Zinc-800*).
11. **Support:** (URL: `tako.id`) -> Warna ikon: Kuning Keemasan (*Amber*).

### 4.3. Footer (Personal Zone)

* **Garis Pemisah:** Garis tipis transparan (*Zinc-200*) memisahkan zona komersial utama dengan area sosial pribadi.
* **Sub-heading:** "Personal & Social" (huruf kapital mikro, berjarak).
* **Deret Ikon Bundar:**
* Tautan: Personal Instagram & Threads.
* Styling: Tombol bundar kecil berbasis *glassmorphism* berisi ikon saja, tanpa teks, diposisikan secara horisontal (`flex-row`).


* **Copyright Text:** Tulisan sangat kecil di batas paling bawah. Tanggal tahun dirender secara dinamis melalui JavaScript ("© [Tahun] Fadd Graphics.").

---

## 5. Technical Requirements & Implementation

### 5.1. HTML Semantics & Structure

* Wajib mengikuti standar HTML5 murni.
* Struktur tulang punggung wajib ada: `<header>`, `<main>`, `<nav>` (untuk kartu tautan), `<section>` (untuk ikon sosial), dan `<footer>`.
* Tidak menggunakan *tag* `<div>` kosong secara berlebihan (*divitis*).

### 5.2. CSS Architecture

* Dianjurkan menggunakan basis *Tailwind CSS* untuk tata letak cepat (Grid, Flex, Spacing, Typography).
* Properti spesifik Apple UI (seperti `backdrop-filter: blur()`, efek *transition-timing-function* khusus) dianjurkan dikonfigurasi melalui Custom CSS terpisah atau konfigurasi khusus.
* **Batasan Ketat:** Seluruh kode wajib *Clean Code*. Tidak boleh memuat komentar (seperti `//` atau `/* */` atau `<!-- -->`) satu karakter pun.

### 5.3. JavaScript Requirements

* Kode logika harus dipisahkan di berkas terpisah (jika memungkinkan) atau ditempatkan dengan aman di batas terbawah *body*.
* Skrip difokuskan hanya untuk utilitas mikro (*dynamic copyright year*).
* **Batasan Ketat:** Tidak memuat kerangka kerja tambahan (React, Vue, jQuery). Murni Vanilla JavaScript. Bebas komentar.

### 5.4. SEO & Accessibility Checklist

* Setiap tag `<a>` harus memiliki `rel="noopener noreferrer"` jika targetnya adalah laman eksternal terbuka di tab baru (`target="_blank"`).
* Ikon sosial yang tidak memiliki teks kasat mata wajib menyertakan atribut `aria-label`.
* Kontras teks terhadap latar (terutama untuk mode terang) wajib memenuhi standar *WCAG AA Minimum*.

---

**End of PRD**