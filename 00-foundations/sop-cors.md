# 🔒 Same Origin Policy & CORS

> Catatan pribadi · theorbitless · updated Mei 2026

---

## 🧠 Same Origin Policy (SOP)

Aturan keras browser: **script dari origin A tidak boleh akses resource dari origin B.**

Origin = protocol + domain + port. Satu saja berbeda = beda origin = diblok.

```
https://tokopedia.com ≠ http://tokopedia.com       (beda protocol)
https://tokopedia.com ≠ https://shopee.com          (beda domain)
https://tokopedia.com ≠ https://api.tokopedia.com   (beda subdomain)
https://tokopedia.com ≠ https://tokopedia.com:8080  (beda port)
```

---

## 🌐 CORS (Cross-Origin Resource Sharing)

Pengecualian resmi dari SOP. Server bisa izinkan origin tertentu lewat header:

```
Access-Control-Allow-Origin: https://tokopedia.com   ✅ spesifik
Access-Control-Allow-Origin: *                        ⚠️ semua origin boleh
```

---

## 💥 CORS Misconfiguration

| Kondisi | Bahaya |
|---|---|
| Wildcard `*` di endpoint sensitif | Bug — siapapun bisa akses |
| Server reflect origin sembarangan + `credentials: true` | Bug serius — script evil.com bisa fetch data pribadi user |

---

## 🤔 Kenapa XSS Bypass SOP?

SOP proteksi **antar origin**. XSS inject script ke dalam origin yang **sama** — jadi SOP tidak berlaku.

Script jahat yang di-inject ke `tokopedia.com` jalan dengan hak akses penuh origin `tokopedia.com`.

---

## 🔬 Praktek yang Sudah Dilakukan

Lihat CORS header di DevTools Tokopedia:
- GraphQL endpoint (`gql.tokopedia.com`)
- `Access-Control-Allow-Credentials: true`
- `Access-Control-Allow-Origin: https://tokopedia.com` → spesifik, konfigurasi **benar** ✅

---

*last updated: Mei 2026*
