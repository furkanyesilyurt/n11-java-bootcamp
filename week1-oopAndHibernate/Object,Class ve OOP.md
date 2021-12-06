# Class

* Java’da sınıf (class) kavramını doğada cins isimlere benzetebiliriz. Bir cins kendi başına belirli bir nesne değildir; ancak belirli türden nesnelerin ortak özelliklerini belirten soyut bir kavramdır. 
* Bir java sınıfının niteliklerini değişkenlerle (attributes, fields), davranışlarını metotlarla (fonksiyon, procedure) belirleriz. Başka bir deyişle, istediğimiz özeliklerini belirterek bir sınıf (cins-isim) tanımlarız.
* Classlar kod içerisinde ömürleri yoktur. Oluşturulacak sınıflar için birer şablon görevi görürler ve bellekte yer tutmazlar.

# Object

* Sınıf (class) soyut bir veri tipidir. Nesne (object) onun somutlaşan bir cismidir. Verileri saklayan ve bu veriler üzerinde işlem yapan metodları saklayan bileşenlerdir. 
* İçinde veri saklayan ve bu veriler üzerinde işlem yapacak olan metodlar bulunduran bileşenlerdir. Nesneler her uygulamada tekrar kullanılabilir. Nesne oluşturduğumuzda hafızada yer kaplar.

Aşağıda çeşitli amaçlar için kullanılan object metodları görülmektedir.

  **clone() :** Bu nesnenin aynısını kopyalar

  **equals(Object obj) :** obj nesnesi, bu nesneye eşit mi kontrolü yapar.

  **finalize():** İlgili nesne bellekten silinmeden hemen önce çağırılan yordam.

  **getClass() :** Bu nesnenin çalışma anında sınıf bilgilerini geri döner.

  **hashCode():** Bu nesnenin hash kodunu geri döner.

  **notify() :** Bu nesnenin bekleme havuzunda olan tek iş parçacığını(thread) uyandırır.

  **notifyAll() :** Bu nesnenin bekleme havuzundaki tüm iş parçacıklarını uyandırır.

  **toString() :** Bu nesnenin String tipinden ifadesini geri döner.

  **wait() :** O andaki iş parçacığının (thread) beklemesini sağlar, bu bekleme notify() veya notifyAll() yordamları sayesinde sona erer.

  **wait(long timeout) :** O andaki iş parçacığının belirtilen süre kadar beklemesini sağlar, bu bekleme notify() veya notifyAll() yordamları sayesinde de sona erebilir.

  **wait(long timeout, int nanos):** O andaki iş parçacığının belirtilen süre kadar beklemesini sağlar, bu bekleme notify() veya notifyAll() yordamları sayesinde de sona erebilir.

  

Class ve object'in ne olduğunu kısaca anlattıktan sonra Nesne Yönelimli Programlama(OOP)'nın ne olduğuna geçelim.

# Nesne Yönelimli Programlama

* Yazılımların karmaşıklığı ve boyutları sürekli arttığı ancak belli bir nitelik düzeyi korumak için gereken bakımın maliyeti zaman ve çaba olarak daha da hızlı arttığı 1960lı yılların sonlarına doğru ortaya çıkan bir programlama yaklaşımıdır. Bir dil, kütüphane veya framework değildir. 
* OOP, aynı zamanda Soyutlama (Abstraction), Kapsülleme (Encapsulation), Miras Alma (Inheritance) ve Çok biçimlilik (Polymorphism) gibi yazılımın bakımını ve aynı yazılım üzerinde birden fazla kişinin çalışmasını kolaylaştıran kavramları da yazılım literatürüne kazandırmıştır.

Kısaca bu 4 temel ilkeden de bahsedelim.

  **1-Abstraction(Soyutlama):**

  Detayların, karmaşıklığın azaltılması anlamına gelmektedir.Bir nesnenin neleri içermesi gerektiğine odaklanmayı ve önemli bilgileri gösterirken istenmeyen ayrıntıları gizlemeyi amaçlar. Büyük projelerde yapılan çalışmaların hepsini bilmek gereksizdir.Projelerin detaylarında kaybolmak yerine işlevleri göstermeye odaklanmak projeyi daha iyi anlamamızı sağlar.

  **2-İnheritance(Kalıtım):**

  Türkçe karşılığı ‘miras alma, kalıtım’dır. Inheritance; bir nesnenin özelliklerinin başka nesneler tarafından kullanılabilmesine olanak sağlar. Sınıflar arasında hiyearşik bir yapı kurabilmek için kullanılır. Inheritance bir sınıfın kendi özellikleri ve metotları yanı sıra kalıtım aldığım base(taban) sınıfın özellikleri ve metotlarına da sahip olabilmesidir.Ancak kalıtım alan sınıf herhangi bir özellik veya metoda sahip olmasa da olur.

  **3-Encapsulation(Kapsülleme):**

  Bir varlığı bütün olarak ele almak ve varlığın yapısını dışarıyla oluşabilecek sonuçlara karşı korumayı amaçlar.Bu mekanizma hakkında genel fikir basittir. Bir nesnede dışarıdan görünmeyen bir özelliğiniz varsa ve erişimi sağlayan yöntemlerle bir araya getirirseniz, belirli bilgileri gizleyebilir ve nesnenin iç durumuna erişimi kontrol edebilirsiniz.

  **4-Polymorphism(Çok Biçimlilik):**

  Genel olarak, birçok biçimde görünme yeteneği.OOP(Nesneye yönelik programlama)’da, polimorfizm, bir programlama dilinin veri türüne veya sınıfına bağlı olarak nesneleri farklı şekilde işleme yeteneğini ifade eder. Daha spesifik olarak, türetilmiş sınıflar için yöntemleri yeniden tanımlama yeteneğidir. OOP’de polimorfizmin en yaygın kullanımı, bir alt sınıf nesnesini belirtmek için bir üst sınıf referansı kullanıldığında ortaya çıkar.



## Kaynakça

* [https://sumeyyeturkmen.medium.com/4-temel-oop-prensibi-9bd4a36d35a1](https://sumeyyeturkmen.medium.com/4-temel-oop-prensibi-9bd4a36d35a1)
* [https://tr.wikipedia.org/wiki/Nesne_yönelimli_programlama](https://tr.wikipedia.org/wiki/Nesne_yönelimli_programlama)
* [https://furkanalaybeg.medium.com/nesne-yönelimli-programlama-oop-nedir-b6f805a9473f](https://furkanalaybeg.medium.com/nesne-yönelimli-programlama-oop-nedir-b6f805a9473f)
* [http://www.baskent.edu.tr/~tkaracay/etudio/ders/prg/java/ch03/class01.htm](http://www.baskent.edu.tr/~tkaracay/etudio/ders/prg/java/ch03/class01.htm)

