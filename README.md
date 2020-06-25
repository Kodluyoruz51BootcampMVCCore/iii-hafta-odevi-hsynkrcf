# III-hafta-odevi


1.Task vs process- task vs Thread vs .. ve c# task vs thread vs .. kıyaslamalarını ve task haricinde diğer yöntemler nelerdir araştırınız.
2.Extension Nedir? --> Extra paket ekleme. <br/>
3.SQLite, bunu doğru şekilde (en güncel yol ile) nasıl kullanmalıyız? (Aktif halde kullanıp uygulama)



## Task Kıyaslamalar

### Task Nedir ?

Task sınıfı, bir değer döndürmeyen ve genellikle zaman uyumsuz olarak yürütülen tek bir işlemi temsil eder. Yani bir işlemi asenkron zamandan bağımsız yapmak için bunu kullanıyormuşuz.
İşlemleri art arda yapmaktansa birbirinden bağımsız task yaratıp birbirine paralel işlem yaratmak. Bu da bize zamandan tasarruf sağlayacaktır.

### Thread Nedir ?

Aynı process ortamında birden fazla iş yürütme imkanı sağlar. Bir process’in çalışmaya başlaması ile birlikte bir thread (main thread) oluşturulur ve process içerisinde birden fazla (multi-thread ) oluşturulabilir. 

#### TASK vs Thread
`Thread` daha düşük düzeyli bir kavramdır: doğrudan bir iş parçacığına başlıyorsanız, iş parçacığı havuzunda yürütmek yerine ayrı bir iş parçacığı olacağını bilirsiniz.
`Task` kodun nerede çalıştırılacağı" nın bir özetinden daha fazlasıdır - gerçekten sadece "gelecekte bir sonucun vaadi" dir.

Yani Task daha gelişmiş bir yapıdadır.

#### TASK vs Process

Processes and threads are the mechanics, task is more conceptual. You can queue a chuck of work to run asynchronously, on windows with .NET for example, this gets run on a thread from the thread pool.

#### TASK vs ValueTask

Net birşey bulamadım en iyisini microsoft açıklar.
[https://docs.microsoft.com/tr-tr/dotnet/api/system.threading.tasks.valuetask-1?view=netcore-3.1]: 

#### TASK vs Parallel

Bir developerın yaptığı test ile karşılaştım sonuçları aşağıda :)
- Parallel.ForEach is quicker than Task.WhenAll. Parallel itself is synchronous.
- Parallel.ForEach is multiple threads solution while Task.WhenAll will probably share threads. If tasks share the same thread, they are just pieces of the thread and will need more time to complete the tasks.
- Because they are both concurrencies, so keep an eye on thread-safe issues.

#### Genel olarak, mümkün olan her yerde daha yüksek düzeyde soyutlama kullanmanızı tavsiye ederim; Modern C# kodunda nadiren açıkça kendi iş parçacığını başlatmanız gerekir.
![All](https://neharustagiblog.files.wordpress.com/2014/09/blog4.png)

## VS Extensions
Visual Studio uzantılarını yüklemek ve yönetmek için **Uzantıları Yönet** iletişim kutusunu kullanın.**Uzantıları Yönet** iletişim kutusunu açmak için **Uzantıları > Yönet Uzantıları**'nıseçin. Veya arama kutusuna **Uzantılar** yazın ve **Uzantıları Yönet** seçin.

![Extension](https://docs.microsoft.com/tr-tr/visualstudio/ide/media/finding-using-visual-studio-extensions/extensions-and-updates.png?view=vs-2019)

### Uzantıları bulma ve yükleme
**Visual Studio Marketplace'ten** uzantılar veya Visual Studio'da Uzantıları Yönet iletişim kutusundan yükleyebilirsiniz.
Visual Studio içinden uzantıları yüklemek için:
1. **Uzantıları > Yönet Uzantıları'ndan**, yüklemek istediğiniz uzantıyı bulun. (Uzantının adını veya bölümünü biliyorsanız, Arama penceresinde arama yapabilirsiniz.)
2. **Download (İndir)** seçeneğini belirleyin.
Uzantı yüklemek için zamanlanır. Visual Studio'nun tüm örnekleri kapatıldıktan sonra uzantınız yüklenir.
Bağımlılıkları olan bir uzantıyı yüklemeye çalışırsanız, yükleyici bunların yüklenmiş olup olmadığını denetler. Bunlar yüklenmezse, Uzantıları Yönet iletişim kutusu, uzantıyı yükleyemeden önce yüklenmesi gereken **bağımlılıkları** listeler.

### Uzantıyı kaldırma veya devre dışı kaldırma
Bir uzantıyı kullanmayı bırakmak isterseniz devre dışı bırakabilir veya kaldırabilirsiniz. Bir uzantı devre dışı bırakıldığında yüklü kalır, ancak etkin değildir. Uzantıyı bulun ve **Kaldır** veya **Devre Dışı Kaldır** tıklatın. Devre dışı bırakılmış bir uzantıyı boşaltmak için Visual Studio'yı yeniden başlatın.
