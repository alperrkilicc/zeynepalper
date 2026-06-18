# 📖 Özelleştirme ve Düzenleme Kılavuzu

Bu kılavuz, mevcut davetiye şablonunun özelleştirilmesi, Kurtlar Vadisi temasından arındırılması, karşılaşılan fonksiyonel hataların giderilmesi ve Google Drive entegrasyonunun gerçekleştirilmesi amacıyla hazırlanmıştır.

---

## 1. 📁 Proje Klasör Yapısı & CSS/JS Konumları

### Mevcut Klasör Şeması ve Kütüphaneler
Projenin hazır kütüphaneleri ve özelleştirme yapıları şu klasörlerde yer almaktadır:
*   **Ana Sayfa Yapısı:** `livanaorg.com/elifpolat/index.html` (Tüm tasarım ve yerel komutlar buradadır.)
*   **Medya Varlıkları:** 
    *   Görseller: `livanaorg.com/elifpolat/public/images/` (`1.jpg`, `2.jpg`, `3.jpg`, `4.jpg`, `bg.jpg`, `cewe.jpg`, `cowo.jpg`)
    *   Müzik: `livanaorg.com/elifpolat/public/music/` (`elif.mp3`)
*   **Hazır Kütüphaneler & Yazı Tipleri (Üst Klasörler):**
    *   UIKit CSS/JS: `cdn.jsdelivr.net/npm/uikit@3.16.24/dist/`
    *   FontAwesome: `cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/`
    *   GSAP & ScrollTrigger: `cdnjs.cloudflare.com/ajax/libs/gsap/3.12.2/`
    *   Google Fonts: `fonts.googleapis.com/` ve `fonts.gstatic.com/`

### Dosyaları Ana Kök Dizine (`zeynepalper`) Taşıma Rehberi (Teknik Detay)
Projenin daha düzenli çalışması ve URL karmaşasından kurtulması için dosyaları kök dizine taşırken aşağıdaki adımları ve kod güncellemelerini harfiyen uygulayınız:

**1. Dosya Taşıma İşlemi:**
- `livanaorg.com/elifpolat/index.html` dosyasını `zeynepalper/` dizinine taşıyın.
- `livanaorg.com/elifpolat/public/` klasörünü (içindeki images ve music ile birlikte) `zeynepalper/` dizinine taşıyın.
- `livanaorg.com` klasörünü artık silebilirsiniz.

**2. Bağlantı Yollarının Düzeltilmesi (index.html):**
Dosyaları kök dizine çıkardığınızda, `index.html` içindeki `../../` ile başlayan yollar artık yanlış yeri gösterecektir. Bunları `./` (mevcut dizin) olarak güncellemeniz gerekir.

| Dosya Türü | Satır No | Eski Hatalı Yol (İç içe klasördeyken) | Yeni Doğru Yol (Kök dizindeyken) |
| :--- | :---: | :--- | :--- |
| **CSS (UIKit)** | 27 | `../../cdn.jsdelivr.net/...` | `./cdn.jsdelivr.net/...` |
| **CSS (Fonts)** | 28 | `../../fonts.googleapis.com/...` | `./fonts.googleapis.com/...` |
| **CSS (Icons)** | 29 | `../../cdnjs.cloudflare.com/...` | `./cdnjs.cloudflare.com/...` |
| **JS (GSAP)** | 30 | `../../cdnjs.cloudflare.com/...` | `./cdnjs.cloudflare.com/...` |
| **JS (ScrollTrigger)** | 31 | `../../cdnjs.cloudflare.com/...` | `./cdnjs.cloudflare.com/...` |
| **JS (Lenis)** | 32 | `../../unpkg.com/...` | `./unpkg.com/...` |
| **Resim (Besmele)** | 165 | `../../upload.wikimedia.org/...` | `./upload.wikimedia.org/...` |
| **JS (UIKit Lib)** | 352 | `../../cdn.jsdelivr.net/...` | `./cdn.jsdelivr.net/...` |

