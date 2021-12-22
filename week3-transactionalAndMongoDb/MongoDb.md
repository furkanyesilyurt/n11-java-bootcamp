# MongoDB Nedir?

MongoDB 2009 yılında geliştirilmiş açık kaynak kodlu bir NoSQL veritabanıdır. Bugün piyasada Cassandra, BigTable, Dynamo gibi birçok NoSQL veritabanı bulunmaktadır.

NoSQL ile ilişkili veritabanı sistemleri arasındaki en büyük fark ilişkisel veritabanı sistemlerinde veriler tablo ve sütunlar ile ilişkili bir şekilde tutulurken NoSQL’de json bir yapıda tutulmasıdır.

NoSQL sistemlerin avantajlarına değinmek gerekirse ilk olarak performans gösterilebilir. Okuma ve yazma işlemleri ilişkisel veritabanlarına göre çok daha hızlı olmaktadır. İkinci olarak ise NoSQL sistemler yatay olarak genişletilebilirler. Binlerce sunucu bir arada çalışarak inanılmaz derecedeki veriler üzerinde işlemler yapabilir.

Ayrıca eklemekte fayda var ki günümüzde Büyük Veri alanında yapılan çalışmalarda NoSQL sistemler yoğun olarak kullanılmaktadır.

![https://github.com/furkanyesilyurt/n11-java-bootcamp/blob/main/week3-transactionalAndMongoDb/mongodb.png](https://github.com/furkanyesilyurt/n11-java-bootcamp/blob/main/week3-transactionalAndMongoDb/mongodb.png)

### Dezavantajları

MongoDB performans olarak MySQL, Oracle ve SQL Server gibi veritabanlarından hızlı olsa da kuralları ve standardı olmadığından dolayı verilerin önemli olduğu uygulamalarda kullanılmaması veya kullanılırken dikkatli olunması gerekir.

MongoDB ile karmaşık sorguların hazırlanması SQL’e göre daha zor olabilir.



Aşağıda MongoDb'de kullanılan komutlar, açıklamaları ve basit örneklendirmeleri görülmektedir.

## TEMEL İŞLEMLER

| Komutlar             | Açıklama                                                     | Örnek                                                        |
| -------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **db**               | Kullanılan veri tabanını görüntülemek için kullanılan komuttur. | _db_                                                         |
| **use**              | Yeni bir veri tabanı oluşturmak veya var olan başka bir veri tabanını kullanmamızı sağlayan komuttur. | use <database>                                               |
| **show**             | Veri tabanlarını veya koleksiyonları listemelek için kullanılır. Böylece kayıtlı olan veri tabanları ve boyutları, koleksiyonlar listelenir. | show databases                            show *collections* |
| **drop()**           | Veri tabanında var olan koleksiyonu silmek için kullanılır.  | db.collection_name.drop()                                    |
| **dropDatabase()**   | Kayıtlı olan veri tabanını silmek için kullanılır. Önce silmek istediğimiz veri tabanının içerisine girip daha sonra sileriz. | use <database>    db.dropDatabase()                          |
| **createCollection** | Koleksiyon oluşturmak için kullanılır. Önce istediğimiz veri tabanının içine girip daha sonra o veri tabanına koleksiyonun ismini vererek yeni bir koleksiyon oluşturmuş oluruz. | use <database> db.createCollection(“collection_name”)        |



## VERİ EKLEME İŞLEMLERİ

| Komutlar                       | Açıklama                                                     | Örnek                                                        |
| ------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **db.collection.insert()**     | Koleksiyona veri eklemek için kullanılır. Eklenmesi istenen koleksiyonun adı verilir ve JSON formatında bir veri verilir. | db.collection_name.insert({"firstName":"osman", "lastName":"yılmaz2"}) |
| **db.collection.insertOne()**  | Koleksiyona tek bir veri eklemek için kullanılır. Eklenmesi istenen koleksiyonun adı verilir ve JSON formatında veri yazılır. | db.collection_name.insertOne({"firstName":"osman", "lastName":"yılmaz2"}) |
| **db.collection.insertMany()** | Koleksiyona birden fazla veri eklemek için kullanılır. Eklenmesi istenen koleksiyonun adı verilir ve eklenmek istenen JSON formatında veriler verilir. | db.collection_name.insertMany({"firstName":"osman", "lastName":"yılmaz2"}{"firstName":"furkan", "lastName":"yesilyurt"}) |



## SORGU İŞLEMLERİ

| Komutlar                 | Açıklama                                                     | Örnek                                                        |
| ------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **db.collection.find()** | Koleksiyon içerisindeki verileri seçmek için kullanılır. Parantez içerisi boş bırakılırsa tüm verileri seçer. Eğer koşul belirtirsek koşula uygun alanları seçer. Örneğin name alanı Esmanur olanları seçme işlemi yanda görüldüğü gibidir. | db.collection_name.find({}) db.collection_name.find( {"name":"Esmanur"} ) |
| **in[]**                 | Verilen alana bakar ve belirtilen değerler içerisinde geçenleri seçer. Örneğin name alanında A ve E geçenleri seçme işlemi: | db.collection_name.find( { "name": { $in: [ "A", "E" ] } } ) |
| **and**                  | Seçilmesi istenen veriye birden fazla koşulu ve ile bağlayabiliriz. Koşullar arasına virgül koymak yeterlidir. Örneğin name’i Esmanur ve age’si 25'ten küçük olanları seçme işlemi: | db.collection_name.find( { "name": "Esmanur", "age": { $lt: 25} } ) |
| **or**                   | Seçilmesi istenen veriye birden fazla koşulu veya ile bağlayabiliriz. Örneğin name’i Esmanur veya age’si 25'ten küçük olanları seçme işlemi: | db.collection_name.find({$or:[{"name":"Esmanur"},{"age":{ $lt:25}} ]}) |
| **$lt**                  | Verinin istenen koşuldan küçük olanlarını almaya yarar.      |                                                              |
| **$gt**                  | Verinin istenen koşuldan büyük olanlarını almaya yarar. Örneğin age alanı 15'ten büyük 25'ten küçük olanları seçme işlemi: | db.collection_name.find( { "age": { $gt: 15, $lt: 25 } } )   |



## VERİ GÜNCELLEME İŞLEMLERİ

| Komutlar                          | Açıklama                                                     | Örnek                                                        |
| --------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **db.collection.update()**        | Koleksiyon içerisindeki verileri güncellemek için bu komut kullanılır. Önce hangi kaydı güncellemek istediğimiz belirtilir. Ardından ise hangi alanı güncellemek istediğimiz belirtilir. Örneğin id’si 2 olanın name’ini Mehmet olarak günceller. | db.collection_name.update({"id": 2}, {$set: {"name": "Mehmet"}}) |
| **db.collection.updateOne()**     | Koleksiyonda tek bir veriyi güncellemek için kullanılır.     | db.collection_name.updateOne(    {"name": "Esmanur"},  {$set: {"name": "Ayşe"}}) |
| **db.collection.updateMany()**    | Koleksiyonda birden fazla veriyi güncellemek için kullanılır. | db.collection_name.updateMany( {}, {$set: {"surname": "KILIÇ"}}) |
| **db.collection.findOneUpdate()** | Koleksiyon içerisindeki ilk veriyi yakalar ve onu günceller. | db.collection_name.findOneUpdate( {"age":23},{$set :{ "name":"Ayşe"} ) |
| **db.collection.replaceOne()**    | id alanı dışında bir verinin tüm içeriğini değiştirmek için kullanılır. Değiştirilen alanlar öncekiyle aynı olmayabilir yani alanlar eklenip çıkarılabilir. Başta değiştirilmek istenen verinin id’si belirtilir daha sonra yeni veri yazılır. | db.collection_name.replaceOne( { "id": "1" }, { "id": "1",  city: [  { name: "İstanbul"},  { name: "Ankara"} ] }) |



## VERİ SİLME İŞLEMLERİ

| Komut                             | Açıklama                                                     | Örnek                                                        |
| --------------------------------- | :----------------------------------------------------------- | ------------------------------------------------------------ |
| **db.collection.remove()**        | Bir koleksiyon içerisindeki veriyi silmek için kullandığımız komuttur. Silinmesi istenen verinin koşulu verilir ve ona göre silme işlemi yapılır. Eğer koşul belirtmezsek tüm veriler silinir. | db.collection_name.remove({}) db.collection_name.remove({"id":1}) |
| **db.collection.deleteOne()**     | Bir koleksiyon içerisindeki verilen koşula göre eşleşen tek veriyi siler. Age alanı 23 olan tek veri silinir: | db.collection_name.deleteOne( { "age": 23} )                 |
| **db.collection.deleteMany()**    | Bir koleksiyon içerisindeki verilen koşula göre eşleşen tüm verileri siler. Age alanı 23 olan tüm veriler silinir: | db.collection_name.deleteMany( { "age": 23} )                |
| **db.collection.findOneDelete()** | Koleksiyon içerisindeki ilk veriyi yakalar ve onu siler. Age alanı 23 olan ilk veriyi yakalar ve siler: | db.collection_name.find**OneDelete**( {"age":23} )           |



### Kaynakça

* [https://medium.com/baakademi/mongodb-shell-komutları-f3a3c96fd20](https://medium.com/baakademi/mongodb-shell-komutları-f3a3c96fd20)

* [https://vizyonergenc.com/icerik/temel-mongodb-komutlari](https://vizyonergenc.com/icerik/temel-mongodb-komutlari)

* [https://www.gtech.com.tr/mongodb-nedir-nerelerde-kullanilir/](https://www.gtech.com.tr/mongodb-nedir-nerelerde-kullanilir/)

* [https://medium.com/@berkekurnaz/nedir-bu-mongodb-994a94a9d1df](https://medium.com/@berkekurnaz/nedir-bu-mongodb-994a94a9d1df)

* [https://www.yusufsezer.com.tr/mongodb-nedir/](https://www.yusufsezer.com.tr/mongodb-nedir/)

  