# Spring Boot Transaction

Transaction işlemi bir veya birden fazla sorguların(SQL) aynı süreçte işlem görmesidir.Method içerisindeki işlemlerin her biri başarılı olması durumunda commit edilmesi herhangi birinin başarısız olması ise işlemin tamamının başarısız olarak kabul edilerek rollback yapması olayıdır. Bu işlem bize veri bütünlüğünü sağlar.

Transaction bloğundaki işlemlerin hepsi başarılı olduğunda Transaction **Commit (Onaylama)** komutu çalışır ve değişiklikler veritabanında gerçekleşmiş olur; ancak bir hata varsa işleyiş bozulur ve transaction **Rollback (Geridönüş)** komutu çalışır, bu şekilde tüm işlemler geri alınır ve en başa dönülür. Böylece veri kaybına karşı bir çeşit koruma mekanizması oluşturulmuş olunur.

Transaction kavramı, ACID olarak tanımlanan aşağıdaki dört temel özellik ile tanımlanabilir;

**Atomicity,** Transaction işlemini bir bütün olarak görür. İşlem sırasında birden fazla veritabanı/tablodaki verinin güncellenmesi gerçekleşiyor ise tüm bunların hepsi birden başarılı olacaktır veya başarısız olacaktır. Herhangi bir sebepten dolayı hata alındığında işlem geçersiz olacaktır.

**Consistency,** Transaction işlemi sonucunda veritabanındaki verinin geçerli durumunun, bir sonraki geçerli duruma geçmesidir. Özetle Transaction tam anlamı ile gerçekleşinceye kadar (constraints, cascades, triggers) işlemden etkilenen verilerin değerlerinin bir önceki geçerli değeri vermesidir.

**Isolation,** Aynı anda aynı veri üzerinde birden fazla Transaction değiştirme gereksinimi olabilir. Transaction’ların birbirlerinin işlemlerinden etkilenmemesi için işlemler Seri olarak yapılması gerekir. Transaction sırasında ilgili ve etkilenecek veri setleri kilitlenir. Taki işlem başarılı ve başarısız olarak sonuç dönünceye kadar.

**Durability,** Transaction sırasında fiziksel veya işlemsel bir hata olması durumunda sistemin kendisini bir önceki geçerli veri durumuna döndürebilme kabiliyetidir.

## Transaction Yönetimi

Spring transaction yönetimi için iki yöntem sunar; *Programatik ve Deklaratif*

**Programatik yöntem,** Transaction işleminin başlatılıp sonlandırılması ve açık kalan bağlantıların kapatılması kodlarının içinde barındıran bir yöntemdir. Bu size aşırı esneklik sağlar ancak bakımı zordur

**Deklaratif yöntem,** Spring altyapısında bazı kurallar çerçevesinde Spring Container tarafından gerçekleştirilir.

> @Transactional Anotasyonu sayesinde yapılır

Sınıf yada metod düzeyinde gerçekleştirilir.Sınıf düzeyinde yazmış olduğunuz anatosyon sınıftaki tüm public metodları kapsar.

```
    @Override
    @Transactional(readOnly = false, propagation = Propagation.REQUIRED)
    public void ilKaydet(String ilAdi) {
	Il il = new Il();
	il.setId(7);
	il.setAdi(ilAdi);
	ilRepo.save(il);
    }
```

____________________________________

## Transaction Özellikleri

![](https://github.com/furkanyesilyurt/n11-java-bootcamp/blob/08ff6aecfc31916f9abdfc6c978eae7dd1dfa148/week3-transactionalAndMongoDb/transaction.png)

### A.Propagation 
Bu özellik ile yeni bir transaction açılıp açılmayacağına, mevcut bir transaction var ise kullanılıp kullanılmayacağına kara verilmesine sağlar.Bu kararı da yukarıda şemadaki parametrelere göre sağlar.

#### A1.Propagation.REQUIRED
Eğer mevcutta bir transaction var ise yeni bir transaction açmadan bu transactionu kullanır,Eğer transaction yoksa yeni bir transaction açar. @Transactional keywordu yazıldığında davranış şekli otomatik olarak “REQUIRED” dır.

#### A2.Propagation.SUPPORTS
Eğer bir transaction var ise o transaction u kullanır .Yok ise transaction’sız çalışır. Yeni bir transaction da açmaz.

#### A3.Propagation.MANDATORY
Eğer bir transaction yok ise exception fırlatır.

#### A4.Propagation.REQUIRES_NEW
Aktif bir transaction var ise bunu bekletir(Suspend), ve yeni bir transaction açar.

#### A5.Propagation..NOT_SUPPORTED
Eğer bir transaction var ise o transaction’u suspend edilir ve yen bir transaction da açmaz.

#### A6.Propagation.NEVER
Eğer bir transaction var ise exception fırlatır.

#### A7.Propagation.NESTED 
Bu parametre JDBC teknolojisin geliştirdiği savepoint ile beraber kullanır.Eğer bir transaction var ise paralelde başka bir transaction açar(Nested transaction) ve bu transaction rollback olurken diğer transaction devam eder .Eğer transaction yok ise “REQIRED” olarak çalışır. Save point teknolojisi kullanıldığı için sadece JDBC kaynak işlemlerinde çalışır.


### readOnly
Bu özellik true olarak set edildiğinde read-only transaction açılır. Veritabanında herhangi bir değişiklik yapılmayacak olan transactionlarda kullanılabilir.

### timeOut
Tanımlanan bu özellik sayesinde belirlenen süre içerisinde sorgunun sonucu gelmediğinde rollback işlemini gerçekleştirir.

### rollbackFor
Sizin belirlemiş olduğunuz class’a göre rollback işleminin yapılıp yapılmayacağını belirler. Belirlenen sınıfın Throwable sınıfından türetilmesi gerekir. Uncheck exception olarak fırlatılan (örn :NullPointerException, ArrayIndexOutOfBound) gibi hata sınıfları bu durumdan etkilenmez ve transaction tarafından rollback edilir.

### Isolation
Uygulama katmanında birden fazla transaction varsa her bir transaction altında yer alan iş parçacıklarının kullanacağı veriyi yönetmek için kullanılır.

____________________________________________

## Kaynakça

* [https://www.tutorialspoint.com/spring/spring_transaction_management.htm](https://www.tutorialspoint.com/spring/spring_transaction_management.htm)
* [https://bidb.itu.edu.tr/seyir-defteri/blog/2013/09/07/t-sql-de-transaction-yapisi-ve-kullanimi](https://bidb.itu.edu.tr/seyir-defteri/blog/2013/09/07/t-sql-de-transaction-yapisi-ve-kullanimi)
* [https://www.baeldung.com/transaction-configuration-with-jpa-and-spring](https://www.baeldung.com/transaction-configuration-with-jpa-and-spring)
* [https://medium.com/@omerfarukicen/spring-framework-transaction-yönetimi-9fbfdf2bb9c3](https://medium.com/@omerfarukicen/spring-framework-transaction-yönetimi-9fbfdf2bb9c3)
* [https://medium.com/@dururyener/transaction-yönetimi-ve-spring-boot-transactional-kullanımı-f894cc66c9d9](https://medium.com/@dururyener/transaction-yönetimi-ve-spring-boot-transactional-kullanımı-f894cc66c9d9)






