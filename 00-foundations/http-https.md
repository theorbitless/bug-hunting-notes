# 🌍 HTTP & HTTPS

> Catatan pribadi · theorbitless · updated Mei 2026

---

## 🧠 Konsep Dasar

HTTP = bahasa komunikasi antara browser dan server. Setiap interaksi di web — buka halaman, login, beli barang — semua itu HTTP request dan response.

---

## 📤 Anatomi Request

```
GET /products HTTP/1.1
Host: tokopedia.com
User-Agent: Mozilla/5.0
Cookie: session=abc123
```

| Bagian | Keterangan |
|---|---|
| Method | Apa yang mau dilakukan |
| Path | Halaman mana yang diminta |
| Host | Domain tujuan |
| User-Agent | Identitas browser — **bisa dipalsukan** |
| Cookie | Tiket identitas user |

---

## 📥 Anatomi Response

```
HTTP/1.1 200 OK
Content-Type: text/html
Set-Cookie: session=xyz789
Server: nginx
```

> `Server: nginx` = information disclosure — kasih tau software yang dipakai

---

## 🔢 Status Codes

| Code | Arti | Hunter Angle |
|---|---|---|
| 200 | OK | Normal |
| 301/302 | Redirect | Perhatikan redirect chain |
| 401 | Belum login | - |
| 403 | Dilarang | **Coba bypass!** |
| 404 | Tidak ditemukan | - |
| 500 | Server error | Mungkin ada info bocor |

---

## 📡 HTTP Methods

| Method | Fungsi |
|---|---|
| GET | Minta data |
| POST | Kirim data |
| PUT | Update data |
| DELETE | Hapus data |
| PATCH | Update sebagian |

---

## 🔐 HTTP vs HTTPS

- **HTTP** = surat tanpa amplop — bisa disadap
- **HTTPS** = surat dalam amplop terkunci — dienkripsi

> ⚠️ HTTPS bukan berarti aman dari bug — hanya proteksi data di jalan!

---

## ⚠️ Man in The Middle Attack

Di WiFi publik, attacker bisa tangkap semua traffic HTTP. Tools seperti Wireshark bisa baca semua data yang lewat. SSL Stripping bisa paksa downgrade dari HTTPS ke HTTP.

---

*last updated: Mei 2026*
