# Manuel Torna Simülatörü

Tarayıcıda çalışan, 3B bir manuel torna tezgâhı simülasyonu ve oyunu. Tek bir HTML dosyası; kurulum gerektirmez. Kardeş proje: [Manuel Freze Simülatörü](https://github.com/Snoop74/manuel-freze-simulator).

## Çalıştırma

`torna.html` dosyasını bir tarayıcıda açın (internet bağlantısı gerekir: three.js ve yazı tipleri CDN'den yüklenir).

## Özellikler

- **Tornalama:** Ø50 alüminyum çubuk, üç ayaklı aynada. Dış çap, alın, kademe, pah, kanal, kesme (parça kopup kızağa düşer), gelincikten punta ve delme, delik kalemiyle bara.
- **Diş çekme:** somun kolu ve diş adımı seçimi (1.0–2.5 mm); diş gerçek helis olarak oluşur, pasolar diş saatiyle hizalanır.
- **Kılavuz ve pafta:** M6–M20 ISO metrik kaba diş. Kılavuz matkabı ölçüsü seçilebilen matkapla delinir; kılavuz ve pafta mil İLERİ dönerken kendini adım kadar çeker, GERİ yönde çıkar. Küçük delik, yüksek devir, kör delik dibi, kalın çubuk ve çelikte yağsız çekme takımı kırar. İç diş parça masasında kesitte görünür.
- **Kumanda panelleri:** her bölüm (iş mili, DRO, takımlar, el çarkları, hareket, otomatik ilerleme, iş emirleri…) ayrı bir pencere. Başlığından sürüklenir, köşesinden büyütülür (içindeki göstergeler, çarklar ve düğmeler pencereyle birlikte büyür), küçültülür ya da kapatılır; düzen tarayıcıda hatırlanır. Üst çubukta panel düğmeleri, hazır düzenler (Temel, Tam, Diş çekme), kamera ve ACİL STOP. Mil panelinde devir ve motor yükü göstergesi; takım kırılınca takımlar paneli yanıp söner ve alarmdan tek tuşla yeni uç takılır.
- **Makine üstünde kumanda:** 3B tezgâhtaki çarklar fareyle sürüklenerek ya da tekerlekle çevrilir; önlükteki mil, somun ve ilerleme kollarına, fener mili kutusundaki devir ve yön kollarına, ilerleme kutusu kollarına, START düğmesine, acil stop mantarına ve soğutma vanasına tıklanır. Üstüne gelince ne işe yaradığı yazar.
- **Kontrol:** taşıyıcı (Z), enine kızak (X, çap okur) ve gelincik kovanı (W) için el çarkları, klavye, otomatik boyuna/enine ilerleme (mm/dev), Z durdurucu, dijital okuma (DRO).
- **Kesme fiziği:** talaş kalınlığı, kalem yükü, birikerek dolan zorlanma göstergesi; çapa göre değişen kesme hızı (Vc); ilerlemeye bağlı yüzey pürüzlülüğü (Ra); ayna, çene, gelincik ve tutucu çarpışmaları; matkapta gagalama ve punta kontrolü.
- **Malzemeler:** Al 6061, S235 (St37) yapı çeliği, C45 çelik, 304 paslanmaz, pirinç, GG25 döküm, Delrin ve PA6 naylon. Her birinin kesme kuvveti, önerilen hızı ve ilerlemesi, talaş tipi (kıvrık, uzun tel, kırık pul, toz, şerit) ve rengi farklı. Paslanmaz sürtülünce işlem sertleşir, Delrin yüksek hızda erir, döküm kuru işlenir.
- **Gerçekçi kesme davranışı:** Taylor modeline göre uç aşınması (yüzey bozulur, çap büyür; uç çevrilir), parçanın ısınması ve soğuyunca küçülmesi, kırılmayan talaşın parçaya sarılması, devire bağlı tırlama kararlılık lobları ve 4 kW mil gücü sınırı (ağır pasoda devir düşer, mil boğulur).
- **Görsel:** metallerde ortam yansıması, ilerlemeye göre görünen helis tornalama izleri, tırlama dalgaları, çelikte ısı rengi (saman → mavi), atölye lambası ve devir tablosu.
- **Ses:** kayıt dosyası yok, tamamı fizikten üretiliyor. Devirle değişen motor uğultusu ve dişli vınlaması; malzemeye göre değişen kesme hışırtısı (alüminyum yumuşak, paslanmaz tiz, döküm çıtırtılı); tırlamada ötme; mil durunca yavaşça sönen ses; kırılmada metal çınlaması; kavrama, somun kolu ve çark çentiği tıkırtıları; küçük atölye yankısı.
- **Talaş biçimi:** ilerleme ve pasoya göre değişir. İnce bitiş pasosunda ya da düşük ilerlemede uzun tel yumağı (parçaya sarılır), sınırda uzun spiral, uygun pencerede kısa kırık "6-9" ve C talaşı, çok ağır pasoda sıkı ve sıcak kıvrık; kanal kaleminde saat yayı, dökümde toz, pirinçte iğne, plastikte şerit. Durum panelinde canlı gösterilir; uzun talaşta nasıl kırılacağı yazılır.
- **Zımpara ve cila:** Takımlar panelinden ya da P tuşuyla zımpara alınır (120, 240, 400 kum, keçe + pasta). Mil dönerken işlenmiş yüzeyin üstünde fareyi basılı tutup sürtünce yüzey parlar, işleme izleri kaybolur. Her kumun inebileceği bir Ra sınırı var ve kaba kum ince yüzeyi yeniden çizer. Tek yerde fazla durmak çapı küçültür.
- **Soğutma ve partiküller:** eklemli hortum, dönen parçadan savrulan sıvı, buğu, spiral talaşlar, kırılma kıvılcımları, ısınma dumanı.
- **Parça masası:** kesilen ya da aynadan sökülen parçalar ayrı bir masada döndürülerek incelenir; yarım kesit, dış/iç çap için kumpas (0.02 mm), boy ölçümü ve mikrometre (0.01 mm). Parça buradan aynaya düz ya da ters bağlanır.
- **Ters bağlama:** parçanın profili, deliği ve diş helisi çevrilerek seçilen çıkıntıyla aynaya bağlanır; çeneler çapa göre kapanır.
- **Konik tornalama:** açısı ayarlanan üst kızak (U ekseni) ve kendi el çarkı; D-d-L'den açı hesabı.
- **Uzun parça:** Ø30 × 180 çubuk ve döner punta. Kesme kuvveti narin parçayı esnetir; puntasız tornalanan uzun parça konik çıkar ve tırlama yapar.
- **İş emirleri:** teknik resim ve tablo, parça üstünde hedef profil çizgisi, teslimde muayene (çap, boy, omuz, pah, kanal, delik, diş, koni, Ra) ve 1–3 yıldızla puanlama. On bir görev: alın ve çap, kademeli mil, kanal ve pah, delik ve bara, M20 cıvata, konik pim, pul (kesilen parça muayene edilir), burç (ters bağlama), uzun mil (punta desteği), M12 kılavuz, M10 pafta.

## Kısayollar

| Tuş | İşlev |
|---|---|
| ← → | Z ekseni (taşıyıcı) |
| ↑ ↓ | X ekseni (enine kızak) |
| PgUp / PgDn | W gelincik kovanı |
| Home / End | U üst kızak |
| Shift | Hızlı hareket |
| Boşluk | Mil start / stop |
| 1–4 | Kol adımı 0.01 / 0.1 / 1 / 10 mm |
| F | Otomatik boyuna ilerleme |
| T | Somun kolu (diş çekme) |
| C | Soğutma sıvısı |
| P | Zımparayı al / bırak |
| Esc | Acil stop: mil ve tüm hareketler |
