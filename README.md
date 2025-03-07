Dağıtık Sistemler İçin Spring Boot + Nginx + PostgreSQL + Redis
Bu proje, yük dengeleme, önbellekleme, yüksek erişilebilirlik ve ölçeklenebilirlik gibi temel dağıtık sistem prensiplerini uygulayarak modern bir mikro servis mimarisi oluşturmayı hedeflemektedir. Docker Compose kullanılarak, tüm bileşenler tek bir komut ile ayağa kaldırılabilir ve birbirleriyle entegre bir şekilde çalışacak şekilde yapılandırılmıştır.

Proje Bileşenleri ve Görevleri
Nginx (Yük Dengeleyici)

Kullanıcı isteklerini arka planda çalışan Spring Boot servisleri arasında dengeli bir şekilde dağıtır.
Failover desteği ile, bir servis kapandığında istekleri ayakta kalan servislere yönlendirerek sistemin sürekliliğini sağlar.
Reverse Proxy olarak çalışarak, istemcilerin direkt backend sunucularıyla iletişime geçmesini engeller ve güvenliği artırır.
Spring Boot (Backend Servisleri - 2 Replika)

RESTful API olarak çalışır ve istemcilerin taleplerini işler.
2 farklı konteynerde replikasyonlu olarak çalıştırılır, böylece yatay ölçeklenebilirlik sağlanır.
PostgreSQL ve Redis ile entegre çalışarak veritabanı işlemlerini yönetir ve önbellek mekanizmasını kullanır.
PostgreSQL (Veritabanı Sunucusu)

Veri tutarlılığı ve güvenilirliği sağlamak için ilişkisel veritabanı olarak kullanılır.
Spring Boot uygulaması ile bağlantılı çalışarak veri saklama ve yönetimini gerçekleştirir.
Redis (Önbellekleme Sunucusu)

Sık erişilen verilerin hızlı bir şekilde getirilmesini sağlar, böylece PostgreSQL üzerindeki yükü azaltır.
Veri saklama süresi (TTL - Time To Live) belirlenerek gereksiz veri yükü önlenir ve sistem performansı optimize edilir.
Dağıtık sistemlerde sık kullanılan key-value tabanlı bir önbellekleme mekanizması sağlar.
Projenin Avantajları
Modüler Yapı: Bileşenler birbirinden bağımsız olarak çalıştığı için esneklik sunar.
Yüksek Erişilebilirlik: Bir servis başarısız olduğunda diğer servisler çalışmaya devam eder.
Ölçeklenebilirlik: Yeni Spring Boot replikaları eklenerek sistem kolayca genişletilebilir.
Performans Artışı: Redis kullanımı sayesinde veritabanına yapılan istekler azaltılır ve yanıt süreleri iyileştirilir.
Kolay Yönetim: Docker Compose ile tüm sistemin tek komutla ayağa kaldırılması sağlanır.
Bu mimari, dağıtık sistemler, yük dengeleme, önbellekleme, yüksek erişilebilirlik ve mikro servis gibi konseptleri uygulamak isteyen geliştiriciler için güçlü bir temel sunmaktadır.


 Proje İçeriği
  Nginx (nginx.conf)

Gelen HTTP isteklerini Spring Boot uygulamasına yönlendirir.
Yük dengelemesi yaparak birden fazla backend servisi yönetir.
Özel hata sayfaları tanımlıdır.
  Spring Boot (app)

PostgreSQL veritabanı ile bağlantılıdır.
Redis önbellekleme mekanizmasını kullanır.
İki replikasyonlu olarak çalışır.
 PostgreSQL (db)

Spring Boot uygulamasının veritabanı olarak kullanılır.
Docker volume ile kalıcı veri saklama özelliğine sahiptir.
 Redis (redis_cache)

Spring Boot tarafından cacheleme için kullanılır.
Uygulama performansını artırır.

mvn clean package -U Ne Yapar?
Bu komutun parçalara ayırarak anlamını inceleyelim:

mvn clean
 Maven’in target/ klasörünü temizler.
 Önceki derleme (build) dosyalarını ve eski bağımlılıkları siler.

mvn package
 Projeyi derler (compile).
 Tüm bağımlılıkları (dependencies) çözer ve gerekli dosyaları toplar.
 JAR veya WAR dosyası oluşturur (target/ klasörü içinde).

-U (Force Update - Bağımlılıkları Güncelle)
 Maven, lokal cache'den bağımsız olarak bağımlılıkları sıfırdan indirir.
 Eğer bağımlılıkların yeni bir sürümü varsa, bunları indirir ve projeye dahil eder


1️ Komutun Bileşenleri
docker-compose up
 docker-compose.yml dosyasında tanımlanan tüm servisleri başlatır.
 Gerekli olan Docker imajlarını indirir (eğer eksikse).
 Tüm container’ları çalıştırır.

--build
 Docker imajlarını yeniden oluşturur.
 Eğer Dockerfile veya kodlarda bir değişiklik yaptıysanız, eski imajları günceller.
 Eski imajları silmeden doğrudan yenisini oluşturur.

-d (Detached Mode - Arka Planda Çalıştır)
 Servisleri arka planda (background) çalıştırır.
 Terminali kilitlemez, komut çalıştırıldıktan sonra terminali kullanmaya devam edebilirsiniz.

2️ Ne İşe Yarar?
 Özetle:
Bu komut Docker Compose kullanarak aşağıdaki işlemleri gerçekleştirir:
 Tüm servisleri başlatır (docker-compose.yml dosyasındaki).
 Güncellenmiş Docker imajlarını oluşturur (--build ile).
 Container’ları arka planda çalıştırır (-d ile)

![image](https://github.com/user-attachments/assets/bba9d69c-9d9d-45da-ba06-1d538e4d174e)