**Not:** `public/images/` ve `public/music/` ile başlayan yolları değiştirmenize gerek yoktur; çünkü `public` klasörünü de `index.html` ile aynı seviyeye (kök dizine) taşıdığınız için bu yollar otomatik olarak çalışmaya devam edecektir.

---

## 2. ✏️ Temel Özelleştirmeler (Adım Adım Kılavuz)

### Tarih, Adres, Harita ve Geri Sayım Güncellemeleri
`index.html` dosyasında nokta atışı satırlar ve güncellenecek alanlar şunlardır:
*   **Ana Ekran Düğün Tarihi:** Satır 159'daki `<p class="hero-date gs-anim">CUMARTESİ, 29 . 08 . 2026</p>` alanından güncellenir.
*   **Ana Ekran Genel Konum/Şehir Bilgisi:** Satır 160'taki `<p class="uk-text-small gs-anim" style="letter-spacing: 2px; opacity: 0.7;">İSTANBUL, TÜRKİYE</p>` alanından değiştirilir.
*   **Kına Merasimi Tarihi ve Günü:** Satır 170 (`28 Ağustos 2026`) ve Satır 172 (`CUMA`) alanlarından güncellenir.
*   **Kına Mekanı ve Adresi:** Satır 175-176'daki `<strong>DURAN EMMİ'NİN KIRAATHANESİ</strong>` ve `Salacak Mah. Üsküdar/İstanbul` alanlarından değiştirilir.
*   **Kına Harita Linki:** Satır 179'daki `href="https://goo.gl/maps/duran-emmi-ornek-link"` özniteliğine yeni Google Maps linki yapıştırılır.
*   **Düğün Merasimi Tarihi ve Günü:** Satır 186 (`29 Ağustos 2026`) ve Satır 188 (`CUMARTESİ`) alanlarından güncellenir.
*   **Düğün Mekanı ve Adresi:** Satır 191-192'deki `<strong>KIZ KULESİ</strong>` ve `Salacak Mevkii, Üsküdar/İstanbul` alanlarından değiştirilir.
*   **Düğün Harita Linki:** Satır 195'teki `href="https://goo.gl/maps/kiz-kulesi-ornek-link"` özniteliğine yeni Google Maps linki yapıştırılır.
*   **Geri Sayım Sayacı (Countdown) Hedef Tarihi:** Satır 407'de bulunan JavaScript kodu güncellenmelidir:
    ```javascript
    const targetDate = new Date("Aug 29, 2026 20:00:00").getTime();
    ```
    Buraya yeni tarih İngilizce ay kısaltmasıyla (Örn: `Sep 15, 2026 19:30:00`) yazılmalıdır.

### Genel Arka Plan Görseli veya Rengi Değişimi
Sitenin arka plan görselleri `public/images/bg.jpg` dosyasından okunmaktadır.
*   **Açılış Ekranı Arka Planı:** Satır 125'teki `<img src="public/images/bg.jpg" ... id="img-opening">`
*   **Ana Sayfa Arka Planı:** Satır 142'deki `<img src="public/images/bg.jpg" ... id="img-main">`
*   **Değişim Yöntemi:** Yeni arka plan görselinizi `public/images/` klasörüne `bg.jpg` ismiyle kaydederek doğrudan değiştirebilirsiniz veya kod üzerindeki `src` yollarını değiştirebilirsiniz. Genel arka plan rengini değiştirmek için Satır 33'teki `html, body { background: transparent; ... }` alanında yer alan `transparent` değerini CSS renk koduyla (Örn: `#111111`) değiştirebilirsiniz.

### Fotoğraf Galerisine Yeni Fotoğraf Ekleme
Sitedeki mevcut galeri elemanları Satır 259-282 arasında yer almaktadır.
*   **Fotoğraf Yolları:** Kodda `public/images/1.jpg`, `2.jpg`, `3.jpg`, `4.jpg` olarak tanımlıdır.
*   **Yeni Fotoğraf Ekleme Adımları:**
    1. Yeni fotoğraflarınızı `public/images/` klasörünün altına `5.jpg`, `6.jpg` gibi isimlerle yükleyin.
    2. Satır 277-282 arasındaki galeri elemanı HTML bloğunu kopyalayıp hemen altına yapıştırın:
       ```html
       <div class="gallery-item gs-gallery">
           <div class="gallery-frame">
               <img src="public/images/5.jpg" alt="Fotoğraf 5">
               <div class="gallery-overlay"><i class="fas fa-search-plus"></i></div>
           </div>
       </div>
       ```

