# Keel — Teknik Gizlilik Açıklaması
Son inceleme: 29 Ekim 2026 · Kapsam: Keel 0.1.14 ve incelenen bulut hizmeti kaynak kodu

Bu sayfa, uygulamanın hangi veriyi nerede kullandığını açıklar. **Tamamlanmış bir KVKK aydınlatma metni veya açık rıza formu değildir.** Hukuki veri sorumlusu kimliği, özel başvuru kanalı, işleme hukuki sebepleri ve uygulanacak yurt dışı aktarım koşulları ayrıca belirlenmelidir. Bu başlıkların kamuya açık GitHub sayfasında bulunmaması, verisi işlenen kullanıcıya gerekli bilgilendirmenin yapılması gereğini kaldırmaz.

## Hangi veri nereye gider?
| İşlem | Bilgisayarında kalanlar | Hizmete iletilen / hizmette işlenenler |
|---|---|---|
| Hesap ve ayarlar | Riot ID, sunucu, hesap/maç kimlikleri, kişisel havuz ve tercihler yerel kayıtlarda tutulur. Kendi Riot API anahtarın ve bulut davet kodun da yerel ayar dosyalarında saklanır. | Kendi Riot anahtarını kullanırken hesap/maç sorguları Riot'a gider. Davetli bulut bağlantısında sorgular Cloudflare Workers üzerinden Riot'a iletilir. |
| Maç geçmişi | İndirilen Riot maç yanıtları, maç kimlikleri, geçmiş listesi ve eşleşen yerel kayıtlar bilgisayarında saklanır. | Bulut kullanılırsa Riot ID, PUUID, maç kimliği, bölge ve gereken sorgu parametreleri hizmet tarafından işlenir. Riot yanıtları maçtaki diğer katılımcıların kimlik ve istatistiklerini de içerebilir. |
| Yerel canlı kayıt ve ayrıntılı analiz | Keel açıkken gözlenen skor, minyon, görüş, eşya ve zaman kayıtları ile yerel analiz bilgisayarında tutulur. | Yerel ayrıntılı raporu açmak, bu kayıtları AI modeline gönderen bir işlem değildir. |
| AI performans puanı | Dönen puan ve kısa gerekçe, ilgili yerel maç kaydıyla önbelleğe alınır. | Şampiyon, rol, mod, süre, sonuç, skor, hasar, altın, minyon, görüş, totem ve skora katkı gibi izinli istatistikler Cloudflare'deki değerlendirme hizmetine gönderilir. Model Cloudflare Workers AI üzerinden çalışır. |
| Güncellemeler ve ortak oyun verileri | İndirilen güncelleme ve ortak veriler yerelde saklanır. | GitHub ve oyun verisi sağlayıcılarına indirme istekleri yapılır. Bu indirme isteklerinin gövdesine kişisel maç arşivi veya Riot anahtarı eklenmez. |

Riot hesabının parolası istenmez. Ortak bulut Riot anahtarı Cloudflare secret olarak hizmette tutulur; masaüstü kurulumuna ve bu depoya eklenmez. Davet kodu, bulut isteklerinde HTTPS üzerinden yetkilendirme için kullanılır.

## AI modeline ne gönderilmez?
Değerlendirme girişinde oyuncu adı/Riot ID, PUUID, maç kimliği, Riot API anahtarı ve davet kodu modelin istemine eklenmez. Bulut hizmeti daveti doğrular; model yalnızca izinli oyun istatistikleriyle değerlendirme yapar. Bunları **doğrudan hesap kimliği çıkarılmış istatistikler** olarak tanımlıyoruz; hiçbir koşulda yeniden ilişkilendirilemeyecekleri iddia edilmiyor.

Destek değerlendirmesinde minyon ve altın; ARAM değerlendirmesinde görüş/totem ölçütleri modele verilen özelliklerden çıkarılır. AI puanı ile yerel ayrıntılı maç raporu ayrı özelliklerdir.

