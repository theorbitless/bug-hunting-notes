# 🔎 Subdomain Enumeration

> Catatan pribadi · theorbitless · updated Mei 2026

---

## 🧠 Konsep Dasar

Nyari semua subdomain yang ada — yang resmi maupun yang terlupakan.

> Subdomain `staging`, `dev`, `uat`, `admin` sering punya proteksi lebih lemah dari domain utama!

---

## 🕵️ Passive Recon via crt.sh

Database SSL certificate publik. Setiap certificate yang pernah diterbitkan tercatat di sana.

Dari satu domain → dapat puluhan subdomain sekaligus, termasuk yang tidak pernah dipublikasikan.

---

## 📊 Kategorisasi Response

| Response | Artinya | Action |
|---|---|---|
| 200 | Hidup | Langsung investigasi |
| 404 | Not found | Cek CNAME — mungkin takeover candidate |
| NXDOMAIN | Tidak exist di DNS | Cek CNAME dulu sebelum skip |
| Timeout | Ada tapi diblok | Catat untuk later |

---

## 🏢 Vendor Recognition dari CNAME

| CNAME mengandung | Vendor |
|---|---|
| `edgesuite.net` | Akamai |
| `cloudflare.net` | Cloudflare |
| `amazonaws.com` | AWS |
| `herokuapp.com` | Heroku — **takeover candidate kalau expired** |
| `github.io` | GitHub Pages |
| `myshopify.com` | Shopify |

---

## 🔬 Praktek yang Sudah Dilakukan

Recon subdomain Tokopedia via crt.sh — ketemu: `mojito`, `m-staging`, `explorer`, `toped-uat`, `digital-uat`, dll.

| Subdomain | Hasil | Kesimpulan |
|---|---|---|
| mojito | 404 via Akamai | Bukan takeover — Akamai masih aktif |
| explorer | NXDOMAIN, tidak ada CNAME | Dihapus total |
| m-staging | Timeout | Ada tapi diblok publik — catat untuk later |

---

## 🛠️ Tools Selanjutnya (butuh Linux)

- `subfinder` — otomatis enum subdomain
- `httpx` — cek status subdomain massal
- `amass` — recon lebih dalam
- `dnsx` — resolve DNS massal

Bisa otomatis cek ratusan subdomain dalam hitungan menit.

---

*last updated: Mei 2026*
