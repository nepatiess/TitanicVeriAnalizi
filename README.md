<img src="https://raw.githubusercontent.com/nepatiess/TitanicVeriAnalizi/refs/heads/main/titanicpng.png" >

# 🚢 Titanic Veri Analizi Projesi

## 📝 Proje Hakkında

Bu proje, 1912 yılında batan RMS Titanic gemisindeki yolcuların hayatta kalma durumlarını analiz eden kapsamlı bir veri bilimi çalışmasıdır. **Pandas** kullanarak veri temizleme, **Seaborn** ile görselleştirme ve istatistiksel analiz teknikleri uygulanmıştır.

### 📊 Proje İstatistikleri
- **Toplam Yolcu:** 891
- **Toplam Sütun:** 12
- **Yolcu Sınıfı:** 3 (1st, 2nd, 3rd)
- **Oluşturulan Grafik:** 8

---

## 🛠️ Kullanılan Teknolojiler

| Teknoloji | Versiyon | Kullanım Amacı |
|-----------|----------|----------------|
| **Python** | 3.8+ | Ana programlama dili |
| **Pandas** | Latest | Veri işleme ve analiz |
| **NumPy** | Latest | Sayısal hesaplamalar |
| **Seaborn** | Latest | İstatistiksel görselleştirme |
| **Matplotlib** | Latest | Grafik çizimi |
| **Jupyter Notebook** | Latest | Etkileşimli geliştirme ortamı |

---

## 🚀 Kurulum ve Çalıştırma

### 1️⃣ Google Colab ile (Önerilen - En Kolay Yöntem)

> ✅ **Google Colab kullanarak herhangi bir kurulum yapmadan projeyi çalıştırabilirsiniz!**

