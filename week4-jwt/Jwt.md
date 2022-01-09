# JSON Web Token nedir?

JSON Web Token (JWT), iletişim yapan birimler arasındaki veri alışverişinin güvenli bir şekilde sağlanması için bir JSON nesnesi (token) kullanarak daha kompakt ve bilginin kendini kendini betimlediği bir yol sunan endüstri standardıdır (RFC 7519). Oluşturulan token, dijital olarak imzalandığı için doğrulanabilir ve güvenilirdir.

**Kompakttır:** Boyutunun küçük olması sayesinde URL üzerinden gönderilebilir, POST parametresi olarak eklenebilir veya HTTP başlığı içerisinde yer alabilir. Kompakt olmasının diğer bir avantajı ise aktarımın hızlı gerçekleşmesidir.

**Kendi-kendini betimler:** Token içerisinde isteği yapan kullanıcı ile ilgili gerekli bütün bilgi mevcuttur. Bu sayede kimliklendirme için veri tabanında birden fazla sorgu yapılması engellenmiş olur. Daha fazla detaylı bilgi için JWT Handbook‘a bakabilirsiniz.

## Kullanım Alanları

JWT’nin en yaygın kullanıldığı senaryo oturum yönetimidir. Kullanıcı uygulamaya giriş yaptığında kendisine bir token verilir. Kullanıcı, tokenın yetkileri doğrultusunda uygulamayı kullanır. JWT’nin kullanıldığı başka oturum yönetimi çözümü de Single Sign On (SSO) özelliğidir.

JWT’nin başka, ve faydalı, bir kullanım alanı da uygulama ve kullanıcı arasında güvenli veri paylaşımıdır. Tokenlar imzalanabildiğinden, ve bu imza bütünlük doğrulama için kullanılabildiğinden, isteklerin manipüle edilip edilmediği doğrulanabilir.

## Neden JWT?

Simple Web Token (SWT) ya da Security Assertion Markup Language (SAML) gibi standartlar varken neden JWT kullanmalıyız?

1. JWT, JSON kullanıyor. JSON, XML formatından daha az efektif veri taşıdığından encode edildiğinde boyut olarak bir JWT token, bir SAML tokendan daha küçük olur.
2. JWT X.509 sertifikalar ile private/public imzalama ve HMAC ile simetrik imzayı desteklerken, SWT sadece HMAC ile imzalamayı, SAML tokenlar ise XML dijital imzaları public/private anahtar kullanarak imzalamayı destekliyor. Fakat bir XML dijital imzalamayı “hatasız” implement etmek, JWT implementasyonuna göre epey zordur.
3. Bir geliştirici olarak XML parse etmeyi, JSON parse etmeye tercih eden pek azdır.
4. JWT boyut olarak küçük ve performanslı çalıştığından, özellikle mobil cihazlarda, genel olarak tüm kullanıcı cihazlarında, işlemesi daha az maliyetlidir.

## JWT Yapısı

JWT ile üretilen token Base64 ile kodlanmış 3 ana kısımdan oluşmaktadır. Bunlar Header(Başlık), Payload(Veri), Signature(İmza) kısımlarıdır.

![]()

```json
{
    "alg": "HS256", (1)
    "typ": "JWT" (2)
}
```

1- Veri bütünlüğünü korumak için kullanılacak cryptotic algoritmayı belirtir.

2- Bir JWT nesnesi olduğunu belirtir

````json
{
  "sub": "1234567890",
  "name": "John Doe",
  "iat": 1516239022
}
````

Yukarıdaki JWT payload içindeki userId alanı eşsiz kullanıcı kodunu, expire token zaman aşımı anını, roles ise kullanıcı yetkilerini temsil etmektedir. Bir token içinde expire alanı olması zorunlu değil, yine roles alanı olması da zorunlu değil fakat eşsizlik ve aidiyeti temsil etmek için userId gibi bir alan olması gerekiyor.

Payload içine ne koyulacağı tamamen geliştiricisine bağlı fakat RFC 7519 birtakım isteğe bağlı alan adını standartlaştırmıştır.

````
HMACSHA256(
base64UrlEncode(header) + “.” +
base64UrlEncode(payload),
)
````

3 parçadan oluşan JWT’nin son parçası JWT imzasıdır. İmza kısmı token üreticisi ve tüketicisi arasındaki veri bütünlüğünü garanti etmektedir. İmza oluşturulurken JOSE başlığında tanımlı algoritma kullanılmaktadır.
