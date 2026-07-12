# Kastet — App Store Yayın Adımları (Mac'siz)

Proje hazır durumda: Capacitor iOS projesi (`ios/`), ikonlar/açılış ekranı ve
Codemagic bulut derleme yapılandırması (`codemagic.yaml`) oluşturuldu.
Bundle ID: **com.bivomedya.kastet** · Takım: Bivo Medya (985WG26M7B)

## 1. Projeyi GitHub'a yükleyin
1. github.com → New repository → ad: `kastet` (Private olabilir) → Create
2. Bu klasörde (`kastet-app`) terminal açıp:
   ```
   git remote add origin https://github.com/KULLANICI_ADINIZ/kastet.git
   git push -u origin main
   ```
   (İlk commit hazır; sadece remote ekleyip push edeceksiniz.)

## 2. App Store Connect API anahtarı oluşturun
1. appstoreconnect.apple.com → **Users and Access** → **Integrations** → **App Store Connect API**
2. **Team Keys** sekmesi → **+** → Ad: `codemagic`, Access: **App Manager** → Generate
3. Şunları not alın / indirin:
   - **Issuer ID** (sayfanın üstünde)
   - **Key ID**
   - **.p8 dosyası** (yalnızca 1 kez indirilebilir!)

## 3. Codemagic hesabı ve bağlantı
1. codemagic.io → GitHub ile giriş yapın → `kastet` reposunu ekleyin
2. **Teams → Personal Account → Integrations → Developer Portal → Manage keys**:
   API anahtarını yükleyin; **adını `kastet-api-key` yapın** (codemagic.yaml bu adı bekliyor)
3. Uygulama ayarlarında workflow otomatik görünür: **Kastet iOS — TestFlight & App Store**
4. **Start new build** → workflow'u seçin → Build

Codemagic imzalama sertifikasını ve provisioning profile'ı API anahtarıyla
otomatik oluşturur (Mac'te sertifika üretmenize gerek yok).

## 4. App Store Connect'te uygulama kaydı
1. appstoreconnect.apple.com → My Apps → **+ New App**
2. Platform: iOS · Name: `Kastet — İskambil Oyunu` · Language: Turkish
   · Bundle ID: `com.bivomedya.kastet` · SKU: `kastet1`
3. Build başarılı olunca TestFlight sekmesinde derleme belirir →
   telefonunuza TestFlight uygulamasıyla kurup test edin

## 5. Mağaza bilgilerini doldurun
- **Ekran görüntüleri:** 6.7" (1290×2796) zorunlu — oyundan görüntüler
- **Açıklama + anahtar kelimeler** (Türkçe)
- **Gizlilik Politikası URL** (zorunlu): oyun hiç veri toplamıyor;
  tek sayfalık metin GitHub Pages'te ücretsiz barındırılabilir
- **App Privacy** anketi: "Data is not collected" seçin
- **Yaş derecelendirmesi:** kart oyunu, kumar yok → 4+
- **Pricing:** Free (ya da istediğiniz fiyat)

## 6. İncelemeye gönderin
App Store sekmesi → derlemeyi seçin → **Submit for Review**.
İlk inceleme genellikle 1-2 gün sürer.

---

## Güncelleme akışı (sonraki sürümler)
1. Oyunda değişiklik yapıldığında `www/` içindeki dosyalar güncellenir
2. `git commit` + `git push`
3. Codemagic'te yeni build başlatın → TestFlight'a otomatik gider
4. App Store Connect'te yeni sürüm oluşturup incelemeye gönderin
