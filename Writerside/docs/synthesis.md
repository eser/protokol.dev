# Sentez

## Sürüm Kontrolü

1.1. Ana branch'imizin ismi `main` olacak şekilde `trunk-based` geliştirme yapıyoruz.
{collapsible="true" default-state="collapsed"}
: Her ne kadar `feature-based` branch'ler daha yetenekli yapılar gibi görünse de, kendimize dürüst olduğumuzda bu karmaşanın oluşturacağı derleme, ortam ve manual operasyon yükünü karşılamaya değecek bir yazılım geliştirme ihtiyacımızın olmaması gerekiyor.

: Bir noktadan sonra yönetilemez bir karmaşa haline gelecek branch sayısı, sürekli ana branch'e yaklaşmak için rebase ve test yükü, kullanıcı testlerinin yapılabilmesi için ortam kurulumları ve çalışmalar bittiğinde birleşecek feature'ların getireceği refactor zahmeti maalesef verimlilik sürecini oldukça baltalıyor.

: Buradaki `trunk-based` geliştirme tercihi her zaman çalışmaları ana branch'e yakın tutacak şekilde ufak, yönetilebilir ve merge-conflict'lerden daha uzak sağlıklı bir sürüm geçmişini sağlayacak bir mental-model'in oluşmasında da bize yardımcı oluyor. Geliştiriciler codebase'de küçük değişiklikler yapılmasına teşvik edildiği için büyük ölçekli refactor işlemlerinin ihtiyacı giderek azalıyor.


1.2. `Feature Branch` yerine `Feature Flag`leri kullanıyoruz.
{collapsible="true" default-state="collapsed"}
: Özellikle `trunk-based` geliştirme yaparken geliştirilmesi tamamlanan, ancak henüz kullanıcıların tümüne veya bir kısmına sunulmayacak geliştirmelerin kodun içinde yaşaması ve bir konfigurasyon aracılığı ile açılıp kapanmasını sağladığı için `Feature Flag`ler oldukça yararlı.

: `Feature Flag`ler bir özelliğin hızlıca geri çekilebilmesi, kontrollü özellik yayılımları, A/B testleri, sürekli entegrasyon ve sürekli ileri doğru veritabanı "migration" stratejileri için oldukça önem taşırlar.


1.3. Elimizdeki *her iş maddesi için* ana branch'e `pull request` açarak geliştirmelerimizi tamamlıyoruz.
{collapsible="true" default-state="collapsed"}
: `feature-based` yaklaşımda olduğu gibi her feature için bir branch oluşturup geliştirmeleri o branch altında tutmak yerine,
- Repo'ya yazmaya yetkimiz varsa, için bir branch oluşturup,
- Repo'ya yazma yetkimiz yoksa, oluşturduğumuz fork üzerinde,

: geliştirmeleri tamamlamalı ve `pull request` açarak ilerlemeliyiz.


