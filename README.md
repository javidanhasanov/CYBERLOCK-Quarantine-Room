

# CYBERLOCK: Quarantine Room  https://javidanhasanov.github.io/CYBERLOCK-Quarantine-Room/

**Kibertəhlükəsizlik simulyasiyası — veb əsaslı interaktiv təlim oyunu**

---

## 📋 İcmal

**CYBERLOCK: Quarantine Room** — istifadəçilərə real həyatda rast gəlinən kibertəhlükələri (fişinq, zəif şifrələr, şübhəli fayllar və s.) tanımağı öyrədən, brauzerdə işləyən, tək fayllı (single-file) interaktiv simulyasiya oyunudur. Oyun iştirakçını "karantin otağına" salır və 5 fərqli tapşırığı həll edərək kilidləri açmasını tələb edir.

Layihə heç bir xarici asılılıq (framework, kitabxana, build aləti) tələb etmir — **təmiz HTML + CSS + Vanilla JavaScript** ilə yazılıb və birbaşa brauzerdə açılır.

---

## 🎯 Məqsəd

Oyunun əsas məqsədi istifadəçilərə aşağıdakı praktiki kibertəhlükəsizlik bacarıqlarını aşılamaqdır:

- Fişinq e-maillərini tanımaq (saxta domen, təcili dil, şübhəli linklər)
- Güclü və zəif şifrələri ayırd etmək
- HTTPS kilidinin yalnız şifrələməni göstərdiyini, saytın etibarlılığını sübut etmədiyini anlamaq
- Təhlükəsiz şifrə yaratmaq qaydalarını tətbiq etmək
- İkiqat uzantılı faylları (`.jpg.exe`) və naməlum mənbədən gələn icra olunan faylları tanımaq

---

## ✨ Əsas Xüsusiyyətlər

Oyun Mexanikası
5 fərqli tapşırıq** — hər biri fərqli təhlükəsizlik mövzusunu əhatə edir
İki oyun rejimi** — Normal (10 dəqiqə) və Speedrun (4 dəqiqə)
Bal sistemi** — hər tapşırıq üçün 100 bal + bonuslar
İpucu sistemi** — hər tapşırıq üçün 3 mərhələli ipucu (−15 bal)
Cərimə mexanizmi** — ilk 2 səhv cəzasız, sonrakılar −10 bal
Nailiyyət nişanları (badges)** — "İlk cəhddə", "İpucusuz", "Sürətli", "Qüsursuz", "Yeni rekord"

İstifadəçi İnterfeysi (UI)
Windows 11 üslubunda **masaüstü mühiti** (desktop)
Pəncərə idarəetmə sistemi** — sürükləmə, minimuma/maksimuma endirmə, bağlama
Başlat menyusu (Start Menu)** — axtarış və son açılan tətbiqlər
Tapşırıq paneli (Taskbar)** — saat, taymer, bildirişlər, ipucu düyməsi
Bildiriş mərkəzi** — toast bildirişləri və oxunmamış sayğacı
Kontekst menyu (sağ klik)** — Mail tətbiqində mesaj əməliyyatları

### Texniki Xüsusiyyətlər
Tək fayl arxitekturası** — bütün kod bir `.html` faylında
Oflayn işləyir** — internet bağlantısı tələb etmir
localStorage davamlılığı** — oyun irəliləyişi avtomatik yadda saxlanılır
Event Bus (Pub/Sub)** — hadisə əsaslı genişləndirilə bilən arxitektura
Responsiv modal sistemi** — debrief, səhv cavab, sertifikat, rejim seçimi modalları

---

## 🎮 Tapşırıqlar

