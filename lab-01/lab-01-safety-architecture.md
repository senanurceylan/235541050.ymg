# LAB 1 · Safety Architecture
**Çıktı:** Safety Function Map
**Föy sürümü:** Genel Sürüm · Şişeleme Hattı
**Hedef makine:** STK Makina – Otomatik Şişe Dolum Makinesi

| Ad Soyad | Öğrenci No | Grup | Tarih |
|---|---|---|---|
| Sena Nur Ceylan | 235541050 |  | 2026-10-22 |

> **Etiketler:** [D] doğrulanmış (üretici kaynağı) · [B] bilinmiyor (kamuya açık kaynakta yok) · [V] varsayımsal (sektör uygulaması, doğrulanmadı)
> **Kapsam notu:** Çalışma yalnızca kamuya açık kaynaklarla yapılmıştır; firmayla iletişim kurulmamış, test yapılmamıştır. Föydeki emniyet mimarisi (E-stop → Safety PLC → STO) **genel bir referans modeldir**; STK makinesinde bu bileşenlerin varlığı kamuya açık kaynaklarda doğrulanamamıştır [B]. Cevaplar "olması gereken" emniyet fonksiyonu üzerinden verilmiştir.

---

## Safety Function Map (makineye uyarlanmış)

```
NORMAL KONTROL YOLU · üretim
[Şişe/flowmetre sensörü] → [PLC (normal kumanda) [D1]] → [Dolum valfi / konveyör [V]]        [IPC / Uzak Erişim · bakım·güncelleme — [B] koşullu]
                                        └········ dijital kesişim noktası ········┘
SAFETY YOLU · koruma · AYRI  (referans model [V])
[E-stop / koruyucu kapak] → [Safety PLC (emniyet kumandası)] → [STO / Kontaktör] → [Safe State]
```

---

## Görev — sırayla cevaplayın

**1) Bu makinede tehlike nedir? İnsan neyden zarar görür?**
Başlıca tehlikeler [V]: (a) hareketli konveyör ve dolum/kapak mekanizmasında **ezilme, sıkışma, el/parmak kapılması**; (b) elektrik panosunda **elektrik çarpması** (A-04); (c) basınçlı hava ile çalışan valf/aktüatör hareketlerinde ani hareket; (d) gıda hattı olduğu için dolaylı olarak **CIP kimyasalına maruziyet** ve kaygan zeminde düşme. Doğrudan insana temas eden ana kaynak hareketli taşıma ve dolum istasyonudur. *(Makinenin gerçek emniyet donanımı [B].)*

**2) Safety function (emniyet fonksiyonu) hangisidir?**
Tanımlanması gereken birincil emniyet fonksiyonu [V]: **"Bir tehlike algılandığında (acil stop'a basılması veya koruyucu kapağın açılması) tehlikeli hareketin güvenli şekilde durdurulması"** — yani hareketli tahrikin güç/tork kaynağının kesilmesi (Safe Torque Off / güvenli duruş). İkincil fonksiyon: kapak açıkken tehlikeli hareketin başlamasının engellenmesi (start kilitlemesi).

**3) Safety-related control system nerede? Şemada işaretleyin.**
Referans modelde **SAFETY YOLU** bölümüdür: E-stop/koruyucu kapak → **Safety PLC** → STO/Kontaktör → Safe State. Bu yol, normal üretim yolundan (PLC → aktüatör) **ayrı** olmalıdır. STK makinesinde ayrı bir emniyet kumanda sisteminin bulunup bulunmadığı **[B]**; S-01…S-03 varlıkları envanterde "koşullu" işaretlenmiştir.

**4) Normal PLC ile Safety PLC farkı nedir?**
Normal PLC [D1] üretim mantığını yürütür; amacı verimli çalışmadır, sertifikalı emniyet bütünlüğü gerektirmez. Safety PLC ise emniyet fonksiyonlarını yürütmek için **sertifikalı** (ör. SIL/PLr düzeyli), arıza durumunda **güvenli tarafa düşen** (fail-safe), kendini test eden bir kumandadır. İkisinin ayrılması, normal PLC'deki bir yazılım hatası veya siber müdahalenin emniyet fonksiyonunu doğrudan bozmamasını sağlar.

**5) PLr / SIL neden var? Bu fonksiyon için neden önemli?**
PLr (ISO 13849'da required Performance Level) ve SIL (IEC 62061/61508'de Safety Integrity Level), bir emniyet fonksiyonunun **ne kadar güvenilir** olması gerektiğini risk büyüklüğüne göre belirler [V]. Yüksek risk (ağır yaralanma, geri döndürülemez) → daha yüksek PLr/SIL → daha fazla yedeklilik, izleme ve düşük arıza olasılığı. Durdurma fonksiyonu insanı koruduğu için uygun PLr/SIL seviyesinde tasarlanmalıdır. *(Bu makine için hedef seviye [B].)*

**6) Safe state (güvenli durum) nedir?**
Makinenin, insana zarar veremeyeceği durumdur [V]: tüm tehlikeli hareketler durmuş, tahrik torku kesilmiş (STO), dolum valfi kapalı, sistem ancak bilinçli bir reset ile yeniden başlatılabilir. Enerji veya hava kesildiğinde de valf ve tahrikler güvenli (kapalı/durmuş) konuma geçmelidir.

**7) Safety function hangi dijital bağımlılıklara sahip?**
[V] Emniyet fonksiyonu şunlara bağımlıdır: emniyet giriş cihazları (E-stop, kapak kilidi — S-01/S-02 [B]), emniyet kumandasının programı/konfigürasyonu (SW, [B]), çıkış elemanları (STO/kontaktör), ve kesişim noktasında normal kontrol sistemiyle paylaşılan sinyaller. **Kritik bağımlılık:** eğer emniyet fonksiyonu normal PLC veya ortak bir ağ üzerinden parametrelenebiliyorsa, o dijital yol bir zayıflık olur. "Dijital kesişim noktası" tam da bu risktir.

**8) Siber müdahale hangi noktadan bu fonksiyonu bozar?**
[V] En kritik nokta **dijital kesişim noktası** ve **IPC / uzak erişim** yoludur: (a) emniyet parametrelerinin (reaksiyon süresi, kapak kilidi mantığı) yetkisiz değiştirilmesi; (b) emniyet ile normal kontrolün aynı kumanda/ağda olması halinde normal taraftan emniyet tarafına geçiş; (c) uzak bakım modülü üzerinden konfigürasyon değişikliği. **Not:** IEC TS 63074, emniyet fonksiyonlarını hedef alan siber tehditlerin değerlendirilmesini ele alır [16]. Fiziksel kablo köprüleme bu standardın kapsamı dışıdır ama gerçek bir risktir (S-01/S-02 köprüleme).

---
**Evidence Pack hedefi:** Safety Function Map → EP 03 Safety Functions.
**Bağlantı:** rapor/03-varlik-envanteri.md (S-01…S-03, A-01, A-04). Safety ve Security ayrıntısı → rapor Aşama 7.
