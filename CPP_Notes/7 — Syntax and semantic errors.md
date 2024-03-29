C++'ta başlangıçta hatalar syntax ya da semantic olmak üzere ikiye ayrılırlar.

Syntax hataları C++'ta dil bilgisine uyulmamasına denk gelmektedir.

```cpp
#include <iostream>

int main()
{
    std::cout < "Hi there"; << x << '\n'; // invalid operator (<), extraneous semicolon, undeclared variable (x)
    return 0 // missing semicolon at end of statement
}
// Burada bir syntax hatasi goruyoruz.
```

Syntax hataları genelde compiler tarafından yakalanır.

Semantic hatalar ise kodun syntax açısından hiçbir hatası olmayıp istenileni yapmaması durumuna denir.

```cpp
#include <iostream>

int main()
{
    int a { 10 };
    int b { 0 };
    std::cout << a << " / " << b << " = " << a / b << '\n'; // division by 0 is undefined in mathematics
    return 0;
}
// Bu bir Semantic error
```

```cpp
#include <iostream>

int main()
{
    int x; // no initializer provided
    std::cout << x << '\n'; // Use of uninitialized variable leads to undefined result

    return 0;
}
```

```cpp
#include <iostream>

int add(int x, int y) // this function is supposed to perform addition
{
    return x - y; // but it doesn't due to the wrong operator being used
}

int main()
{
    std::cout << "5 + 3 = " << add(5, 3) << '\n'; // should produce 8, but produces 2

    return 0;
}
```

```cpp
#include <iostream>

int main()
{
    return 0; // function returns here

    std::cout << "Hello, world!\n"; // so this never executes
}
```
