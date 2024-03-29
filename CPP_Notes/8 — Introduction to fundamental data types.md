Hafızanın en küçük birimine " Binary Digit" denir. 0 ve 1'lerden oluşur. 10111010 gibi.

Hafızanın sıralanmış şekline " Memory Adress " denir. Her bir hafıza adresi içerisinde 1 byte veri tutar. 1 byte veri 8 bit'e denk olmaktadır.


![](https://www.learncpp.com/images/CppTutorial/Section2/MemoryAddresses.png?ezimgfmt=rs:188x180/rscb2/ngcb2/notWebP)
Yukarıda bir memory adress yapısı

# Data Types

Bilgisayar yapısında değerleri anlatmak için kullanılan terim Data Types (Veri Yapısı).

Int bir data typedır. Biz 65 değerinde bir integer define ettiğimizde CPU bunu 65'e denk gelen binary formatına çevirir ve bu şekilde işler.

Veri yapıları kendi içerisinde de gruplara ayrılır.

## Fundemental Data Types

Aşağıda bulunan tabloda fundemental veri tiplerine yer verilmiştir.

| Type                                                                               | Kategori             | Anlamı                                 | Örnek   |
| ---------------------------------------------------------------------------------- | -------------------- | -------------------------------------- | ------- |
| float<br>double<br>long double                                                     | Floating Point       | kesirli kısmı olan bir sayı            | 3.14159 |
| bool                                                                               | Integral (Boolean)   | Doğru veya Yanlış                      | true    |
| char  <br>wchar_t  <br>char8_t (C++20)  <br>char16_t (C++11)  <br>char32_t (C++11) | Integral (Character) | tek bir metin karakteri                | 'c'     |
| short int  <br>int  <br>long int  <br>long long int (C++11)                        | Integral (Integer)   | 0 dahil pozitif ve negatif tam sayılar | 64      |
| std::nullptr_t (C++11)                                                             | Null Pointer         | null pointer (Boş İşaretçi)            | nullptr |
| Void                                                                               | Void                 | no type                                | n/a     |

### \_t Suffix
t demek " type " anlamına gelmektedir.
