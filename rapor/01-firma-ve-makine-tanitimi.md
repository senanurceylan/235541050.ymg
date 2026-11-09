# 1. FİRMA VE MAKİNE TANITIMI

> **Etiketler:** [D] doğrulanmış · [B] bilinmiyor · [V] varsayımsal · [D-beyan] firma beyanı, bağımsız doğrulanmadı.
> **Kapsam:** Çalışma yalnızca kamuya açık kaynaklarla yapılmıştır. Hedef firmayla iletişim kurulmamış, sistemlerine erişilmemiş, test yapılmamıştır.

## 1.1 Firma: STK Makina

| Özellik | Bilgi | Etiket | Kaynak |
|---|---|---|---|
| Kuruluş | 1981, Sakarya | [D] | [3][6] |
| Konum | Sakarya 1. OSB, 10. Yol No:5, Arifiye / Sakarya | [D] | [2] |
| Faaliyet alanı | Gıda makineleri; özellikle süt ve süt ürünleri işleme hatları, anahtar teslim tesis kurulumu | [D] | [3] |
| Hizmetler | Ar-Ge, tasarım, proje, üretim, montaj, devreye alma, satış ve satış sonrası hizmet | [D] | [3] |
| İhracat | "120'den fazla ülke" (sitede 115/120/121 gibi farklı rakamlar geçiyor) | [D] (tutarsızlık notuyla) | [2][3] |
| Belgeler | Katalogda "ISO-CE-TSE" ifadesi; "Belgelerimiz" sayfasında 17 görsel, açıklama yok | [D-beyan] / kapsam [B] | [4][6] |
| Otomasyon/SCADA/uzaktan servis hizmeti | Sitede ayrı bir hizmet olarak anılmıyor | [B] | [3] |

**Ürün portföyündeki yeri:** Şişe dolum makinesi, "Dolum ve Paketleme" kategorisindeki altı üründen biridir (diğerleri: yoğurt sütü dolum, ayran ve yoğurt sütü dolum, shrink, vakum paketleme, termoform paketleme) [7]. Firma bu makineyi büyük olasılıkla tek başına değil, anahtar teslim süt tesisinin hat sonu ekipmanı olarak konumlandırmaktadır [V].

## 1.2 Makine: Otomatik Şişe Dolum Makinesi

**Tanım [D]:** Süt, ayran, meyve suyu ve diğer sıvı gıdaları şişelere hassas ve hijyenik biçimde dolduran, PLC kontrollü ve dokunmatik ekranlı bir dolum makinesi [1].

### Doğrulanmış özellikler [D]

| # | Özellik | Kaynak |
|---|---|---|
| D1 | PLC kontrollü çalışma | [1] |
| D2 | Dokunmatik ekran (HMI) | [1] |
| D3 | Elektromanyetik flowmetre ile hacimsel dolum | [1] |
| D4 | Farklı şişe hacimlerine uyum | [1] |
| D5 | Otomatik dolum ve kapak kapatma **seçenekleri** (kapak kapatma opsiyonel) | [1] |
| D6 | Hedef ürünler: süt, ayran, meyve suyu, sıvı gıdalar | [1] |
| D7 | Hedef kullanıcılar: süt ve sıvı gıda üreticileri, endüstriyel hatlar | [1] |
| D8 | Katalogda "Şişe Dolum Makinası / Bottle Filling Machine" olarak, görselle yer alıyor; teknik föy yok | [6] |

### Bilinmeyen özellikler [B]
Model kodu ve varyantları; kapasite (şişe/saat); dolum memesi sayısı; lineer/rotary yapısı; PLC ve HMI marka/modeli; flowmetre dışındaki sensörler; motorlar ve sürücüler; pnömatik sistem; paslanmaz çelik kalitesi; boyutlar ve enerji ihtiyacı; haberleşme protokolleri ve ağ arayüzleri; uzaktan erişim; emniyet donanımı; CIP entegrasyonu; makineye özel CE uygunluk beyanı.

> ⚠️ Kardeş ürün "Ayran ve Yoğurt Sütü Dolum" makinesinin değerleri (100–2000 g; 1200–5600 adet/saat [5]) **bardak/kase dolumuna** aittir ve şişe dolum makinesine **aktarılmamıştır**.

### Yayımlanmış güvenlik açıkları
"STK Makina" için yapılan web aramasında (2026-10-20) eşleşen CVE/güvenlik duyurusu bulunamamıştır; ayrıntı ve sınırlamaları için bkz. `lab-05` ve `rapor/00-evidence-pack-durum.md` EP 10. Bu sonuç "zafiyetsiz" anlamına gelmez.

## 1.3 Çalışmanın uygunluk değerlendirmesi
Makine, proje için **yeterlidir**, ancak iç yapısına ait birçok veri kamuya açık kaynakta bulunmadığından ([B]) analiz, açıkça işaretlenmiş **varsayımsal referans mimari** üzerinden yürütülmektedir. Bu yaklaşım, IEC 62443-3-2'nin bölge/kanal yöntemi ve NIST SP 800-82r3 ile uyumludur ([12][13]) ve akademik olarak kabul görür. Bilgi eksikliğinin şeffaf yönetimi, metodolojik bir güç olarak ele alınmıştır.

## 1.4 Doğrulanması gerekenler
| # | Konu | Durum |
|---|---|---|
| H1 | Varsayımsal referans mimari kabul ediliyor mu? | Hocaya sorulacak |
| H2 | Dört hazır tehdit aktörü profilinin adları | Ders materyalinden doğrulanacak (Aşama 5) |
| H3 | Beş değerlendirme parametresinin adları | Ders materyalinden doğrulanacak (Aşama 5) |
| H4 | Beşinci (özgün) profil | Belirlendi: meraklı ve sınırlı yetkili iç kullanıcı |

## Kaynaklar
[1] STK Makina, "Şişe Dolum Makinesi," ürün sayfası. https://www.stkmakina.com/sise-dolum-makinesi (Erişim: 20.10.2026)
[2] STK Makina, Ana sayfa. https://www.stkmakina.com/ (Erişim: 20.10.2026)
[3] STK Makina, "Hakkımızda." https://www.stkmakina.com/hakkimizda-p-2 (Erişim: 20.10.2026)
[4] STK Makina, "Belgelerimiz." https://www.stkmakina.com/belgelerimiz-p-10 (Erişim: 20.10.2026)
[5] STK Makina, "Ayran ve Yoğurt Sütü Dolum." https://www.stkmakina.com/ayran-ve-yogurt-sutu-dolum (Erişim: 20.10.2026)
[6] STK Makina, "STK Makina Dijital Katalog," PDF, 2024. https://www.stkmakina.com/foto/1779257448-STK%20Makina%20Dijital%20Katalog.pdf (Erişim: 20.10.2026)
[7] STK Makina, "Dolum ve Paketleme." https://www.stkmakina.com/dolum-ve-paketleme (Erişim: 20.10.2026)
