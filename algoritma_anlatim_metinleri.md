# STAJYER YERLEŞTİRME ALGORİTMALARI - DETAYLI ANLATIM METİNLERİ

---

## 🚀 ALGORİTMA 1: GREEDY (AÇGÖZLÜ) ALGORİTMASI

### 📌 TEMEL MANTIK

Greedy algoritması, her adımda **yerel olarak en iyi görünen seçimi** yaparak ilerler. "Açgözlü" ismini, geleceği düşünmeden anlık en avantajlı kararı almasından alır. Bizim projemizde, öğrencileri **GNO (Not Ortalaması)** puanına göre sıralayıp, en yüksek puanlı öğrenciden başlayarak sırayla tercihlere yerleştirme yapar.

---

### 🔄 NASIL ÇALIŞIR? (ADIM ADIM)

**Algoritma Akışı:**

```
1️⃣ ÖN İŞLEM:
   • Tüm öğrencileri GNO'ya göre büyükten küçüğe sırala
   • Firma kontenjanlarını hazırla

2️⃣ ANA DÖNGÜ (Her öğrenci için):
   a) En yüksek GNO'lu öğrenciyi al
   b) Öğrencinin tercihlerini sırayla kontrol et (1. → 2. → 3. → 4. → 5.)
   
   c) Her tercih için:
      - Firma kontenjanı dolu mu?
        ├─ HAYIR → Öğrenciyi yerleştir, kontenjanı 1 azalt, BİTİR
        └─ EVET  → Sonraki tercihe geç
   
   d) Hiçbir tercihe yerleşemediyse → Boşta kal

3️⃣ SONUÇ:
   • Tüm öğrenciler işlendi → Atama matrisi döndür
```

---

### 💡 SOMUT ÖRNEK

**Veri Seti:**
```
Öğrenci    GNO    Tercih 1    Tercih 2    Tercih 3
─────────────────────────────────────────────────
Ali        3.8    Firma_A     Firma_B     Firma_C
Ayşe       3.6    Firma_A     Firma_C     Firma_B
Mehmet     3.2    Firma_B     Firma_A     Firma_C
Zeynep     2.9    Firma_A     Firma_B     Firma_C
Can        2.5    Firma_C     Firma_A     Firma_B

Kontenjan: Firma_A=2, Firma_B=1, Firma_C=2
```

**Greedy'nin Adım Adım Çalışması:**

```
TUR 1: Ali (GNO=3.8, en yüksek)
  → 1. Tercih: Firma_A
  → Kontenjan var mı? EVET (2)
  ✅ Ali → Firma_A'ya yerleşti
  📊 Durum: A=1, B=1, C=2

TUR 2: Ayşe (GNO=3.6, 2. sırada)
  → 1. Tercih: Firma_A
  → Kontenjan var mı? EVET (1)
  ✅ Ayşe → Firma_A'ya yerleşti
  📊 Durum: A=0, B=1, C=2

TUR 3: Mehmet (GNO=3.2, 3. sırada)
  → 1. Tercih: Firma_B
  → Kontenjan var mı? EVET (1)
  ✅ Mehmet → Firma_B'ye yerleşti
  📊 Durum: A=0, B=0, C=2

TUR 4: Zeynep (GNO=2.9, 4. sırada)
  → 1. Tercih: Firma_A
  → Kontenjan var mı? HAYIR (0) ❌ Sonraki tercihe geç
  → 2. Tercih: Firma_B
  → Kontenjan var mı? HAYIR (0) ❌ Sonraki tercihe geç
  → 3. Tercih: Firma_C
  → Kontenjan var mı? EVET (2)
  ✅ Zeynep → Firma_C'ye yerleşti (3. tercihi!)
  📊 Durum: A=0, B=0, C=1

TUR 5: Can (GNO=2.5, 5. sırada)
  → 1. Tercih: Firma_C
  → Kontenjan var mı? EVET (1)
  ✅ Can → Firma_C'ye yerleşti
  📊 Durum: A=0, B=0, C=0
```

**SONUÇ:**
- Ali → Firma_A (1. tercih) = 100 puan
- Ayşe → Firma_A (1. tercih) = 100 puan
- Mehmet → Firma_B (1. tercih) = 100 puan
- Zeynep → Firma_C (3. tercih) = 60 puan ⚠️
- Can → Firma_C (1. tercih) = 100 puan

**Toplam Memnuniyet: 460 puan**

---