| # | Tətbiq | Tapşırıq | Mövzu | Həll Yolu |
|---|--------|----------|-------|-----------|
| 1 | **Mail** | Saxta E-mail | Fişinq e-maili | `paypa1-secure.com` domenli mesajı phishing kimi bildir |
| 2 | **Security Center** | Şifrə Gücü | Zəif/güclü şifrə | 6 şifrə kartını düzgün səbətlərə sürüklə (drag & drop) |
| 3 | **Browser** | Fişinq Linki | Saxta bank saytı | `bank-az.click` saytını "Saytı bildir" düyməsi ilə bildir |
| 4 | **Settings** | Şifrə Dəyişmə | Güclü şifrə yaratma | 12+ simvol, 4 kateqoriyadan ən azı 3-ü |
| 5 | **File Explorer** | Şübhəli Fayl | Zərərli fayllar | `photo.jpg.exe` və `free_vpn_installer.msi` fayllarını karantinə al |

Hər tapşırıq həll edildikdən sonra **"Debrief"** modalı açılır və üç suala cavab verir:
- **Nə oldu?** — tapşırığın texniki izahı
- **Niyə vacibdir?** — real dünyada təsiri
- **Necə qorunmalı?** — praktiki tövsiyələr

---

## 🏆 Bal Sistemi

| Hadisə | Bal |
|--------|-----|
| Tapşırıq həlli (əsas) | +100 |
| 30 saniyə ərzində həll | +20 |
| 3+ tapşırığı ardıcıl ilk cəhddə həll (streak) | ×1.2 |
| İpucu istifadəsi | −15 |
| Səhv cavab (3-cü və sonrakı) | −10 |

**Maksimum nəzəri bal:** ~840 bal (bütün bonuslar daxil)

---

## ⏱️ Taymer Sistemi

Normal rejim** — 10 dəqiqə
Speedrun rejimi** — 4 dəqiqə
- Sayğac **ilk tətbiq açılanda** başlayır (rejim seçimindən sonra)
- Son 60 saniyədə taymer **qırmızı rəngə** keçir
- Vaxt bitdikdə "Vaxt bitdi!" ekranı açılır
- Oyun yenilənəndə (refresh) qalan vaxt **qorunur** (timestamp əsaslı)

---

## 🏗️ Texniki Arxitektura

### Fayl Strukturu

```
index.html
├── <head>          → Meta, title
├── <body>
│   ├── #boot-screen      → Yükləmə ekranı
│   ├── #desktop          → Masaüstü mühiti
│   │   ├── #wallpaper
│   │   ├── #desktop-icons
│   │   ├── #lock-widget  → Bal + kilid göstəricisi
│   │   ├── #windows-layer
│   │   ├── #toast-container
│   │   ├── #start-menu
│   │   ├── #context-menu
│   │   ├── #notif-panel
│   │   └── #taskbar
│   ├── #modal-backdrop
│   ├── #escape-screen    → Oyun sonu ekranı
│   └── <script>          → Bütün tətbiq məntiqi (IIFE)
└── (CSS — inline <style> bloka daxil)
```

### JavaScript Modulları (bir IIFE daxilində)

| Modul | Təyinat |
|-------|---------|
| `S()` / `ICONS` | SVG ikon kitabxanası |
| `APPS` / `TASKS` | Tətbiq və tapşırıq təyinatları |
| `state` | Qlobal oyun vəziyyəti |
| `events` | Event Bus (Pub/Sub) |
| `saveState()` / `loadState()` | localStorage davamlılığı |
| `notifications` | Bildiriş mərkəzi meneceri |
| `toast()` | Keçici bildiriş funksiyası |
| `showContextMenu()` | Sağ klik menyusu |
| `showModal()` / `closeModal()` | Modal idarəetmə |
| `startTimer()` / `tickTimer()` | Taymer idarəetmə |
| `openApp()` / `closeWindow()` | Pəncərə meneceri |
| `solveTask()` / `registerWrong()` | Tapşırıq həlli məntiqi |
| `useHint()` | İpucu sistemi |
| `RENDERERS.*` | Tətbiq rendererləri (mail, security, browser, settings, files) |
| `renderTaskbar()` / `renderStartMenu()` | Taskbar və Start Menyu |
| `showEndScreen()` | Oyun sonu ekranı |
| `showModeModal()` / `runBoot()` | Boot ardıcıllığı və rejim seçimi |

### Dizayn Prinsipləri

