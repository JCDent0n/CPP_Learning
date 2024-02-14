
# 2.12 — Header guards

Daha önce de söylediğimiz gibi header dosyaları içerisinde fonksiyon def.'ler ve variable identifierlarını birden fazla define etmek probleme yol açar.

```cpp
int main()
{
    int x; // this is a definition for variable x
    int x; // compile error: duplicate definition

    return 0;
}

// Burada görüldüğü gibi iki adet değişken declare edilmiş birbirinin kopyası oldukları için yanlıştır bu durum
```

```cpp
#include <iostream>

int foo() // this is a definition for function foo
{
    return 5;
}

int foo() // compile error: duplicate definition
{
    return 5;
}

int main()
{
    std::cout << foo();
    return 0;
}
// Burada ise bir fonksiyonu birden fazla defa define etmiş durumda bu durum yine yanlıştır.
```

Yukarıda bulunan durumlar genellikle çözümü basitti daha kompleks bir şeye geçersek bazen header dosyaları birbirinin içerisinde include edilebilir örneğin;

square.h:
```cpp
int getSquareSides()
{
    return 4;
}

```

wave.h
```cpp
#include "square.h"
```

main.cpp
```cpp
#include "square.h"
#include "wave.h"

int main()
{
    return 0;
}
```

Yukarıda bulunan program compile edilmeyecektir. Çünkü iki headerdan biri diğerini include ettiği için birbirini kopyalıyor ve bu durumda compiler fonk. def. duplication olduğu için durumu kabul etmiyor ve hata veriyor.

## Header Guard

Yukarıda yer alan kod hatalarının tekrarlanmaması için kullandığımız yöntemdir. Aynı zamanda include guard'da denir

```cpp
#ifndef SOME_UNIQUE_NAME_HERE
#define SOME_UNIQUE_NAME_HERE

// your declarations (and certain types of definitions) here

#endif

// Burada örnek bir header guard kullanımı gözükmekte SOME_UNIQUE_NAME_HERE yerine istenilen isim konulmalıdır ama syntax gereği bu şekilde yazılmalıdır yani tüm harfler büyük.

// #ifndef kısmı bu isme sahip bir şey include edilmiş mi diye bakar.
// #define kısmı eğer bu isimde bir şey define edilmemişse define eder.
// #endif kısmı ise bu iki koşuldan biri sağlanıyorsa koddan çıkışı sağlar.
```

square.h:
```cpp
#ifndef SQUARE_H
#define SQUARE_H

int getSquareSides()
{
    return 4;
}

#endif

// Normal kullanımda bir header guard örneği
```

## Önceki Örneği Header Guard İle Yapma

square.h:
```cpp
#ifndef SQUARE_H
#define SQUARE_H

int getSquareSides()
{
    return 4;
}

#endif
```

wave.h:
```cpp
#ifndef WAVE_H
#define WAVE_H

#include "square.h"

#endif
```


main.cpp:
```cpp
#include "square.h"
#include "wave.h"

int main()
{
    return 0;
}
```

Preprocessor çalıştıktan sonra kod aşağıda ki gibi olur.

main.cpp:
```cpp
// Square.h included from main.cpp
#ifndef SQUARE_H // square.h included from main.cpp
#define SQUARE_H // SQUARE_H gets defined here

// and all this content gets included
int getSquareSides()
{
    return 4;
}

#endif // SQUARE_H

#ifndef WAVE_H // wave.h included from main.cpp
#define WAVE_H
#ifndef SQUARE_H // square.h included from wave.h, SQUARE_H is already defined from above
#define SQUARE_H // so none of this content gets included

int getSquareSides()
{
    return 4;
}

#endif // SQUARE_H
#endif // WAVE_H

int main()
{
    return 0;
}
```

## Header Guard Dosyaları Farklı Kod Dosyalarında Include Edilmeyi Engellemez

square.h:
```cpp
#ifndef SQUARE_H
#define SQUARE_H

int getSquareSides()
{
    return 4;
}

int getSquarePerimeter(int sideLength); // forward declaration for getSquarePerimeter

#endif
```

square.cpp:
```cpp
#include "square.h"  // square.h is included once here

int getSquarePerimeter(int sideLength)
{
    return sideLength * getSquareSides();
}
```

main.cpp:
```cpp
#include "square.h" // square.h is also included once here
#include <iostream>

int main()
{
    std::cout << "a square has " << getSquareSides() << " sides\n";
    std::cout << "a square of length 5 has perimeter length " << getSquarePerimeter(5) << '\n';

    return 0;
}
```

Bu durumda Square.h Square.cpp içerisinde include edilecek yani header dosyası square.cpp boyunca koşacak ve arından sonlanacak. Ama bu sırada main.cpp dosyası bu işlemleri aynı anda işlediği için header dosyası başka yerde daha önce include edilmiş olacak bu nedenle main.cpp çalıştığında square.h dosyası include edilemeyecek çünkü zaten square.cpp içerisinde define edilmiş olacak ve \#ifndef üzerinden geçemeyecek. Compile durumunda bir sıkıntı yaşanmayacak ama link durumunda hata çıkacaktır.


==ÇÖZÜM==
_______
square.h:
```cpp
#ifndef SQUARE_H
#define SQUARE_H

int getSquareSides(); // forward declaration for getSquareSides
int getSquarePerimeter(int sideLength); // forward declaration for getSquarePerimeter

#endif
```

square.cpp:
```cpp
#include "square.h"

int getSquareSides() // actual definition for getSquareSides
{
    return 4;
}

int getSquarePerimeter(int sideLength)
{
    return sideLength * getSquareSides();
}
```

main.cpp:
```cpp
#include "square.h" // square.h is also included once here
#include <iostream>

int main()
{
    std::cout << "a square has " << getSquareSides() << " sides\n";
    std::cout << "a square of length 5 has perimeter length " << getSquarePerimeter(5) << '\n';

    return 0;
}
```

Yukarıda görüldüğü gibi fonksiyon definition header içerisine değil .cpp dosyası içerisinde yer almakta. Linker bu durumda hata vermeyecektir ve çalışmaya devam edecektir.
