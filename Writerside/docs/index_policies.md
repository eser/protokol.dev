# Temel İlkeler

## Sürüm Kontrolü

Ana branch'imizin ismi `main` olacak şekilde `trunk-based` geliştirme yapıyoruz.
{collapsible="true" default-state="collapsed"}
: Her ne kadar `feature-based` branch'ler daha yetenekli yapılar gibi görünse de, kendimize dürüst olduğumuzda bu karmaşanın oluşturacağı derleme, ortam ve manual operasyon yükünü karşılamaya değecek bir yazılım geliştirme ihtiyacımızın olmaması gerekiyor.

: Bir noktadan sonra yönetilemez bir karmaşa haline gelecek branch sayısı, sürekli ana branch'e yaklaşmak için rebase ve test yükü, kullanıcı testlerinin yapılabilmesi için ortam kurulumları ve çalışmalar bittiğinde birleşecek feature'ların getireceği refactor zahmeti maalesef verimlilik sürecini oldukça baltalıyor.

: Buradaki `trunk-based` geliştirme tercihi her zaman çalışmaları ana branch'e yakın tutacak şekilde ufak, yönetilebilir ve merge-conflict'lerden daha uzak sağlıklı bir sürüm geçmişini sağlayacak bir mental-model'in oluşmasında da bize yardımcı oluyor. Geliştiriciler codebase'de küçük değişiklikler yapılmasına teşvik edildiği için büyük ölçekli refactor işlemlerinin ihtiyacı giderek azalıyor.


`Feature Branch` yerine `Feature Flag`leri kullanıyoruz.
{collapsible="true" default-state="collapsed"}
: Özellikle `trunk-based` geliştirme yaparken geliştirilmesi tamamlanan, ancak henüz kullanıcıların tümüne veya bir kısmına sunulmayacak geliştirmelerin kodun içinde yaşaması ve bir konfigurasyon aracılığı ile açılıp kapanmasını sağladığı için `Feature Flag`ler oldukça yararlı.

: `Feature Flag`ler bir özelliğin hızlıca geri çekilebilmesi, kontrollü özellik yayılımları, A/B testleri, sürekli entegrasyon ve sürekli ileri doğru veritabanı "migration" stratejileri için oldukça önem taşırlar.


Elimizdeki *her iş maddesi için* ana branch'e `pull request` açarak geliştirmelerimizi tamamlıyoruz.
{collapsible="true" default-state="collapsed"}
: `feature-based` yaklaşımda olduğu gibi her feature için bir branch oluşturup geliştirmeleri o branch altında tutmak yerine,
- Repo'ya yazmaya yetkimiz varsa, için bir branch oluşturup,
- Repo'ya yazma yetkimiz yoksa, oluşturduğumuz fork üzerinde,

: geliştirmeleri tamamlamalı ve `pull request` açarak ilerlemeliyiz.


Mümkün oldukça `cherry-pick` işlemlerinden kaçınıyoruz.
{collapsible="true" default-state="collapsed"}
: Doğrusal sürüm kontrol sistemlerinden Git ve benzeri dağıtık sürüm kontrol sistemlerine geçiş nedenlerimizden biri de `cherry-pick` gibi operasyonlardan kaçınmak ve bunun için branch yapılarını kullanmaktı.

: `cherry-pick` işlemi bir commit'i mevcut dalın tarihine ekler, sürüm geçmişinde kopukluklar oluşturur ve orijinal commit'in bağlamını veya bağımlılıklarını taşıdığı için sürüm geçmişinin tekrar yazılmasına neden olur. Bu nedenle bu işlemden sonra `fast-forward` dışında seçeneğimiz kalmaz ve ana branch'den kopya almış branch'leri rebase ederek alt branchleri güncel tutma imkanımız kalmaz.


## Deployment

## İletişim ve Kültür

Mümkün olduğunca `asenkron iletişim` kullanıyoruz.
{collapsible="true" default-state="collapsed"}
: Bilgilendirme, soru ve benzeri iletişim ihtiyaçlarımızı mümkün olan en "ortak" alanda, yazılı, okunması kolay ve detay-bilgi içermeyen bir biçimde sağlamalıyız. Böylelikle karşımızdaki insanlar takvim meşguliyetleri, saat-farklılıkları veya odaklanma ihtiyaçları gibi dezavantajları hissetmeksizin "uygun olduklarında" geri dönüş sağlayabilecekler.

Atıfta bulunalım.
{collapsible="true" default-state="collapsed"}
: Başka birinden aldığımız, gördüğümüz, işittiğimiz ve öğrendiğimiz kavramları kullanır veya paylaşırken bizim için konunun orijini olan kimselere atıfta bulunmamız oldukça önem arz ediyor.
