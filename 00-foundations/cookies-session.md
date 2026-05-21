# 🍪 Cookie & Session

> Catatan pribadi · theorbitless · updated Mei 2026

---

## 🧠 Konsep Dasar

Cookie = teks kecil yang disimpen browser. Server kasih cookie waktu login → browser kirim cookie itu di setiap request berikutnya → server kenal kamu dari cookie, bukan password lagi.

---

## 🚩 Cookie Flags

| Flag | Fungsi |
|---|---|
| `HttpOnly` | Cookie tidak bisa dibaca JavaScript — **tameng utama dari XSS cookie stealing** |
| `Secure` | Cookie hanya dikirim lewat HTTPS — proteksi dari penyadapan WiFi publik |
| `SameSite=Strict` | Cookie tidak dikirim ke request dari domain lain — **tameng dari CSRF** |
| `SameSite=Lax` | Cookie dikirim untuk navigasi normal, tidak untuk request background |
| `Expires` | Cookie yang expired-nya terlalu lama = window lebar buat attacker |

---

## 💀 Cookie Stealing via XSS

```
Korban login → browser simpen cookie session
→ korban buka website jahat
→ JS jahat jalan di background
→ baca document.cookie
→ kirim ke server attacker
→ attacker login tanpa password
```

Korban tidak sadar sama sekali.

> Tameng: flag `HttpOnly` bikin `document.cookie` tidak bisa dibaca JS

---

## 📌 Cookie Consent Banner

Popup "Setujui Cookie" = cookie **tracking & analytics** (Google Analytics, Facebook Pixel) — bukan cookie session.

- Kalau ditolak → masih bisa login & pakai website
- Cookie session tidak perlu izin karena wajib untuk fungsi website

---

## 🔬 Praktek yang Sudah Dilakukan

Lihat cookie Tokopedia di DevTools:
- Cookie `DID` → punya `HttpOnly` dan `Secure` ✅
- Cookie tracking (`_ga`, `_fbp`) → tidak perlu flag karena JS perlu baca mereka

---

*last updated: Mei 2026*