### ⚠️ GREEDY'NİN SORUNSALI

**Zeynep neden 3. tercihine yerleşti?**

Çünkü Ali ve Ayşe (daha yüksek GNO) Firma_A'nın kontenjanını bitirdi. Zeynep'in GNO'su düşük olduğu için sıra ona geldiğinde ilk 2 tercihi doluydu.

**Daha İyi Çözüm Var mıydı?**

Evet! Eğer Ayşe Firma_C'ye (2. tercihi, 80 puan) yerleşseydi:
- Ayşe → Firma_C (80 puan)
- Zeynep → Firma_A (100 puan)
- **Toplam: 480 puan** (+20 puan!)

Ama Greedy geleceği göremez, sadece "şu an en iyi" seçimi yapar. Bu yüzden **yerel optimum'a takılır**.

---

### ✅ AVANTAJLARI

1. **Çok Hızlı:**
   - Zaman Karmaşıklığı: O(n log n + n×k)
     - n log n: Öğrencileri sıralama
     - n×k: Her öğrenci için k tercih kontrol etme
   - 100 öğrenci için: ~0.02 saniye

2. **Basit Implementasyon:**
   - Anlaşılır kod mantığı
   - Az satır kod (~30 satır)

3. **Deterministik:**
   - Aynı veri her zaman aynı sonucu verir
   - Tahmin edilebilir

4. **Garanti Çözüm:**
   - Her öğrenci için bir atama yapar (veya boş bırakır)
   - Hiçbir kontenjan aşılmaz

---

### ❌ DEZAVANTAJLARI

1. **Yerel Optimum Tuzağı:**
   - Global (genel) en iyi çözümü bulamayabilir
   - İlk seçimler sonraki seçimleri kısıtlar

2. **GNO Bias'ı:**
   - Sadece GNO'ya bakar
   - Düşük GNO'lu öğrencilere haksızlık olabilir

3. **Geri Dönüşsüz (Non-Backtracking):**
   - Yaptığı atamayı geri alamaz
   - "Keşke baştan yapsaydım" düşüncesi yok

4. **Kısa Vadeli Düşünür:**
   - Sadece şu anki öğrenciyi düşünür
   - Geride gelenleri umursamaz

---

### 📊 KOD YAPISI (PYTHON)

```python
def greedy_atama(ogrenciler_df, firmalar_df):
    # 1. SIRALAMA (En önemli adım!)
    sirali_ogrenciler = ogrenciler_df.sort_values('GNO', ascending=False)
    
    # 2. HER ÖĞRENCİ İÇİN
    for idx, ogrenci in sirali_ogrenciler.iterrows():
        # 3. TERCİHLERİ DENE (1'den 5'e)
        for tercih_no in range(1, 6):
            tercih_firma = ogrenci[f'Tercih{tercih_no}']
            
            # 4. KONTENJAN KONTROLÜ
            if firmalar[tercih_firma]['Kontenjan'] > 0:
                # YERLEŞTIR
                ogrenci['Yerleştiği_Firma'] = tercih_firma
                firmalar[tercih_firma]['Kontenjan'] -= 1
                break  # Bu öğrenci bitti, sonraki öğrenciye geç
    
    return ogrenciler_df, firmalar_df
```

---

### 🎯 KULLANIM SENARYOLARI

**Greedy Ne Zaman Tercih Edilmeli?**

✅ **İdeal Durumlar:**
- Çok hızlı çözüm gerektiğinde
- Büyük veri setleri (n > 10,000)
- "Yeterince iyi" çözüm yeterli olduğunda
- Gerçek zamanlı sistemler (online atama)

❌ **Uygun Olmayan Durumlar:**
- Maksimum kalite aranıyorsa
- Küçük veri setlerinde (n < 100)
- Adalet ve denge önemliyse
- Offline hesaplama (zaman bol)

---

### 📈 PERFORMANS

**Deneysel Sonuçlar (n=100, m=20):**
- **Süre:** 0.023 saniye
- **Memnuniyet Skoru:** 7,240
- **Yerleşme Oranı:** 92%
- **1. Tercih Oranı:** 45%

---

---

## ⛰️ ALGORİTMA 2: HILL CLIMBING (TEPEYİ TIRMANA)

### 📌 TEMEL MANTIK