1.4. Commit mesajlarını "Conventional Commits 1.0.0" standartına göre yazıyoruz.
{collapsible="true" default-state="collapsed"}
: Conventional Commits, commit mesajlarının daha iyi taranabilmesi ve geliştirme maddelerinin birbirinden ayrılabilmesi için yardımcı bir standart sunar. Detaylar: [conventionalcommits.org](https://www.conventionalcommits.org/tr/v1.0.0/)

: Kullandığımız tipler: `build`, `chore`, `ci`, `docs`, `feat`, `fix`, `perf`, `refactor`, `revert`, `style`, `test`.


1.5. Branch isimleri içerdiği geliştirmenin türü ve **iş maddelerinin** id'lerini taşır.
{collapsible="true" default-state="collapsed"}
: Branch'lerin hangi amaçla açıldığının takibini sağlamak için branch isimleri belirli bir biçimde olmalıdır. Buradaki biçim yine Conventional Commits'in tarif ettiği tip kategorizasyonu ile aynıdır. Feature geliştirmeleri için açılan branch'ler `feat/JIRA-4`, bugfix'ler için `fix/JIRA-12` ve benzerleri şekilde isimlendirilebilirler.


1.6. `cherry-pick` işlemlerinden kaçınıyoruz.
{collapsible="true" default-state="collapsed"}
: Doğrusal sürüm kontrol sistemlerinden Git ve benzeri dağıtık sürüm kontrol sistemlerine geçiş nedenlerimizden biri de `cherry-pick` gibi operasyonlardan kaçınmak ve bunun için branch yapılarını kullanmaktı.

: `cherry-pick` işlemi bir commit'i mevcut dalın tarihine ekler, sürüm geçmişinde kopukluklar oluşturur ve orijinal commit'in bağlamını veya bağımlılıklarını taşıdığı için sürüm geçmişinin tekrar yazılmasına neden olur. Bu nedenle bu işlemden sonra `fast-forward` dışında seçeneğimiz kalmaz ve ana branch'den kopya almış branch'leri rebase ederek alt branchleri güncel tutma imkanımız kalmaz.

: `Feature Flag`lerinin de desteği ile ana branch'de birleşen kod zaten `cherry-pick` edilmişçesine uygulamanın son sürümünü yansıtmalı ve olası "conflict"lerin çözülmüş bir kopyası olmalı. Eğer halen "birleşmiş sürüm"de sorunlar varsa, bunlar eski sürümleri değiştirerek değil, yeni bir commit ile yamalanmalıdır.


1.7. Sürüm numaraları için `semantic versioning` kullanıyoruz.
{collapsible="true" default-state="collapsed"}
: `semantic versioning` yani anlamsal sürümleme, sürüm numaralarının standartize edilebilmesi ve doğru kategorilendirilmesi için bir dizi yönlendirme sunar. Detaylar: [semver.org](https://semver.org/lang/tr/)


1.8. Sürümleri belirlemek için `tag` kullanıyoruz.
{collapsible="true" default-state="collapsed"}
: Kodun ana branch'de bulunan bir noktasından sürüm çıkabilmek için, ilgili commit id'ye bir tag ekleyerek ilerliyoruz.

: Bu sayede yayınlama aşamasında çalışan ve `continuous delivery` sağlayan pipeline'lar verilen tag'i `semantic versioning` araçları ile tanımlayarak nasıl bir paket çıkması gerektiğine karar verebilir hale geliyorlar.


## Sınama ve Yayınlama

2.1. `Continuous Integration`, `Continuous Delivery` ve `Continuous Deployment`'ı ayrı süreçler olarak ele alıyoruz.
{collapsible="true" default-state="collapsed"}
: `Continuous Integration` iletilen geliştirmenin projenin bütünü ile adaptasyonunu, `Continuous Delivery` sürümlerin paketlenip taşınabilir hale getirilmesini, `Continuous Deployment` ise ilgili sürümlerin ilgili ortamlara yüklenmesini hedeflediği için bu kavramları birbirinden izole halde tutmak iyi bir pratiktir.


2.2. `GitHub Actions` kullanıyoruz.
{collapsible="true" default-state="collapsed"}
: GitHub Actions `Continuous Integration` ve `Continuous Delivery` aşamalarında kullanılan pipeline'ların kod üzerinden tanımlanması, GitHub'ın sağladığı araçlarla takip edilebilmesi, bağımlılıkların güvenlik taramalarından geçirilmesi ve kolayca tekrar kullanılabilmesini sağlamaktadır.


2.3. `GitOps` kullanıyoruz.
{collapsible="true" default-state="collapsed"}
: GitOps bir `Continuous Deployment` çözümü olarak operasyonların da Git üzerinden kontrol edilebilmesi ve böylece mevcut uygulama altyapısının proje codebase'indeki yapı ile "senkron" kalmasını sağlar. GitOps, yükleme yapılan ortamlardaki gerçek durum ile geliştiricinin "planladığı durum"u senkronize etmesi açısından iyi bir pratiktir.


## İletişim ve Kültür

3.1. Mümkün olduğunca `asenkron iletişim` kullanıyoruz.
{collapsible="true" default-state="collapsed"}
: Bilgilendirme, soru ve benzeri iletişim ihtiyaçlarımızı mümkün olan en "ortak" alanda, yazılı, okunması kolay ve detay-bilgi içermeyen bir biçimde sağlamalıyız. Böylelikle karşımızdaki insanlar takvim meşguliyetleri, saat-farklılıkları veya odaklanma ihtiyaçları gibi dezavantajları hissetmeksizin "uygun olduklarında" geri dönüş sağlayabilecekler.

3.2. Atıfta bulunalım.
{collapsible="true" default-state="collapsed"}
: Başka birinden aldığımız, gördüğümüz, işittiğimiz ve öğrendiğimiz kavramları kullanır veya paylaşırken bizim için konunun orijini olan kimselere atıfta bulunmamız oldukça önem arz ediyor.
