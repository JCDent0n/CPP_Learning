İncomplete type -> Declare edilmiş ama define edilmemiş. Compiler varlığından haberdar ama hafızası içerisinde ne kadar yer açması gerektiğini bilmiyor.

Değişkenler incomplete type lar ile define edilemez.

```cpp
void value; // won't work, variables can't be defined with incomplete type void
// Yukarıda olduğu gibi bu şekil yanlıştır.
```

## Void Kullanan Fonksiyonlar

Void kullanan fonksiyonlar değer döndüremezler. Eğer döndürürlerse compiler bize hata verecektir.

```cpp
void writeValue(int x) // void here means no return value
{
    std::cout << "The value of x is: " << x << '\n';
    // no return statement, because this function doesn't return a value
}
```

```cpp
void noReturn(int x) // void here means no return value
{
    std::cout << "The value of x is: " << x << '\n';

    return 5; // error
}
// Yukarıda ki durumda kod hata verecektir.
```

Fonkisyon içerisinde eğer parametre kullanmayacaksak C'nin parametre içerisine void yazarak değil boş bırakarak yapılmalıdır aşağıda olduğu gibi

```cpp
int getValue() // empty function parameters is an implicit void
{
    int x{};
    std::cin >> x;

    return x;
}
```
