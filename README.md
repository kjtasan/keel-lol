<p align="center">
  <img src="docs/images/cover.svg" alt="keel. — Şampiyon seçimine hazırlan. Maçını değerlendir. Riot anahtarı olmadan başla." width="1280">
</p>

<p align="center">
  <a href="https://github.com/kjtasan/keel-lol/releases/latest"><img src="docs/images/download.svg" alt="Windows için Keel’i indir" width="246" height="48"></a>
</p>

<p align="center">
  <a href="#kurulum">Kurulum</a> · <a href="#riot-api-anahtarı-gerekli-mi">API anahtarı</a> · <a href="https://github.com/kjtasan/keel-lol/releases">Sürüm notları</a> · <a href="https://github.com/kjtasan/keel-lol/issues">Sorun bildir</a>
</p>

Keel, League of Legends’ta şampiyon seçiminden maç sonuna kadar kullanabileceğin bir masaüstü yardımcısıdır. Takımına ve rakiplerine göre şampiyon seçenekleri sunar; rün, eşya ve sihirdar büyülerini kısa bir maç planıyla gösterir. Kütüphaneden şampiyonları ve eşleşmeleri inceleyebilir, geçmiş maçlarının sonuçlarına bakabilir ve Keel açıkken kaydedilen maçlarını rolüne göre değerlendirebilirsin.

> **Riot API anahtarı zorunlu değil.** Şampiyon önerileri, rün ve eşya hazırlığı, kütüphane, sessiz mod, yerel maç kaydı ve ortak veri yenileme anahtarsız çalışır. Geçmiş maçlarını Riot’tan almak ve kişisel havuzunu yenilemek için kendi anahtarını veya kapalı test davetini kullanabilirsin.

## Seçimler değiştikçe öneriler de değişir

Takımın ve karşı takım şampiyon seçtikçe Keel seçenekleri yeniden değerlendirir. Koridor rakibin netleştiğinde eşleşme verisini kullanır; henüz belli değilse kör seçim için uygun adayları değerlendirir. Her önerinin gerekçesini ve hangi noktalarda yeterli veri bulunmadığını görebilirsin.

<p align="center">
  <img src="docs/images/draft.webp" alt="Keel şampiyon seçimi ekranı: iki takımın seçimleri, üç şampiyon önerisi ve önerilerin gerekçeleri" width="1264" loading="lazy">
</p>

*Örnek seçim ekranı. Öneriler rolüne, seçimlere ve mevcut veriye göre değişir.*

## Maça hazırlan, sonrasında dönüp bak

Aşağıdaki özelliklerin tamamını **Riot anahtarı eklemeden** kullanabilirsin. Doğrulanmış ortak rün ve eşya dizilimleri kurulumla hazır gelir; kişisel maç geçmişinin boş olması bu önerileri engellemez.

| Bölüm | Ne işe yarar? |
|---|---|
| **Şampiyon seçimi** | Rolünü, takımını ve rakiplerini dikkate alan seçenekler sunar. Seçim başlayınca ana sayfadan otomatik geçiş yapar. |
| **Maç hazırlığı** | Kilitlediğin şampiyon için rün, eşya ve sihirdar büyüsü seçeneklerini kısa bir koridor planıyla gösterir. |
| **Sessiz mod** | Oyun sırasında bildirimlerle bölmez. Hazırladığın planı ve eşya önerilerini açıp inceleyebilirsin. |
| **Kütüphane** | Şampiyonların yaygın rollerini, dizilimlerini, takım arkadaşlarıyla uyumunu ve rakip eşleşmelerini bir araya getirir. |
| **Maç analizi** | Maçtaki katkını, inceleyebileceğin noktaları ve sonraki maç için en fazla iki somut hedefi gösterir. Uygun geçmiş maçlarınla karşılaştırır; varsa canlı kaydınla gelişimini tamamlar. |
| **Veri merkezi** | Kullanılan kaynakları ve veri kapsamını gösterir; yama ve ortak eşleşme verilerini yenileyebilirsin. |



**Keel kapalıyken oynadığın maçlar da listelenir.** Maç geçmişim bölümündeki **Geçmişi yenile** düğmesi son 20 maçı getirir; daha eskileri 20’şer maç halinde, son 200 maç kapsamında yükleyebilirsin. Maç sonu skoru, eşyalar, hasar, görüş ve skora katkı bilgileri gösterilir. Varsa eşleşen Keel canlı analizi aynı karttan açılır. Bu özellik kendi Riot anahtarınla veya kapalı test davetiyle çalışır.

**Maç kartında rakibini ve hazırlığını da gör.** Yeşil çerçevede oynadığın şampiyon, kırmızı çerçevede koridor rakibin yer alır. Yanlarında mod, koridor, tarih, skor, büyü ve rün ikonları, eşyalar ve AI puanı gösterilir. İkonların adlarına üzerlerine gelerek ulaşabilirsin. Bulut davetiyle 10 üzerinden AI puanı hazırlanır; “Neden?” ile kısa Türkçe gerekçesi açılır. Puan, rol ve maç sonu istatistiklerine dayalı yaklaşık bir yorumdur. Oyuncu adı, PUUID, maç kimliği ve Riot anahtarı modele gönderilmez. Puanlar saklanır; kapalı testte günlük değerlendirme sınırı vardır.

<p align="center"><img src="docs/images/history-row.webp" alt="Örnek verilerle Keel maç geçmişi: yeşil ve kırmızı şampiyon portreleri, VS, skor, büyüler, rünler, eşyalar ve AI puanı" width="1264" loading="lazy"></p>

