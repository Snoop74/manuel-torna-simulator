# Manuel Torna Simülatörü

Tarayıcıda çalışan, 3B bir manuel torna tezgâhı simülasyonu ve oyunu. Tek bir HTML dosyası; kurulum gerektirmez. Kardeş proje: [Manuel Freze Simülatörü](https://github.com/Snoop74/manuel-freze-simulator).

## Çalıştırma

`torna.html` dosyasını bir tarayıcıda açın (internet bağlantısı gerekir: three.js ve yazı tipleri CDN'den yüklenir).

## Özellikler

- **Tornalama:** Ø50 alüminyum çubuk, üç ayaklı aynada. Dış çap, alın, kademe, pah, kanal, kesme (parça kopup kızağa düşer), gelincikten punta ve delme, delik kalemiyle bara.
- **Diş çekme:** somun kolu ve diş adımı seçimi (1.0–2.5 mm); diş gerçek helis olarak oluşur, pasolar diş saatiyle hizalanır.
- **Kontrol:** taşıyıcı (Z), enine kızak (X, çap okur) ve gelincik kovanı (W) için el çarkları, klavye, otomatik boyuna/enine ilerleme (mm/dev), Z durdurucu, dijital okuma (DRO).
- **Kesme fiziği:** talaş kalınlığı, kalem yükü, birikerek dolan zorlanma göstergesi; çapa göre değişen kesme hızı (Vc); ilerlemeye bağlı yüzey pürüzlülüğü (Ra); ayna, çene, gelincik ve tutucu çarpışmaları; matkapta gagalama ve punta kontrolü.
- **Soğutma ve partiküller:** eklemli hortum, dönen parçadan savrulan sıvı, buğu, spiral talaşlar, kırılma kıvılcımları, ısınma dumanı.
- **İş emirleri:** teknik resim ve tablo, parça üstünde hedef profil çizgisi, teslimde muayene (çap, boy, omuz, pah, kanal, delik, diş, Ra) ve 1–3 yıldızla puanlama. Beş görevlik kampanya: alın ve çap, kademeli mil, kanal ve pah, delik ve bara, M20 cıvata.

## Kısayollar

| Tuş | İşlev |
|---|---|
| ← → | Z ekseni (taşıyıcı) |
| ↑ ↓ | X ekseni (enine kızak) |
| PgUp / PgDn | W gelincik kovanı |
| Shift | Hızlı hareket |
| Boşluk | Mil start / stop |
| 1–4 | Kol adımı 0.01 / 0.1 / 1 / 10 mm |
| F | Otomatik boyuna ilerleme |
| T | Somun kolu (diş çekme) |
| C | Soğutma sıvısı |
| Esc | Tüm hareketleri durdur |
