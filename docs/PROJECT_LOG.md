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