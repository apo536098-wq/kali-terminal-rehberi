# 🐉 Kali Linux & Terminal Ustası Rehberi

Siber güvenlik dünyasına adım atanlar için kapsamlı, pratik ve ileri düzey detaylarla bezeli Türkçe başlangıç rehberi.

---

## 📋 İçindekiler

* [Kali Linux Nedir?](#-kali-linux-nedir)
* [Kurulum ve İlk Yapılandırma](#-kurulum-ve-ilk-yapılandırma)
* [Terminal Temelleri](#-terminal-temelleri)
* [Dosya Sistemi ve İzinler](#-dosya-sistemi-ve-izinler)
* [Ağ ve Sistem Yönetimi](#-ağ-ve-sistem-yönetimi)
* [Paket Yönetimi](#-paket-yönetimi)
* [Süreç ve Hizmet Yönetimi](#-süreç-ve-hizmet-yönetimi)
* [Kullanıcı ve Grup Yönetimi](#-kullanıcı-ve-grup-yönetimi)
* [Metin İşleme ve Pipe'lar](#-metin-işleme-ve-pipelar)
* [Sık Kullanılan Siber Güvenlik Araçları](#-sık-kullanılan-siber-güvenlik-araçları)
* [Terminal İpuçları ve Kısayollar](#-terminal-ipuçları-ve-kısayollar)
* [Kaynaklar ve İleri Okuma](#-kaynaklar-ve-ileri-okuma)

---

## 🎯 Kali Linux Nedir?

**Kali Linux**, Offensive Security tarafından geliştirilen, Debian tabanlı, sızma testleri (penetrasyon testleri), adli bilişim (digital forensics), tersine mühendislik ve siber güvenlik araştırmaları için özel olarak optimize edilmiş bir Linux dağıtımıdır.

### 🔑 Temel Özellikleri

| Özellik                        | Açıklama                                                                          |
| ------------------------------ | --------------------------------------------------------------------------------- |
| **600+ Güvenlik Aracı**        | Nmap, Metasploit, Burp Suite, Aircrack-ng gibi endüstri standardı araçları içerir |
| **Debian Tabanlı**             | APT paket yöneticisi, geniş yazılım desteği ve Debian ekosistemi                  |
| **Çeşitli Masaüstü Ortamları** | Xfce varsayılan olmak üzere GNOME, KDE Plasma ve diğer ortamları destekler        |
| **Live Boot**                  | Kurulum yapmadan USB/DVD üzerinden çalıştırılabilir                               |
| **ARM Desteği**                | Raspberry Pi ve çeşitli ARM cihazları için sürümleri bulunur                      |
| **FHS Uyumlu**                 | Standart Linux dosya sistemi hiyerarşisine uygundur                               |

### ⚡ Root Kullanıcısı ve `kali` Kullanıcısı

Kali Linux 2020.1'den itibaren varsayılan olarak **root yerine normal kullanıcı** modeliyle gelir. Root yetkisi gerektiğinde `sudo` kullanılabilir.

```bash
# Root şifresini değiştir
sudo passwd root

# Root kullanıcısına geç
su -

# Alternatif olarak root shell aç
sudo -i
```

> ⚠️ Root yetkisini yalnızca gerçekten gerektiğinde kullanmak ve çalıştıracağın komutları kontrol etmek iyi bir güvenlik pratiğidir.

---

# 💾 Kurulum ve İlk Yapılandırma

## 1. Sistem Güncellemesi

İlk kurulumdan sonra paket listesini güncellemek ve sistemi yükseltmek iyi bir başlangıçtır.

```bash
# Paket listesini güncelle ve sistemi yükselt
sudo apt update && sudo apt full-upgrade -y

# Gereksiz paketleri temizle
sudo apt autoremove -y
sudo apt autoclean
```

## 2. Temel Araçların Kurulumu

```bash
# Derleme araçları ve temel yardımcı programlar
sudo apt install -y build-essential git curl wget vim neofetch htop

# Python3 ve sanal ortam araçları
sudo apt install -y python3 python3-pip python3-venv

# Ağ araçları
sudo apt install -y net-tools dnsutils whois traceroute
```

## 3. Zsh ve Oh-My-Zsh

Zsh, Bash'e alternatif gelişmiş bir shell'dir.

```bash
# Zsh kur
sudo apt install -y zsh

# Zsh'i varsayılan shell yapmak için
chsh -s "$(which zsh)"
```

Oh My Zsh kullanmak istersen resmi kurulum yöntemini tercih et.

> ⚠️ İnternetten shell script'i doğrudan `curl | sh` şeklinde çalıştırmadan önce içeriğini incelemek daha güvenlidir.

---

# 🖥️ Terminal Temelleri

Terminal veya shell, Linux sistem yönetiminin temel araçlarından biridir.

Kali Linux'ta Bash yaygın olarak kullanılan shell'lerden biridir.

## 📌 Temel Navigasyon Komutları

| Komut    | Açıklama                                       | Örnek                     |
| -------- | ---------------------------------------------- | ------------------------- |
| `pwd`    | Bulunduğun dizini gösterir                     | `pwd`                     |
| `ls`     | Dosya ve klasörleri listeler                   | `ls -lah`                 |
| `cd`     | Dizin değiştirir                               | `cd /var/log`             |
| `mkdir`  | Klasör oluşturur                               | `mkdir proje`             |
| `touch`  | Dosya oluşturur veya zaman damgasını günceller | `touch rapor.md`          |
| `cp`     | Dosya/kopya oluşturur                          | `cp kaynak.txt hedef.txt` |
| `mv`     | Dosya taşır veya yeniden adlandırır            | `mv eski.txt yeni.txt`    |
| `rm`     | Dosya veya klasör siler                        | `rm dosya.txt`            |
| `cat`    | Dosya içeriğini gösterir                       | `cat dosya.txt`           |
| `less`   | Dosyayı sayfalayarak gösterir                  | `less /var/log/syslog`    |
| `head`   | Dosyanın başını gösterir                       | `head -n 5 dosya.txt`     |
| `tail`   | Dosyanın sonunu gösterir                       | `tail -n 20 dosya.txt`    |
| `find`   | Dosya arar                                     | `find . -name "*.conf"`   |
| `locate` | Veritabanından hızlı dosya arar                | `locate nmap`             |

### `cd` Kullanımı

```bash
cd ~
cd ..
cd -
cd /var/log
```

* `cd ~` → Ev dizinine gider.
* `cd ..` → Bir üst dizine çıkar.
* `cd -` → Önceki dizine döner.

### Klasör Oluşturma

```bash
mkdir proje
mkdir -p proje/{src,docs,tests}
```

### Dosya Kopyalama

```bash
cp kaynak.txt hedef.txt
cp -r kaynak/ hedef/
```

### Dosya Silme

```bash
rm dosya.txt
rm -r klasor/
```

> ⚠️ `rm -rf` son derece dikkatli kullanılmalıdır. Yanlış bir yol ciddi veri kaybına neden olabilir.

---

# 📖 Yardım ve Bilgi Komutları

```bash
# Kısa açıklama
whatis nmap

# Manuel sayfası
man nmap

# Yardım
nmap --help

# Komutun konumunu bul
which nmap
whereis nmap

# Komut türünü öğren
type cd
type ls
```

---

# 📂 Dosya Sistemi ve İzinler

## Linux Dosya Sistemi Hiyerarşisi

```text
/
├── /bin    → Temel kullanıcı komutları
├── /sbin   → Sistem yönetim komutları
├── /etc    → Yapılandırma dosyaları
├── /home   → Kullanıcı ev dizinleri
├── /root   → Root kullanıcısının ev dizini
├── /var    → Log, cache ve değişken veriler
├── /tmp    → Geçici dosyalar
├── /usr    → Kullanıcı programları ve kütüphaneler
├── /opt    → Opsiyonel / üçüncü parti yazılımlar
└── /proc   → Süreç ve kernel bilgilerini sunan sanal dosya sistemi
```

> Not: Modern Linux dağıtımlarında `/bin`, `/sbin` ve `/lib` gibi dizinlerin `/usr` altında birleştirildiği sistemler de bulunabilir.

---

## 🔐 Dosya İzinleri

Linux'ta temel izinler:

* `r` → Read
* `w` → Write
* `x` → Execute

```bash
ls -la
```

Örnek:

```text
-rwxr-xr-- 1 kali kali 1234 Aug 14 10:00 script.sh
```

İzin yapısı:

```text
-rwxr-xr--
 │  │  │
 │  │  └── Others: rwx/r--
 │  └───── Group: r-x
 └──────── Owner: rwx
```

### Sayısal İzinler

| İzin | Değer | Açıklama   |
| ---- | ----: | ---------- |
| `r`  |     4 | Okuma      |
| `w`  |     2 | Yazma      |
| `x`  |     1 | Çalıştırma |

### `chmod`

```bash
chmod 755 script.sh
chmod 644 dosya.txt
chmod +x program.sh
```

Örneğin:

```text
755 = rwxr-xr-x
644 = rw-r--r--
```

### Sahiplik Değiştirme

```bash
sudo chown root:root dosya.txt
sudo chown kali:kali dizin/ -R
```

---

# 🌐 Ağ ve Sistem Yönetimi

## Ağ Yapılandırması ve İzleme

| Komut        | Açıklama                              | Örnek                               |
| ------------ | ------------------------------------- | ----------------------------------- |
| `ip a`       | IP adreslerini ve arayüzleri listeler | `ip a`                              |
| `ip r`       | Yönlendirme tablosunu gösterir        | `ip r`                              |
| `ifconfig`   | Eski tarz ağ arayüz bilgisi           | `ifconfig`                          |
| `iwconfig`   | Kablosuz arayüz bilgisi               | `iwconfig`                          |
| `ping`       | ICMP bağlantı testi                   | `ping -c 4 8.8.8.8`                 |
| `traceroute` | Ağ yolunu gösterir                    | `traceroute example.com`            |
| `mtr`        | Ping + traceroute analizi             | `mtr example.com`                   |
| `ss`         | Soket ve bağlantıları gösterir        | `ss -tulpn`                         |
| `netstat`    | Ağ bağlantılarını gösterir            | `netstat -tulpn`                    |
| `nmap`       | Ağ keşfi ve port taraması             | `nmap 192.168.1.1`                  |
| `curl`       | HTTP/HTTPS istekleri                  | `curl -I https://example.com`       |
| `wget`       | Dosya indirme                         | `wget https://example.com/file.zip` |
| `whois`      | Domain kayıt bilgileri                | `whois example.com`                 |
| `dig`        | DNS sorgulama                         | `dig example.com A`                 |
| `host`       | Basit DNS sorgusu                     | `host example.com`                  |
| `nslookup`   | DNS sorgulama                         | `nslookup example.com`              |

> ⚠️ Ağ tarama araçlarını yalnızca sahibi olduğun veya açıkça test iznin bulunan sistemlerde kullan.

---

## DNS ve Hostname

```bash
# Hostname görüntüle
hostname

# Hostname değiştir
sudo hostnamectl set-hostname yeni-hostname

# Hosts dosyasını düzenle
sudo nano /etc/hosts

# DNS yapılandırmasını incele
cat /etc/resolv.conf
```

---

# 📡 Kablosuz Ağ ve Monitor Mode

Kablosuz güvenlik laboratuvarlarında monitor mode kullanılabilir.

```bash
# Kablosuz arayüzleri listele
iw dev
```

Monitor mode için:

```bash
sudo ip link set wlan0 down
sudo iw dev wlan0 set type monitor
sudo ip link set wlan0 up
```

Aircrack-ng araç seti ile:

```bash
sudo airmon-ng start wlan0
```

Monitor mode'dan çıkmak için:

```bash
sudo airmon-ng stop wlan0mon
```

> ⚠️ Kablosuz ağ testlerini yalnızca kendi ağında veya yazılı izin verilen laboratuvarlarda gerçekleştir.

---

# 📦 Paket Yönetimi

Kali Linux, Debian tabanlı olduğu için **APT** paket yöneticisini kullanır.

## APT

```bash
# Paket listesini güncelle
sudo apt update

# Paketleri yükselt
sudo apt upgrade -y

# Daha kapsamlı sistem yükseltmesi
sudo apt full-upgrade -y

# Paket ara
apt search nmap

# Paket bilgisi
apt show nmap

# Paket kur
sudo apt install nmap

# Paket kaldır
sudo apt remove nmap

# Paket ve yapılandırma dosyalarını kaldır
sudo apt purge nmap

# Gereksiz bağımlılıkları temizle
sudo apt autoremove -y

# Paket önbelleğini temizle
sudo apt autoclean

# Bozuk bağımlılıkları düzelt
sudo apt --fix-broken install
```

---

## DPKG

`.deb` paketleriyle doğrudan çalışmak için `dpkg` kullanılabilir.

```bash
# .deb paket kur
sudo dpkg -i paket.deb

# Paket kaldır
sudo dpkg -r paket_adi

# Kurulu paketleri listele
dpkg -l

# Belirli paketi ara
dpkg -l | grep nmap
```

---

# ⚙️ Süreç ve Hizmet Yönetimi

## Süreç Yönetimi

| Komut          | Açıklama                          |
| -------------- | --------------------------------- |
| `ps aux`       | Çalışan süreçleri listeler        |
| `top`          | Etkileşimli süreç izleyici        |
| `htop`         | Gelişmiş süreç izleyici           |
| `kill PID`     | PID üzerinden süreç sonlandırır   |
| `killall isim` | İsme göre süreç sonlandırır       |
| `pkill desen`  | Desene göre süreç sonlandırır     |
| `jobs`         | Shell arka plan işlerini gösterir |
| `fg %1`        | İşi ön plana getirir              |
| `bg %1`        | İşi arka planda çalıştırır        |

Örnek:

```bash
ps aux
ps aux | grep nginx

kill 1234
killall firefox
pkill -f "python3 script.py"
```

---

# 🔧 Systemd Hizmet Yönetimi

```bash
# Hizmet durumunu görüntüle
sudo systemctl status ssh

# Hizmeti başlat
sudo systemctl start ssh

# Hizmeti durdur
sudo systemctl stop ssh

# Hizmeti yeniden başlat
sudo systemctl restart ssh

# Açılışta otomatik başlat
sudo systemctl enable ssh

# Otomatik başlatmayı kapat
sudo systemctl disable ssh

# Hizmet loglarını takip et
sudo journalctl -u ssh -f
```

---

# 👥 Kullanıcı ve Grup Yönetimi

## Kullanıcı Bilgileri

```bash
whoami
id
```

## Kullanıcı Oluşturma

```bash
sudo adduser yeni_kullanici
```

## Kullanıcıyı Sudo Grubuna Ekleme

```bash
sudo usermod -aG sudo yeni_kullanici
```

## Şifre Değiştirme

```bash
sudo passwd yeni_kullanici
```

## Kullanıcı Silme

```bash
sudo deluser yeni_kullanici
```

## Grup Oluşturma

```bash
sudo groupadd guvenlik
```

## Kullanıcıyı Gruba Ekleme

```bash
sudo usermod -aG guvenlik yeni_kullanici
```

---

## `/etc/passwd`

```bash
cat /etc/passwd
```

Genel yapı:

```text
kullaniciadi:x:UID:GID:aciklama:ev_dizini:shell
```

## `/etc/shadow`

```bash
sudo cat /etc/shadow
```

> `/etc/shadow` hassas kimlik doğrulama bilgileri içerir. Dosyayı paylaşırken dikkatli olun.

---

# 🔧 Metin İşleme ve Pipe'lar

Pipe (`|`), bir komutun çıktısını başka bir komutun girdisine aktarmak için kullanılır.

## Temel Pipe

```bash
cat /etc/passwd | grep kali
```

Daha doğrudan kullanım:

```bash
grep kali /etc/passwd
```

## Birden Fazla Pipe

```bash
cat erisim.log | grep "404" | wc -l
```

---

## `grep`

```bash
# Büyük/küçük harf duyarsız arama
grep -i "hata" log.txt

# Eşleşen satırları hariç tut
grep -v "başarılı" log.txt

# Recursive arama
grep -r "password" /etc/

# Extended regex
grep -E "hata|uyarı" log.txt
```

---

## `awk`

```bash
awk '{print $1, $4}' erisim.log

awk -F: '{print $1}' /etc/passwd
```

---

## `sed`

```bash
# Ekrana değiştirilmiş çıktı ver
sed 's/eski/yeni/g' dosya.txt

# Dosyayı doğrudan değiştir
sed -i 's/foo/bar/g' dosya.txt
```

> ⚠️ `sed -i` dosyanın içeriğini doğrudan değiştirdiğinden önemli dosyalarda önce yedek almak iyi fikirdir.

---

## `sort` ve `uniq`

```bash
sort log.txt | uniq -c | sort -nr
```

Bu yapı, tekrar eden satırları sayıp en yüksek sayıdan en düşüğe sıralamak için kullanılabilir.

---

## `cut`

```bash
cut -d: -f1 /etc/passwd
```

---

## `wc`

```bash
# Satır sayısı
wc -l dosya.txt

# Kelime sayısı
wc -w dosya.txt
```

---

## `xargs`

```bash
find . -name "*.txt" -print0 | xargs -0 -n 1 echo
```

> ⚠️ `xargs` ile silme gibi geri dönüşü zor işlemler yapmadan önce komutu `echo` ile test etmek daha güvenlidir.

---

## `tee`

```bash
echo "test" | tee log.txt
```

Hem terminale çıktı verir hem de dosyaya yazar.

---

# 🛡️ Sık Kullanılan Siber Güvenlik Araçları

> ⚠️ Aşağıdaki araçlar eğitim, savunma ve yetkili güvenlik testleri için kullanılmalıdır. Hedef sistemin sahibi değilseniz veya açık bir izniniz yoksa tarama, parola denemesi, exploit veya paket enjeksiyonu gerçekleştirmeyin.

---

## 🕵️ Bilgi Toplama ve Keşif

| Araç             | Açıklama                                       | Temel Kullanım                    |
| ---------------- | ---------------------------------------------- | --------------------------------- |
| **Nmap**         | Ağ keşfi ve port taraması                      | `nmap ***.***.*.*`                |
| **Masscan**      | Çok hızlı port tarayıcı                        | Yetkili laboratuvarlarda kullanın |
| **Recon-ng**     | Reconnaissance framework                       | `recon-ng`                        |
| **theHarvester** | E-posta ve subdomain araştırması               | `theHarvester`                    |
| **Shodan**       | İnternete açık sistemler hakkında arama motoru | Shodan CLI                        |
| **Maltego**      | Görsel OSINT ve ilişki analizi                 | GUI                               |
| **WHOIS / Dig**  | Domain ve DNS bilgisi                          | `whois example.com`               |

### Nmap Örneği

Kendi/lab sisteminiz üzerinde:

```bash
nmap -sV ***.***.*.**
```

Servis ve versiyon bilgisi elde etmek için kullanılabilir.

---

# 🌐 Web Uygulama Güvenliği

| Araç            | Açıklama                                  |
| --------------- | ----------------------------------------- |
| **Burp Suite**  | Web proxy ve güvenlik test platformu      |
| **OWASP ZAP**   | Açık kaynak web güvenlik tarayıcısı/proxy |
| **Nikto**       | Web sunucusu güvenlik kontrol aracı       |
| **Gobuster**    | Dizin ve kaynak keşfi                     |
| **Dirb**        | Web içerik keşfi                          |
| **SQLMap**      | SQL Injection test otomasyonu             |
| **WPScan**      | WordPress güvenlik tarayıcısı             |
| **Curl / Wget** | Manuel HTTP işlemleri                     |

Örnek:

```bash
curl -I https://example.com
```

> SQL Injection, brute-force veya içerik keşfi gibi testleri yalnızca izinli sistemlerde gerçekleştirin.

---

# 📡 Kablosuz Ağ Güvenliği

| Araç                  | Açıklama                               |
| --------------------- | -------------------------------------- |
| **Aircrack-ng**       | Wi-Fi güvenlik test araç seti          |
| **Aireplay-ng**       | Paket enjeksiyonu için kullanılan araç |
| **Airodump-ng**       | Kablosuz paket yakalama                |
| **Wifite**            | Kablosuz güvenlik test otomasyonu      |
| **Fern WiFi Cracker** | GUI tabanlı kablosuz güvenlik aracı    |
| **Kismet**            | Kablosuz ağ dedektörü ve analiz aracı  |

Kablosuz testler yalnızca kendi cihazlarınızda veya açıkça yetkilendirilmiş laboratuvarlarda yapılmalıdır.

---

# 🎯 Sızma Testi ve Exploit Araçları

| Araç                     | Açıklama                                                           |
| ------------------------ | ------------------------------------------------------------------ |
| **Metasploit Framework** | Güvenlik testi ve exploit geliştirme/uygulama framework'ü          |
| **Searchsploit**         | Exploit Database üzerinde yerel arama                              |
| **BeEF**                 | Browser Exploitation Framework                                     |
| **Empire / Starkiller**  | Post-exploitation ve adversary simulation araçları                 |
| **Mimikatz**             | Windows kimlik bilgisi ve kimlik doğrulama araştırmaları için araç |

### Searchsploit

```bash
searchsploit apache
```

---

# 📊 Ağ Analizi ve Sniffing

| Araç              | Açıklama                                    |
| ----------------- | ------------------------------------------- |
| **Wireshark**     | Grafiksel paket analizörü                   |
| **Tshark**        | Wireshark'ın terminal arayüzü               |
| **Tcpdump**       | Komut satırı paket yakalama                 |
| **Netcat (`nc`)** | Ağ bağlantıları için çok amaçlı araç        |
| **Ncat**          | Netcat'in gelişmiş sürümü                   |
| **Socat**         | Çift yönlü veri aktarımı ve ağ bağlantıları |

### Tcpdump

Kendi/lab arayüzünüzde paket yakalamak:

```bash
sudo tcpdump -i eth0 -w capture.pcap
```

### Tshark

```bash
sudo tshark -i eth0
```

---

# 🔑 Parola Güvenliği

| Araç                | Açıklama                                  |
| ------------------- | ----------------------------------------- |
| **John the Ripper** | Hash parola güvenliği testi               |
| **Hashcat**         | GPU hızlandırmalı parola hash testi       |
| **Hydra**           | Online kimlik doğrulama güvenlik testi    |
| **Crunch**          | Wordlist oluşturucu                       |
| **CeWL**            | Yetkili testlerde özel wordlist oluşturma |

> ⚠️ Parola kırma veya brute-force araçlarını yalnızca kendi hash'lerinizde, CTF/lab ortamlarında veya yazılı olarak yetkilendirilmiş sistemlerde kullanın.

---

# 🧪 Adli Bilişim (Forensics)

| Araç           | Açıklama                           |
| -------------- | ---------------------------------- |
| **Autopsy**    | Disk imajı analiz platformu        |
| **Sleuth Kit** | Komut satırı adli bilişim araçları |
| **Binwalk**    | Firmware ve binary analiz aracı    |
| **Foremost**   | Dosya kurtarma                     |
| **Volatility** | Bellek/RAM analizi                 |

### Örnekler

```bash
autopsy
```

```bash
fls -r disk.img
```

```bash
binwalk firmware.bin
```

```bash
foremost -i disk.img -o output/
```

---

# 🚀 Terminal İpuçları ve Kısayollar

## ⌨️ Klavye Kısayolları

| Kısayol    | İşlev                           |
| ---------- | ------------------------------- |
| `Ctrl + C` | Çalışan komutu durdur           |
| `Ctrl + Z` | Süreci suspend durumuna al      |
| `Ctrl + D` | EOF gönder / shell'den çık      |
| `Ctrl + L` | Ekranı temizle                  |
| `Ctrl + A` | Satır başına git                |
| `Ctrl + E` | Satır sonuna git                |
| `Ctrl + U` | Satır başından imlece kadar sil |
| `Ctrl + K` | İmleçten satır sonuna kadar sil |
| `Ctrl + W` | Önceki kelimeyi sil             |
| `Ctrl + R` | Komut geçmişinde ara            |
| `Ctrl + G` | Arama modundan çık              |
| `Tab`      | Otomatik tamamlama              |
| `↑ / ↓`    | Komut geçmişinde gezin          |

---

# 🧠 Bash İpuçları

## Komut Geçmişi

```bash
history
```

Belirli bir komutu çalıştırmak:

```bash
!42
```

Son komutu tekrar çalıştırmak:

```bash
!!
```

Son kullanılan komutun son argümanı:

```bash
!$
```

> ⚠️ `history expansion` özelliklerini kullanırken komutu çalıştırmadan önce neyin çalışacağını kontrol etmek iyi bir alışkanlıktır.

---

# 🔗 Alias

Geçici alias:

```bash
alias ll='ls -lah'
alias update='sudo apt update && sudo apt upgrade -y'
```

Kalıcı yapmak için:

```bash
echo "alias ll='ls -lah'" >> ~/.bashrc
source ~/.bashrc
```

---

# 🔀 Komutları Birleştirme

## `&&`

İlk komut başarılıysa ikinci komutu çalıştırır:

```bash
komut1 && komut2
```

## `||`

İlk komut başarısızsa ikinci komutu çalıştırır:

```bash
komut1 || komut2
```

## `;`

Komutları sırayla çalıştırır:

```bash
komut1 ; komut2
```

---

# 💤 Arka Planda Çalıştırma

```bash
komut &
```

Örneğin:

```bash
sleep 60 &
```

Uzun süre çalışan işlemler için `tmux` veya `screen` gibi terminal multiplexer'ları da tercih edilebilir.

---

# 🛡️ Güvenli Çalışma İlkeleri

```text
1. Önemli komutları çalıştırmadan önce ne yaptığını kontrol et.
2. Mümkünse --dry-run gibi güvenli test seçeneklerini kullan.
3. rm -rf gibi geri dönüşü zor komutlarda yolu iki kez kontrol et.
4. Önemli dosyalarda değişiklik yapmadan önce yedek al.
5. Büyük sistem değişikliklerinden önce VM snapshot al.
6. Root yetkisini yalnızca gerektiğinde kullan.
7. İnternetten indirilen script'leri çalıştırmadan önce incele.
8. Siber güvenlik araçlarını yalnızca yetkili sistemlerde kullan.
9. Önemli sistem dosyalarını doğrudan değiştirmeden önce yedekle.
10. CTF ve eğitim laboratuvarlarını öğrenme ortamı olarak kullan.
```

---

# 🧪 Güvenli Öğrenme Laboratuvarı

Siber güvenlik öğrenirken gerçek sistemler yerine izole laboratuvarlar kullanmak önerilir.

Örneğin:

```text
┌─────────────────────────────┐
│        Kali Linux           │
│       Test Makinesi         │
└──────────────┬──────────────┘
               │
               │ İzole Lab Ağı
               │
┌──────────────▼──────────────┐
│       Eğitim Hedefi         │
│  DVWA / Metasploitable vb.  │
└─────────────────────────────┘
```

Bu yaklaşım sayesinde ağ tarama, web güvenliği, trafik analizi ve güvenlik testleri kontrollü bir ortamda öğrenilebilir.

---

# 📚 Kaynaklar ve İleri Okuma

| Kaynak                                                 | Açıklama                            |
| ------------------------------------------------------ | ----------------------------------- |
| [Kali Linux Documentation](https://www.kali.org/docs/) | Kali Linux resmi dokümantasyonu     |
| [Hack The Box](https://www.hackthebox.com/)            | Siber güvenlik laboratuvarları      |
| [TryHackMe](https://tryhackme.com/)                    | Adım adım siber güvenlik eğitimleri |
| [OverTheWire](https://overthewire.org/wargames/)       | Linux ve terminal öğrenme oyunları  |
| [Exploit Database](https://www.exploit-db.com/)        | Exploit arşivi                      |
| [OWASP](https://owasp.org/)                            | Web uygulama güvenliği kaynakları   |
| [Linux Command](https://linuxcommand.org/)             | Linux komut satırı kaynakları       |

---

# 🎓 Önerilen Öğrenme Sırası

Siber güvenliğe yeni başlıyorsan aşağıdaki sırayla ilerlemek faydalı olabilir:

```text
1. Linux temel komutları
        ↓
2. Dosya sistemi ve izinler
        ↓
3. Bash scripting
        ↓
4. Ağ temelleri
        ↓
5. TCP/IP ve DNS
        ↓
6. HTTP / HTTPS
        ↓
7. Nmap ve ağ keşfi
        ↓
8. Wireshark ve trafik analizi
        ↓
9. Web güvenliği
        ↓
10. Burp Suite / OWASP
        ↓
11. CTF ve güvenlik laboratuvarları
        ↓
12. Metasploit ve exploit araştırmaları
        ↓
13. Adli bilişim
        ↓
14. İleri seviye güvenlik araştırmaları
```

---

# 🏁 Sonuç

Kali Linux'u öğrenmek yalnızca güvenlik araçlarının komutlarını ezberlemek değildir.

Asıl hedef:

* Linux'u anlamak
* Ağların nasıl çalıştığını öğrenmek
* HTTP/DNS/TCP/IP gibi protokolleri anlamak
* Terminal üzerinde rahat çalışmak
* Log ve trafik analizi yapabilmek
* Güvenlik açıklarının neden oluştuğunu anlamak
* Güvenli laboratuvarlarda pratik yapmak
* Savunma ve saldırı tekniklerinin çalışma mantığını öğrenmek

**Araçları değil, önce temelleri öğren.**

> 🐉 **Kali Linux bir amaç değil, siber güvenlik öğrenme yolculuğunda kullanılan bir araçtır.**

---

## ⚠️ Yasal ve Etik Kullanım

Bu rehber eğitim amaçlıdır.

Sistem tarama, güvenlik testi, parola denemeleri, exploit çalıştırma, paket enjeksiyonu veya benzeri işlemler yalnızca:

* Size ait sistemlerde,
* Açıkça izin verilen sistemlerde,
* CTF/laboratuvar ortamlarında,
* Yazılı yetkilendirme kapsamında

gerçekleştirilmelidir.

İzinsiz sistemlere yönelik güvenlik testi hukuki ve etik sorunlara yol açabilir.
