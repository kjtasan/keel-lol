# Keel — Teknik Gizlilik Açıklaması
Son inceleme: 29 Ekim 2026 · Kapsam: Keel 0.1.15 ve incelenen bulut hizmeti kaynak kodu

Bu sayfa, uygulamanın hangi veriyi nerede kullandığını açıklar. **Tamamlanmış bir KVKK aydınlatma metni veya açık rıza formu değildir.** Hukuki veri sorumlusu kimliği, işleme hukuki sebepleri ve uygulanacak yurt dışı aktarım koşulları ayrıca belirlenmelidir. Bu başlıkların kamuya açık GitHub sayfasında bulunmaması, verisi işlenen kullanıcıya gerekli bilgilendirmenin yapılması gereğini kaldırmaz.

## Kısaca: veriler geliştiriciye mi gönderiliyor?
Keel, bilgisayarındaki kişisel maç arşivini geliştiriciye e-posta, Discord mesajı veya otomatik bir kullanıcı raporu olarak göndermez. Yerel maç kayıtları ve ayrıntılı analiz bilgisayarında tutulur. Destek için kendin gönderdiğin mesaj, ekran görüntüsü veya dosyalar ise seçtiğin iletişim kanalından geliştiriciye ulaşır.

**Bu, uygulamanın hiç veri işlemediği veya bulutta hiç kayıt bulunmadığı anlamına gelmez.** Davetli bulut bağlantısını kullandığında hesap/maç sorguları Keel'in Cloudflare üzerinde işlettiği hizmetten geçer; isteğe bağlı AI yorumu için seçilmiş oyun istatistikleri hizmete iletilir. Kota/davet kayıtları ve AI sonuç önbelleği aşağıda açıklanan biçimde saklanır. Bu hizmetin yönetimi geliştiricidedir; hizmetteki kayıtların geliştiricinin erişemeyeceği kayıtlar olduğu iddia edilmez. Otomatik bir raporun geliştiricinin bilgisayarına gelmemesi ile bulutta veri işlenmesi farklı durumlardır.

## Hangi veri nereye gider?
| İşlem | Bilgisayarında kalanlar | Hizmete iletilen / hizmette işlenenler |
|---|---|---|
| Hesap ve ayarlar | Riot ID, sunucu, hesap/maç kimlikleri, kişisel havuz ve tercihler yerel kayıtlarda tutulur. Kendi Riot API anahtarın ve bulut davet kodun da yerel ayar dosyalarında saklanır. | Kendi Riot anahtarını kullanırken hesap/maç sorguları Riot'a gider. Davetli bulut bağlantısında sorgular Cloudflare Workers üzerinden Riot'a iletilir. |
| Maç geçmişi | İndirilen Riot maç yanıtları, maç kimlikleri, geçmiş listesi ve eşleşen yerel kayıtlar bilgisayarında saklanır. | Bulut kullanılırsa Riot ID, PUUID, maç kimliği, bölge ve gereken sorgu parametreleri hizmet tarafından işlenir. Riot yanıtları maçtaki diğer katılımcıların kimlik ve istatistiklerini de içerebilir. |
| Yerel canlı kayıt ve ayrıntılı analiz | Keel açıkken gözlenen skor, minyon, görüş, eşya ve zaman kayıtları ile yerel analiz bilgisayarında tutulur. | Yerel ayrıntılı raporu açmak, bu kayıtları AI modeline gönderen bir işlem değildir. |
| İsteğe bağlı AI yorumu | Dönen değerlendirme, ilgili yerel maç kaydıyla önbelleğe alınır. Eski AI yanıtlarının puan alanları da saklanabilir; bunlar güncel karttaki yerel maç puanı değildir. | Şampiyon, rol, mod, süre, sonuç, skor, hasar, altın, minyon, görüş, totem ve skora katkı gibi izinli istatistikler Cloudflare'deki değerlendirme hizmetine gönderilir. Model Cloudflare Workers AI üzerinden çalışır. |
| Güncellemeler ve ortak oyun verileri | İndirilen güncelleme ve ortak veriler yerelde saklanır. | GitHub ve oyun verisi sağlayıcılarına indirme istekleri yapılır. Bu indirme isteklerinin gövdesine kişisel maç arşivi veya Riot anahtarı eklenmez. |

