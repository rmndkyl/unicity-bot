# Unicity Bot

**Versi:** 1.0.0 · **Harga:** Rp 150.000 (~$9) · **Kontak pembelian:** [@rmndkyl](https://t.me/rmndkyl)

LYID Premium Edition. Automasi daily check-in + quest completion untuk Unicity Network SphereQuests.

## Kebutuhan

| Item | Detail |
|---|---|
| Runtime | Node.js 18+ |
| Wallet | EVM / sesuai chain proyek (kamu sendiri) |
| Proxy | tidak perlu |
| Captcha | tidak perlu |
| Akses | akun proyek yang kamu kelola sendiri |

## Pembayaran

E-Wallet: DANA / GoPay / ShopeePay · Bank: BCA / Seabank · Crypto: contact for wallet address.
Pembeli menghubungi [@rmndkyl](https://t.me/rmndkyl), kirim bukti transfer, lalu terima license key.

---

🌐 **Website:** https://quest.unicity.network

## Fitur

- ✅ **Auth otomatis** — BIP32 key derivation + Sphere ECDSA signing (no browser)
- ✅ **Daily check-in** — +50 XP per hari
- ✅ **Quest automation** — start → check → poll → claim
- ✅ **GitHub integration** — auto star repos + follow (dengan GitHub PAT)
- ✅ **Multi-wallet** — baca dari accounts.json, dukung banyak wallet
- ✅ **Universal credentials** — 1 file untuk semua social accounts
- ✅ **Profile & leaderboard** — points, rank, level, referrals

## Setup

```bash
npm install
```

### 1. Edit accounts.json

```json
{
  "accounts": [
    {
      "id": "wallet1",
      "label": "Wallet 1",
      "enabled": true,
      "mnemonic": "your twelve word seed phrase goes here ...",
      "socials": {
        "github": {
          "username": "yourgithub",
          "token": "ghp_xxxxxxxxxxxx"
        },
        "twitter": {
          "username": "yourtwitter",
          "note": "Twitter API berbayar, skip untuk sekarang"
        },
        "discord": {
          "username": "YourDiscord"
        },
        "google": {
          "email": "you@gmail.com",
          "password": "",
          "app_password": ""
        }
      }
    }
  ]
}
```

### 2. Generate GitHub PAT

1. Login GitHub → https://github.com/settings/tokens
2. Generate new token (classic)
3. Centang: **public_repo** + **user:follow**
4. Copy token ke `accounts.json` → `socials.github.token`

### 3. Run

```bash
# Interactive mode
node index.js

# Auto mode (semua wallet)
node index.js --daily

# Specific wallet
node index.js --daily --id=wallet1
```

## Cara Tambah Akun Baru

### Tambah wallet baru ke accounts.json:

```json
{
  "accounts": [
    { "id": "wallet1", "label": "Wallet 1", "enabled": true, "mnemonic": "...", "socials": { ... } },
    { "id": "wallet2", "label": "Wallet 2", "enabled": true, "mnemonic": "...", "socials": { ... } }
  ]
}
```

### Yang perlu diisi per wallet:

| Field | Wajib | Keterangan |
|-------|-------|------------|
| `id` | ✅ | Identifier unik, bebas |
| `label` | ❌ | Nama tampilan (default = id) |
| `enabled` | ❌ | true/false (default true) |
| `mnemonic` | ✅ | 12 word seed phrase Sphere wallet |
| `socials.github.username` | ❌ | GitHub username |
| `socials.github.token` | ❌ | GitHub PAT (scopes: public_repo, user:follow) |
| `socials.twitter.username` | ❌ | Twitter username |
| `socials.discord.username` | ❌ | Discord username |
| `socials.google.email` | ❌ | Google email |

### Bot akan otomatis:
1. Baca semua accounts yang `enabled: true`
2. Untuk setiap wallet: auth → check-in → GitHub star/follow → quest check
3. Match social accounts berdasarkan `socials.github.token` per wallet
4. Report summary di akhir

## Menu

```
1. Run Daily (semua wallet)
2. Show Quest List
3. Show Profile
4. Show Accounts
5. Run All
6. Exit
```

## File Structure

```
unicity-bot/
├── index.js              # Main bot
├── config.json           # API config, delays
├── mnemonic.txt          # Fallback single wallet (legacy)
├── src/
│   ├── api.js            # Quest API wrapper
│   ├── auth.js           # BIP32 + Sphere signing
│   └── github.js         # GitHub star/follow
├── utils/
│   ├── banner.js
│   ├── logger.js
│   └── utils.js          # + loadAccounts()
└── .gitignore

└── accounts.json         # Universal credentials (multi-wallet)
```

## Auth Flow

```
mnemonic → BIP32(m/44'/0'/0'/0/0) → signing key
challenge → "Sphere Signed Message:\n" + msg → double SHA256 → ECDSA secp256k1
verify → JWT (2h expiry)
```

## Security

- `mnemonic.txt` — GITIGNORED
- GitHub PAT di `accounts.json` per wallet, bukan di bot config
- JWT auto-refresh setiap 2 jam

## Support

DM @rmndkyl di Telegram.

## License

PROPRIETARY — LYID (Layer Airdrop ID)

## 💰 Harga

| Lisensi | Harga | Fitur |
|---------|-------|-------|
| **Single** | Rp 150.000 / ~$10 | 1 device, lifetime |
| **Bundle (3 bot)** | Rp 150.000 / ~$16 | Pilih 3 bot, hemat 20% |
| **Pro (semua bot)** | Rp 150.000 / ~$70 | Semua bot + update, hemat 30% |

**Cara beli:** Chat [@OG_LYID_bot](https://t.me/OG_LYID_bot) di Telegram → /buy

**Bayar pakai:**
- 🇮🇩 DANA / GoPay / ShopeePay / BCA / Seabank
- 🌐 Crypto (USDT/SOL/ETH)

## 🔧 Troubleshooting

| Masalah | Solusi |
|---------|--------|
| `Cannot find module` | Jalankan `npm install` di folder bot |
| `insufficient balance` | Pastikan wallet punya cukup token untuk gas |
| `429 Too Many Requests` | Tunggu 30-60 detik, bot auto-retry |
| Bot diam/tidak jalan | Cek `config.json` — pastikan API key valid |
| License invalid | Chat [@OG_LYID_bot](https://t.me/OG_LYID_bot) → /verify |

**Butuh bantuan?** Join [Discord](https://discord.gg/ZK2NVkfSNn) atau chat [@layerairdrop](https://t.me/layerairdrop)
