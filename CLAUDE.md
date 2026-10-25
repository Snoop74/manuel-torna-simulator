# Manuel Torna Simülatörü — proje notu

İlk sürüm 2026-10-05'te yapıldı: `torna.html` (tek dosya, Türkçe arayüz). Kardeş proje: manuel freze simülatörü.

## Kardeş proje: freze

- Kaynak: `../freze/freze.html` (yan klasör)
- GitHub: https://github.com/Snoop74/manuel-freze-simulator — canlı: https://snoop74.github.io/manuel-freze-simulator/
- CSS (tasarım dili) freze'den birebir alındı; ikisini tutarlı tut.

## Mimari (torna.html)

- three.js r128 (cdnjs) + OrbitControls (jsDelivr), derleme adımı yok.
- **Parça modeli:** eksen boyunca 0.1 mm aralıklı istasyonlar (`a` = ayna alnından uzaklık, -40…200). `R[i]` dış yarıçap, `Ri[i]` delik yarıçapı; malzeme `R > Ri`. Aynadan itibaren ilk boş istasyondan sonrası koparsa parça düşer (`checkDetach` / `dropPiece`).
- **Kalem profili:** `toolF(T, du)` kalem ucunun alt zarfı. 95° sağ kalemde referans burnun en sol/en alt teğetleri (du ≥ 0), ana ağız gelinciğe doğru yatık. Kanal/kesme kaleminde referans sol köşe.
- **Diş:** somun kolu takılıyken `threadScan`, istasyon başına helis faz kutularında (`Gr`, 0.05 mm) diş dibini tutar; mesh köşe başına `min(R, Gr(u))` ile helis çizer. Somun kolu yeniden kapanınca mil açısı `uref`'e hizalanır (diş saati).
- **Yük modeli:** freze'deki gibi ~1 mm yol penceresinde ortalanır; talaş = f/f_önerilen, yük = talaş × (kavrama genişliği / ap). Vc kalem ucunun çapında hesaplanır. Ra = f²/(8rε) (düşük Vc'de ×2.5). Diş pasosunda yük = V kesit artışı / 0.45 mm².
- **İş emirleri:** `JOBS` Z değerleri bitmiş alına göre (Z0 alın, Z− aynaya). `targets(J)` hedef profili üretir; muayene, puan (70/15/15), yıldız ve teknik resim freze ile aynı mantıkta.

- **Parça verisi:** `extractPiece(i0,i1)` profil, iz ve helis kutularını kopyalar; `mountPiece(d, flip, stick)` geri yazar (ters çevirmede helis fazı u' = −u + c ile yeniden eşlenir). `startIdx/endIdx` malzemenin sınırları; parça a=0'dan başlamak zorunda değil. Çeneler `buildJaws(r)` ile tutulan çapa kapanır.
- **Parça masası:** ayrı WebGLRenderer (`bench`), yarım kesit için clipping plane + ShapeGeometry kesit kapağı, kumpas/mikrometre raycast ile istasyon okur.
- **Üst kızak:** U ekseni hareketi `um·cos(α)` Z'ye, `−um·sin(α)` X'e dağıtılır.

- **Malzemeler:** `MATS` (kc, vcf, ff, rho, c, alpha, E, talaş tipi, renkler). `vcOf(T)` önerilen hızı malzemeye göre ölçekler; yük `kcR = (kc/700)^0.25` ile hafifçe artar (zorluk asıl olarak ff, vcf, aşınma ve güçte). `setMaterial(k)` parçayı yeniden renklendirir.
- **Gerçekçilik:** uç aşınması `S.wear[]` (Taylor, vr^2.5) → Ra, çap ofseti `wearOff`, yük; ısı `S.temp` + `thermF` (taramalarda kalem konumu thermF'e bölünür, R soğuk geometridir); talaş sarılması `S.wrap` (+ `buildWrap` kuş yuvası); tırlama `chatterLimit()` lobları; mil gücü `P_MAX`, `S.rpmEff`, boğulma.
- **Görsel:** RoomEnvironment + ACES; `addMarks(material)` shader'ı `mark` özniteliğinden (ilerleme, Ra, tırlama) helis izi ve dalga çizer; `surfColor()` malzeme ve ısı rengi.

- **Kılavuz/pafta:** `METRIC`, `applyTailSize()` (G5 matkap Ø, G6 kılavuz, G7 pafta). `tryTapDie()` temas kontrolleri ve `S.tap` (kovanı mil sürer: −dir·p·rpm), `tapCut()` dişi helis faz uzayında açar: pafta `Gr`/`S.zone`, kılavuz `GrI`/`S.zoneI` (iç diş, `threadRI`). Mil yönü `S.dir` (geri yönde kalemler kesmez, otomatik ilerleme ters döner).
- **Tezgâh görünümü:** `rbox()` yuvarlatılmış kutu (ExtrudeGeometry), `lever()`, `dialTexture()`; `addMottle()` döküm boya ve beton için dünya koordinatında gürültü (UV gerekmez). Atölye (zemin çizgileri, duvarlar, dolap, tezgâh, varil) ve tezgâh ayrıntıları yalnızca görsel; çarpışma ölçüleri `carriageHit`/`tailHit` sabitlerinde, onlara dokunmadan değiştirilebilir. Mil lambası, start düğmesi, acil stop mantarı ve önlük kolları durumla oynar.
- **Arayüz:** bölümler `data-panel` id'li; `PM` (panel yöneticisi) başlangıçta onları `.panel` pencerelerine sarar (`#panelLayer`). `.pendant` gizli kalır, yalnızca kaynak. Konum/boyut `localStorage['torna-panels-v1']`'de. İçerik ölçeği container query (`cqw`) ile. `PM.lamp()` `updateHud`'dan, `drawGauge()` her karede. Alarm/rapor/toast `body`'ye taşınır ki panellerin üstünde kalsın. 900 px altında paneller sahnenin altında alt alta dizilir.
- **Talaş biçimi:** `chipForm(T, f, ap, vr, thread)` → snarl/spring/short/tight/clock/flake/dust/ribbon/gum/thread/torn. Kural: f/breakF ve ap/(2·rε) eşiği (soğutma breakF'i %10 düşürür, paslanmazda breakF yüksek). `S.apNow` kaldırılan hacimden tahmin edilir. Biçimler `CK` indeksli InstancedMesh boruları (`chipGeos`); uzun biçimler `S.wrap`'ı besler.
- **Esneme:** değişken kesitli kiriş integrali δ = F/E·∫(L−s)²/I(s) ds + en narin bölümün L/d oranı.

## Test etme

Preview'de `file://` sayfaları çalışmıyor; `python -m http.server` ile servis edip açın. Test yardımcıları `.claude/testlib.js` içinde (git dışı). Fizik testleri için geçici olarak `window.__T = { S, motion, ... }` açığa çıkarıp `motion(1/60)`'ı döngüde çağırmak en güvenilir yol (preview sekmesi kare hızını düşürüyor). Yayınlamadan önce kancayı silin.

## Sıradaki fikirler

- Komparatörle salgı ölçme (ters bağlamada eksen kaçıklığı)
- Tırtıl çekme, iç diş, yumuşak çene (işlenmiş yüzeyde iz bırakmadan bağlama)
- Gerçek atölye sesleri; takım ofseti ve güvenlik alışkanlıkları (ayna anahtarı, koruma kapağı)
- Aynı gerçekçilik paketini freze simülatörüne taşımak
