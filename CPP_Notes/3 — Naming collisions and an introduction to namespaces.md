a.cpp:

```cpp
#include <iostream>

void myFcn(int x)
{
    std::cout << x;
}
```

main.cpp:

```cpp
#include <iostream>

void myFcn(int x)
{
    std::cout << 2 * x;
}

int main()
{
    return 0;
}
```
Yukarıda bulunan kod dizinleri farklı isimlerde yer alacak farklı dosyalarda ama compile edilirken ikisi kendi içinde düzgün compile edildiği halde linker hatası verecek. NEDEN
Çünkü ikisinde de aynı fonksiyon tanımlanmış.


Global namespace aşağıda görüldüğü gibi int main(){} dışında kalan yerlerdir veya bir fonksiyon dışı vb.

```cpp
#include <iostream> // handled by preprocessor

// All of the following statements are part of the global namespace
void foo();    // okay: function forward declaration in the global namespace
int x;         // compiles but strongly discouraged: uninitialized variable definition in the global namespace
int y { 5 };   // compiles but discouraged: variable definition with initializer in the global namespace
x = 5;         // compile error: executable statements are not allowed in the global namespace

int main()     // okay: function definition in the global namespace
{
    return 0;
}

void goo();    // okay: another function forward declaration in the global namespace
//yukarıda yazan kodlar global namespace'i göstermektedir. Okuyunuz
```


Namespaceler içerisinde sadece declaration ve definitionlar yer alabilir.

std::cout komutu yazıldığında komut aslında sadece couttur std ise namespacedir.

"::" operatörü scope resolution operator'dür. yani sağda bulunan statement solda bulunan namespacein içinde yer alır diyor.

qualified name -> Önüne prefix alan identifierlardır.
```cpp
#include <iostream>

using namespace std; // this is a using directive that allows us to access names in the std namespace with no namespace prefix

int main()
{
    cout << "Hello world!";
    return 0;
}
//Yukarıda bulunan durumda using namespace std denilerek cout ve cin gibi komutlar yazarken prefix kullanmaya gerek kalmayacak. Ama peki bu kullanılmalı mı?
```

```cpp
#include <iostream> // imports the declaration of std::cout

using namespace std; // makes std::cout accessible as "cout"

int cout() // defines our own "cout" function in the global namespace
{
    return 5;
}

int main()
{
    cout << "Hello, world!"; // Compile error!  Which cout do we want here?  The one in the std namespace or the one we defined above?

    return 0;
}
//Bu kod dizininde ise neden namespace olarak kullanılmaması gerektiğini görüyoruz. Çünkü cout'u aynı zamanda bir fonksiyon olarak tanımlamış bu tanımlanan durumda compiler hangisini nasıl ele alacağını algılayamadığı için hata verecektir.
```