---

## 3. ⚙️ Fonksiyonel Düzenlemeler & Kod Temizliği

### Açılış Ekranının (Loading) Devre Dışı Bırakılması
Sitenin ilk açılışındaki 1 saniyelik boş yükleme ve buton ekranını kaldırıp doğrudan ana sayfayı göstermek için:
1.  Satır 152'de yer alan ana içerik kapsayıcısını bulun:
    ```html
    <main id="main-content" style="opacity: 0; pointer-events: none;">
    ```
    Bu satırı şu şekilde güncelleyin (görünür ve tıklanabilir yapın):
    ```html
    <main id="main-content" style="opacity: 1; pointer-events: all;">
    ```
2.  Satır 123-126 arasındaki açılış arka plan katmanını (`<div id="-opening" ...>...</div>`) ve Satır 128-138 arasındaki açılış içeriğini (`<div id="opening-content">...</div>`) koddan tamamen silin.

### Kına Bölümünün Silinmesi (Sadece Düğün Kalacak Şekilde)
1.  Satır 216 ile 232 arasında yer alan Kına sütun bloğunu (`<div class="uk-first-column"> ... </div>`) tamamen silin.
2.  Geriye kalan Düğün sütununun tam ortalanması için Satır 214'teki grid yapısında bulunan `uk-child-width-1-2@s` sınıfını `uk-child-width-1-1` olarak güncelleyebilirsiniz.

### Ömer Baba Sözünün Silinmesi
1.  Satır 168 ile 176 arasında yer alan ve sonu `- Ömer Baba` ile biten alıntı seksiyonunu tamamen koddan temizleyin:
    ```html
    <section class="uk-section">
        ...
    </section>
    ```

### Katılım Durumu (RSVP) Formunun Silinmesi
1.  Satır 289 ile 301 arasında yer alan Katılım Durumu sütun bloğunu (`<div class="uk-first-column"> ... </div>`) tamamen silin.
2.  Kalan Dijital Anı Defteri alanının tam genişlik kaplaması için üst kapsayıcıdaki grid ayarlarını düzenleyebilirsiniz.

---

## 4. 🔄 Konsept Değişimi & "Livanaorg" Temizliği

### Kurtlar Vadisi Temasından Çıkış & İsim Değişiklikleri
Sitedeki "Elif" ve "Polat" isimleri ile konsept replikleri şu satırlardan temizlenmelidir:
*   **Sekme Başlığı:** Satır 13 (`<title>Elif &amp; Polat - Düğün Davetiyesi</title>`)
*   **Giriş Ekranı İsimleri:** Satır 131 (`Elif<br>...<br>Polat`)
*   **Ana Sayfa Başlığı:** Satır 157 (`Elif ... Polat`)
*   **Kurtlar Vadisi Repliği:** Satır 161'deki *"Ölüm ölüm dediğin nedir ki gülüm..."* sözünü tamamen silip yerine kendi davetiye sözünüzü yazın.
*   **Gelin İsim ve Aile Bilgisi:** Satır 188 (`Elif Eylül`) ve Satır 189 (`Ayşe Eylül'ün Kızı`)
*   **Damat İsim ve Aile Bilgisi:** Satır 194 (`Polat Alemdar`) ve Satır 195 (`Ömer &amp; Nazife Candan'ın Oğlu`)
*   **WhatsApp Bildirim Mesajı İçeriği:** Satır 444 (`Elif & Polat Düğün Merasimi`) ve Satır 451 (`Vadi Konsepti`) metinlerini kendinize göre güncelleyin.
*   **Kapanış Bilgileri:** Satır 324 (`Elif &amp; Polat`), Satır 328 (`Ayşe Eylül &amp; Ömer - Nazife Candan`), Satır 331 (`© 2026 Elif &amp; Polat`) ve Satır 332 (`Vadi'nin Derinliklerinden Sevgilerle`) alanlarını güncelleyin.

