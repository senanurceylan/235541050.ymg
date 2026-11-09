# Siber Emniyet Dosyası — 15 Başlık Durum Tablosu (Evidence Pack EP 01–15)

> **Durum ölçeği (hoca):** **Yok** · **Taslak** · **Var** · **Doğrulanmış**
> **İlke:** Klasör/dosya varlığı "tamamlandı" sayılmaz; aşağıdaki durum, belgenin **içeriğine** göre verilmiştir. Hiçbir başlık boş bırakılmamıştır.
> **Önemli:** Makinenin iç yapısına ait birçok veri kamuya açık kaynakta yoktur [B]. Bu nedenle **hiçbir başlık "Doğrulanmış" değildir**; en güçlüler "Var" düzeyindedir. Bu, dürüstlük gereğidir, eksiklik değil.
> **Güncelleme:** 2026-11-09

| EP | Başlık | Durum | Dayanak belge (içerik) | Gerekçe |
|---|---|---|---|---|
| **01** | Asset Inventory (Varlık envanteri) | **Var** | `rapor/03-varlik-envanteri.md` | 55 varlık, 10 kategori, kritiklik ve "iz" sütunlarıyla tam; CISA rehberi yöntemiyle [11]. Zayıflık: cihaz marka/modeli [B]. |
| **02** | Network Architecture (Ağ mimarisi) | **Taslak** | `rapor/sekiller/sekil-3-1-bolge-kanal-modeli.svg`, Lab 2 | Varsayımsal referans mimari (seviye katmanları, bölgeler) çizildi. Gerçek ağ topolojisi, protokol ve IP yapısı [B]; bu yüzden "Var" değil. |
| **03** | Safety Functions (Emniyet fonksiyonları) | **Taslak** | `lab-01-safety-architecture.md` | Emniyet fonksiyonu, safe state, PLr/SIL mantığı "olması gereken" düzeyinde tanımlı. Gerçek emniyet donanımı (S-01…S-03) [B]. |
| **04** | Cyber Risk Assessment (Siber risk değerlendirmesi) | **Taslak** | `lab-03-threat-risk-matrix.md` | 3 senaryo L×S×E ile puanlı. Tam risk matrisi (Aşama 8) ve daha fazla senaryo (Aşama 6) eksik. |
| **05** | Zone & Conduit (Bölge ve bağlantılar) | **Var** | `lab-02-...md`, `rapor/03` Tablo 3.2, Şekil 3.1 | Bölgeler (Z1–Z5, Z-Safety) ve kanallar (C1–C5) tanımlı, her geçişte kontrol belirtilmiş. En olgun başlıklardan biri. |
| **06** | Remote Access Procedure (Uzaktan erişim prosedürü) | **Taslak** | `lab-04-secure-remote-access.md` | 6 karar (aracı, tünel, kimlik, hesap, kayıt, zamanlama) + mevcut→hedef. Tam adım adım prosedür belgesi değil. Gerçek uzak erişim varlığı [B]. |
| **07** | User / Role Matrix (Kullanıcı/yetki matrisi) | **Taslak** | `rapor/03` Tablo 3.9 (R-01…R-06) | Roller ve varsayımsal erişimler listeli. HMI kullanıcı seviyeleri [B]; ayrıntılı yetki-işlem matrisi henüz yapılmadı. |
| **08** | Software / Firmware Inventory | **Taslak** | `rapor/03` Tablo 3.6 (SW-01…SW-05) | Yazılım/firmware varlıkları listeli ama **sürüm bilgisi [B]**. Lab 5 ile tamamlanacak. |
| **09** | SBOM (Yazılım bileşenleri listesi) | **Taslak** | `lab-05-...md` (hazırlanıyor) | Gerçek bileşen listesi üreticide; bizde [B]. Lab 5'te eğitim amaçlı çerçeve + bilinmeyen işaretlemesiyle ele alınıyor. |
| **10** | Vulnerability Records (Güvenlik açığı kayıtları) | **Taslak** | `lab-05-...md` | `"STK Makina" CVE/advisory/vulnerability` sorgusuyla (2026-10-20) eşleşen kayıt dönmedi. **Bu "zafiyetsiz" demek değildir;** marka/sürüm [B] olduğu için cihaz bazlı eşleştirme kapsam dışı. Arama kaydı tutuldu. |
| **11** | Patch / Update Records (Yama/güncelleme kayıtları) | **Taslak (yalnız prosedür)** | `lab-05-...md` Soru 3/5 | **İki ayrı şey:** (a) Gerçekleştirilmiş yama/güncelleme kaydı → **YOK** (hiç yapılmadı). (b) Yama karar süreci / telafi edici önlem taslağı → **VAR**. Yapılmamış işlem yapılmış gösterilmemiştir. |
| **12** | Backup & Restore (Yedekleme/geri yükleme) | **Yok** | `rapor/03` P-08'de yalnızca varlık olarak anılıyor | Yedekleme/geri yükleme prosedürü belgesi yok. Öneri Aşama 9'da verilecek. |
| **13** | Incident Response (Olay müdahalesi) | **Yok** | — | Lab 6 (CRA Incident Simulation) henüz yapılmadı. |
| **14** | Change Management (Değişiklik yönetimi) | **Yok** | TOWS'ta yalnızca strateji olarak anılıyor (WT2) | Değişiklik yönetimi prosedürü belgesi yok. Aşama 9'da ele alınacak. |
| **15** | Verification / Test (Doğrulama/test) | **Yok** | — | Proje "çalışan test" içermiyor (hoca istemiyor). Belge doğrulama/gözden geçirme planı Aşama 10'da tanımlanacak. |

## Özet
- **Var (2):** EP 01 Asset Inventory, EP 05 Zone & Conduit.
- **Taslak (9):** EP 02, 03, 04, 06, 07, 08, 09, 10 ve **EP 11 (yalnız yama karar prosedürü; gerçekleştirilmiş yama kaydı YOK).**
- **Yok (4):** EP 12 Backup/Restore, EP 13 Incident Response, EP 14 Change Mgmt, EP 15 Verification/Test.
- **Doğrulanmış (0):** Makine iç verileri [B] olduğu için hiçbiri bu düzeyde değil.

> Sayım: Var = 2 (EP 01, 05). Taslak = 9 (EP 02,03,04,06,07,08,09,10,11). Yok = 4 (EP 12,13,14,15). Toplam 15. ✔
> EP 11 özel durum: **prosedür/karar taslağı var, gerçekleştirilmiş yama kaydı yok** — ikisi ayrı tutulmuştur.

## Başlıkların lab/aşama ile ilişkisi
| EP | İlişkili çalışma |
|---|---|
| 01 | Aşama 3 |
| 02, 05 | Lab 2 + Aşama 3 |
| 03 | Lab 1 + Aşama 7 |
| 04 | Lab 3 + Aşama 6/8 |
| 06 | Lab 4 |
| 07 | Aşama 3 + Aşama 5 |
| 08, 09, 10, 11 | **Lab 5** |
| 13 | Lab 6 |
| 12, 14, 15 | Aşama 9/10 |