- **Mərkəzləşdirilmiş tapşırıq həlli** — `solveTask()` və `registerWrong()` bütün tapşırıqlar üçün vahid giriş nöqtəsidir
- **Event əsaslı rabitə** — tapşırıq hadisələri (`task:solved`, `task:wrong`, `hint:used`) Event Bus vasitəsilə yayımlanır
- **Pəncərə abstraksiyası** — hər tətbiq `openWindows` Map-də saxlanılır, `zTop` ilə z-index idarə olunur
- **Renderer pattern** — hər tətbiq üçün `RENDERERS[appId]` funksiyası `body` elementini qəbul edir

---

## 🚀 İstifadə

### Tələblər
- Müasir brauzer (Chrome, Edge, Firefox, Safari — 2022+ versiya)
- JavaScript aktiv olmalıdır
- İnternet bağlantısı **tələb olunmur**

### İşə Salma

**Metod 1 — Birbaşa açma:**
```bash
# Faylı brauzerdə açmaq kifayətdir
open index.html        # macOS
start index.html       # Windows
xdg-open index.html    # Linux
```

**Metod 2 — Lokal server (tövsiyə olunur):**
```bash
# Python 3 ilə
python -m http.server 8000

# Node.js ilə
npx serve .

# Sonra brauzerdə açın: http://localhost:8000
```

> **Qeyd:** Bəzi brauzerlər `file://` protokolu ilə `localStorage`-a məhdudiyyət qoya bilər. Tam funksionallıq üçün lokal server tövsiyə olunur.

---

## 💾 Yadda Saxlama (Persistence)

Oyun vəziyyəti `localStorage`-da `cyberlock_save_v1` açarı altında saxlanılır:

```json
{
  "score": 240,
  "bestScore": 480,
  "solved": { "mail": true, "password": true },
  "hintsUsed": { "mail": 1 },
  "wrong": { "browser": 2 },
  "firstTry": { "mail": true },
  "consecutive": 2,
  "totalWrong": 2,
  "mode": "normal",
  "timerDuration": 600000,
  "timerEnd": 1710000000000,
  "timerStarted": true,
  "escaped": false,
  "recentApps": ["mail", "browser"]
}
```

**Sıfırlama:** Başlat menyusundakı güc düyməsi və ya oyun sonu ekranındakı "Yenidən başla" düyməsi `localStorage`-u təmizləyir və səhifəni yeniləyir.

---

## ⚙️ Konfiqurasiya

### Oyun parametrlərinin dəyişdirilməsi

```javascript
// Fayl müddəti (ms)
const DEFAULT_DURATION  = 10 * 60 * 1000;   // 10 dəqiqə
const SPEEDRUN_DURATION =  4 * 60 * 1000;   //  4 dəqiqə

// Tapşırıq balları — TASKS obyektində
mail: { points: 100, ... }

// İpucu cəriməsi — useHint() funksiyasında
state.score = Math.max(0, state.score - 15);

// Səhv cavab cəriməsi — registerWrong() funksiyasında
if (state.totalWrong > 2) penalty = 10;
```

### Yeni tapşırıq əlavə etmək

1. `APPS` massivinə yeni tətbiq təyinatı əlavə edin
2. `TASKS` obyektinə tapşırıq təyinatı əlavə edin (`hints`, `debrief`, `wrongNote` daxil)
3. `TASK_ORDER` massivinə tapşırıq ID-sini əlavə edin
4. `RENDERERS` obyektinə uyğun renderer funksiyası yazın

---

## 🎨 Dizayn Sistemi

CSS dəyişənləri (custom properties) vasitəsilə rəng palitrası idarə olunur:

```css
:root {
  --bg: #f3f3f3;
  --surface: #ffffff;
  --accent: #0067c0;         /* Windows 11 mavisi */
  --text: #1b1b1b;
  --text-2: #5b5b5b;
  --text-3: #8a8a8a;
  --danger: #c42b1c;
  --success: #0f7b3f;
  --warn: #b26b00;
  /* ... */
}
```

