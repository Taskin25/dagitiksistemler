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
