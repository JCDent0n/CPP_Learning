preprocesslernmiş dosyalara translation unit denir.

preprocess, compile ve link olaylarının hepsine translation denir.

# Preprocessing Directives

\# ile başlarlar ve newline ile biterler.

en basiti \#include bu preprocessor dahil edildiğinde yanında bulunan dosyanın içeriğini koda dahil eder. Mesela iostream i include yanında kullanırsak içeriğini o kod dizinine dahil eder.


```cpp
#include <iostream>

int main()
{
    std::cout << "Hello, world!\n";
    return 0;
}
```

# Macro Defines

Makrolar ise \#define preprocessor'u ile oluşur.
ikiye ayrılır;
1. Object-Like macro
2. Function-like macro -> Bu tip biraz güvensiz olduğu için fazla kullanılmaz.

```
#define identifier
#define identifier substitution_text
//örnek object like macrolara
```

```cpp
#include <iostream>

#define MY_NAME "Alex"

int main()
{
    std::cout << "My name is: " << MY_NAME << '\n';

    return 0;
}
//Object-like macros with substitution text yapısına bir örnek bu şekildedir.
```

```cpp
// The contents of iostream are inserted here

int main()
{
    std::cout << "My name is: " << "Alex" << '\n';

    return 0;
}
// Macro işleme konulunca kod burada olduğu gibi olmaktadır
```

```cpp
#define USE_YEN
//Object-like macros without substitution text örnek olarak gözüktüğü gibi yanında herhangi bir şekilde substution text yer almamakta.
```

# Conditional Compilations

En çok kullanılan yapıları \#ifdef, \#ifndef, \#endif

\#ifdef eğer preprocessor da tanımlanan şey \#ifdef ve \#endif aralığında ise compile edilir.
```cpp
#include <iostream>

#define PRINT_JOE

int main()
{
#ifdef PRINT_JOE
    std::cout << "Joe\n"; // will be compiled since PRINT_JOE is defined
#endif

#ifdef PRINT_BOB
    std::cout << "Bob\n"; // will be excluded since PRINT_BOB is not defined
#endif

    return 0;
}
// Yukarıda bulunan Kod dizinin Joe yazdıracaktır çünkü PRINT_JOE tanımlanmış.
```

\#ifndef ise \#ifdef'in tam zıttıdır.
```cpp
#include <iostream>

int main()
{
#ifndef PRINT_BOB
    std::cout << "Bob\n";
#endif

    return 0;
}
//Bu kod ise Bob yazdıracaktır çünkü gözüktüğü gibi PRINT_BOB Macrosu hiç tanımlanmamıştır.
```

\#if 0 bu preprocessor ise direkt olarak arasında bulunan kod bloğunu compile etmez.
```cpp
#include <iostream>

int main()
{
    std::cout << "Joe\n";

#if 0 // Don't compile anything starting here
    std::cout << "Bob\n";
    std::cout << "Steve\n";
#endif // until this point

    return 0;
}
// Yukarıda bulunan kod if 0 aralığında olan şeyleri compile etmeyecek sadece Joe bastıracaktır.
```

