# root@slayer 🔴

> Gobuster'ın Türkçe versiyonu — Dizin, DNS ve Sanal Host Keşif Aracı

```
██████╗  ██████╗  ██████╗ ████████╗ ██╗
██╔══██╗██╔═══██╗██╔═══██╗╚══██╔══╝ ██║
██████╔╝██║   ██║██║   ██║   ██║    ██║
██╔══██╗██║   ██║██║   ██║   ██║    ╚═╝
██║  ██║╚██████╔╝╚██████╔╝   ██║    ██╗
╚═╝  ╚═╝ ╚═════╝  ╚═════╝   ╚═╝    ╚═╝
```

---

## ⚡ Kurulum

```bash
git clone https://github.com/Kyzerz53/GOBUSTER-T-RK-.git
cd GOBUSTER-T-RK-
sudo bash TrGobuster
```

---

## 📖 Kullanım Kılavuzu

### 🔍 Temel Dizin Tarama
```bash
root@slayer dir -u http://HEDEF.com -w /usr/share/wordlists/dirb/common.txt
root@slayer dir -u http://HEDEF.com -w /usr/share/wordlists/dirb/common.txt -t 50
root@slayer dir -u http://HEDEF.com -w /usr/share/wordlists/dirb/common.txt -o sonuc.txt
```

---

### 📁 Gizli Dizin & Dosya Bulma
```bash
# Yaygın uzantıları tara
root@slayer dir -u http://HEDEF.com -w liste.txt -x php,html,asp,aspx,jsp,txt

# Yedek & config dosyaları bul
root@slayer dir -u http://HEDEF.com -w liste.txt -x bak,old,zip,tar,gz,sql,env,config,yml,json

# Sadece başarılı sonuçları göster
root@slayer dir -u http://HEDEF.com -w liste.txt -s 200,301,302
```

---

### 🔓 403 Bypass — Header Enjeksiyonu
```bash
root@slayer dir -u http://HEDEF.com -w liste.txt -H "X-Forwarded-For: 127.0.0.1"
root@slayer dir -u http://HEDEF.com -w liste.txt -H "X-Real-IP: 127.0.0.1"
root@slayer dir -u http://HEDEF.com -w liste.txt -H "X-Original-URL: /admin"
root@slayer dir -u http://HEDEF.com -w liste.txt -H "X-Rewrite-URL: /admin"
root@slayer dir -u http://HEDEF.com -w liste.txt -H "Referer: https://HEDEF.com/admin"
root@slayer dir -u http://HEDEF.com -w liste.txt -H "X-Custom-IP-Authorization: 127.0.0.1"
```

---

### 🛡️ WAF / IPS Bypass
```bash
# Bot gibi görün
root@slayer dir -u http://HEDEF.com -w liste.txt --useragent "Googlebot/2.1"
root@slayer dir -u http://HEDEF.com -w liste.txt --useragent "Mozilla/5.0 (compatible; bingbot/2.0)"
root@slayer dir -u http://HEDEF.com -w liste.txt --useragent "curl/7.64.1"

# Yavaş tarama — rate limit atlatma
root@slayer dir -u http://HEDEF.com -w liste.txt -t 5 --timeout 30
```

---

### 🌐 API Endpoint Keşfi
```bash
root@slayer dir -u http://HEDEF.com/api -w liste.txt -x json,xml -t 30
root@slayer dir -u http://HEDEF.com/api/v1 -w liste.txt -x json -t 30

# Özel API wordlist ile
root@slayer dir -u http://HEDEF.com -w /usr/share/seclists/Discovery/Web-Content/api/api-endpoints.txt
```

---

### 🔑 Kimlik Doğrulama Bypass
```bash
# Basic Auth deneme
root@slayer dir -u http://HEDEF.com -w liste.txt -U admin -P admin

# Cookie ile kimlik doğrulama
root@slayer dir -u http://HEDEF.com -w liste.txt -c "PHPSESSID=abc123; isAdmin=true"
```

---

### 🌍 DNS Alt Alan Keşfi
```bash
root@slayer dns -d HEDEF.com -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt
root@slayer dns -d HEDEF.com -w liste.txt --show-ips
```

---

### 🖥️ Sanal Host (VHost) Keşfi
```bash
root@slayer vhost -u http://HEDEF.com -d HEDEF.com -w liste.txt
root@slayer vhost -u http://HEDEF.com -d HEDEF.com -w liste.txt -t 40
```

---

### ⚡ CTF Hızlı Komutlar
```bash
# Hızlı başlangıç
root@slayer dir -u http://HEDEF.com -w /usr/share/wordlists/dirb/common.txt -t 50

# Tam kapsamlı tarama
root@slayer dir -u http://HEDEF.com \
  -w /usr/share/seclists/Discovery/Web-Content/raft-large-directories.txt \
  -x php,html,txt,bak,zip,sql,env \
  -t 50 -o sonuc.txt

# 403 bypass + gizli dizin birlikte
root@slayer dir -u http://HEDEF.com -w liste.txt \
  -x php,html -H "X-Forwarded-For: 127.0.0.1" -t 30
```

---

## 📋 Bayraklar (Flags)

| Bayrak | Açıklama | Örnek |
|--------|----------|-------|
| `-u` | Hedef URL | `-u http://hedef.com` |
| `-w` | Kelime listesi | `-w /usr/share/wordlists/dirb/common.txt` |
| `-t` | İş parçacığı sayısı | `-t 50` |
| `-x` | Dosya uzantıları | `-x php,html,txt` |
| `-o` | Çıktı dosyası | `-o sonuc.txt` |
| `-s` | Kabul edilecek kodlar | `-s 200,301` |
| `-b` | Reddedilecek kodlar | `-b 404,403` |
| `-H` | HTTP başlığı | `-H "X-Forwarded-For: 127.0.0.1"` |
| `-c` | Çerez | `-c "session=abc123"` |
| `-U` | Kullanıcı adı | `-U admin` |
| `-P` | Şifre | `-P admin` |
| `--useragent` | User-Agent | `--useragent "Googlebot/2.1"` |
| `--timeout` | Zaman aşımı (sn) | `--timeout 30` |
| `--show-ips` | IP göster (DNS) | `--show-ips` |

---

## 📂 Önerilen Wordlistler

| Liste | Kullanım |
|-------|----------|
| `/usr/share/wordlists/dirb/common.txt` | Hızlı başlangıç |
| `/usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt` | CTF standart |
| `/usr/share/seclists/Discovery/Web-Content/raft-large-directories.txt` | Kapsamlı |
| `/usr/share/seclists/Discovery/Web-Content/big.txt` | Büyük |
| `/usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt` | DNS |

```bash
# Wordlist kur
sudo apt install seclists dirb -y
```

---

## ⚠️ Yasal Uyarı

Bu araç yalnızca **yetkili** sistemlerde ve **eğitim amaçlı** kullanım içindir.
İzinsiz sistemlere karşı kullanmak **yasaldır.**

---

## 🔗 Kredi

- Orijinal: [gobuster](https://github.com/OJ/gobuster) — OJ Reeves & Christian Mehlmauer
- Türkçe versiyon: **root@slayer** by Kyzerz53