### Arka Plan Müzik Değişimi ve Otomatik Oynatma Politikaları
*   **Müzik Bağlantısı:** Satır 120'de yer alan `<audio id="bgMusic" loop="" src="public/music/elif.mp3"></audio>` kodundaki `elif.mp3` yerine yeni müzik dosyanızın adını yazın (Örn: `public/music/muzik.mp3`).
*   **Otomatik Oynatma Engeli:** Modern tarayıcılar kullanıcı sayfada hiçbir yere tıklamadan müziğin otomatik çalmasını engeller. Sitede yer alan "Davetiyeyi Aç" butonu (Satır 136) tam olarak bu engeli aşmak için tasarlanmıştır. Butona tıklandığı an Satır 356'daki `audio?.play()` tetiklenir ve müzik sorunsuzca başlar. Eğer açılış ekranını kaldırırsanız, müziğin çalabilmesi için kullanıcının sayfada herhangi bir yere (örneğin ekrana veya müzik disk butonuna) ilk dokunuşu yapması gerekecektir.

### Livanaorg Mutlak Bağlantılarının Temizlenmesi
Klasör yapısındaki `livanaorg.com` kaldırıldıktan sonra, kod içerisinde harici bir mutlak URL (`http://livanaorg.com/...`) bağımlılığı bulunmamaktadır. Tüm kütüphane ve varlık erişimleri yerel klasör yolları (`../../` veya `./`) üzerinden sağlandığı için 1. maddedeki taşıma adımlarını uygulamanız temizlik için tamamen yeterlidir.

---

## 5. 🚨 Sonsuz Aşağı Kayma (Scroll) Hatasının Çözümü (Kritik)

### Hatanın Nedeni
Sayfa ilk yüklendiğinde, ana içerik alanı (`#main-content`) `opacity: 0; pointer-events: none;` stilleri ile gizlidir. Sayfa akışında yer kaplamadığı veya boyutları tam hesaplanamadığı için, pürüzsüz kaydırma kütüphanesi **Lenis**, sayfa yüksekliğini eksik/hatalı hesaplamaktadır. "Davetiyeyi Aç" butonuna basılıp ana sayfa görünür hale geldiğinde sayfa aniden uzamakta, fakat Lenis bu yükseklik değişiminden haberdar olmadığı için sayfa sonundaki "Davet edenler" kısmından sonra bile aşağıya doğru sonsuz bir boşluğa/karanlığa kaymaya devam etmektedir. Ayrıca `lenis` değişkeni Satır 339'daki `try {}` bloğu içerisinde `const lenis` şeklinde lokal tanımlandığı için dış fonksiyonlardan erişilemez durumdadır.

### Kesin Çözüm Adımları
1.  **Lenis Değişkenini Küresel (Global) Yapın:**
    Satır 339-343 arasındaki pürüzsüz kaydırma kod bloğundaki `const lenis` tanımını `window.lenis` olarak değiştirerek dışarıdan erişilebilir kılın:
    ```javascript
    try {
        window.lenis = new Lenis({ duration: 1.2, easing: (t) => Math.min(1, 1.001 - Math.pow(2, -10 * t)) });
        function raf(time) { window.lenis.raf(time); requestAnimationFrame(raf); }
        requestAnimationFrame(raf);
    } catch (e) { console.log("Native scroll used"); }
    ```
2.  **Davetiye Açıldığında Yüksekliği Yenileyin:**
    Satır 347'de başlayan `openInvitation()` fonksiyonunun içerisindeki animasyonların tamamlandığı veya içeriklerin görünür olduğu alana (Satır 393 civarı, `initParallax?.();` komutunun hemen üzerine) **Lenis Yenileme** ve **GSAP ScrollTrigger Yenileme** komutlarını ekleyin:
    ```javascript
    // Boyutları yeniden hesapla ve kaydırma sınırlarını bıçak gibi kes
    if (window.lenis) {
        window.lenis.resize();
    }
    ScrollTrigger.refresh();
    ```

