# 🌐 IP Address

> Catatan pribadi · theorbitless · updated Mei 2026

---

## 🧠 Konsep Dasar

IP address = alamat perangkat di internet. Komputer tidak ngerti nama — cuma ngerti angka.

- **IPv4**: format `192.168.1.1` — 4 oktet, masing-masing 8 bit, nilai 0-255. Total 32 bit
- **IPv6**: format `2001:db8::ff00:42` — total 128 bit, jauh lebih banyak kombinasi

**Bit & oktet:**
1 bit = satu saklar (nyala/mati). 8 bit = 256 kombinasi (0-255). Makanya tiap oktet nilainya 0-255.

---

## 📐 Subnet & CIDR

`192.168.1.0/24` artinya:
- 24 bit pertama = network (dikunci)
- Sisa 8 bit = host → 256 kombinasi - 2 = **254 host** yang bisa dipakai

> Makin kecil angka slash → makin luas jaringannya

---

## 🏷️ Jenis-Jenis IP

| Jenis | Range | Keterangan |
|---|---|---|
| Private | `10.x.x.x`, `172.16-31.x.x`, `192.168.x.x` | Tidak bisa diakses dari internet |
| Public | Semua selain private | Bisa diakses dari internet |
| Loopback IPv4 | `127.0.0.1` | Diri sendiri, untuk testing lokal |
| Loopback IPv6 | `::1` | Versi IPv6 dari loopback |
| Cloud Metadata | `169.254.169.254` | Ada di AWS/GCP/Azure — nyimpen credentials & config server |

---

## 🏢 ASN (Autonomous System Number)

ASN = KTP perusahaan di internet. Dari satu ASN bisa dapat **seluruh blok IP** yang dimiliki perusahaan.

> Hunter angle: expand attack surface dari 1 IP → ratusan IP sekaligus

---

## 🛡️ CDN vs Origin IP

CDN (Cloudflare, Akamai) = tameng di depan server asli. IP publik yang keliatan = IP CDN, bukan origin.

**Kenapa hunter cari origin IP?** Proteksinya lebih lemah.

**Cara nemuin origin IP:**
- DNS history
- Subdomain yang tidak pakai CDN
- MX record
- SSL certificate di crt.sh

---

## 🎯 Bug Hunter Angle

| Temuan | Potensi Bug |
|---|---|
| Private IP muncul di error message | Information disclosure |
| IPv6 tidak dikonfigurasi firewall | Bypass proteksi |
| Header `X-Forwarded-For` bisa dimanipulasi | Bypass IP restriction |
| Cloud metadata `169.254.169.254` | Target utama SSRF |

---

*last updated: Mei 2026*
