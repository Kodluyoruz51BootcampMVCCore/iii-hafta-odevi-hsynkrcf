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

## Extension Metod Nedir? Nasıl Yazılır ?
Basit ve Kısa olarak anlatıyorum, bende MVC için extension metod yazmıştım.

- Extension metodlar herhangi bir yeni nesne oluşturmadan, üzerinde işlem yaptığınız nesne üzerinden çağrılabilen "genişletilmiş" manasına gelen çok pratik metodlardır. Bu metodları kullanarak hem extra iş yükünden kurtulmuş olursunuz, hem de sürekli aynı kodları yazmak zorunda kalmazsınız.

  ```cs
  public static class ExtensionClass  {  
    public static int IntCevir(this string Deger)  
    {  
        return Int32.Parse(Deger);  
    }  
  }  
  ```
- Genellikle ilk string'e bir extension yazarak başlarız. Burada dikkat etmeniz gereken en önemli nokta parametrenin this anahtar kelimesi ile başlamasıdır. Bu ifade ile metodumuzun extension metod olduğunu belirtiyoruz. Şöyle kullanılıyor;

![Extension](https://www.hikmetokumus.com/MakImages/24-08-2012-02.jpg)

###### Buda benim yaptığıma benzer bir örnek kendi html extension metodunuzu yazabilirsiniz.
  ```cs
   //Example of a Static class
    public static class HtmlHelpers
    {
        //Your Extension method
        public static MvcHtmlString DatePickerDropDowns(this HtmlHelper html,
            string dayName, string monthName, string yearName,
            int? beginYear = null, int? endYear = null,
            int? selectedDay = null, int? selectedMonth = null, int? selectedYear = null, bool localizeLabels = true)
        {
            //Example
            return new MvcHtmlString("Example");
        }
    }
  ```
###### Yazdığınız metodu böyle kullanabilirsiniz.
@using YourProject.HtmlHelpers;

@Html.DatePickerDropDowns(...)