Hill Climbing, **yerel arama (local search)** algoritmasıdır. Bir dağın zirvesine tırmanırken "her adımda yukarı çık" mantığıyla çalışır. Başlangıç çözümünden (genelde Greedy sonucu) başlar, rastgele komşu çözümler üretir ve **daha iyi skorlu olanı kabul eder**. Bu şekilde adım adım iyileştirme yapar.

**Dağ Metaforu:**
- Başlangıç: Dağın eteğinde rastgele bir noktadasınız
- Amaç: Zirveye ulaşmak (en yüksek memnuniyet skoru)
- Yöntem: Her adımda "yukarı" giden yönü seçmek

---

### 🔄 NASIL ÇALIŞIR? (ADIM ADIM)

```
1️⃣ BAŞLANGIÇ:
   • Greedy algoritmasıyla bir başlangıç çözümü elde et
   • Bu çözümün skorunu hesapla (current_score)
   • Best_score = current_score olarak kaydet

2️⃣ İTERATİF ARAMA (3000 iterasyon):
   
   FOR i = 1 to 3000:
       a) KOMŞU ÇÖZÜM ÜRET:
          • Rastgele bir öğrenci seç
          • Bu öğrenciyi rastgele bir tercihine taşı (MOVE)
          VEYA
          • İki öğrencinin yerini değiştir (SWAP)
       
       b) YENİ ÇÖZÜMÜ DEĞERLENDİR:
          • new_score = memnuniyet_skoru_hesapla(yeni_çözüm)
       
       c) KARAR VER:
          IF new_score > current_score:
              ✅ Yeni çözümü kabul et
              current_score = new_score
              
              IF new_score > best_score:
                  best_score = new_score
                  best_solution = yeni_çözüm
          ELSE:
              ❌ Yeni çözümü reddet, eskisine devam et

3️⃣ SONUÇ:
   • En iyi bulunan çözümü döndür (best_solution)
```

---

### 💡 SOMUT ÖRNEK

**Başlangıç (Greedy Sonucu):**
```
Ali → Firma_A (100)
Ayşe → Firma_A (100)
Mehmet → Firma_B (100)
Zeynep → Firma_C (60)
Can → Firma_C (100)

Toplam: 460 puan
```

**Hill Climbing İterasyonları:**

```
İTERASYON 1:
  Hamle: Ayşe ile Mehmet SWAP
  Sonuç: Ayşe → Firma_B (80), Mehmet → Firma_A (100)
  Yeni Skor: 440
  Karar: 440 < 460 ❌ REDDET

İTERASYON 2:
  Hamle: Zeynep'i Firma_A'ya MOVE
  Sonuç: BAŞARISIZ (Kontenjan dolu)
  Karar: ❌ ATLAT

İTERASYON 3:
  Hamle: Ayşe ile Zeynep SWAP
  Sonuç: Ayşe → Firma_C (80), Zeynep → Firma_A (100)
  Yeni Skor: 480
  Karar: 480 > 460 ✅ KABUL ET
  
  📊 Güncel En İyi: 480 puan

İTERASYON 4:
  Hamle: Can'ı Firma_B'ye MOVE
  Sonuç: BAŞARISIZ (Kontenjan dolu)
  Karar: ❌ ATLAT

İTERASYON 5-3000:
  • Başka hiçbir SWAP/MOVE iyileştirme sağlamıyor
  • Algoritma 480 puanda takılı kaldı
  
SONUÇ: 480 puan (Greedy'den +20 puan iyileştirme!)
```

---

### 🎲 KOMŞULUK FONKSİYONU

Hill Climbing'de **komşu çözüm** nasıl üretilir?

**1. MOVE Operasyonu:**
```
Bir öğrenciyi başka bir tercihine taşı

Örnek:
  Ayşe: Firma_A → Firma_C'ye taşı
  Koşul: Firma_C'de kontenjan olmalı
```

**2. SWAP Operasyonu:**
```
İki öğrencinin firmalarını değiştir

Örnek:
  Ayşe (Firma_A) ↔ Zeynep (Firma_C)
  Koşul: Kontenjan uygunluğu kontrol edilmeli
```

**3. Rastgelelik:**
- Her iterasyonda hangi öğrenciyi seçeceği RASTGELE
- Hangi tercihe gideceği RASTGELE
- Bu sayede çözüm uzayını keşfeder

---

### ✅ AVANTAJLARI

1. **Greedy'den Daha İyi:**
   - Ortalama %3-5 daha yüksek skor
   - Yerel optimumlardan bir miktar kurtulabilir

