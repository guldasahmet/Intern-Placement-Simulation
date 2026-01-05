# 🎓 Stajyer Yerleştirme Simülatörü

Modern ve interaktif bir stajyer-firma eşleştirme sistemi. Farklı algoritmaları karşılaştırarak en optimal yerleştirme çözümünü bulur.

## 🚀 Özellikler

- **Otomatik Veri Üretimi**: Rastgele öğrenci ve firma verileri oluşturma
- **3 Farklı Algoritma**:
  - 🎯 Greedy (Açgözlü) Algoritma
  - ⛰️ Hill Climbing (Tepe Tırmanışı)
  - 🔥 Simulated Annealing (Benzetimli Tavlama)
- **Dinamik Simülasyon**: Firmaların öğrencileri reddetme senaryosu
- **Karşılaştırmalı Analiz**: Algoritma performans raporları
- **Modern GUI**: PyQt5 ile geliştirilmiş kullanıcı dostu arayüz

## 📋 Gereksinimler

```bash
pip install pandas PyQt5
```

## 🎮 Kullanım

```bash
python main_gui.py
```

## 📊 Algoritma Karşılaştırması

Program, her algoritmanın:
- Memnuniyet skorunu
- Çözüm süresini
- İterasyon sayısını
- Yerleşen öğrenci sayısını

karşılaştırmalı olarak gösterir.

## 📁 Proje Yapısı

```
├── main_gui.py                        # Ana GUI uygulaması
├── veri_olustur.py                    # Veri seti oluşturucu
├── algo_greedy.py                     # Greedy algoritması
├── algo_heuristic_hill_climbing.py    # Hill Climbing algoritması
├── algo_heuristic_annealing.py        # Simulated Annealing algoritması
├── proje_ogrenciler.csv               # Öğrenci verileri
└── proje_firmalar.csv                 # Firma verileri
```

## 🎯 Proje Amacı

Bu proje, kombinatoryal optimizasyon problemlerinde farklı algoritmaların performansını karşılaştırmayı ve stajyer yerleştirme sürecini simüle etmeyi amaçlamaktadır.

## 👨‍💻 Geliştirici

2025-2026 Python Programlama Dönem Projesi

---

⭐ Projeyi beğendiyseniz yıldız vermeyi unutmayın!