*Örnek geçmiş ekranı; gerçek hesabın verilerini içermez. Görseldeki puanlar yerleşimi göstermek için örnektir.*

Eşya, rün ve sihirdar büyüsü adlarında **oyundaki Türkçe karşılıklar** kullanılır. Eşya kütüphanesi Sihirdar Vadisi kapsamına göre süzülür.

<p align="center">
  <img src="docs/images/library.webp" alt="Keel kütüphanesi: şampiyon görselleri, arama ve rün, eşya, ikili, rakip bölümleri" width="1264" loading="lazy">
</p>

<details>
<summary><strong>Ana sayfayı da incele</strong></summary>

Ana sayfadan seçim ekranına, kütüphaneye, maç geçmişine ve veri merkezine geçebilirsin. League bağlantısı otomatik kurulur.

![Keel’in Ahri görselli güncel ana sayfası ve bölüm bağlantıları](docs/images/home-current.webp)

</details>

> **0.1.14 ile yenilendi:** Daha hızlı logo açılışı, düzeltilen başlangıç odağı ve dar pencerelerde düzgün kalan bölüm kartları. [Sürüm notlarını incele.](https://github.com/kjtasan/keel-lol/releases/tag/v0.1.14)

## Kurulum

**Windows 10 (19041 ve sonrası) veya Windows 11 · 64 bit**

1. [Son sürümün kurulum dosyasını indir.](https://github.com/kjtasan/keel-lol/releases/latest)
2. Kurulumu tamamla ve masaüstü kısayolundan Keel’i aç.
3. League istemcisini aç. Şampiyon seçimi başlayınca Keel ilgili ekrana otomatik geçer.

Başlamak için Riot anahtarı eklemen, Python kurman veya komut satırı kullanman gerekmez. Görüntüleme bileşeni eksikse kurulum Microsoft WebView2’yi internet üzerinden hazırlar.

## Riot API anahtarı gerekli mi?

**Genel kullanım için hayır.** Anahtar eklemediğinde takım ve rakip seçimlerine göre ortak verilerden öneri almaya devam edersin. Keel açıkken oynadığın maçların yerel kaydı için de anahtar gerekmez.

**Kişisel havuzunu eklemek istersen:** **Hesabım** bölümüne Riot ID’ni, sunucunu ve kendi [Riot geliştirici anahtarını](https://developer.riotgames.com/) ekleyebilirsin. Keel geçmiş maçlarını inceleyerek en az 5 maç oynadığın şampiyonları kişisel değerlendirmeye katar. Yeterli kişisel maç bulunmadığında genel verilerden yararlanır.

**Kapalı test davetin varsa:** Hesabım → Kapalı test · Bulut bağlantısı alanına hizmet adresini ve kişiye özel davet kodunu ekleyebilirsin. Ortak Personal API Key hizmeti yalnızca küçük, davetli özel test grubu içindir; herkese açık erişim sunmaz.

Kendi Riot anahtarını girersen anahtar bilgisayarında saklanır. Davetli bulut bağlantısında ortak anahtar hizmette gizli tutulur ve kullanıcılara verilmez; maç verileri hizmet üzerinden alınır, indirilen geçmiş bilgisayarında saklanır. Riot hesabının şifresi istenmez.

## Güncellemeler ve verilerin

- **Uygulama kendini günceller.** 0.1.2 ve sonrasında Keel açılışta yeni sürümü arka planda kontrol eder, doğrular ve otomatik indirir. Kurulumu oyun, şampiyon seçimi ve veri işlemleri bittikten sonra yapar; ardından yeniden açılır.
- **Maç geçmişin korunur.** Kişisel havuzun, maç kayıtların ve ayarların program dosyalarından ayrı, kendi bilgisayarında tutulur. Yeni sürüm kurulurken silinmez.
- **Ortak veriler kurulumla gelir.** Şampiyon, görsel ve eşleşme verilerini kullanmak için kendi maç arşivini toplaman gerekmez. Oyun verilerini ayrıca **Veri merkezi** üzerinden yenileyebilirsin.

<details>
<summary><strong>İlk sürümler ve kurulum hakkında</strong></summary>

0.1.4 veya daha eski bir sürümde güncelleme denetimi “kontrol ediliyor” durumunda kalıyorsa [son kurulum dosyasını](https://github.com/kjtasan/keel-lol/releases/latest) bir kez indirip mevcut kurulumun üzerine yükle. 0.1.5, paketlenmiş uygulamadaki güvenli bağlantı dosyası eksikliğini düzeltir. Hesap ayarların ve maç kayıtların korunur; sonraki güncellemeleri Keel yönetir.

Windows yayıncı sertifikası henüz eklenmemiştir. Resmî dağıtım adresi bu deponun [Releases](https://github.com/kjtasan/keel-lol/releases) bölümüdür. Keel’in güncelleme sistemi sürüm bilgisinin imzasını ve indirilen kurulum dosyasının bütünlüğünü kontrol eder.

</details>

---

Keel geliştirme aşamasındadır. Öneriler mevcut veriye dayanır; kazanma garantisi vermez. Görseller örnek hesap ve seçimlerle hazırlanmıştır.

Bu depo uygulama tanıtımını ve Windows kurulumlarını içerir. Kişisel veriler, Riot anahtarları ve ham maç arşivi yayımlanmaz.

Keel, Riot Games tarafından desteklenmez veya onaylanmaz. League of Legends ve ilgili oyun görselleri Riot Games’e aittir.
