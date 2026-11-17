# CYBERLOCK — Quarantine Room

> Təhlükəsizlik simulyasiyası: istifadəçini 5 real kiberhücum ssenarisi ilə sınaqdan keçirən, brauzer əsaslı interaktiv təlim platforması.

---

## 📌 Haqqında

**CYBERLOCK**, veb-brauzerdə işləyən, işletim sistemi masaüstünü imitasiya edən kiber təhlükəsizlik təlim oyunudur. İstifadəçi "Quarantine Room"-dan çıxmaq üçün phishing, zəif şifrə, yoluxmuş fayl kimi real təhlükələri tanıyıb zərərsizləşdirməlidir.

- **Stack:** HTML5 · CSS3 (CSS Variables) · Vanilla JavaScript (ES6)
- **Asılılıq:** Yoxdur — tək fayl, oflayn işləyir
- **Hədəf:** Korporativ təlim, təhsil, fərqindəlik (awareness) proqramları

---

## ✨ Əsas imkanlar

| Modul | Təsvir |
|---|---|
| 📧 **Mail** | Saxta göndərən domenini (`paypa1-secure.com`) tanıma |
| 🔐 **Şifrə Oyunu** | Drag & drop — zəif/güclü şifrələri kateqoriyalaşdırma |
| 🌐 **Browser** | Çoxsaylı tab, saxta bank saytı, phishing login, malware yükləmə |
| ⚙️ **Settings** | Real vaxt şifrə gücü ölçən, 5 qayda validasiyası |
| 📁 **File Explorer** | Tam fayl sistemi, qovluq naviqasiyası, ikiqat uzantı aşkarlama |
| 🛡 **Antivirus** | Skan, təhdid aşkarlama, təmizləmə |
| 🎨 **Theme** | Light / Dark — wallpaper daxil tam dəyişir |
| 🔔 **Bildirişlər** | Mail, virus, sistem hadisələri üçün toast + panel |

---

## 🚀 Başlama

```bash
# Tək fayl — heç bir build lazım deyil
open index.html
# və ya
python3 -m http.server 8080
```

Brauzer tələbləri: **Chrome / Edge / Firefox (son 2 versiya)** — `backdrop-filter`, `CSS Variables`, `localStorage` dəstəyi.

---

## 🎯 Tapşırıq axını

```
Boot → Desktop → [5 tapşırıq] → Debrief → Escape Screen
```

1. **Saxta E-mail** — `paypa1` domenini tanı, phishing kimi bildir
2. **Şifrə Gücü** — 6 kartı düzgün səbətə sürüklə
3. **Phishing Linki** — `bank-az.click`-i rəsmi saytla qarışdırma
4. **Şifrə Dəyişmə** — 12+ simvol, 4 kateqoriya tələbi
5. **Şübhəli Fayl** — `.jpg.exe` və naməlum `.msi`-i bildir

**Hər tapşırıq:** +100–150 bal · sürət bonusu +20 · streak ×1.2 · ipucu −15 · 3-cü səhvdən sonra −10.

---

## 🏗 Arxitektura

```
index.html
├── <style>        CSS Variables + Light/Dark tema
└── <script>
    ├── ICONS       SVG ikon kitabxanası (inline)
    ├── APPS        Tətbiq reyestri (id, icon, taskId)
    ├── TASKS       Tapşırıq metadata (hints, debrief, points)
    ├── FS          Virtual fayl sistemi (buildFS)
    ├── state       Qlobal vəziyyət + localStorage persist
    ├── events      Sadə pub/sub event bus
    ├── RENDERERS   { mail, security, browser, settings, files }
    └── boot()      Boot animasiyası → Desktop
```

**Dizayn prinsipləri:**
- **Zero-dependency** — framework, build, bundler yoxdur
- **Renderer pattern** — hər tətbiq öz `render(body, app)` funksiyası ilə
- **Idempotent save** — hər dəyişiklikdə `saveState()`, reload-da bərpa
- **Simulyasiya təhlükəsizliyi** — heç bir xarici şəbəkə sorğusu yoxdur

---

## 💾 Persistensiya

`localStorage` açarları:

| Açar | Məzmun |
|---|---|
| `cyberlock_save_v3` | Bal, həll olunmuş tapşırıqlar, timer, tema, virus vəziyyəti |
| `cyberlock_notifs_v3` | Son 40 bildiriş |

**Reset:** Start Menu → Power → "Yenidən başlat" və ya DevTools → `localStorage.clear()`.

---

## 🔒 Təhlükəsizlik qeydi

> Bu layihə **tam simulyasiyadır**. Bütün "phishing" səhifələri, "virus" faylları və "bank" interfeysləri dekorativdir. Heç bir məlumat toplanmır, ötürülmür və ya saxlanmır. Real dünyada bu üsullardan istifadə qanunsuzdur.

---

## 🧩 Genişləndirmə

Yeni tapşırıq əlavə etmək üçün:

1. `TASKS` obyektinə yeni entry yaz (`debrief`, `hints`, `wrongNote`)
2. `RENDERERS`-ə uyğun renderer funksiyası əlavə et
3. `APPS` massivinə `{ id, icon, taskId }` əlavə et
4. `TASK_ORDER` massivini yenilə

---

## 📄 Lisenziya

MIT — təhsil və daxili təlim məqsədləri üçün sərbəst istifadə.

---

**Müəllif:** Cyberlock Security Lab · **Versiya:** 3.0.0 (2026)