Riot hesabının parolası istenmez. Ortak bulut Riot anahtarı Cloudflare secret olarak hizmette tutulur; masaüstü kurulumuna ve bu depoya eklenmez. Davet kodu, bulut isteklerinde HTTPS üzerinden yetkilendirme için kullanılır.

## AI modeline ne gönderilmez?
Değerlendirme girişinde oyuncu adı/Riot ID, PUUID, maç kimliği, Riot API anahtarı ve davet kodu modelin istemine eklenmez. Bulut hizmeti daveti doğrular; model yalnızca izinli oyun istatistikleriyle değerlendirme yapar. Bunları **doğrudan hesap kimliği çıkarılmış istatistikler** olarak tanımlıyoruz; hiçbir koşulda yeniden ilişkilendirilemeyecekleri iddia edilmiyor.

Destek değerlendirmesinde minyon ve altın; ARAM değerlendirmesinde görüş/totem ölçütleri modele verilen özelliklerden çıkarılır. Karttaki maç puanı ve ayrıntılı rapor bilgisayarında hazırlanır; bunları açmak model çağrısı yapmaz. İsteğe bağlı bulut AI yorumu ayrı bir özelliktir.

## Saklama süreleri ve önbellek
- **Bilgisayarındaki veriler:** Maç geçmişi, kişisel kayıtlar, yerel AI sonuçları ve ayarlar kullanıcı tarafından yönetilir. Genel bir otomatik silme süresi yoktur; uygulamayı kaldırmak kişisel veri klasörünü otomatik temizlemez.
- **Riot sorgu hizmeti:** İncelenen kod ham maç yanıtını, hesap adını veya PUUID'yi kendi kalıcı veritabanına yazmaz. Yanıtlar bellekte önbelleğe alınabilir; tekrar kullanım süresi 60 saniye, sınırı 16 kayıt ve kayıt başına 1 MB'dir. Süre dolması, kaydın tam o saniyede fiziksel bellekten silinmesi garantisi değildir; kapasite değişimi veya süreç yeniden başlatılması da temizlemeyi etkiler.
- **Bulut kota/davet kayıtları:** Davet özetleri, geçerlilik/kota bilgileri ve kullanım sayaçları hizmette tutulur. Günlük sayaçlar yeni günün isteğinde yenilenir; bunun tüm kayıtların sabit bir saatte silindiği anlamına geldiği iddia edilmez.
- **AI sonuçları:** Değerlendirme isteğinin istatistiklerinden üretilen özet anahtarı ile puan, kısa gerekçe ve model/sürüm bilgisi Cloudflare Durable Objects içinde **kalıcı önbelleğe** yazılır. İncelenen kodda bu sonuçlar için otomatik silme süresi tanımlı değildir. Ham model istemi ve ham Riot maç yanıtı bu AI sonuç kaydına yazılmaz.
- **Davet yönetimi:** İşletmecinin yerel yönetim kayıtlarında davet etiketi, kodu, son kullanma zamanı ve kotası bulunabilir. Buluta davetin kendisi yerine özeti ve izin bilgileri yapılandırılır; istek sırasında kullanılan kod doğrulama için işlenir.
- **Günlükler:** İncelenen Cloudflare yapılandırmasında uygulama gözlemlenebilirlik günlükleri kapalıdır. Yerel LCU istek günlüğü uç nokta, zaman, sonuç ve süre bilgisi içindir; kimlik doğrulama başlıkları veya yanıt gövdeleri için değildir. Bu açıklama, hizmet sağlayıcıların tüm ağ/operasyon kayıtlarının sıfır olduğu iddiasını içermez.

## Erişim ve güvenliğin sınırları
Yerel kayıtlar, kendi Riot API anahtarını eklediysen anahtarın ve bulut davet kodun yerel dosyalarda tutulur. İncelenen sürüm bu ayar dosyaları için uygulamaya özel bir şifreli kasa kullanmaz. Bilgisayarına veya kullanıcı dosyalarına erişebilen kişiler/yazılımlar bu verilere de erişebilir; hesaplara göre yerel ayırma, bilgisayar yöneticisine karşı şifreleme anlamına gelmez.

Bulut hizmetinin yönetim yetkisi geliştiricidedir; Cloudflare de hizmet sağlayıcı olarak verileri işler. Yalnızca senin erişebileceğin, geliştiricinin veya hizmet sağlayıcının erişmesinin teknik olarak imkânsız olduğu bir sistem taahhüt etmiyoruz. HTTPS, bağlantı sırasında iletimi korumak içindir; yerel dosyaları veya bulutta saklanan sonuçları yalnızca kullanıcının çözebileceği uçtan uca şifreleme iddiası değildir.

