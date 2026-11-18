# BIL545 Veri Madenciliğinde İleri Konular · Proje 1

**Konu 9.7:** Hava kalitesi ve kirlilik epizotları: Pekin PM2.5 verisiyle kirlilik epizodu tespiti ve birliktelik analizi

**Dönem:** 2026–2027 Güz · **Öğretim üyesi:** Dr. Selma Güzel · Üsküdar Üniversitesi, Fen Bilimleri Enstitüsü

---

## 🎥 Proje sunum videosu

> **Sunum video bağlantısı (Google Drive):** [BURAYA_GOOGLE_DRIVE_VIDEO_LINKINI_YAPISTIRIN]

*(Erişim izni: "Bağlantıya sahip olan herkes görüntüleyebilir".)*

---

## 👥 Grup (4 kişi · temel kapsam + Ek paket 1)

**Grup adı:** _(doldurun)_ · **İletişim sorumlusu:** _(doldurun)_

| Öğrenci adı soyadı | Öğrenci no | Sorumlu olduğu alt başlıklar (defterde ve sunumda) |
| :--- | :--- | :--- |
| **Süleyman Balsak** | 254312022 | **Bölüm 1:** 1.1 veri künyesi, 1.2 keşifsel analiz, 1.3 eksiklik analizi, 1.5 sızıntı deneyi ve baseline, 1.6 kategorik kodlama, 1.7 Weka ZeroR / J48 kontrolü |
| **Seda Erten** | 254312008 | **Bölüm 2:** 2.1 beş modelin `TimeSeriesSplit` ile karşılaştırması, 2.2 karar ağacının yorumu (`export_text`), 2.3 iç içe CV ile optimist yanlılık, 2.4 McNemar testi, 2.5 Proje 2'ye aktarılacak model |
| **İlkin Urcan** | 244329078 | **Bölüm 3:** 3.1 veri küpü (roll-up / drill-down) ve Simpson paradoksu, 3.2 Apriori ile hedefe yönelik kurallar ve ilgi ölçütleri, 3.3 Weka Apriori kontrolü |
| **Aslıhan Semiz Varlı** | 254329024 | **Ek paket 1:** `ccp_alpha` budama eğrisi, rastgele orman doyum eğrisi (1–500 ağaç, OOB ve test), rastgele sütunla Gini ve permütasyon önemi |

Ayrıntılı katkı beyanı (kod, analiz, yorum, sunum hazırlığı) defterin sonundaki **Katkı beyanı** bölümündedir.

---

## 📊 Veri kümesi

- **Ad:** Beijing PM2.5 Data (PRSA), UCI Machine Learning Repository
- **Kaynak:** Liang, X. vd. (2015). Assessing Beijing's PM2.5 pollution: severity, weather impact, APEC and winter heating. *Proceedings of the Royal Society A*, 471, 20150257.
- **İçerik:** 1 Ocak 2010 – 31 Aralık 2014, saatlik ≈43.800 kayıt; PM2.5 (ABD Büyükelçiliği) ve meteoroloji ölçümleri (Pekin Başkent Havaalanı)
- **Hedef:** kirlilik epizodu = PM2.5 > 75 µg/m³ (Çin GB 3095-2012, 24 saatlik II. sınıf sınırı)
- **Lisans:** CC BY 4.0
- **Veri depoda yok.** Defterin ilk veri hücresi veriyi doğrudan UCI'dan indirir:
  `https://archive.ics.uci.edu/ml/machine-learning-databases/00381/PRSA_data_2010.1.1-2014.12.31.csv`

---

## ▶️ Defterin çalıştırılması

1. `proje1/BIL545_Proje1_Beijing_PM25.ipynb` dosyasını Google Colab'da açın (**Dosya → Not defteri yükle** ya da GitHub sekmesi).
2. **Çalışma zamanı → Tümünü çalıştır.** İlk hücre `mlxtend` paketini kurar, kütüphane sürümlerini yazdırır ve tohumu (`SEED = 42`) sabitler.
3. Defter, Weka kontrolleri için `beijing_weka.arff` ve `beijing_apriori.arff` dosyalarını üretip indirir.
   - **Weka sınıflandırma:** Explorer → Classify → ZeroR ve J48, Cross-validation, Folds = 10
   - **Weka Apriori:** Associate → Apriori; `lowerBoundMinSupport=0.05`, `metricType=Confidence`, `minMetric=0.5`, `numRules=1000`, `car=True`
4. Toplam çalışma süresi Colab ücretsiz katmanında birkaç dakikadır.

---

## 🧭 Değerlendirme protokolü

- Son %20 (zamansal) dokunulmayan test kümesi; model seçimi ve karşılaştırmalar ilk %80'de.
- Geliştirme verisinde `TimeSeriesSplit(n_splits=5, gap=24)`; veri zaman serisi olduğu için karıştırılmaz.
- Bütün ön işleme `Pipeline` içinde; sonuçlar ortalama ± standart sapma.
- Ölçütler: F1 (pozitif sınıf: epizot) ve dengeli doğruluk.
- İki modelin farkı: dokunulmayan test kümesinde McNemar testi (Dietterich, 1998).

---

## 📌 Sonuç özeti

_(Defter çalıştırıldıktan sonra doldurulacak: baseline ve en iyi modelin F1 ± std değeri, sızıntı deneyinin sonucu, karıştırılmış bölme ile zamansal bölme farkı, McNemar sonucu, öne çıkan birliktelik kuralları, Proje 2'ye aktarılan model.)_

---

## 📁 Dizin yapısı

```text
├── README.md                     # Grup, veri, çalıştırma, sonuç özeti, katkı
├── proje1/
│   └── BIL545_Proje1_Beijing_PM25.ipynb # Kod, çıktılar ve bütün yazılı cevaplar
└── proje2/                       # Proje 2 teslimi
```

---

## 🤖 Yapay zekâ beyanı

_(Hangi araç, hangi aşamada ve ne için kullanıldı. Ayrıntısı defterdeki Yapay zekâ beyanı bölümünde.)_
