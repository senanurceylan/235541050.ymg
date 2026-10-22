# LAB 3 · Threat & Risk + Risk Matrix
**Çıktı:** Risk Register
**Föy sürümü:** Genel Sürüm · Şişeleme Hattı
**Hedef makine:** STK Makina – Otomatik Şişe Dolum Makinesi

| Ad Soyad | Öğrenci No | Grup | Tarih |
|---|---|---|---|
| Sena Nur Ceylan | 235541050 |  | 2026-10-22 |

> **Kavram:** Senaryo beş parçadır: **kim → hangi kapı → ne yapar → zincir → FİZİKSEL sonuç**. Skor = L × S × E (her biri 1–3).
> **Kural:** S=3 ise skor düşük olsa bile senaryo öne alınır — insana zarar görünür kalır.
> **Skala:** L (olasılık), S (safety/insana etki), E (etki büyüklüğü/yayılım) 1–3. Kritik 18–27 · Yüksek 9–17 · Orta 4–8 · Düşük 1–3.
> **Önemli:** Aşağıdaki senaryolar **varsayımsal risklerdir**, doğrulanmış güvenlik açığı değildir. "Hangi kapı" sütunundaki bileşenlerin (uzak erişim, varsayılan hesap vb.) bizim makinemizde gerçekten bulunduğu **doğrulanmamıştır [B]**; "eğer varsa" mantığıyla kurulmuştur.

---

## Görev — üç senaryo kurun ve puanlayın

**Risk Register**

| # | Senaryo (kim → kapı → zincir → fiziksel sonuç) | L | S | E | Skor | Öncelik |
|---|---|---|---|---|---|---|
| R1 | **Dış saldırgan → uzak bakım/erişim kanalı (C4) [B] → PLC mantığını veya emniyet parametresini değiştirir → koruyucu kapak/E-stop tepkisi gecikir, hareketli konveyör/dolum mekanizması durmaz → operatörün eli sıkışır/ezilir** | 1 | 3 | 2 | 6 | **Öncelikli (S=3 kuralı)** |
| R2 | **Meraklı/sınırlı yetkili iç kullanıcı (operatör) → HMI ayar ekranı (zayıf/parolasız erişim [B]) → flowmetre kalibrasyon katsayısını veya reçeteyi değiştirir → sistematik eksik/fazla dolum, fark edilmez → yanlış/kontamine ürün tüketiciye ulaşır (dolaylı insana zarar + yasal dolum toleransı ihlali)** | 2 | 2 | 2 | 8 | Orta-üst |
| R3 | **Dış saldırgan → OT'ye bağlı ofis ağı / segmentsiz anahtar (C3) [B] → PLC'yi veya HMI'ı hizmet dışı bırakır (DoS) → makine beklenmedik şekilde durur/alarm basar, valf belirsiz konumda kalır → ürün taşması, kaygan zemin, duruş; acil müdahale sırasında yaralanma riski** | 1 | 2 | 2 | 4 | Orta |

**Puanlama gerekçesi (kısa):**
- R1: Olasılık düşük (uzak erişimin varlığı [B], L=1) ama insana doğrudan ağır zarar potansiyeli (S=3) olduğu için **altın kural gereği öne alınır**.
- R2: İçeriden, düşük yetkiyle, fark edilmeden yapılabildiği için olasılığı daha yüksek (L=2); gıda güvenliği ve yasal sonuç (S=2, E=2).
- R3: Kullanılabilirlik etkisi; doğrudan yaralanma dolaylı (S=2).

**1) En yüksek öncelikli senaryonuz hangisi? Bir cümleyle: neden bu?**
**R1.** Çünkü skoru en yüksek olmasa da (6), tek senaryo S=3'tür: emniyet fonksiyonunu hedef alıp insana doğrudan fiziksel zarar verebilir; altın kural gereği insana zarar görünür kalmalıdır.

**2) S=3 olup skoru düşük kalan senaryonuz var mı? Nasıl görünür kılacaksınız?**
Evet, **R1** (S=3, skor 6). Görünür kılmak için: Risk Register'da ayrı bir "Safety-critical" bayrağıyla işaretlenir, skor sıralamasından bağımsız olarak önlem listesinin en üstüne konur ve raporun risk matrisinde (Aşama 8) kırmızı/safety kategorisinde gösterilir. Önlemi (emniyet bölgesinin ayrılması, uzak erişimin varsayılan kapalı olması) öncelikli gereksinim yapılır.

> **Altın kural:** Zincir "veri çalındı" ile bitiyorsa emniyet bulgusu değildir — bir adım daha gidin: bu, hattaki insana ne yapar? Yukarıdaki üç senaryonun üçü de fiziksel/insan sonucu ile bitirilmiştir (ezilme, kontamine ürün, taşma+duruş).

---
**Evidence Pack hedefi:** Risk Register → EP 04 Risk Assessment.
**Bağlantı:** rapor/03-varlik-envanteri.md (A-01, A-02, F-01, P-01, P-02, C3, C4); rapor/02 hata durumları HD3/HD4/HD6/HD9. Tam risk matrisi → rapor Aşama 8.
