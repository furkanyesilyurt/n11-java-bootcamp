# Spring Core

Java ile geliştirme yapmayı kolaylaştıran Core Container, AOP, Data Access, Web gibi modüllerden oluşan bir framework-kütüphanedir.

Spring platformunda yer alan Spring Boot, Spring Data, Spring MVC, Spring Batch, Spring Security gibi projelerin temelinde Spring framework yer alır.

Spring framework temelinde ise Spring Core modülünde yer alan IoC Container vardır.

## IoC Conteiner

Sınıflardan nesne oluşturmak, oluşan nesnelerin ihtiyaç duyduğu nesneleri bağlamak ve yönetmek için kullanılan prensip ve desenlerinin bir araya geldiği araçlardır.

**NOT:** Tasarım prensibleri (DRY, SOLID, SoC ,KISS, YAGNI) uyulması gereken kuralları belirtirken, tasarım desenleri bu kuralların uygulamalarıdır.

Spring framewok **I**nversion **o**f **C**ontrol prensibini uygulamak için genellikle **D**ependency **I**njection tasarım desenini kullanır.

# Spring Boot

**Spring Boot,** temel olarak framework ile aynı anlama gelmez ancak onun bir uzantısıdır. Spring framework, bize yapının sağladığı kütüphaneleri kullanmamızı sağlarken Spring Boot’un temel amacı kod uzunluğunu kısaltmak ve web geliştirmeyi en kolay şekilde bize sunmaktır. Ayrıca Spring uygulamasını kurmak için yapmamız gereken temel konfigürasyonları bizim için gerçekleştirir. Yani Spring Boot, Spring Framework’un kolaylaştırılmış halidir diyebiliriz.

Ancak yine de dikkat etmek gerekir ki, Spring Boot bir uygulama sunucusu ya da web container değildir. Otomatik olarak kod üretmez sadece gerekli ayarlamaları bizim için otomatik hale getirir.,

**JPA,** açılımı Java Persistence API olan bu kavram ORM yapısını bizim için çağırır ve kullanır. Kalıcı olarak veri tutma gereği duyduğumuz zamanlarda kullanırız.

**POJO Class,** model sınıflarımızdaki veri yapılarıyla alakalı bir kavramdır. Tablolardaki kayıtları ORM’den faydalanarak POJO model sınıflarına dönüştürürüz. Pojo classımızı @Entity etiketiyle işaretlediğimizde veritabanında oluşturulacak bir yapı olduğunu söylemiş oluruz. JPA sayesinde kayıtlarımız veritabanıyla doğrudan ilişkilendirilir.

# Spring Data

**Spring Data**, **Spring Framework** ekosisteminde yer alan bir kütüphanedir. Interfaceler aracılığı ile veri iletişimini hazır metodlarla birlikte kullanmamıza aracılık etmektedir.

Projemizde var olan entitymizin alanlarına göre dinamik olarak metodlar oluşturup sql söz dizimine gerek kalmadan veri alabilmemiz mümkün olup veritabanı bağımsız çalışmaktadır.

Çok karıştırılan bir nokta ise Hibernate’in yerini aldığı. Bu oldukça yanlış bir düşünce **Spring Data** Hibernate ile birlikte çalışabilir ancak yerini alan bir yapı değildir. **Spring Data**‘nın çalışması için bir JPA aracına ihtiyac bulunmaktadır.