2. **Orta Hızda:**
   - 3000 iterasyon: ~2 saniye
   - Hala pratik kullanım için yeterli hızlı

3. **Basit Mantık:**
   - Anlaşılır: "Daha iyi ise al, değilse alma"
   - Implementasyon kolay

4. **Esneklik:**
   - İterasyon sayısını ayarlayabilirsiniz
   - Komşuluk fonksiyonunu özelleştirebilirsiniz

---

### ❌ DEZAVANTAJLARI

1. **Yerel Maksimumda Takılır:**
   ```
   Dağ Metaforu:
   
      ^  (Global Max)
     /|\
    / | \___/^\ (Local Max - Hill Climbing burada takılır)
   /  |     | \
   ```
   - Asıl zirveyi bulamayabilir
   - Yakındaki "tepeciği" zirve sanır

2. **Başlangıç Çözümüne Bağımlı:**
   - Greedy kötü başlarsa, Hill Climbing de kötü çıkar
   - "Garbage In, Garbage Out"

3. **Global Optimum Garantisi Yok:**
   - Sadece komşularına bakar
   - Uzak ama daha iyi çözümleri göremez

4. **Stokastik (Her seferinde farklı):**
   - Aynı veri farklı sonuç verebilir
   - Rastgelelik yüzünden tahmin edilemez

---

### 📊 KOD YAPISI

```python
def hill_climbing(ogrenciler, firmalar, iterasyon=3000):
    # 1. BAŞLANGIÇ (Greedy'den gelen çözüm)
    current_solution = ogrenciler.copy()
    current_score = memnuniyet_skoru_hesapla(current_solution)
    
    best_solution = current_solution
    best_score = current_score
    
    # 2. İTERATİF ARAMA
    for i in range(iterasyon):
        # a) Rastgele öğrenci seç
        random_student = np.random.choice(ogrenciler.index)
        
        # b) Komşu çözüm üret (SWAP veya MOVE)
        neighbor = generate_neighbor(current_solution, random_student)
        
        # c) Değerlendir
        neighbor_score = memnuniyet_skoru_hesapla(neighbor)
        
        # d) Karar: Sadece daha iyi ise kabul et
        if neighbor_score > current_score:
            current_solution = neighbor
            current_score = neighbor_score
            
            if neighbor_score > best_score:
                best_solution = neighbor
                best_score = neighbor_score
    
    return best_solution, best_score
```

---

### 🎯 KULLANIM SENARYOLARI

**Hill Climbing Ne Zaman Tercih Edilmeli?**

✅ **İdeal Durumlar:**
- Orta ölçek problemler (100 < n < 1000)
- Zaman kısıtlı ama kalite de önemli
- Greedy'den daha iyi sonuç istiyorsanız
- Başlangıç çözümü iyi ise

❌ **Uygun Olmayan Durumlar:**
- Çok büyük çözüm uzayı (n > 10,000)
- Maksimum kalite şart (kritik uygulamalar)
- Başlangıç çözümü çok kötü

---

### 📈 PERFORMANS

**Deneysel Sonuçlar (n=100, m=20):**
- **Süre:** 1.87 saniye
- **Memnuniyet Skoru:** 7,580
- **İyileştirme:** Greedy'den +340 puan (+4.7%)
- **Yerleşme Oranı:** 96%

---

---

## 🔥 ALGORİTMA 3: SIMULATED ANNEALING (TAVLAMALı BENZETME)

### 📌 TEMEL MANTIK

Simulated Annealing (SA), **termodinamiğin tavlama sürecinden** esinlenmiş bir algoritmadır. Metal tavlama işleminde malzeme önce çok ısıtılır, sonra yavaşça soğutulur. Bu süreçte atomlar rastgele hareket eder, ama zamanla en kararlı (optimal) düzene geçerler.

SA'nın Hill Climbing'den **kritik farkı:** Kötü çözümleri de **belirli bir olasılıkla kabul eder**. Bu sayede yerel optimumlardan kaçabilir ve global optimuma yaklaşır.

**Fiziksel Benzetme:**
- **Yüksek sıcaklık** → Atomlar çok hareketli (kötü çözümler kabul edilir)
- **Düşük sıcaklık** → Atomlar sakinleşir (sadece iyi çözümler kabul edilir)
- **Soğutma** → Sistem en kararlı hale gelir (global optimum)

---

### 🔄 NASIL ÇALIŞIR? (ADIM ADIM)

