# Ad-Soyad: Hüseyin Can Akkaya E-posta: hcaakkaya@gmail.com

# 🏥 Fiziksel Tıp ve Rehabilitasyon Verisi Üzerinde EDA & Veri Hazırlama

Bu proje, **2235 gözlem ve 13 özellikten oluşan** Fiziksel Tıp ve Rehabilitasyon veri seti üzerinde  
**Keşifsel Veri Analizi (EDA)** ve **Özellik Mühendisliği (Feature Engineering)** uygulamalarını kapsamaktadır.  
Amaç: **Hedef değişken olan `TedaviSuresi` etrafında veriyi temiz, tutarlı ve modele hazır hale getirmek.**

---

## 📂 Veri Seti Genel Bilgi

- **Gözlem Sayısı:** 2235
- **Özellik Sayısı:** 13
- **Hedef Değişken:** `TedaviSuresi` (Tedavi süresi)

### Sütunlar

- `HastaNo`, `Yas`, `Cinsiyet`, `KanGrubu`, `Uyruk`, `KronikHastalik`,  
  `Bolum`, `Alerji`, `Tanilar`, `TedaviAdi`, `TedaviSuresi`,  
  `UygulamaYerleri`, `UygulamaSuresi`

---

## 🛠️ Yapılan Adımlar

### 1. Veri Keşfi

- Veri `pandas` ile Excel’den yüklendi.
- `.head()`, `.info()`, `.describe()` ile temel yapısı incelendi.
- Eksik değerler `isnull().sum()` ile analiz edildi.

### 2. Veri Temizleme

- Sütun isimlerindeki boşluklar giderildi.
- `TedaviSuresi` ve `UygulamaSuresi` string değerlerden sayısala dönüştürüldü:
  - `"5 seans"` → `TedaviSuresi_num_seans = 5`
  - `"20 dakika"` → `UygulamaSuresi_num_dk = 20`
- Eksik değer doldurma stratejileri:
  - **Mod** ile: `Cinsiyet`, `Bolum`, `Tanilar`
  - **"Bilinmiyor"** ile: `KanGrubu`, `KronikHastalik`, `Alerji`, `UygulamaYerleri`

### 3. Yaş Grupları

- `pd.cut()` ile yaşlar kategorilere ayrıldı (`0-15`, `16-25`, `26-39`, `40-59`, `60-74`, `75+`).
- Ek olarak manuel fonksiyon ile `Child`, `Young Adult`, `Middle Age` gibi etiketler verildi.

### 4. Görselleştirmeler

- Histogram: Tedavi süresi dağılımı
- Countplot: Cinsiyet, Kan grubu, Uyruk vb. kategorik dağılımlar
- Korelasyon Matrisi & Heatmap: sayısal sütunlar arası ilişki
- Scatterplot: Yaş ↔ Tedavi süresi, Uygulama süresi ↔ Tedavi süresi
- Boxplot: Cinsiyet ↔ Tedavi süresi karşılaştırması

### 5. Feature Engineering

- **Kronik Hastalıklar:**
  - `KronikHastalikSayisi` (hastalık adedi)
  - `Diyabet`, `Hipertansiyon` binary flagleri
- **Tanılar:**
  - `TaniSayisi` (tanı adedi)
  - `OmurgaSorunu` (Bel/Boyun/Omurga varsa 1)
- **Alerji:** `AlerjiVarMi` (Var=1, Yok=0)
- **Uygulama Yerleri:** `UygulamaYeriSayisi`
- **Tedavi Yoğunluğu:** `TedaviYogunlugu = TedaviSuresi_num_seans × UygulamaSuresi_num_dk`
- **One-Hot Encoding:** `Cinsiyet`, `KanGrubu`, `Uyruk`, `Bolum`, `Alerji`, `UygulamaYerleri` dummy değişkenlere çevrildi.

### 6. Temizlenmiş Veri Seti

- Gereksiz sütunlar (`HastaNo`, `TedaviSuresi`, `UygulamaSuresi`) çıkarıldı.
- Sonuç: **`rehab_model_ready.csv`** – modele hazır, temiz ve dönüştürülmüş veri seti.

---

## 📊 Çıkarımlar

- Tedavi süresi dağılımı **sağa çarpık**, çoğu hasta kısa sürede tedavi oluyor.
- Kronik hastalık ve tanı sayısı arttıkça **tedavi süresi uzuyor**.
- Bölüm ve yaş gruplarına göre tedavi yoğunluklarında belirgin farklılıklar var.
- Tedavi süresi ile tedavi yoğunluğu arasında **yüksek korelasyon** bulundu.

---

## 🚀 Kullanım

```bash
# Repoyu klonla
git clone https://github.com/<HCAAKKAYA>/<pusula_huseyin_can_akkaya>.git
cd <pusula_huseyin_can_akkaya>

# Gereksinimleri yükle
pip install -r requirements.txt

# Notebook'u aç
jupyter notebook main.ipynb
```

---

## 📦 Gereksinimler

- Python 3.8+
- pandas, numpy, matplotlib, seaborn

```bash
pip install pandas numpy matplotlib seaborn
```

---

## 📈 Sonraki Adımlar

- Regresyon & ağaç tabanlı modellerle tahminleme
- Model performansı (MAE, RMSE) ölçümü
- NLP tabanlı özellik mühendisliği (Tanılar & Kronik Hastalıklar için)

---

## 👤 Yazar

- **Hüseyin Can Akkaya**  
  Yönetim Bilişim Sistemleri Yüksek Lisans Öğrencisi  
  [LinkedIn](https://linkedin.com/in/hcakkkaya) | [GitHub](https://github.com/HCAKKAYA)
