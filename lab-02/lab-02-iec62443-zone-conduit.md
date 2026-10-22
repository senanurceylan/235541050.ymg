# LAB 2 · IEC 62443 Mini Workshop
**Çıktı:** Zone / Conduit Diagram
**Föy sürümü:** Genel Sürüm · Şişeleme Hattı
**Hedef makine:** STK Makina – Otomatik Şişe Dolum Makinesi

| Ad Soyad | Öğrenci No | Grup | Tarih |
|---|---|---|---|
| Sena Nur Ceylan | 235541050 |  | 2026-10-22 |

> **Kavram:** Zone = benzer kritiklikteki cihazları bir bölgeye topla. Conduit = bölgeler arası her geçişe kontrollü bir kapı. 62443'ün maddesini ezberlemiyoruz, mantığını uyguluyoruz.
> **Not:** Föyün verdiği varlık listesi genel bir örnektir. Aşağıda hem föyün listesini bölgelere ayırdım hem de bizim makinemizin **kendi** varlık envanterine (rapor Aşama 3, Şekil 3.1) bağladım. Bizim makinemizde ofis ağı / uzak servis erişiminin **gerçekte var olup olmadığı bilinmiyor [B]**; aşağıda "eğer varsa" mantığıyla ele alınmıştır.

---

## Görev A — varlıkları bölgelere ayırın

**Föyün varlık listesi:** PLC · HMI · Robot kontrolörü · Safety PLC · SCADA istemcisi · Mühendislik istasyonu · Uzak servis erişimi · Ofis ağı (ERP/e-posta)

**1) Hangi varlıklar aynı bölgede? Bölgeleri adlandırıp gruplandırın.**

| Bölge | İçindeki varlıklar | Ortak güvenlik gereksinimi |
|---|---|---|
| **Z-Safety (Emniyet bölgesi)** | Safety PLC, E-stop/kapak kilidi | En yüksek bütünlük; üretim ağından ayrı; değişiklik sıkı kontrollü |
| **Z1 Saha/proses** | Flowmetre, dolum valfi, şişe sensörü, konveyör motoru (robot kontrolörü bizde yok → yerine konveyör/kapak modülü) | Fiziksel koruma, sinyal bütünlüğü |
| **Z2 Kontrol** | PLC (normal kumanda) | Yetkili erişim, program değişiklik kontrolü |
| **Z3 Denetim** | HMI, SCADA istemcisi | Operatör kimlik doğrulama, rol ayrımı |
| **Z4 Tesis/kurumsal** | Ofis ağı (ERP/e-posta) | OT'den tam ayrılmış, yalnızca kontrollü veri |
| **Z5 Uzak erişim** | Uzak servis erişimi, mühendislik istasyonu (geçici bağlanır) | MFA, kişisel hesap, kayıt, varsayılan kapalı |

**Makinemize bağlama:** Bizim doğrulanmış varlıklarımız PLC [D1] → Z2, HMI [D2] → Z3, elektromanyetik flowmetre [D3] → Z1. Safety PLC, SCADA, ofis ağı ve uzak erişimin varlığı bizim makinemizde **[B]**'dir. Bkz. rapor/sekiller/sekil-3-1-bolge-kanal-modeli.svg.

**2) Safety PLC'yi hangi bölgeye koydunuz — neden?**
Ayrı bir **Z-Safety** bölgesine koydum. Gerekçe: Emniyet fonksiyonu, normal üretim veya ofis ağındaki bir arıza ya da siber müdahaleden **bağımsız** kalmalıdır (IEC TS 63074 mantığı [16]). Emniyet, en yüksek bütünlük gereksinimine sahiptir; üretim kontrolüyle aynı bölgede olursa saldırı yüzeyi paylaşılır. *(Bizim makinede ayrı emniyet kumandasının varlığı [B]; bu bir tasarım gereksinimi olarak öneriliyor.)*

**3) Bölgeler arası geçişler (conduit) nerede? Her geçişte ne kontrol edilecek?**

| Conduit | Bağladığı bölgeler | Kontrol edilecek |
|---|---|---|
| C1 | Z1 ↔ Z2 (saha ↔ PLC) | Fiziksel kablaj bütünlüğü; sinyal doğrulama |
| C2 | Z2 ↔ Z3 (PLC ↔ HMI) | Kimlik doğrulama; yalnızca gerekli komut/veri; protokol türü bizde [B] |
| C3 | Z2/Z3 ↔ Z4 (OT ↔ ofis ağı) | **Tek yönlü/kontrollü veri; segmentasyon; doğrudan erişim yok** |
| C4 | Z5 ↔ Z2/Z3 (uzak erişim ↔ kontrol) | MFA, kişisel hesap, oturum kaydı, varsayılan kapalı |
| C5 | Mühendislik ist. ↔ Z2 (programlama portu) | Yetkili cihaz; USB/dizüstü kontrolü; değişiklik kaydı |
| C-Safety | Z-Safety ↔ Z2 | Minimum; emniyet parametrelerine yazma kısıtlı |

---

## Görev B — uzak erişim kararı (6 satır)

> Not: Bu kararlar bizim makinemiz için **tasarım önerisidir**; makinenin gerçek uzak erişim yapılandırması [B]. Seçimler savunma (güvenli) tarafı esas alır.

| Karar | Seçenekler | Seçimimiz + neden |
|---|---|---|
| **Aracı?** | Doğrudan / Jump server | **Jump server (ara nokta)** — kontrol ağına doğrudan erişim verilmemeli; tek, denetlenen giriş noktası olmalı |
| **Tünel?** | Açık / VPN | **VPN** — trafik şifreli ve kimliği doğrulanmış kanaldan geçmeli; açık/şifresiz erişim kabul edilemez |
| **Kimlik?** | Parola / MFA | **MFA** — tek parola çalınırsa yetmemeli; ikinci faktör zorunlu |
| **Hesap?** | Paylaşılan / Kişisel | **Kişisel** — kim ne yaptı izlenebilsin; paylaşılan hesap sorumluluğu siler |
| **Kayıt?** | Yok / Tam oturum kaydı | **Tam oturum kaydı** — olay sonrası inceleme ve CRA kanıtı için şart (bkz. Lab 6) |
| **Zamanlama?** | Sürekli açık / Varsayılan kapalı | **Varsayılan kapalı** — erişim yalnızca gerektiğinde, süreli açılmalı; sürekli açık kapı en büyük risktir |

---
**Evidence Pack hedefi:** Zone / Conduit Diagram → EP 05 Zone & Conduit.
**Bağlantı:** rapor/03-varlik-envanteri.md Tablo 3.2; Şekil 3.1. Standart: IEC 62443-3-2 [12], CISA OT varlık rehberi [11].
