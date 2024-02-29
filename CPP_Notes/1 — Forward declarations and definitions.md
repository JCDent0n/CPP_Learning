

```cpp
#include <iostream>

  

int main()

{

    std::cout << "The sum of 3 and 4 is: " << add(3, 4) << '\n';

    return 0;

}

  

int add(int x, int y)

{

    return x + y;

}

//Yukarıda bulunan kod çalışmayacaktır. Çünkü Add fonksiyonu sonradan tanımlanmış. Bu nedenle Compiler Add'i tanımlamadığımızı söyleyecek.
```


```cpp
#include <iostream>

int add(int x, int y)
{
    return x + y;
}

int main()
{
    std::cout << "The sum of 3 and 4 is: " << add(3, 4) << '\n';
    return 0;
}
//Burada bulunan kod dizilimi fonksiyonun çalışması için uygun biçimde reorder edilmiş halidir.
```


```cpp
#include <iostream>

int add(int x, int y); // forward declaration of add()

int main()
{
    std::cout << "The sum of 3 and 4 is: " << add(3, 4) << '\n';
    return 0;
}

// note: No definition for function add
// Kod declare edilmiş ama define edilmediği için linker hatası alınacak.
```

```cpp
#include <iostream>

int add(int x, int y); // forward declaration of add() (using a function declaration)

int main()
{
    std::cout << "The sum of 3 and 4 is: " << add(3, 4) << '\n'; // this works because we forward declared add() above
    return 0;
}

int add(int x, int y) // even though the body of add() isn't defined until here
{
    return x + y;
}
// Bu bir forward declaration örneğidir.
```

Define etmek compiler'in bir işlemi bu define edilen şeyle başlatabilmesi demek yani verileri vs kullanılabilecek yapıda.
```cpp
int x{5};
int doMath(int x, int y)
{
	return x+y;
}
// Bu yapı define yapısıdır.
```


Declaration ise verilen verileri sadece compiler var olduğunu anlar ama işleme alamaz çünkü sadece ifade edilir.
```cpp
int doMath(int x, int y);
int x;
// bu yapılar ise sadece declare edilmiştir.
```