## Saklama süreleri ve önbellek
- **Bilgisayarındaki veriler:** Maç geçmişi, kişisel kayıtlar, yerel AI sonuçları ve ayarlar kullanıcı tarafından yönetilir. Genel bir otomatik silme süresi yoktur; uygulamayı kaldırmak kişisel veri klasörünü otomatik temizlemez.
- **Riot sorgu hizmeti:** İncelenen kod ham maç yanıtını, hesap adını veya PUUID'yi kendi kalıcı veritabanına yazmaz. Yanıtlar bellekte önbelleğe alınabilir; tekrar kullanım süresi 60 saniye, sınırı 16 kayıt ve kayıt başına 1 MB'dir. Süre dolması, kaydın tam o saniyede fiziksel bellekten silinmesi garantisi değildir; kapasite değişimi veya süreç yeniden başlatılması da temizlemeyi etkiler.
- **Bulut kota/davet kayıtları:** Davet özetleri, geçerlilik/kota bilgileri ve kullanım sayaçları hizmette tutulur. Günlük sayaçlar yeni günün isteğinde yenilenir; bunun tüm kayıtların sabit bir saatte silindiği anlamına geldiği iddia edilmez.
- **AI sonuçları:** Değerlendirme isteğinin istatistiklerinden üretilen özet anahtarı ile puan, kısa gerekçe ve model/sürüm bilgisi Cloudflare Durable Objects içinde **kalıcı önbelleğe** yazılır. İncelenen kodda bu sonuçlar için otomatik silme süresi tanımlı değildir. Ham model istemi ve ham Riot maç yanıtı bu AI sonuç kaydına yazılmaz.
- **Davet yönetimi:** İşletmecinin yerel yönetim kayıtlarında davet etiketi, kodu, son kullanma zamanı ve kotası bulunabilir. Buluta davetin kendisi yerine özeti ve izin bilgileri yapılandırılır; istek sırasında kullanılan kod doğrulama için işlenir.
- **Günlükler:** İncelenen Cloudflare yapılandırmasında uygulama gözlemlenebilirlik günlükleri kapalıdır. Yerel LCU istek günlüğü uç nokta, zaman, sonuç ve süre bilgisi içindir; kimlik doğrulama başlıkları veya yanıt gövdeleri için değildir. Bu açıklama, hizmet sağlayıcıların tüm ağ/operasyon kayıtlarının sıfır olduğu iddiasını içermez.

## Hizmet sağlayıcılar ve yurt dışı işleme
Riot Games hesap/maç verisi sağlar. Cloudflare Workers, Durable Objects ve Workers AI bulut bağlantısı, kota, önbellek ve AI değerlendirmesinde kullanılır. GitHub kurulum ve güncelleme dosyalarını sağlar. Bağlantı kurulurken bu hizmetler IP adresi, zaman ve istek boyutu gibi olağan ağ/operasyon bilgilerini kendi koşullarına göre işleyebilir.

Cloudflare'in Workers AI için açıkladığı içerik kullanım ilkeleri, Keel'in ayrıca seçtiği Durable Objects önbelleğinin silindiği anlamına gelmez. Sağlayıcının çıkarım hizmeti ile Keel'in kalıcı sonuç önbelleği ayrı değerlendirilmelidir. [Cloudflare Workers AI veri kullanımı](https://developers.cloudflare.com/workers-ai/platform/data-usage/), [Cloudflare gizlilik politikası](https://www.cloudflare.com/privacypolicy/), [Riot gizlilik bildirimi](https://www.riotgames.com/en/privacy-notice) ve [GitHub gizlilik açıklaması](https://docs.github.com/en/site-policy/privacy-policies/github-general-privacy-statement) ilgili sağlayıcıların uygulamalarını açıklar.

Verilerin yalnızca Türkiye içinde işlendiği/saklandığı garantisi verilmez. Bu teknik sayfa, yurt dışı aktarım için gerekli hukuki mekanizmaların tamamlandığına ilişkin bir beyan değildir.

## Tercihler ve başvurular
Bulut bağlantısı isteğe bağlıdır. Hesabım bölümünden bağlantıyı kaldırabilirsin; bu işlem mevcut kişisel kayıtları silmez ve buluttaki kalıcı AI önbelleğini otomatik temizlemez. Kullanım tercihin, her veri işleme faaliyeti için kendiliğinden geçerli bir hukuki dayanak veya toplu açık rıza olarak sunulmaz.

İncelenen sürümde bulut AI sonuçlarını kullanıcıya özel olarak listeleyen/silen bir arayüz yoktur. Veri başvurusu için işletmeciden özel iletişim kanalı istenmelidir. [Herkese açık sorun alanında](https://github.com/kjtasan/keel-lol/issues) yalnızca özel iletişim talebini ilet; kişisel verilerini, API anahtarını veya davet kodunu yayımlama.

[KVKK'nın aydınlatma yükümlülüğü açıklaması](https://www.kvkk.gov.tr/Icerik/2033/Aydinlatma-Yukumlulugu-) doğrultusunda gerekli kimlik, iletişim, amaç, hukuki sebep, alıcı grupları ve haklar bilgisi ilgili kullanıcılara veri elde edilirken ayrıca sunulmalıdır.
