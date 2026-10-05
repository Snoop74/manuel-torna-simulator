# Manuel Torna Simülatörü — proje notu

İlk sürüm 2026-10-05'te yapıldı: `torna.html` (tek dosya, Türkçe arayüz). Kardeş proje: manuel freze simülatörü.

## Kardeş proje: freze

- Kaynak: `C:\Users\Onat\Desktop\freze\freze.html`
- GitHub: https://github.com/Snoop74/manuel-freze-simulator — canlı: https://snoop74.github.io/manuel-freze-simulator/
- CSS (tasarım dili) freze'den birebir alındı; ikisini tutarlı tut.

## Mimari (torna.html)

- three.js r128 (cdnjs) + OrbitControls (jsDelivr), derleme adımı yok.
- **Parça modeli:** eksen boyunca 0.1 mm aralıklı istasyonlar (`a` = ayna alnından uzaklık, -40…100). `R[i]` dış yarıçap, `Ri[i]` delik yarıçapı; malzeme `R > Ri`. Aynadan itibaren ilk boş istasyondan sonrası koparsa parça düşer (`checkDetach` / `dropPiece`).
- **Kalem profili:** `toolF(T, du)` kalem ucunun alt zarfı. 95° sağ kalemde referans burnun en sol/en alt teğetleri (du ≥ 0), ana ağız gelinciğe doğru yatık. Kanal/kesme kaleminde referans sol köşe.
- **Diş:** somun kolu takılıyken `threadScan`, istasyon başına helis faz kutularında (`Gr`, 0.05 mm) diş dibini tutar; mesh köşe başına `min(R, Gr(u))` ile helis çizer. Somun kolu yeniden kapanınca mil açısı `uref`'e hizalanır (diş saati).
- **Yük modeli:** freze'deki gibi ~1 mm yol penceresinde ortalanır; talaş = f/f_önerilen, yük = talaş × (kavrama genişliği / ap). Vc kalem ucunun çapında hesaplanır. Ra = f²/(8rε) (düşük Vc'de ×2.5). Diş pasosunda yük = V kesit artışı / 0.45 mm².
- **İş emirleri:** `JOBS` Z değerleri bitmiş alına göre (Z0 alın, Z− aynaya). `targets(J)` hedef profili üretir; muayene, puan (70/15/15), yıldız ve teknik resim freze ile aynı mantıkta.

- **Parça verisi:** `extractPiece(i0,i1)` profil, iz ve helis kutularını kopyalar; `mountPiece(d, flip, stick)` geri yazar (ters çevirmede helis fazı u' = −u + c ile yeniden eşlenir). `startIdx/endIdx` malzemenin sınırları; parça a=0'dan başlamak zorunda değil. Çeneler `buildJaws(r)` ile tutulan çapa kapanır.
- **Parça masası:** ayrı WebGLRenderer (`bench`), yarım kesit için clipping plane + ShapeGeometry kesit kapağı, kumpas/mikrometre raycast ile istasyon okur.
- **Üst kızak:** U ekseni hareketi `um·cos(α)` Z'ye, `−um·sin(α)` X'e dağıtılır.
- **Esneme:** `deflection()` ankastre kiriş δ = F·x³/(3EI) + narinlik terimi; döner punta (G4, punta deliği gerekir) oturunca çok azalır. Kesimde profil δ kadar az kesilir, Ra büyür, δ > 0.35 kırar.

## Test etme

Preview'de `file://` sayfaları çalışmıyor; `python -m http.server` ile servis edip açın. Fizik testleri için geçici olarak `window.__T = { S, motion, ... }` açığa çıkarıp `motion(1/60)`'ı döngüde çağırmak en güvenilir yol (preview sekmesi kare hızını düşürüyor). Yayınlamadan önce kancayı silin.

## Sıradaki fikirler

- Kumpas / mikrometre ile ölçme, komparatör
- Tırtıl çekme, iç diş, yumuşak çene (işlenmiş yüzeyde iz bırakmadan bağlama)
- Takım aşınması ve el çarkı boşluğu (usta modu)