- **Şrift:** Segoe UI (sistem şrifti) + fallback stack
- **Künc radiusu:** 8–12px (Windows 11 üslubu)
- **Kölgələr:** yumşaq, çoxqatlı (`box-shadow`)
- **Animasiyalar:** 120–240ms keçidlər, `cubic-bezier` easing

---

## ⚠️ Məhdudiyyətlər

- **Yalnız simulyasiya** — heç bir real məlumat göndərilmir, heç bir şəbəkə sorğusu icra olunmur
- **Xarici linklər bloklanıb** — brauzer tətbiqində "Şifrəmi unutdum" linki yalnız status bar önizləməsi göstərir
- **Drag & Drop** — yalnız desktop brauzerlərdə tam işləyir (mobil üçün optimallaşdırılmayıb)
- **localStorage** — inkognito rejimdə və ya `file://` protokolunda məhdudiyyət ola bilər
- **Çoxdilli dəstək** — hazırda yalnız Azərbaycan dilindədir (state.lang sahəsi gələcək genişlənmə üçün hazırdır)

---

## 🔒 Təhlükəsizlik Qeydləri

- Oyun **heç bir real şifrə və ya istifadəçi məlumatı** toplamır
- Brauzer tətbiqindəki forma sahələri yalnız **simulyasiya** məqsədi daşıyır
- Xarici linklər `preventDefault()` ilə bloklanır
- Heç bir `fetch`, `XMLHttpRequest` və ya WebSocket sorğusu yoxdur
- Bütün məlumatlar yalnız istifadəçinin öz brauzerində (`localStorage`) saxlanılır

---

## 🧪 Test Ssenariləri

| Ssenari | Gözlənilən Nəticə |
|---------|-------------------|
| Bütün 5 tapşırığı ipucusuz, ilk cəhddə həll et | "Qüsursuz" + "İpucusuz" + "İlk cəhddə" nişanları |
| Speedrun rejimində 4 dəqiqədən tez bitir | "Sürətli" nişanı |
| 3 tapşırığı ardıcıl ilk cəhddə həll et | Streak ×1.2 bonusu aktivləşir |
| Vaxt bitdikdə | "Vaxt bitdi!" ekranı, irəliləyiş saxlanılır |
| Səhifəni yenilə | Timer və bal bərpa olunur |
| 3 dəfə səhv şifrə kartı yerləşdir | Avtomatik ipucu toast-ı açılır |

---

## 🛠️ Genişləndirmə Yolları

Layihə gələcəkdə aşağıdakı istiqamətlərdə genişləndirilə bilər:

- **Çoxdilli dəstək** — `state.lang` sahəsi artıq mövcuddur; i18n lüğəti əlavə etmək kifayətdir
- **Server əsaslı lider cədvəli** — bal və nəticələri backend-ə göndərmək
- **Yeni tapşırıqlar** — 2FA simulyasiyası, şifrə meneceri, sosial mühəndislik ssenariləri
- **Mobil optimallaşdırma** — toxunma (touch) hadisələri üçün drag & drop
- **Səs effektləri** — Web Audio API ilə
- **PWA dəstəyi** — service worker + manifest əlavə etməklə oflayn quraşdırıla bilən tətbiq

---

## 📄 Lisenziya

Bu layihə **təhsil məqsədi** ilə hazırlanmışdır. Kommersiya istifadəsi üçün müəlliflə əlaqə saxlayın.

---

## 🙏 Təşəkkür

- Dizayn istinadı: **Microsoft Windows 11** (Fluent Design)
- İkonlar: **Lucide** üslubunda əl ilə hazırlanmış inline SVG
- Təhlükəsizlik məsləhətləri: **OWASP**, **CISA**, **NCSC** tövsiyələri əsasında

---

## 📞 Əlaqə

Suallar, təkliflər və ya səhv bildirişləri üçün layihə müəllifi ilə əlaqə saxlayın.

---

**CYBERLOCK: Quarantine Room** — *"Bir yanlış klik hər şeyi dəyişə bilər. Hazırsan?"* 🔐