---

## 6. 📸 Ziyaretçi Fotoğraf Yükleme & Google Drive Entegrasyonu

Ziyaretçilerinizin yüklediği fotoğrafların doğrudan Google Drive klasörünüze yüklenmesi için tamamen ücretsiz olan "Google Apps Script" altyapısını kullanabilirsiniz.

### Adım 1: Google Apps Script Kodunun Hazırlanması
1.  Google Drive'ınızda fotoğrafların birikeceği yeni bir klasör oluşturun. Klasörün URL adresindeki uzun rastgele karakter dizisini (Klasör ID'si) kopyalayın.
2.  [script.google.com](https://script.google.com) adresine gidin ve **"Yeni Proje"** oluşturun.
3.  Aşağıdaki kodu editöre yapıştırın ve `GOOGLE_DRIVE_KLASOR_ID_BURAYA` alanına kopyaladığınız ID'yi yazın:

```javascript
function doPost(e) {
  try {
    var data = JSON.parse(e.postData.contents);
    var fileContent = data.file;
    var fileName = data.name;
    var contentType = data.type;
    
    // Base64 formatındaki dosyayı decode etme
    var decodedFile = Utilities.base64Decode(fileContent.split(",")[1]);
    var blob = Utilities.newBlob(decodedFile, contentType, fileName);
    
    // Hedef klasöre dosyayı kaydetme
    var folder = DriveApp.getFolderById("10p1_OXl7iftObfYegyNu-fer0ZFGSSfA");
    var file = folder.createFile(blob);
    
    return ContentService.createTextOutput(JSON.stringify({ "status": "success", "url": file.getUrl() }))
      .setMimeType(ContentService.MimeType.JSON);
  } catch (error) {
    return ContentService.createTextOutput(JSON.stringify({ "status": "error", "message": error.toString() }))
      .setMimeType(ContentService.MimeType.JSON);
  }
}
```

### Adım 2: Web Uygulaması Olarak Dağıtma (Deploy)
1.  Sağ üstteki **"Dağıt" (Deploy)** butonuna tıklayıp **"Yeni dağıtım"** seçeneğini seçin.
2.  Dişli çark simgesinden türü **"Web uygulaması" (Web app)** olarak belirleyin.
3.  Ayarları şu şekilde yapın:
    *   *Uygulamayı şu kişi olarak yürüt:* **Ben (E-posta adresiniz)**
    *   *Erişimi olanlar:* **Herkes (Anyone)** *(Bu ayar ziyaretçilerin şifresiz yükleme yapabilmesi için kritiktir).*
4.  **"Dağıt"** butonuna basın, gerekli Google izinlerini onaylayın ve dağıtım sonunda size verilen **Web Uygulaması URL'sini (Web App URL)** kopyalayın.

### Adım 3: Sitenin HTML/JS Tarafındaki Bağlantısı
1.  `index.html` dosyasında Satır 311 civarında yer alan "Anı Yükle" buton alanını gizli bir dosya seçici (`input`) tetikleyecek şekilde güncelleyin:
    ```html
    <input type="file" id="photoUploader" style="display:none;" accept="image/*" onchange="uploadPhoto(this)">
    <button onclick="document.getElementById('photoUploader').click()" class="uk-button uk-button-small" style="background: var(--gold-gradient); color: #000; border-radius: 30px; padding: 10px 25px; font-weight: bold; border: none; width: 100%; display: flex; align-items: center; justify-content: center;">
        <i class="fas fa-cloud-upload-alt" style="margin-right: 8px;"></i> Anı Yükle
    </button>
    ```
2.  Aynı dosyadaki `<script>` etiketlerinin en sonuna (Satır 485 civarı) aşağıdaki dosya yükleme fonksiyonunu ekleyin ve `FOTO_YUKLEME_WEB_APP_URL_BURAYA` alanına kopyaladığınız Web Uygulaması URL'sini yapıştırın:
    ```javascript
    function uploadPhoto(fileInput) {
        const file = fileInput.files[0];
        if (!file) return;

        // Kullanıcıya yükleme başladığına dair bilgi verme
        const originalText = fileInput.nextElementSibling ? fileInput.nextElementSibling.innerHTML : "Anı Yükle";
        if(fileInput.nextElementSibling) fileInput.nextElementSibling.innerHTML = "<i class='fas fa-spinner fa-spin'></i> Yükleniyor...";

        const reader = new FileReader();
        reader.onload = function(e) {
            const payload = {
                file: e.target.result,
                name: file.name,
                type: file.type
            };

            fetch("FOTO_YUKLEME_WEB_APP_URL_BURAYA", {
                method: "POST",
                body: JSON.stringify(payload)
            })
            .then(res => res.json())
            .then(data => {
                if(data.status === "success") {
                    alert("Fotoğrafınız başarıyla Dijital Anı Defteri'ne yüklendi! Teşekkür ederiz.");
                } else {
                    alert("Yükleme hatası: " + data.message);
                }
            })
            .catch(err => {
                alert("Bağlantı hatası oluştu.");
                console.error(err);
            })
            .finally(() => {
                if(fileInput.nextElementSibling) fileInput.nextElementSibling.innerHTML = originalText;
                fileInput.value = ""; // Seçiciyi sıfırla
            });
        };
        reader.readAsDataURL(file);
    }
    ```

---

## 7. 🌟 Ekstra Profesyonel Özelleştirmeler

Bu bölüm, davetiyenizin sosyal medyada paylaşılırken profesyonel görünmesi ve tarayıcı detaylarının eksiksiz olması için eklenmiştir.

### 1. WhatsApp & Sosyal Medya Paylaşım Önizlemeleri (Meta OG Etiketleri)
Mevcut `index.html` dosyasında sosyal medya önizleme etiketleri (Open Graph) bulunmamaktadır. Link gönderildiğinde şık bir kart görünümü oluşması için Satır 21'deki `<meta charset="UTF-8">` satırının hemen altına aşağıdaki kodları ekleyin:

```html
<!-- Sosyal Medya Önizleme Etiketleri -->
<meta property="og:title" content="Zeynep & Alper - Düğün Davetiyesi">
<meta property="og:description" content="Bu mutlu günümüzde sizleri de aramızda görmekten onur duyarız.">
<meta property="og:image" content="https://site-adresiniz.com/public/images/bg.jpg">
<meta property="og:url" content="https://site-adresiniz.com">
<meta property="og:type" content="website">
```
*   **og:image:** Buraya yazacağınız link, paylaşım yapıldığında görünecek olan küçük resimdir. `public/images/bg.jpg` veya özel bir kare görsel (`og-image.jpg`) kullanmanız önerilir.

### 2. Tarayıcı Sekme Başlığı ve Favicon
*   **Sekme Başlığı:** Sitede iki farklı başlık alanı bulunmaktadır. Bunları yeni isimlerle güncelleyin:
    *   Satır 3: `<title>Özel Davetiye</title>`
    *   Satır 25: `<title>Elif &amp; Polat - Düğün Davetiyesi</title>`
*   **Favicon (Sekme İkonu):** Tarayıcı sekmesinde görünen küçük ikon için Satır 26'daki `<title>` etiketinin altına şu kodu ekleyin:
    ```html
    <link rel="icon" type="image/png" href="public/images/favicon.png">
    ```
    *Not: `public/images/` klasörüne 32x32 boyutlarında `favicon.png` adında bir resim atmanız yeterlidir.*

### 3. Alt Bilgi (Footer) İmzaları ve Telif Yazıları
Sitenin en altındaki telif ve konsept yazılarını şu satırlardan güncelleyebilir veya silebilirsiniz:
*   **Telif Yazısı:** Satır 331'deki `© 2026 Elif &amp; Polat` alanını kendi isimlerinizle değiştirin.
*   **Konsept İmzası:** Satır 332'deki `"Vadi'nin Derinliklerinden Sevgilerle"` yazısını silebilir veya kendi özel notunuzu ekleyebilirsiniz.

### 4. Harici Analitik ve Gizli Scriptler (Temizlik)
*   **Mellon Script (Kritik Not):** Satır 7-17 arasında yer alan `<script> function mellon... </script>` bloğu, sayfanın eski bir kopyasını şifreli (base64) olarak barındırmaktadır. Siz `index.html` üzerinde değişiklik yapsanız bile, bazı durumlarda bu script eski içeriği geri yükleyebilir. **Temiz bir çalışma için Satır 7 ile 17 arasındaki bu script bloğunu tamamen silmeniz önerilir.**
*   **Analitik Kodları:** Yapılan taramada dosyada gizli bir Google Analytics veya takip kodu tespit edilmemiştir. Site tamamen yerel kütüphaneler ve standart JS motorları ile çalışmaktadır, bu da maksimum hız ve gizlilik sağlar.

---

## 8. 🎛️ %100 Yerel Admin Paneli Kullanım Kılavuzu

Davetiyenizi kodlama bilmeden, tamamen görsel bir arayüz üzerinden özelleştirebilmeniz için %100 yerel ve çevrimdışı çalışan bir yönetim altyapısı kurulmuştur.

### 1. Paneli Başlatma
*   Proje klasörünün içine yerleştirilen `admin.html` dosyasını bilgisayarınızda veya telefonunuzda herhangi bir tarayıcı (Chrome, Edge, Safari vb.) ile çift tıklayarak açın.
*   Bu panel **tamamen internet bağımsız (çevrimdışı)** çalışır. Hiçbir veriyi sunucuya göndermez, gizliliğinizi korur.

### 2. Genel Ayarların Yapılması
Panel arayüzünü açtığınızda sizi karşılayan form elemanlarını kullanarak şu alanları düzenleyebilirsiniz:
*   **İsim ve Aileler:** Gelin/Damat adlarını, tam adlarını ve aile isimlerini doğrudan kutucuklara yazın.
*   **Tarih ve Zamanlar:** Geri sayım sayacının hedef alacağı tam tarih ve saati takvim seçicisinden belirleyin. Düğün ve kına merasimi gün/saat/adres bilgilerini güncelleyin.
*   **Bölüm Switchleri (Açma/Kapama):** "Kına Bölümünü Göster", "RSVP Formunu Göster" veya "Açılış Ekranını Göster" switch'lerini kullanarak istemediğiniz bölümleri tek tıkla gizleyin. (Örneğin kına alanını kapattığınızda düğün alanı otomatik olarak tam genişlik kaplayacaktır).

### 3. 📸 Dinamik Galeri (Hatıralarımız) Yönetimi
*   Panelin alt kısmında yer alan **"📸 Galeri / Hatıralarımız Yönetimi"** alanındaki "Fotoğrafları Seç" butonuna basın.
*   Davetiyede görünmesini istediğiniz tüm düğün/nişan fotoğraflarını topluca seçin.
*   Seçtiğiniz fotoğrafların isimleri liste halinde ekrana gelecektir. İstemediğiniz resimleri yanındaki **"Sil"** butonuna basarak listeden çıkartabilirsiniz.

### 4. Değişiklikleri Kaydetme ve Canlıya Alma
1.  Formu doldurduktan ve fotoğrafları seçtikten sonra en alttaki **"Değişiklikleri Kaydet ve Ayar Dosyasını İndir"** butonuna tıklayın.
2.  Tarayıcınız otomatik olarak **`ayarlar.js`** adında bir dosya indirecektir.
3.  İndirilen bu `ayarlar.js` dosyasını kopyalayın ve davetiyenizin ana klasörüne (`index.html` dosyasının hemen yanına) yapıştırın.
4.  Panelde galeri için seçtiğiniz fotoğrafları da aynı isimlerle **`public/images/`** klasörünün içine atmayı unutmayın.
5.  `index.html` sayfasını yenilediğinizde tüm yeni isimler, tarihler, sayaç ve galeri görselleri anında aktif olacaktır!

*(Not: Eğer `ayarlar.js` dosyasını klasörden silerseniz, davetiye hiçbir hata vermeden otomatik olarak kendi içindeki orijinal varsayılan verilerle çalışmaya devam eder).*