```
1️⃣ BAŞLANGIÇ AYARLARI:
   • T₀ = 150 (Başlangıç Sıcaklığı)
   • α = 0.99 (Soğuma Oranı)
   • current_solution = Greedy sonucu
   • best_solution = current_solution

2️⃣ İTERATİF ARAMA (10,000 iterasyon):
   
   FOR i = 1 to 10,000:
       
       a) KOMŞU ÇÖZÜM ÜRET:
          • Rastgele bir öğrenci seç
          • SWAP veya MOVE yap
       
       b) SKOR FARKI HESAPLA:
          ΔE = new_score - current_score
       
       c) METROPOLİS KRİTERİ (SA'nın özü!):
          
          IF ΔE > 0:  (Yeni çözüm daha iyi)
              ✅ Her zaman kabul et
          
          ELSE:  (Yeni çözüm daha kötü)
              Kabul olasılığı hesapla:
              P(kabul) = e^(ΔE / T)
              
              Zar at (0-1 arası rastgele sayı):
              IF random() < P(kabul):
                  ✅ Kötü çözümü kabul et! (Yerel tuzaktan kaçış)
              ELSE:
                  ❌ Reddet
       
       d) EN İYİYİ GÜNCELLE:
          IF new_score > best_score:
              best_solution = new_solution
              best_score = new_score
       
       e) SICAKLIĞI DÜŞÜR:
          T = α × T  (Örnek: 150 → 148.5 → 147...)

3️⃣ SONUÇ:
   • En iyi bulunan çözümü döndür
```

---

### 🌡️ METROPOLİS KRİTERİ (SA'NIN KALBI)

**Formül:**
$$P(\text{kabul}) = e^{\frac{\Delta E}{T}}$$

**Ne Demek?**

| Durum | ΔE | Sıcaklık (T) | P(kabul) | Yorum |
|-------|-----|--------------|----------|-------|
| Yeni çözüm daha iyi | +10 | 150 | %100 | ✅ Her zaman kabul |
| Yeni çözüm biraz kötü | -5 | 150 | 96.7% | ✅ Hemen hemen kesin kabul |
| Yeni çözüm kötü | -20 | 150 | 87.5% | ✅ Yüksek olasılıkla kabul |
| Yeni çözüm çok kötü | -50 | 150 | 71.3% | 🟡 Orta olasılıkla kabul |
| Sistem soğudu | -10 | 10 | 36.8% | 🟡 Düşük olasılıkla kabul |
| Sistem çok soğuk | -10 | 1 | 0.005% | ❌ Neredeyse hiç kabul etme |

**Mantık:**
- **Başlangıçta (T yüksek):** Kötü çözümleri çok kabul eder → **Exploration (Keşif)**
- **Sonlarda (T düşük):** Sadece iyi çözümleri kabul eder → **Exploitation (Sömürü)**

---

### 💡 SOMUT ÖRNEK

**Başlangıç (Greedy Sonucu):** 460 puan

```
İTERASYON 1 (T=150):
  Hamle: Ayşe ile Can SWAP
  Sonuç: Ayşe → Firma_C (80), Can → Firma_A (???)
  Yeni Skor: 420 (-40 puan KÖTÜ!)
  
  Metropolis Kriteri:
    P = e^(-40/150) = e^(-0.27) = 76.3%
    Zar: random() = 0.55 < 0.763
    Karar: ✅ KABUL ET! (Yerel tuzaktan kaçmak için risk aldık)
  
  Güncel: 420 puan (geçici olarak düştü)

İTERASYON 500 (T=54):
  Hamle: Zeynep ile Ayşe SWAP
  Sonuç: Zeynep → Firma_A (100), Ayşe → Firma_C (80)
  Yeni Skor: 480 (+60 puan İYİ!)
  
  Karar: ✅ KABUL ET (ΔE > 0, kesin kabul)
  EN İYİ GÜNCELLE: 480 puan

İTERASYON 3000 (T=7):
  Hamle: Mehmet'i Firma_C'ye MOVE
  Sonuç: Skor: 460 (-20 puan KÖTÜ)
  
  Metropolis:
    P = e^(-20/7) = e^(-2.86) = 5.7%
    Zar: random() = 0.82 > 0.057
    Karar: ❌ REDDET (Artık sistem soğudu, risk almıyor)
  
  Güncel: 480 puan (değişmedi)

İTERASYON 5000-10000 (T→0):
  • Sistem tamamen soğudu
  • Artık sadece iyileştirme arıyor
  • 480 puanda stabil kaldı (platoya ulaştı)

SONUÇ: 480 puan (Greedy +20, Hill Climbing ile aynı)
```

