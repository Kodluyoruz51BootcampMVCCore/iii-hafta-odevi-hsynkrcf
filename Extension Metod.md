
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
