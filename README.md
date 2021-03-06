# Bu yazi dizisi 3 bolumden olusmaktadir

- Jmeter nasil calistirilir ? [Repo](https://github.com/coderaction/jmeter-first-run) 
- Jmeter bir endpoint'e nasil istek gonderilir? [Repo](https://github.com/coderaction/jmeter-rest-api-load-test) 
- Jmeter Auth token kullanilan bir endpointte token alinip diger apilere nasil otomatik bir sekilde verilir?  

# Load Test Nedir neden kullaniriz ?

Birim ve entegrasyon testleri kodun islevsel olarak dogru olmasini saglarken, yuk testi de ayni derecede onemli olan performansini olcer.Kodda ki darbagozin nerede oldugunu, uygulamanin verimli bir sekilde olceklenmesini, uygulamanin yanit verme suresinin ve veriminin ne oldugunu yuk testlerinde gorebiliriz.

## Apache Jmeter ile Test Plani olusturalim

Simdi adim adim bir endpoint'e post atmayi deneyelim...


## Adim 1

Test planına sağ tıklayın ve Add> Threads (Users)> Thread Group'u seçin. Bir test planında en az 1 Konu Grubu olmalıdır.

[![](https://github.com/coderaction/jmeter-rest-api-load-test/blob/main/images/thread%20group.png?raw=true)]()

Daha sonra asagida ki gibi bir gorsel ile karsilasacaksiniz 


[![](https://github.com/coderaction/jmeter-rest-api-load-test/blob/main/images/jmater-thread-group.png)]()

## Adim 2 

1 - Number of Threads(users) 50 kullanici olsun ve sisteme surekli olarak req gondersin 

> Number of Threads (users): Hedef server’a bağlanan kullanıcı veya bağlantı sayısını simüle eder. Örneğin; Number of Threads (users) 1000 olarak ayarlarsak; JMeter, test edilen hedef server’a 1000 kullanıcı isteği oluşturacak ve simüle edecektir.

2 - Ramp-Up period (in seconds) Bunu tanimladigimizda maximum kullaniciya (1.de tanimladigimiz degere) kac saniye de ulasmak istedigini belirtmis oldugun alan oluyor

> Tüm kullanıcıların sisteme girmesi ve testin sonlanması için geçen süredir. Örneğin; 1000 kullanıcı için ramp-up time 100s olarak ayarlanırsa server’a her bir saniyede 10 kullanıcı giriş yapmış olur. 50s olarak ayarlanırsa her saniyede sisteme 20 kullanıcı giriş yapmış olacaktır.

3 - Scheduler Configuration alaninda testin kac kez veya ne kadar sureyle calistirmak isteediginizi belirttiginiz bir alan bulunuyor 

> Loop Count: Testin kaç kez koşulacağını tanımlar. Örneğin; thread group:100, loop count:10 olan bir testte 100 kullanıcı da hedef server’a 10 kere bağlanmasını simüle eder. Yani server’a 1000 kullanıcı bağlanmış olacaktır.

## Adim 3 

Artik bir api'ye post atma islemine gecebiliriz. Oncelikle http requeset page olusturmamiz gerekiyor,

[![](https://github.com/coderaction/jmeter-rest-api-load-test/blob/main/images/httpRequesetJmeter.png)]()

 Olusturmus oldugumuz http request uzerinden artik post islemleri gerceklestirebiliriz
 burada onemli adimlardan birisi base url ile istek atilacak endpoint adresini ayirmaniz. Ornek vermem gerekirse 

https://www.milliyet.com.tr/pembenar/ bir endpoint'e get isteginde bulunmak istiyorsunuz 

Server Name or Ip: www.milliyet.com.tr 
Path Alanina: /pembenar

olarak yazmaniz gerekiyor ornek olarak 

[![](https://github.com/coderaction/jmeter-rest-api-load-test/blob/main/images/http-request.png)]()

Eğer benim gibi Body JSON gönderiyorsanız. Test Plan >Add > Config Element > HTTP Header Manager oluşturup “Content-Type” olarak application/json girin.

[![](https://github.com/coderaction/jmeter-rest-api-load-test/blob/main/images/httpheadermanager.png)]()

[![](https://github.com/coderaction/jmeter-rest-api-load-test/blob/main/images/httpHeaderManagercontentType.png)]()

## Adim 4 

Artik islemlerimiz tamam requeest gonderip responslari alabilirz, responslari alip analiz edebilmemiz icin Thread Group Listener’lar eklememiz gerekiyor.

- Aggregate Graph
- View Result in Table
- View Results Tree gibi…

> bu repo icerisinde bulunan jmx uzantili dosya aslinda yukari da hazirlamis oldugumuz yapinin kaydedilmis halidir, sizde jmter'i calistirip open diyerek bu dosyayi acabilir dogrudan kullanabilirsiniz.

> Ben suanda View Result Tree ekliyorum.

[![](https://github.com/coderaction/jmeter-rest-api-load-test/blob/main/images/viewResultTree.png)]()

Daha sonrasinda jmeter'imizi calistiralim. 

[![](https://github.com/coderaction/jmeter-rest-api-load-test/blob/main/images/jmeterviewresulttreee.png)]()


Yesil renkler requesti gondermis oldugunuz isteklerin basarili istekleri kirmizilar ise basarisiz istekleri nitelendirir.

**Sampler Result:** Web server tarafindan dondurulen datalari gosteriyor. 
**Request:** Bu sekmeyi tikladiginizda body ve header sekmeleri karsiniza cikiyor ve ayrica gondermis oldugunuz tum datayi da buradann gorebilirsiniz

**Response Data:** Alinan verileri formatli olarak sizlere gosterir.


### Todos
 - Thread Group Listener tiplerini bir arkadas anlatabilirse sevinicem.
 - Online bir endpoint bulunup (ibb endpointleri olur) jmx dosyasi duzenlenebilir
 - Jmeter ile sonuclari nasil yorumlariz yazilmasi gerekiyor