Bu sayfa, belirtilen sürümün incelenen kaynak koduna dayanır. Canlı Cloudflare hesabının bütün erişim izinleri, sağlayıcı günlükleri ve yedekleri bağımsız olarak denetlenmiş değildir. Kaynak kod incelemesi, kapsamlı bir güvenlik denetimi veya eksiksiz hukuki uygunluk belgesi olarak sunulmaz.

## Hizmet sağlayıcılar ve yurt dışı işleme
Riot Games hesap/maç verisi sağlar. Cloudflare Workers, Durable Objects ve Workers AI bulut bağlantısı, kota, önbellek ve AI değerlendirmesinde kullanılır. GitHub kurulum ve güncelleme dosyalarını sağlar. Bağlantı kurulurken bu hizmetler IP adresi, zaman ve istek boyutu gibi olağan ağ/operasyon bilgilerini kendi koşullarına göre işleyebilir.

Cloudflare'in Workers AI için açıkladığı içerik kullanım ilkeleri, Keel'in ayrıca seçtiği Durable Objects önbelleğinin silindiği anlamına gelmez. Sağlayıcının çıkarım hizmeti ile Keel'in kalıcı sonuç önbelleği ayrı değerlendirilmelidir. [Cloudflare Workers AI veri kullanımı](https://developers.cloudflare.com/workers-ai/platform/data-usage/), [Cloudflare gizlilik politikası](https://www.cloudflare.com/privacypolicy/), [Riot gizlilik bildirimi](https://www.riotgames.com/en/privacy-notice) ve [GitHub gizlilik açıklaması](https://docs.github.com/en/site-policy/privacy-policies/github-general-privacy-statement) ilgili sağlayıcıların uygulamalarını açıklar.

Verilerin yalnızca Türkiye içinde işlendiği/saklandığı garantisi verilmez. Bu teknik sayfa, yurt dışı aktarım için gerekli hukuki mekanizmaların tamamlandığına ilişkin bir beyan değildir.

## Tercihler ve başvurular
Bulut bağlantısı isteğe bağlıdır. Hesabım bölümünden bağlantıyı kapatabilirsin; bu işlem mevcut kişisel kayıtları silmez ve buluttaki kalıcı AI önbelleğini otomatik temizlemez. Kullanım tercihin, her veri işleme faaliyeti için kendiliğinden geçerli bir hukuki dayanak veya toplu açık rıza olarak sunulmaz.

İncelenen sürümde bulut AI sonuçlarını kullanıcıya özel olarak listeleyen/silen bir arayüz yoktur. Gizlilik sorularını, verilerine ilişkin erişim/silme taleplerini ve destek başvurularını aşağıdaki kanallardan iletebilirsin:
- **E-posta:** [lysander.yedek@gmail.com](mailto:lysander.yedek@gmail.com)
- **Discord kullanıcı adı:** `kjtasan` (özel mesaj)

Bu kanallardan gönderdiğin mesajlar, ekler ve iletişim bilgilerin başvurunu yanıtlamak için geliştirici tarafından görülür ve kullanılan e-posta/Discord hizmetinde işlenir. İletişim hizmetlerinin kendi gizlilik ve saklama uygulamaları da geçerlidir. Başlangıçta yalnızca talebini ve yanıt verebilmek için gerekli bilgileri paylaş; Riot parolanı, API anahtarını veya davet kodunu gönderme. Bir kaydı bulmak veya talebin sana ait olduğunu doğrulamak için gereken ek bilgiler, ihtiyaç halinde özel kanaldan açıklanır. Kimlik içermeyen özet anahtarlarla tutulan AI önbelleğinde her sonucu bir kullanıcıyla eşleştirip seçerek silmenin mevcut sürümde garanti edilmediğini belirtiriz.

