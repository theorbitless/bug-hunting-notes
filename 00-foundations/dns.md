# 🔍 DNS — Domain Name System

> Catatan pribadi · theorbitless · updated Mei 2026

---

## 🧠 Konsep Dasar

DNS = buku telepon internet. Kamu ketik nama domain → DNS cariin IP-nya → browser connect ke IP itu.

**Flow:**
```
Browser → DNS Resolver → Root Server → TLD Server → Nameserver domain → dapat IP
```

---

## 🏗️ Struktur Domain

```
mail  .  google  .  com
 ↑          ↑        ↑
subdomain  domain   TLD
```

---

## 📋 Record Types

| Record | Fungsi | Hunter Angle |
|---|---|---|
| A | Domain → IPv4 | Paling dasar, dicari pertama |
| AAAA | Domain → IPv6 | Sering lupa diamankan |
| CNAME | Alias → domain lain | Cek subdomain takeover |
| MX | Alamat server email | Bocorkan vendor email & blok IP |
| TXT | Teks bebas | Sering bocor token, API key, info vendor |
| NS | Siapa yang kelola DNS | Peta infrastruktur DNS |

---

## 💥 Subdomain Takeover via CNAME

```
Perusahaan setup CNAME → vendor luar
→ kontrak habis → vendor hapus service
→ CNAME lupa dihapus
→ hunter daftar ulang domain vendor
→ subdomain perusahaan nunjuk ke server hunter
```

> Bounty lumayan untuk bug ini!

---

## 🚨 Zone Transfer (AXFR)

Kalau DNS server salah konfigurasi → bisa kasih **seluruh daftar subdomain** ke siapapun yang minta.

Seperti buku telepon internal bocor ke publik.

---

## 🔬 Praktek yang Sudah Dilakukan

Recon DNS GitHub dan Tokopedia pakai `nslookup`:
- **GitHub**: pakai Microsoft untuk email, NSOne + AWS untuk DNS
- **Tokopedia**: pakai Bytedance/TikTok untuk email, AWS untuk DNS, 18+ vendor dari TXT record (Salesforce, Atlassian, Stripe, dll)

---

*last updated: Mei 2026*
