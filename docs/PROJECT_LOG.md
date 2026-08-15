# Proje Günlüğü -Military Border Security
## 15.08.2026 -Proje Kurulumu

### Yapılanlar
- Veri seti analiz edildi: 7070 train/ 1756 valid/ 873 tesr görüntüsü
- Sınıf dağılımı çıkarıldı: Drone(5115), Vehicle(2130), Person(408)- ciddi sınıf dengesizliği tespit edildi
- GPU kontrolü yapıldı: yerel makine Nvdia GPU yok, eğitim için Google Colab kullanılmasına karar verildi
- Git + Github rreposu oluşturuldu: military-border-security
- ROS2 workspace iskeleti (src, docs) Git takibine alındı, ilk commit yapıldı
- VS Code eklentileri kuruldu: PYlance, Gitlens, ROS, Docker, YAML, Jupyter

### Kararlar ve Gerekçeler
- Veri seti (mbs_ds) ile kod (mbs_ws) ayrı tutuldu- büyük veri dosyalarının Git reposunun şişiememesi için
- Person sınıfının azlığı nedeniyle augmentation + class weighting stratejisi planlandı

### Sıradaki adımlar
- Google Drive 'a veri seti yükleme tamamlanacak
- Colab notebook kurulumu (Drive bağlantısı + ultralytics YOLO kurulumu)
- Baseline model eğitimi


## 15.08.2026 - Baseline MOdel Eğitimi(v1)
- Yolov11n modeli, augmentation olmadan, 50 epoch eğitildi(Google Colab, Tesla T4 GPU, ~1.8 saat)
- Parametreler: imgsz= 640, batch=16, patience=10

### Sonuçlar(mAP50/Recall)
| Sınıf | mAP50 | Recall |
|---|---|---|---|---|----|
| Drone | 0.972 | 0.973  |
|Vehicle| 0.611 | 0.549  |
|Person | 0.396 | 0.333  |
| Genel | 0.660 | 0.618  |

### Analiz
- Sınıf dengesizliği hipotezi doğrulandı: en az örneğe sahip sınıf (Person, 408 bbox) en düşük performansı verdi
- Person recall'ı %33 - modelin gerçek insan örneklerinin 2/3'ünü kaçırdığı anlamına geliyor, sınır güvenliği senaryosunda kabul edilemez seviyede

### Karar
- Bir sonraki adımda Person sınıfına yönelik veri augmentation (Albumentation) ve/veya class weighting uygulanacak
- Hedef: Person mAP50'yi en az %60+ seviyesine çıkartmak