Keel artık daha hızlı açılıyor; küçük pencerelerde bölüm kartları okunaklı kalıyor.

## Bu sürümde
- Küçük pencerelerde kart metinlerinin dar bir sütuna sıkışması düzeltildi. Kartlar alana göre yan yana veya alt alta yerleşiyor.
- Açılışta küçültme düğmesinin seçili görünmesi giderildi.
- Logo daha erken görünüyor ve yerine kaydıktan sonra arayüz açılıyor. Oyun zaten açıkken de açılış animasyonu korunuyor.
- İlk ekranın hazırlanmasındaki gereksiz beklemeler azaltıldı.

## Öneri kalitesi
Bu sürüm açılış ve arayüz iyileştirmelerine odaklanıyor. Şampiyon önerilerini sıralama yöntemi, rün/eşya seçimi ve ortak oyun verileri değişmedi; öneri kalitesinde bir artış iddia edilmiyor.

## Bilinen sorunlar
- Windows yayıncı sertifikası henüz yok. SmartScreen, uygulamayı tanımadığına dair uyarı gösterebilir; aşağıdaki indirme doğrulamasını kullan.
- Bazı şampiyon/rol/eşleşmelerinde yeterli örnek bulunmayabilir. Keel bu durumlarda veri sınırını gösterir; her seçim için rakibe özel bir öneri garanti edilmez.
- Keel kapalıyken oynanan maçlarda dakika bazlı yerel kayıt bulunmaz. Bu maçlar için Riot maç sonu verileri gösterilir.

## Kurulum ve dosya doğrulama
Kurucuyu yalnızca bu deponun Releases bölümünden indir. Dosyanın SHA-256 değeri aşağıdakiyle eşleşiyorsa ve bu kaynağa güveniyorsan, tanınmayan uygulama SmartScreen ekranında **Ek bilgi → Yine de çalıştır** seçeneğini kullanabilirsin. Bu adım yalnızca tanınmayan uygulama uyarısı içindir; bir tehdit tespiti veya yönetici engeli için güvenlik korumalarını kapatma.

**Dosya:** `Keel-Setup-0.1.14.exe`  
**SHA-256:**
```text
df1037954f17aa0137abcc602bea6e6e68a262a28de002897761c56efd726af0
```

PowerShell ile denetlemek için:
```powershell
Get-FileHash .\Keel-Setup-0.1.14.exe -Algorithm SHA256
```
Ayrıca sürüme eklenen `SHA256SUMS.txt` dosyasını kullanabilirsin. Özet eşleşmesi yayımlanan dosyayla aynı kopyayı indirdiğini gösterir; Windows yayıncı imzasının yerine geçmez.

**Doğrulama:** 444 test geçti. Kart yerleşimleri beş pencere genişliğinde kontrol edildi. Kurucunun HTTPS üzerinden indirilmesi, güncelleme imzası ve dosya özeti doğrulandı. Bu kontroller, oyun içi kazanma oranında artış ölçümü değildir.

Hesap ayarların ve kişisel maç kayıtların korunur. Keel güncellemeyi açılışta kontrol eder; oyun veya şampiyon seçimi sırasında kurulumu bekletir.
