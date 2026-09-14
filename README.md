# root@slayer 🔴

> Gobuster'ın Türkçe versiyonu — Orijinal kaynak kodundan derlenir, aynı hız ve güç.

```
██████╗  ██████╗  ██████╗ ████████╗ ██╗
██╔══██╗██╔═══██╗██╔═══██╗╚══██╔══╝ ██║
██████╔╝██║   ██║██║   ██║   ██║    ██║
██╔══██╗██║   ██║██║   ██║   ██║    ╚═╝
██║  ██║╚██████╔╝╚██████╔╝   ██║    ██╗
╚═╝  ╚═╝ ╚═════╝  ╚═════╝   ╚═╝    ╚═╝
     @  S L A Y E R  —  Dizin & DNS Keşif Aracı
```

---

## ⚡ Kurulum (Tek Komut)

```bash
sudo bash slayer_build.sh
```

Bu kadar. Script otomatik olarak:
- Go'yu kurar (yoksa)
- Gobuster kaynak kodunu indirir
- Türkçeye çevirir
- Derler ve sisteme kurar

---

## 🚀 Kullanım

```bash
# Dizin tarama
root@slayer dir -u http://hedef.com -w /usr/share/wordlists/dirb/common.txt

# Uzantılı tarama
root@slayer dir -u http://hedef.com -w wordlist.txt -x php,html,txt -t 50

# Sonuçları kaydet
root@slayer dir -u http://hedef.com -w wordlist.txt -o sonuc.txt

# DNS alt alan keşfi
root@slayer dns -d hedef.com -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt

# Sanal host keşfi
root@slayer vhost -u http://hedef.com -d hedef.com -w wordlist.txt

# Yardım
root@slayer --help
root@slayer dir --help
```

---

## 🛡️ CTF & Pentest İpuçları

### 403 Bypass — Header Enjeksiyonu
```bash
root@slayer dir -u http://HEDEF -H "X-Forwarded-For: 127.0.0.1" -w liste.txt
root@slayer dir -u http://HEDEF -H "X-Real-IP: 127.0.0.1" -w liste.txt
root@slayer dir -u http://HEDEF -H "X-Original-URL: /admin" -w liste.txt
root@slayer dir -u http://HEDEF -H "X-Rewrite-URL: /admin" -w liste.txt
root@slayer dir -u http://HEDEF -H "Referer: https://HEDEF/admin" -w liste.txt
```

### WAF / IPS Bypass
```bash
root@slayer dir -u http://HEDEF --useragent "Googlebot/2.1" -w liste.txt
root@slayer dir -u http://HEDEF --useragent "Mozilla/5.0 (compatible; bingbot/2.0)" -w liste.txt
root@slayer dir -u http://HEDEF -t 5 --timeout 30 -w liste.txt   # yavaş tarama
```

### Gizli Dosya & Yedek Keşfi
```bash
root@slayer dir -u http://HEDEF -w liste.txt -x php,html,asp,aspx,jsp,bak,old,zip,sql,env
```

### API Endpoint Keşfi
```bash
root@slayer dir -u http://HEDEF/api -w liste.txt -x json,xml -t 30
```

### Kimlik Doğrulama
```bash
root@slayer dir -u http://HEDEF -w liste.txt -U admin -P admin
root@slayer dir -u http://HEDEF -w liste.txt -c "PHPSESSID=abc123; isAdmin=true"
```

---

## 📋 Önerilen Wordlistler

| Liste | Kullanım |
|-------|----------|
| `/usr/share/wordlists/dirb/common.txt` | Hızlı başlangıç |
| `/usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt` | CTF standart |
| `/usr/share/seclists/Discovery/Web-Content/raft-large-directories.txt` | Kapsamlı |
| `/usr/share/seclists/Discovery/Web-Content/big.txt` | Büyük |
| `/usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt` | DNS |

```bash
# SecLists kurulumu
sudo apt install seclists -y

# Dirb wordlistleri
sudo apt install dirb -y
```

---

## 🖥️ Gereksinimler

- Kali Linux / Debian tabanlı sistem
- İnternet bağlantısı (ilk kurulum için)
- `sudo` yetkisi

---

## ⚠️ Yasal Uyarı

Bu araç yalnızca **yetkili** sistemlerde ve **eğitim amaçlı** kullanım içindir.
İzinsiz sistemlere karşı kullanmak yasaldır.

---

## 🔗 Kredi

- Orijinal proje: [gobuster](https://github.com/OJ/gobuster) — OJ Reeves & Christian Mehlmauer
- Türkçe versiyon: **root@slayer**
