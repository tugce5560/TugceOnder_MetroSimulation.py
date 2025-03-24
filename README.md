# Metro Simulation Projesi

## Proje Başlığı ve Kısa Açıklama

**Metro Simulation** adlı bu proje, şehir içi metro hatları ve istasyonları arasında en hızlı ve en az aktarmalı rotaları bulmak için kullanılan bir simülasyon sistemidir. Kullanıcılar, iki istasyon arasındaki rotaları, aktarma sayısını en aza indirgeyerek veya en hızlı şekilde hesaplayarak öğrenebilirler. Bu proje, kullanıcıların farklı metro hatları arasında geçiş yaparken ihtiyaç duyduğu en verimli rotaları bulmalarını sağlayacak şekilde tasarlanmıştır.

---

## Kullanılan Teknolojiler ve Kütüphaneler

Bu projede aşağıdaki Python kütüphaneleri kullanılmıştır:

- **heapq**: 
  - A* algoritmasında kullanılan **priority queue** (öncelikli kuyruk) için kullanılmıştır. Bu kütüphane, sıralı bir şekilde öğeleri en küçükten en büyüğe doğru depolamak için kullanılır ve A* algoritmasının en hızlı yol bulma mantığını destekler.
  
- **collections**:
  - **deque**: BFS algoritmasında, ilk giren ilk çıkar (FIFO) mantığıyla çalışan bir veri yapısı olarak kullanılmıştır. BFS algoritmasının doğru çalışabilmesi için bu yapı gereklidir.
  - **defaultdict**: Anahtarlar için varsayılan değerler belirlemek amacıyla kullanılmıştır, bu da istasyonlar arasında yapılan bağlantıları düzenli tutmamıza yardımcı olur.

---

## Algoritmaların Çalışma Mantığı

### 1. BFS (Breadth-First Search) Algoritması

**BFS** algoritması, bir ağdaki tüm düğümleri en kısa yol ile keşfetmek için kullanılan en temel arama algoritmalarından biridir. Bu algoritma, seviyeli bir yapıyı takip ederek arama yapar ve her seferinde bir istasyonun komşularını keşfeder. Bu şekilde en az aktarmalı rotayı bulur.

- **BFS'in Çalışma Mantığı**:
  - Başlangıç istasyonundan başlanır ve her istasyonun komşuları sırayla gezilir.
  - İstasyonlar, aktarma sayısını minimize etmek için sırayla ziyaret edilir.
  - BFS, bir istasyondan hedef istasyona ulaşana kadar bir seviyede, yani aktarmada bir artış olmadan ilerler.
  
- **Neden BFS Kullanıyoruz?**
  - BFS, en az sayıda aktarma ile hedefe ulaşmayı garanti eder çünkü her seviyede komşu istasyonlara sırasıyla ulaşılır.

### 2. A* (A-star) Algoritması

**A*** algoritması, genellikle harita üzerinde en kısa yolu bulmak için kullanılan bir algoritmadır ve BFS'in daha optimize edilmiş bir versiyonudur. Bu algoritma, her istasyonu değerlendiren bir **fiyatlandırma fonksiyonu** kullanır ve hedef istasyona olan uzaklığı tahmin ederek daha hızlı bir çözüm bulur.

- **A* Algoritmasında Kullanılan Fiyatlandırma**:
  - A* algoritmasında kullanılan temel bileşen, her istasyonun "g-cost" (geçilen mesafe) ve "h-cost" (hedefe olan tahmini mesafe) değerlerinin toplamıdır.
  - Bu şekilde en kısa yol hızlı bir şekilde bulunur.

- **Neden A* Kullanıyoruz?**
  - A* algoritması, özellikle büyük veri setlerinde (çok sayıda istasyon ve bağlantı olduğunda) çok daha verimli bir yol bulma sağlar.
  - Hedefe ulaşma yolunu tahmin ederek, gereksiz yolları eleyip en hızlı sonucu verir.

---

## Örnek Kullanım ve Test Sonuçları

Projenin temel fonksiyonlarının nasıl çalıştığını anlamak için aşağıdaki test senaryolarına göz atabilirsiniz.

```python
# Örnek kullanım
metro = MetroAgi()

# İstasyonlar ekleyelim
metro.istasyon_ekle("K1", "Kızılay", "Kırmızı Hat")
metro.istasyon_ekle("K2", "Ulus", "Kırmızı Hat")
metro.istasyon_ekle("M1", "AŞTİ", "Mavi Hat")
metro.istasyon_ekle("T1", "Batıkent", "Turuncu Hat")

# Bağlantılar ekleyelim
metro.baglanti_ekle("K1", "K2", 4)
metro.baglanti_ekle("K2", "M1", 5)
metro.baglanti_ekle("T1", "K2", 6)

# En az aktarmalı rota
rota = metro.en_az_aktarma_bul("K1", "M1")
print("En az aktarmalı rota:", " -> ".join(i.ad for i in rota))

# En hızlı rota
rota, sure = metro.en_hizli_rota_bul("K1", "M1")
print(f"En hızlı rota ({sure} dakika):", " -> ".join(i.ad for i in rota))
