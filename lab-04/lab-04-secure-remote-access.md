# LAB 4 · Secure Remote Access
**Çıktı:** Secure Architecture
**Föy sürümü:** Genel Sürüm · Şişeleme Hattı
**Hedef makine:** STK Makina – Otomatik Şişe Dolum Makinesi

| Ad Soyad | Öğrenci No | Grup | Tarih |
|---|---|---|---|
| Sena Nur Ceylan | 235541050 |  | 2026-10-22 |

> **Kavram:** İki katman, ikisi de şart: **erişim güvenliği** (girişi zorlaştır: ara nokta, VPN, MFA, kişisel hesap, kayıt, varsayılan kapalı) + **emniyet bağımsızlığı** (saldırgan girse bile insan korunur).
> **Not:** Bu föy çözüm tasarlatmaz; **gereksinimi** tanımlatır. Tasarım kararı firmanındır. Aşağıdaki "mevcut" tablosu, makinemiz için **varsayımsal/bilinmeyen** durumu temsil eder; gerçek yapılandırma [B].

---

## Görev A — mevcut → hedef

> **İpucu (föy):** uzak bakım modülü bugün internete DOĞRUDAN açık olabilir (örnek senaryo). Bizim makinede uzak erişimin varlığı/biçimi **[B]**; en kötü-durum varsayımıyla "mevcut" sütunu doldurulmuştur.

| MEVCUT (varsayımsal en kötü durum [B/V]) | HEDEF (beş ilkeyle yeniden tasarım) |
|---|---|
| Uzak erişim doğrudan internete açık olabilir | **Ara nokta (jump server):** kontrol ağına doğrudan erişim yok, tek denetlenen giriş |
| Şifreli tünel olmadan bağlantı | **VPN:** tüm uzak trafik şifreli ve kimliği doğrulanmış kanaldan |
| Tek parola / olası varsayılan kimlik | **MFA:** ikinci faktör zorunlu; varsayılan parolalar değiştirilmiş |
| Paylaşılan servis hesabı | **Kişisel hesap:** her erişim bireysel ve izlenebilir |
| Oturum kaydı yok | **Tam oturum kaydı:** olay incelemesi ve CRA kanıtı için |
| Erişim sürekli açık | **Varsayılan kapalı:** erişim yalnızca gerektiğinde, süreli ve onaylı açılır |
| Emniyet ile kontrol aynı ağda olabilir | **Emniyet bölgesi ayrı:** uzak yol emniyet fonksiyonuna erişemez |

---

## Görev B — functional safety köprüsü

**1) Saldırgan tüm önlemlere rağmen içeri girerse: emniyet fonksiyonu etkilenir mi? Neden?**
**Etkilenmemelidir** — eğer emniyet fonksiyonu kontrol sisteminden ve uzak erişim yolundan **bağımsız** tasarlandıysa. Sebebi: E-stop → Safety PLC → STO zinciri ayrı bir emniyet bölgesinde (Z-Safety) çalışır ve uzak yoldan parametrelenemez/yazılamaz. Böylece saldırgan normal PLC'yi veya HMI'ı ele geçirse bile, koruyucu kapak açıldığında veya E-stop'a basıldığında tehlikeli hareket yine durur. **Ancak** emniyet ile kontrol aynı kumandada/ağda ise (ki bizim makinede bu durum [B]), o zaman emniyet de etkilenebilir — bu kabul edilemez bir tasarımdır. Bu, Lab 1'deki "dijital kesişim noktası" riskidir.

**2) Emniyet fonksiyonunun kontrol sisteminden bağımsız çalışması için GEREKSİNİMİ yazın (çözümü değil).**
**Gereksinim:** "Makinenin emniyet fonksiyonu (acil durdurma ve koruyucu kapak kilidi), normal kontrol sisteminden (PLC/HMI) ve her türlü uzak erişim yolundan **mantıksal ve fiziksel olarak bağımsız** olmalı; emniyet parametreleri uzaktan veya normal kontrol ağı üzerinden değiştirilememeli; uzak erişim veya normal kontrol tamamen devre dışı kalsa dahi emniyet fonksiyonu güvenli durumu (STO/safe state) sağlayabilmelidir."

İlgili doğrulama gereksinimi: Bu bağımsızlık, ISO 13849 / IEC 62061 kapsamında uygun PLr/SIL ile ve IEC TS 63074'ün emniyet-güvenlik etkileşimi değerlendirmesiyle gösterilmelidir [16].

---
**Evidence Pack hedefi:** Secure Architecture → EP 02 + EP 06.
**Bağlantı:** rapor/03 (C4 uzak erişim kanalı, Z-Safety); Lab 2 Görev B kararları; Lab 1 safety fonksiyonu. Standartlar: IEC 62443-3-2 [12], IEC TS 63074 [16].