**Not:** Büyük problemlerde (n>100) SA genelde Hill Climbing'den daha iyi olur.

---

### 🌡️ SOĞUTMA TAKVİMİ (COOLING SCHEDULE)

**Geometrik Soğutma:**
$$T_{i+1} = \alpha \times T_i$$

| İterasyon | Sıcaklık | Davranış |
|-----------|----------|----------|
| 0 | 150.0 | Çok rastgele, her şeyi kabul |
| 1000 | 54.1 | Hala esnek, kötüyü de alır |
| 3000 | 7.0 | Seçici olmaya başladı |
| 5000 | 0.9 | Sadece iyi çözümler |
| 10000 | 0.0 | Tamamen dondu (Hill Climbing gibi) |

**Grafik:**
```
Sıcaklık
  150│████
     │    ████
  100│        ████
     │            ████
   50│                ████
     │                    ████
    0│________________________████████
      0   2000  4000  6000  8000  10000
              İterasyon
```

---

### ✅ AVANTAJLARI

1. **Global Optimuma Yaklaşır:**
   - Yerel maksimumlardan kaçabilir
   - Tüm algoritmaların en iyisi

2. **Teorik Garanti:**
   - Sonsuz iterasyonda global optimumu bulur (teorik)
   - Pratikte %95-99 başarı

3. **Robust (Dayanıklı):**
   - Başlangıç çözümü kötü olsa da toparlar
   - Farklı problem tiplerine adapte olur

4. **Esnek:**
   - Sıcaklık parametrelerini ayarlayabilirsiniz
   - Problem özelliğine göre optimize edilebilir

---

### ❌ DEZAVANTAJLARI

1. **En Yavaş:**
   - 10,000 iterasyon: ~3 saniye
   - Büyük problemlerde (n>1000) çok yavaş

2. **Parametre Hassasiyeti:**
   - T₀, α değerleri kritik
   - Yanlış parametre = kötü sonuç
   - Deneme-yanılma gerekir

3. **Stokastik:**
   - Her çalıştırmada farklı sonuç
   - Reproducibility için seed gerekli

4. **Convergence Belirsiz:**
   - Ne zaman duracağını bilmek zor
   - Çok erken durma = kötü sonuç
   - Çok geç durma = zaman kaybı

---

### 📊 KOD YAPISI

```python
def simulated_annealing(ogrenciler, firmalar, T0=150, alpha=0.99, max_iter=10000):
    # 1. BAŞLANGIÇ
    current = ogrenciler.copy()
    best = current.copy()
    current_score = memnuniyet_skoru_hesapla(current)
    best_score = current_score
    
    T = T0  # Sıcaklık
    
    # 2. ANA DÖNGÜ
    for i in range(max_iter):
        # a) Komşu üret
        neighbor = generate_neighbor(current)
        neighbor_score = memnuniyet_skoru_hesapla(neighbor)
        
        # b) Skor farkı
        delta = neighbor_score - current_score
        
        # c) METROPOLİS KRİTERİ
        if delta > 0:
            # Daha iyi → Kabul et
            current = neighbor
            current_score = neighbor_score
            
            if neighbor_score > best_score:
                best = neighbor
                best_score = neighbor_score
        
        else:
            # Daha kötü → Olasılıkla kabul et
            probability = np.exp(delta / T)
            
            if np.random.rand() < probability:
                current = neighbor
                current_score = neighbor_score
        
        # d) Sıcaklığı düşür
        T = alpha * T
    
    return best, best_score
```

---

### 🎯 KULLANIM SENARYOLARI

**Simulated Annealing Ne Zaman Tercih Edilmeli?**

✅ **İdeal Durumlar:**
- **Kalite öncelikli** uygulamalar
- Kritik kararlar (offline hesaplama)
- Karmaşık çözüm uzayı
- Yerel optimumların çok olduğu problemler
- Zaman kısıtı yok

❌ **Uygun Olmayan Durumlar:**
- Gerçek zamanlı sistemler (çok yavaş)
- Basit problemler (overkill)
- Parametre ayarı yapılamıyorsa

---

### 📈 PERFORMANS