[Herkese açık sorun alanını](https://github.com/kjtasan/keel-lol/issues) genel hata bildirimleri için kullanabilirsin; buraya kişisel hesap/maç bilgisi, özel yazışma, API anahtarı veya davet kodu ekleme.

[KVKK'nın aydınlatma yükümlülüğü açıklaması](https://www.kvkk.gov.tr/Icerik/2033/Aydinlatma-Yukumlulugu-) doğrultusunda gerekli kimlik, iletişim, amaç, hukuki sebep, alıcı grupları ve haklar bilgisi ilgili kullanıcılara veri elde edilirken ayrıca sunulmalıdır.


## Otomatik kapalı test bağlantısı
Bu bölüm, 0.1.15 masaüstü sürümündeki otomatik test erişimini ve bulut kayıt akışını açıklar. İlk açılışta rastgele bir kurulum kodu oluşturulur, bilgisayardaki bağlantı ayarına kaydedilir ve HTTPS üzerinden erişim isteğinde kullanılır. Bu kod Riot hesabının parolası veya ortak Riot API anahtarı değildir. Bulut kodun SHA-256 özetiyle kurulum isteğini, oluşturulma zamanını ve test erişimi durumunu saklar. Onaylanmış kayıtlarda bitiş zamanı ve kota da vardır. Yeni cihaz, test yöneticisinin onayı olmadan Riot/AI verilerine erişemez; mevcut kayıtlı davetler korunur.

Bekleyen isteklerin 7 günlük geçerlilik kontrolü vardır; temizlik gelen isteklerle yapılır ve tam 7. günde fiziksel silme garantisi değildir. Onaylı/iptal edilmiş kurulum kayıtları için genel bir otomatik silme süresi yoktur. Kayıt deposu toplam 100 kayıtla sınırlıdır. Yönetici kurulumların özet kimliklerini ve erişim durumlarını görebilir; otomatik cihazlar için en fazla 5 aktif onay ve 30 günlük izin uygulanır. İletişim için kendin bilgi paylaşmadığın sürece rastgele kurulum kodu kendi başına adın/e-posta adresin değildir; bunun tüm hizmeti anonim kıldığı iddia edilmez.

Hesabım bölümünden tek düğmeyle bulut bağlantısını kesebilirsin. Tercih sonraki açılışlarda korunur. Yerel bağlantı kodu yeniden açabilmen için dosyada tutulur; bağlantıyı kapatmak kurulum kaydını, maç geçmişini veya kalıcı AI önbelleğini silmez. Yeniden açıldığında aynı kurulum kodu kullanılır. Genel yerel özellikler bulut kapalıyken çalışmaya devam eder. Başvuru iletişimi yukarıdaki Discord ve e-posta kanallarıdır.


### Profil simgesi
Bağlı hesabın profil simgesi, mevcut League istemcisi bilgisinden veya indirilen maçtaki ilgili oyuncunun son bilinen simge kimliğinden alınır ve yerel profil kaydında hatırlanır. Görsel, genel simge kimliği ve katalog sürümü kullanılarak Riot Data Dragon üzerinden indirilip bilgisayarda önbelleğe alınır; görsel isteğine Riot ID, PUUID, davet kodu veya Riot API anahtarı eklenmez. Simge kimliği AI değerlendirmesine gönderilmez. League kapalıyken görüntülenen simge son bilinen simge olabilir.



### Birden fazla hesap ve otomatik havuz
Bu bilgisayara eklenen Riot hesaplarının kimliği, sunucusu, şampiyon havuzu ve profil simgesi ayrı yerel kayıtlarda saklanır. Eski tek hesap korunarak listeye aktarılır; farklı kurulumların verileri kendiliğinden birleştirilmez. League'de açık hesap kayıtlı ve eşleşme tekilse Keel ona geçer. Bilinmeyen hesap kullanıcı tarafından Hesap ekle ile eklenir; sunucu tahmin edilmez.

Hesap tespiti/geçişinde kayıtlı havuz hemen kullanılır. Havuz eksikse veya son hazırlama zamanı en az altı saat önceyse, bağlantı hazır olduğunda arka planda Riot maç sorguları yapılabilir. Sürekli zaman aralıklı sorgulama eklenmemiştir. Bulut kapatma tercihi korunur; kapatmak hesap veya maç kayıtlarını silmez. Devam eden havuz/geçmiş/AI işleri başladıkları hesaba bağlı kalır. İlk ekleme bildirimi kısa süre gösterilir; tekrarını önlemek için tarayıcı oturumunda yalnızca rastgele işlem kimliği tutulur.

Geliştirme kurulumundaki güncelleme öncesinde yerel veritabanı yedeklenmiştir; bu işlem her kullanıcının kurulumunda otomatik yedek bulunduğu taahhüdü değildir. Keel'in mevcut yerel yedekleri GitHub'a veya Keel bulutuna gönderilmez.