1. [Google Colab](https://colab.research.google.com) sayfasını açın
2. **Dosya → Not Defteri Yükle** seçeneğini tıklayın
3. `titanic_analiz.ipynb` dosyasını yükleyin
4. **Çalışma Zamanı → Tümünü Çalıştır** ile projeyi başlatın

### 2️⃣ Yerel Kurulum (Opsiyonel)

> ℹ️ **Bilgi:** Yerel bilgisayarınızda çalıştırmak için Python 3.8+ yüklü olmalıdır.

```bash
# 1. Gerekli kütüphaneleri yükleyin
pip install pandas numpy seaborn matplotlib jupyter

# 2. Jupyter Notebook'u başlatın
jupyter notebook

# 3. titanic_analiz.ipynb dosyasını açın
```

---

## 📊 Veri Seti Bilgileri

### Sütun Açıklamaları

| Sütun Adı | Açıklama | Veri Tipi |
|-----------|----------|-----------|
| `PassengerId` | Yolcu benzersiz kimlik numarası | int |
| `Survived` | Hayatta kalma durumu (0 = Hayır, 1 = Evet) | int |
| `Pclass` | Bilet sınıfı (1 = 1st, 2 = 2nd, 3 = 3rd) | int |
| `Name` | Yolcu adı | object |
| `Sex` | Cinsiyet | object |
| `Age` | Yaş | float |
| `SibSp` | Gemideki kardeş/eş sayısı | int |
| `Parch` | Gemideki ebeveyn/çocuk sayısı | int |
| `Ticket` | Bilet numarası | object |
| `Fare` | Yolcu ücreti | float |
| `Cabin` | Kabin numarası | object |
| `Embarked` | Biniş limanı (C = Cherbourg, Q = Queenstown, S = Southampton) | object |

### Eksik Veriler

> ⚠️ **Dikkat:** Veri setinde eksik değerler bulunmaktadır!

- **Age:** ~177 eksik değer (Medyan ile dolduruldu)
- **Cabin:** Çok fazla eksik (Projede kullanılmadı)
- **Embarked:** 2 eksik değer (Mode ile dolduruldu)

---

## 🔬 Analiz Adımları

### 1. Veri Yükleme ve İnceleme
- Titanic veri setini URL'den yükleme
- İlk 5-10 satırı görüntüleme (`df.head()`)
- Genel bilgileri kontrol etme (`df.info()`)
- İstatistiksel özet çıkarma (`df.describe()`)

### 2. Veri Temizleme

**Age Sütunu:**
```python
# Yaş medyanını hesapla
yas_medyan = df['Age'].median()

# Eksik yaşları doldur
df['Age'].fillna(yas_medyan, inplace=True)
```

**Embarked ve Fare:**
- Embarked: En sık geçen değer (mode) ile doldurma
- Fare: Medyan değer ile doldurma

### 3. Özellik Mühendisliği

**Yaş Grupları Oluşturma:**

```python
def yas_grubu(yas):
    if yas <= 12:
        return 'Çocuk'
    elif yas <= 18:
        return 'Genç'
    elif yas <= 60:
        return 'Yetişkin'
    else:
        return 'Yaşlı'

df['Yas_Grubu'] = df['Age'].apply(yas_grubu)
```

- **Çocuk:** 0-12 yaş
- **Genç:** 13-18 yaş
- **Yetişkin:** 19-60 yaş
- **Yaşlı:** 60+ yaş

### 4. Gruplama Analizi

```python
# Cinsiyete göre
df.groupby('Sex')['Survived'].mean()

# Sınıfa göre
df.groupby('Pclass')['Survived'].mean()

# Yaş grubuna göre
df.groupby('Yas_Grubu')['Survived'].mean()
```

### 5. Görselleştirmeler

1. **Countplot:** Cinsiyete göre hayatta kalma
2. **Countplot:** Sınıfa göre hayatta kalma
3. **Boxplot:** Sınıf ve bilet fiyatı ilişkisi
4. **Barplot:** Yaş grubuna göre hayatta kalma oranı
5. **Heatmap:** Sınıf ve cinsiyet kombinasyonu

---

## 📈 Önemli Bulgular

### 🎯 Ana Sonuçlar

#### Cinsiyete Göre Hayatta Kalma
- 👩 **Kadınlar:** %74 hayatta kaldı
- 👨 **Erkekler:** %19 hayatta kaldı
- **Sonuç:** "Women and children first" kuralı açıkça uygulanmış!

#### Sınıfa Göre Hayatta Kalma
- 💎 **1. Sınıf:** %63 hayatta kaldı
- 🎩 **2. Sınıf:** %47 hayatta kaldı
- 👷 **3. Sınıf:** %24 hayatta kaldı
- **Sonuç:** Zenginlik hayatta kalmada büyük avantaj sağlamış!

#### Yaş Grubuna Göre Hayatta Kalma
- 👶 **Çocuklar:** En yüksek hayatta kalma oranı
- 👨 **Yetişkinler:** Orta düzey hayatta kalma
- 👴 **Yaşlılar:** En düşük hayatta kalma oranı

#### En Şanslı ve Şanssız Gruplar
- ✅ **En Şanslı:** 1. sınıf kadınlar (%96)
- ❌ **En Şanssız:** 3. sınıf erkekler (%14)

---

## 📊 Görselleştirme Örnekleri

### 1. Cinsiyete Göre Hayatta Kalma
- **Grafik Tipi:** Countplot
- **X Ekseni:** Cinsiyet (male/female)
- **Hue:** Survived (0/1)
- **Sonuç:** Kadınların büyük çoğunluğu kurtarıldı

### 2. Sınıfa Göre Hayatta Kalma
- **Grafik Tipi:** Countplot
- **X Ekseni:** Pclass (1/2/3)
- **Hue:** Survived (0/1)
- **Sonuç:** 3. sınıfta ölüm oranı çok yüksek

### 3. Bilet Fiyatı Dağılımı
- **Grafik Tipi:** Boxplot
- **X Ekseni:** Pclass (1/2/3)
- **Y Ekseni:** Fare (Bilet Ücreti)
- **Sonuç:** 1. sınıf biletleri 10 kat daha pahalı

### 4. Isı Haritası
- **Grafik Tipi:** Heatmap
- **Satırlar:** Pclass
- **Sütunlar:** Sex
- **Değerler:** Hayatta kalma oranı
- **Sonuç:** Sosyo-ekonomik statü ve cinsiyet kombinasyonu kritik!

---

## 🔍 Teknik Detaylar

### Kullanılan Pandas Fonksiyonları
```python
pd.read_csv()           # Veri yükleme
df.head()               # İlk satırları görme
df.info()               # Genel bilgi
df.describe()           # İstatistiksel özet
df.isnull().sum()       # Eksik veri sayısı
df.fillna()             # Eksik veri doldurma
df.groupby()            # Gruplama
df.pivot_table()        # Pivot tablo
df.apply()              # Fonksiyon uygulama
```

### Kullanılan Seaborn Fonksiyonları
```python
sns.countplot()         # Sayma grafiği
sns.boxplot()           # Kutu grafiği
sns.barplot()           # Çubuk grafiği
sns.heatmap()           # Isı haritası
sns.set_style()         # Stil ayarı
```

---

## 📚 Kaynaklar

### Veri Seti
- **Kaynak:** [Kaggle - Titanic Dataset](https://www.kaggle.com/c/titanic/data)
