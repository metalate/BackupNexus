# BackupNexus

> PostgreSQL, MySQL, MSSQL ve MongoDB için otomatik yedekleme ve geri yükleme aracı — modern GUI ve tam CLI desteğiyle.

![Sürüm](https://img.shields.io/badge/sürüm-1.0.0-4a6cf7?style=flat-square)
![Platform](https://img.shields.io/badge/platform-Windows%2010%20%2F%2011-lightgrey?style=flat-square)
![Lisans](https://img.shields.io/badge/lisans-Ticari-blue?style=flat-square)
![GUI](https://img.shields.io/badge/GUI-PySide6%20(Qt6)-brightgreen?style=flat-square)

---

<p align="center">
  <img src="screenshots/dashboard.png" alt="BackupNexus Ana Ekran Görüntüsü" width="900"/>
</p>

---

## Genel Bakış

**BackupNexus**, Windows için profesyonel düzeyde bir veritabanı yedekleme otomasyon aracıdır. Tek bir satır komut yazmadan veritabanı yedeklemelerini yapılandırmanıza, çalıştırmanıza ve zamanlamanıza olanak tanıyan temiz ve modern bir grafik arayüz sunar. PostgreSQL, MySQL/MariaDB, MSSQL ve MongoDB'yi kutudan çıktığı gibi destekleyen uygulama; tek seferlik tam yedeklemelerden otomatik artımlı yedekleme zincirlerine, uzak bulut yüklemelerine, e-posta raporlarına ve geri yükleme iş akışlarına kadar her şeyi tek bir uygulamadan yönetmenizi sağlar.

Kurumsal yazılımların yükü olmadan güvenilir ve denetlenebilir bir yedekleme çözümüne ihtiyaç duyan geliştiriciler, veritabanı yöneticileri ve sistem yöneticileri için tasarlanmıştır.

---

## Ekran Görüntüleri

| Dashboard                                         | Yedekleme — Yapılandırma                                |
|:-------------------------------------------------:|:-------------------------------------------------------:|
| ![Dashboard](screenshots/dashboard.png)           | ![Backup Configure](screenshots/backup_configure.png)   |

| Yedekleme — Çalıştırma                            | Preflight Kontrolü                                      |
|:-------------------------------------------------:|:-------------------------------------------------------:|
| ![Backup Run](screenshots/backup_run.png)         | ![Preflight](screenshots/preflight.png)                 |

| Geri Yükleme                                      | Geçmiş                                                  |
|:-------------------------------------------------:|:-------------------------------------------------------:|
| ![Restore](screenshots/restore.png)               | ![History](screenshots/history.png)                     |

| Ayarlar — E-posta                                 | Ayarlar — Zamanlama                                     |
|:-------------------------------------------------:|:-------------------------------------------------------:|
| ![Settings Email](screenshots/settings_email.png) | ![Settings Schedule](screenshots/settings_schedule.png) |

| Koyu Tema                                         | Açık Tema                                               |
|:-------------------------------------------------:|:-------------------------------------------------------:|
| ![Dark Theme](screenshots/dark_theme.png)         | ![Light Theme](screenshots/light_theme.png)             |

---

## Temel Özellikler

- **4 Veritabanı Türü** — PostgreSQL, MySQL/MariaDB, MSSQL, MongoDB
- **3 Yedekleme Modu** — Tam (Full), Artımlı (Incremental) ve Diferansiyel (Differential) yedekleme
- **Preflight Doğrulama** — Her çalıştırmadan önce bağlantıyı, araçları ve kimlik bilgilerini kontrol eder
- **Gerçek Zamanlı Log Görüntüleyici** — Yedekleme ve geri yükleme ilerlemesini uygulama içinde canlı olarak izleyin
- **Uzak Yükleme** — FTP, SFTP ve Google Drive desteği
- **E-posta Bildirimleri** — Yapılandırılabilir alıcılarla SMTP tabanlı başarı/başarısızlık raporları
- **Windows Görev Zamanlayıcı** — GUI'den doğrudan günlük veya haftalık yedekleme planlayın
- **Yedekleme Geçmişi** — Çalıştırma başına ayrıntılı loglarla filtrelenebilir denetim kaydı
- **Profil Yönetimi** — Prod, staging ve dev yapılandırmaları arasında anında geçiş yapın
- **Koyu ve Açık Tema** — Anında geçiş yapılabilen tam temalı arayüz
- **Çok Dil Desteği** — Türkçe, İngilizce, Almanca, Rusça, Japonca, Çinçe, Korece, İspanyolca, Fransızca, Arapça ve İsveçce arayüz
- **Bütünlük Kontrolü** — SHA256 sağlama toplamları yetkisiz yapılandırma değişikliklerini tespit eder
- **Denetim Logu** — Her işlemin ekleme-yalnız JSONL kaydı
- **Paralel Yedekleme** — Birden fazla veritabanını aynı anda yedekleyin
- **Bağımsız Çalıştırılabilir Dosya** — Python kurulumu gerekmez

---

## Uygulama Rehberi

BackupNexus, sol kenar çubuğuyla gezinilen **6 sayfaya** ayrılmıştır. Her sayfanın işlevi aşağıda açıklanmıştır.

---

### Dashboard

<p align="center">
  <img src="screenshots/dashboard.png" alt="Dashboard" width="800"/>
</p>

Dashboard, yedekleme ortamınızın anlık sağlık özetini sunar:

| Kart                    | Açıklama                                                        |
|-------------------------|-----------------------------------------------------------------|
| **Son Yedekleme**       | En son yedekleme çalıştırmasının zaman damgası                  |
| **Toplam Çalıştırma**   | Toplam yedekleme çalıştırma sayısı                              |
| **Başarı Oranı**        | Başarılı çalıştırmaların yüzdesi (son 50 çalıştırma)            |
| **Son Başarısızlıklar** | Başarısız veya durdurulan çalıştırma sayısı (son 50 çalıştırma) |

Üç hızlı işlem düğmesiyle doğrudan **Yedekleme Başlat**, **Geri Yükleme** veya **Tüm Geçmiş** sayfalarına atlayabilirsiniz. Alt panel, son 5 yedekleme çalıştırmasını durumlarıyla birlikte gösterir — herhangi bir satıra tıklayarak tam Geçmiş sayfasını açabilirsiniz.

---

### Kurulum Sihirbazı

İlk yapılandırma için rehberli 4 adımlı sihirbaz:

1. **Şablonları Kopyala** — Paketlenmiş örneklerden `config/config.json` ve `config/.env` oluşturur. Mevcut dosyaların üzerine yazmadan önce onay ister.
2. **Veritabanlarını Keşfet** — Bir veya daha fazla ana bilgisayarı otomatik olarak tarar ve tespit edilen tüm PostgreSQL, MySQL, MSSQL ve MongoDB örneklerini listeler. Hangilerinin yapılandırmanıza ekleneceğini seçin.
3. **Preflight Çalıştır** — Yapılandırmanızı doğrular: gerekli CLI araçlarının yüklü olduğunu, veritabanlarına erişilebilir olduğunu ve kimlik bilgilerinin doğru olduğunu kontrol eder. HATA / UYARI / TAMAM göstergeleriyle tam rapor sunar.
4. **Ayarlara Git** — E-posta, bulut ve zamanlama yapılandırmasını tamamlamak için Ayarlar sayfasına yönlendirir.

---

### Yedekleme

<p align="center">
  <img src="screenshots/backup_configure.png" alt="Yedekleme Sayfası" width="800"/>
</p>

Yedekleme sayfasının üç sekmesi vardır:

#### Yapılandırma Sekmesi

- **Yapılandırma Dosyaları** — `config.json` ve `.env` yollarını ayarlayın; canlı bütünlük durumu (TAMAM / UYUŞMAZLIK / EKSİK) görüntülenir.
- **Veritabanı Seçimi** — Yapılandırılmış tüm veritabanlarının onay kutulu listesi (ad, tür, host:port). Tümünü etkinleştirin veya belirli olanları seçin. Satır içi düzenleyiciyle girdileri düzenleyin.
- **Yedekleme Modu** — **Tam Yedekleme** (eksiksiz döküm) veya **Artımlı Yedekleme** (son tam yedeklemeden bu yana olan değişiklikler) arasında seçim yapın.
- **Hedefler** — Her çalıştırma için yerel depolama ve Google Drive yüklemesini etkinleştirin/devre dışı bırakın. E-posta alıcılarını ve saklama süresini (gün olarak) ayarlayın.

#### Çalıştırma Sekmesi

<p align="center">
  <img src="screenshots/backup_run.png" alt="Yedekleme Çalıştırma" width="800"/>
</p>

**Yedeklemeyi Başlat** düğmesine tıkladığınızda, başlamadan önce tam olarak neyin çalıştırılacağını gösteren Çalıştırma Özeti iletişim kutusu açılır (seçili veritabanları, hedefler, bütünlük durumu). Onaylandıktan sonra:

- Animasyonlu bir ilerleme çubuğu yedeklemenin devam ettiğini gösterir.
- Gerçek zamanlı log görüntüleyici her adımı gerçekleşirken yayınlar.
- **Durdur** düğmesi çalışan bir yedeklemeyi güvenle iptal etmenizi sağlar.
- Tamamlandığında, hangi veritabanlarının başarılı veya başarısız olduğunu, saklama temizleme istatistiklerini ve e-posta teslim durumunu gösteren bir sonuç iletişim kutusu açılır.

#### Preflight Sekmesi

<p align="center">
  <img src="screenshots/preflight.png" alt="Preflight" width="800"/>
</p>

Yedeklemeye başlamadan önce preflight kontrollerini bağımsız olarak çalıştırın. Sonuçlar tablosu renk kodludur:

| Renk    | Önem Derecesi | Anlam                                       |
|---------|---------------|---------------------------------------------|
| Kırmızı | HATA          | Yedeklemenin çalışmasını engeller           |
| Sarı    | UYARI         | Sorunlara yol açabilir, dikkatli devam edin |
| Yeşil   | TAMAM         | Kontrol başarılı                            |

---

### Geri Yükleme

<p align="center">
  <img src="screenshots/restore.png" alt="Geri Yükleme" width="800"/>
</p>

Geri Yükleme sayfası güvenli, adım adım bir geri yükleme iş akışı sunar:

1. **Yedekleme Seçin** — Bir tablo tüm mevcut yedekleri listeler (veritabanı adı, tür, oluşturma zamanı, dosya boyutu, yol). Yenilemek için **Yenile**'ye tıklayın.
2. **Hedef Veritabanı Seçin** — Açılır listeden geri yükleme yapılacak veritabanını seçin.
3. **Preflight** — Herhangi bir veriye dokunmadan önce geri yüklemenin başarılı olacağını doğrulayın.
4. **Deneme Çalıştırması** — Değişiklik yapmadan geri yüklemeyi simüle edin (preflight + sahte geri yükleme mantığı çalıştırır).
5. **Geri Yükle** — Gerçek geri yüklemeyi çalıştırın. Kazaları önlemek için bir onay iletişim kutusu `RESTORE` yazmanızı gerektirir.

İlerleme ve tüm geri yükleme adımları aşağıdaki log görüntüleyicide canlı olarak gösterilir.

---

### Geçmiş

<p align="center">
  <img src="screenshots/history.png" alt="Geçmiş" width="800"/>
</p>

Her yedekleme çalıştırmasının eksiksiz, filtrelenebilir denetim kaydı:

- **Duruma Göre Filtrele** — Tümü / Başarılı / Başarısız / Durduruldu
- **Profile Göre Filtrele** — Belirli bir ortam profiliyle sınırlandırın
- **Moda Göre Filtrele** — Tümü / Tam / Artımlı

Geçmiş tablosu zaman damgasını, profili, yedekleme modunu, durumu ve sonuçların özetini gösterir. Herhangi bir satıra çift tıklandığında **Ayrıntı İletişim Kutusu** açılır ve şunları içerir:

- Tam zaman damgaları, profil adı, yapılandırma yolu
- Sonuç sayıları: başarılı veritabanları, başarısız veritabanları
- Saklama istatistikleri: silinen dosyalar, saklanan dosyalar
- E-posta teslim durumu
- Hata özeti (varsa)
- Ham kaydı dışa aktarmak için **JSON Kopyala** düğmesi

---

### Ayarlar

<p align="center">
  <img src="screenshots/settings_email.png" alt="Ayarlar" width="800"/>
</p>

Ayarlar, sol taraftaki listeden seçilen 7 bölüme ayrılmıştır:

#### Genel
- **Salt Okunur Mod** — Tüm yedekleme ve geri yükleme işlemlerini devre dışı bırakır (yalnızca denetim erişimi için kullanışlı).
- **Tema** — Koyu ve Açık mod arasında anında geçiş yapın.
- **Dil** — Arayüz dilini Türkçe, İngilizce, Almanca, Rusça, Japonca, Çinçe, Korece, İspanyolca, Fransızca, Arapça ve İsveçce arasında değiştirin.

#### Bulut (Google Drive)
- Google Drive yüklemelerini etkinleştirin.
- Google hizmet hesabı kimlik bilgileri JSON'u ve token dosyasına giden yolları ayarlayın.
- Hedef Google Drive Klasör Kimliğini girin.

#### E-posta
- SMTP e-posta bildirimlerini etkinleştirin.
- Alıcı, gönderici, SMTP sunucusu, port ve kullanıcı adını yapılandırın.
- Parolalar `config/.env` dosyasından okunur (config.json'da saklanmaz).
- **Test** düğmesi bağlantıyı doğrulamak için doğrulama e-postası gönderir.

#### Zamanlama

<p align="center">
  <img src="screenshots/settings_schedule.png" alt="Zamanlama Ayarları" width="800"/>
</p>

- Windows Görev Zamanlayıcı aracılığıyla zamanlanmış yedeklemeleri etkinleştirin.
- Yedekleme saatini ve sıklığını (Günlük veya Haftalık) ayarlayın.
- **Görev Oluştur / Güncelle** düğmesi zamanlanmış görevi Windows Görev Zamanlayıcısı'na kaydeder.
- **Görevi Sil** onu kaldırır.
- Görevin bir sonraki planlanan çalıştırma zamanını gösterir.

#### Profiller
- Mevcut yapılandırmayı adlandırılmış profil olarak kaydedin (örn. `üretim`, `staging`).
- Bir açılır listeden profiller arasında geçiş yapın — her profilin kendi `config.json` ve `.env` dosyası vardır.
- Profilleri yeniden adlandırın, silin veya başlangıçta varsayılan olarak ayarlayın.

#### Hakkında
- Yüklü sürümü ve uygulama bilgilerini görüntüler.

#### Güncellemeler
- Tek bir tıklamayla daha yeni sürümleri kontrol edin.
- Mevcut sürüme karşı en son sürümü gösterir.
- Uygulama içinden güncellemeleri indirip yükleyin.

---

## Sistem Gereksinimleri

| Gereksinim              | Ayrıntılar                                            |
|-------------------------|-------------------------------------------------------|
| **İşletim Sistemi**     | Windows 10 veya Windows 11 (64-bit)                   |
| **Python**              | Gerekmez — bağımsız `.exe`                            |
| **PostgreSQL araçları** | `pg_dump`, `psql` (PostgreSQL yedekliyorsanız)        |
| **MySQL araçları**      | `mysqldump`, `mysql` (MySQL/MariaDB yedekliyorsanız)  |
| **MSSQL araçları**      | `sqlcmd` (MSSQL yedekliyorsanız)                      |
| **MongoDB araçları**    | `mongodump`, `mongorestore` (MongoDB yedekliyorsanız) |

Veritabanı CLI araçlarının yalnızca gerçekten kullandığınız veritabanı türleri için yüklenmesi gerekir. Sistem PATH'inizde (veya `config.json` aracılığıyla yapılandırılmış) erişilebilir olmaları gerekir.

---

## Kurulum

1. [Releases](../../releases) sayfasından en son sürümü indirin.
2. Zip dosyasını tercih ettiğiniz dizine çıkarın.
3. `BackupNexus.exe` dosyasını çalıştırın.
4. İlk açılışta lisans anahtarınızı girerek etkinleştirin.

---

## Hızlı Başlangıç Yapılandırması

BackupNexus **ayarları** **sırlardan** ayırır:

- **`config/config.json`** — Veritabanı bağlantıları, yedekleme hedefleri, e-posta sunucusu, zamanlama. Şifre yok.
- **`config/.env`** — Yalnızca şifreler (`DB_PASS`, `SMTP_PASS`, `FTP_PASS`, vb.).

**Kurulum Sihirbazı** (kenar çubuğu → Kurulum) her iki dosyayı şablonlardan oluşturur ve tüm süreçte size rehberlik eder. Manuel olarak yapılandırmayı tercih ederseniz:

**`config/config.json`** (minimal örnek):
```json
{
  "backup_root": "backups",
  "databases": [
    {
      "name": "uygulamam",
      "type": "postgres",
      "host": "localhost",
      "port": 5432
    }
  ]
}
```

**`config/.env`**:
```
DB_USER=postgres
DB_PASS=sifreniz_burada
```

---

## Fiyatlandırma ve Lisans

**BackupNexus**, tek seferlik ömür boyu satın alma olarak sunulan ticari bir üründür.

| Plan                 | Fiyat | Ayrıntılar                                                       |
|----------------------|-------|------------------------------------------------------------------|
| **Ömür Boyu Lisans** | $50   | Tek kullanıcı · 1 cihaza kadar · Ömür boyu erişim · Abonelik yok |

[**Şimdi Satın Al →**](https://metaldev.lemonsqueezy.com/checkout/buy/d9a2b152-3fea-4e43-bedb-b028a683eed4)

> Lisans anahtarınız satın alma işleminin hemen ardından e-posta ile teslim edilir.
> Etkinleştirmek için ilk açılışta uygulamaya girin.

Bu yazılım tescilli bir üründür. Yeniden dağıtım, tersine mühendislik veya alt lisans verilmesi yasaktır. Tam koşullar için [LICENSE](LICENSE) dosyasına bakın.

---

## Destek

Lisans sorunları veya teknik sorularınız için:

📧 backupnexus.support@gmail.com
---

## Dil

- 🇬🇧 [English README](README.md)