**Deneysel Sonuçlar (n=100, m=20):**
- **Süre:** 3.12 saniye
- **Memnuniyet Skoru:** 7,640
- **İyileştirme:** Greedy'den +400 puan (+5.5%)
- **İyileştirme:** Hill'den +60 puan (+0.8%)
- **Yerleşme Oranı:** 99%

**Convergence:**
```
Skor
8000│                    ┌────────
7500│              ┌─────┘
7000│         ┌────┘
6500│    ┌────┘
6000│────┘
    └────────────────────────────
    0  2000 4000 6000 8000 10000
           İterasyon
```

---

---

## 📊 3 ALGORİTMANIN KARŞILAŞTIRMASI

### Hız vs Kalite Trade-off

```
        HIZ (Saniye)
         0.02        2         3
    GREEDY -----> HILL ----> ANNEALING
      7,240      7,580       7,640
    
    ↑ Hızlı ama Düşük Kalite
    ↓ Yavaş ama Yüksek Kalite
```

### Özet Tablo

| Özellik | Greedy | Hill Climbing | Simulated Annealing |
|---------|--------|---------------|---------------------|
| **Mantık** | Açgözlü | Yerel arama | Stokastik global arama |
| **Süre** | 0.02 sn | 2 sn | 3 sn |
| **Skor** | 7,240 | 7,580 | 7,640 |
| **Karmaşıklık** | O(n log n) | O(iter×n) | O(iter×n) |
| **Kötü Çözüm Kabulü** | ❌ Hiç | ❌ Hiç | ✅ Evet (olasılıkla) |
| **Global Optimum** | ❌ Hayır | 🟡 Belki | ✅ Yaklaşır |
| **Başlangıç Bağımlılığı** | - | ✅ Yüksek | 🟡 Orta |
| **Kullanım** | Hız gerekli | Orta ölçek | Kalite kritik |

---

## 🎤 SUNUMDA NASIL ANLATALIM?

### Önerilen Akış:

1. **GREEDY (3 dakika):**
   - "En hızlı ama en basit"
   - GNO sıralaması görselini göster
   - 5 öğrencilik örneği adım adım yürüt
   - "Zeynep neden 3. tercihine yerleşti?" sorusunu sor

2. **HILL CLIMBING (3 dakika):**
   - "Greedy'yi iyileştirme arayışı"
   - Dağ metaforunu kullan
   - Ayşe-Zeynep SWAP örneğini göster
   - "Yerel maksimum tuzağı" kavramını açıkla

3. **SIMULATED ANNEALING (4 dakika):**
   - "Metal tavlama benzetmesi"
   - Metropolis formülünü yaz
   - Sıcaklık grafiğini göster
   - "Kötüyü neden kabul eder?" sorusunu cevapla

4. **KARŞILAŞTIRMA (2 dakika):**
   - 3 algoritmanın sonuçlarını yan yana koy
   - "Hangi durumda hangisini kullanmalıyız?"
   - Trade-off grafiğini göster

**Toplam: ~12 dakika**

---

## 🎯 SORU-CEVAP İÇİN HAZIR OLUN

**Olası Sorular:**

1. **"Neden Greedy her zaman kötü değil?"**
   → Çünkü GNO iyi bir heuristik. Çoğu durumda %90 optimal sonuç verir.

2. **"Hill Climbing neden takılır?"**
   → Sadece yukarı çıkar, aşağı inemez. Bazen aşağı inip yeniden çıkmak gerekir.

3. **"Simulated Annealing'de T₀=150 nereden geldi?"**
   → Deneysel olarak ayarlandı. Problem büyüklüğüne göre değişir.

4. **"3 saniye çok mu?"**
   → Offline sistemlerde normal. Gerçek zamanlı sistemler Greedy kullanır.

5. **"Hangisi en iyi?"**
   → Duruma göre! Hız → Greedy, Kalite → SA, Denge → Hill Climbing.

---

## 📝 ÖNEMLİ KAVRAMLAR (VURGULAYINIZ)

1. **Yerel vs Global Optimum**
2. **Exploration vs Exploitation**
3. **Metropolis Kriteri**
4. **Convergence (Yakınsama)**
5. **Trade-off (Hız-Kalite Dengesi)**
6. **Stokastik vs Deterministik**
7. **Komşuluk Fonksiyonu**
8. **Cooling Schedule**

---

**Bu metinleri sunumunuzda notlara yazabilir veya slaytlarda kısa kısa özetleyebilirsiniz!**
