# 2.11 — Header files

Header dosyalarının amacı declarationları kod dosyalarına yaymaktır.

\#include \<iostream> yazıldığında bu durum preprocessorun kullanıldığı yere iostream'in içeriğinin olduğu gibi yerleştirilmesi demektir.

```cpp
#include <iostream>

int main()
{
    std::cout << "Hello, world!";
    return 0;
}
//Yukarıda ki kodda gördüldüğü gibi #include <iostream> yerine iostream'in içeriği gelecektir.

```

## Using header files to propagate forward declarations

önceki notlarda iki adet kod dosyamız vardı bunlardan biri;

add.cpp:
```cpp
int add(int x, int y)
{
    return x + y;
}
```

diğeri ise main.cpp:
```cpp
#include <iostream>

int add(int x, int y); // forward declaration using function prototype

int main()
{
    std::cout << "The sum of 3 and 4 is " << add(3, 4) << '\n';
    return 0;
}
```

Yukarıda yer alan kodlar aynı işlevi Header dosyası kullanarak yapabilir birazdan göreceğiz.

Header dosya formatı "xxx.h" şeklinde olmaktadır sonunda .h bulunmalıdır.

add.h:
```cpp
// 1) We really should have a header guard here, but will omit it for simplicity (we'll cover header guards in the next lesson)

// 2) This is the content of the .h file, which is where the declarations go
int add(int x, int y); // function prototype for add.h -- don't forget the semicolon!
// Burada header içerisinde ana kodda kullanılacak fonksiyon declare edilimiş.
```

main.cpp:
```cpp
#include "add.h" // Insert contents of add.h at this point.  Note use of double quotes here.
#include <iostream>

int main()
{
    std::cout << "The sum of 3 and 4 is " << add(3, 4) << '\n';
    return 0;
}
// Burada gözüktüğü gibi main içerisinde header dosyası eklenmiş ve bir farklılık var normalde açılı parantez kullanılırken burada çift tırnak işareti kullanılmış neden?
```

add.cpp:
```cpp
#include "add.h" // Insert contents of add.h at this point.  Note use of double quotes here.

int add(int x, int y)
{
    return x + y;
}
// Burada ise görüldüğü gibi bu kod dizini içerisinde fonksiyon define edilmiş. Header kullanımı eğer belli bir fonksiyon için veya bir kaynak kodu yani .cpp uzantılı bir dosya için özel olarak yazılmış ise aynı isime sahip olmaları daha sağlıklı olacaktır.
```

![[Pasted image 20240211160924.png]]
Yukarıda bulunan görsel işlemin bilgisayar bazında nasıl gerçekleştiğini göstermektedir.

## ODR Kuralının bozulabilmesi

Daha önceki derslerde değinmiştik ODR Kuralı bir fonksiyonun veya bir değişkenin tek bir yerde tanımlanmasından söz ediyordu. Bu durumda bir Header dosyası içerisinde fonksiyonun veya bir değişkenin define edilmesini istemeyiz çünkü bazı durumlarda problem yaratabilirler. Örneğin;

add.h
```cpp
// We really should have a header guard here, but will omit it for simplicity (we'll cover header guards in the next lesson)

// definition for add() in header file -- don't do this!
int add(int x, int y)
{
    return x + y;
}
```

main.cpp
```cpp
#include "add.h" // Contents of add.h copied here
#include <iostream>

int main()
{
    std::cout << "The sum of 3 and 4 is " << add(3, 4) << '\n';

    return 0;
}
```

add.cpp
```cpp
#include "add.h" // Contents of add.h copied here
```

Yukarıda bulunan kodlar kendi aralarında compile edilmesinde bir problem bulunmaz çünkü her kod dosyası kendi içerisinde compile ediliyor ve problem olmuyor. Asıl problem linker işlemi başladığında ortaya çıkacaktır.
##  Açılı Parantez vs Çift Tırnak

Açılı parantez kendimizin oluşturmadığı header dosyalarını kod içerisine eklerken kullanılır. Mesela \#include \<iostream> yazıldığı zaman iostream standart library içerisinde bulunuyor bu nedenle açılı parantez kullanılır.

Çift tırnak ise bizim yazdığımız header dosyalarını eklerken belirtmek için kullanılır yukarıda var olan kodlarda örneği bulunmakta inceleyiniz.

Header dosyaları ana kod içerisinde kullanılırken \#include \<xxx.h> şeklinde kullanılmalıdır. iostream bir istisnadır. (İnternet üzerinde ''Why doesn’t iostream have a .h extension?'' araması ile bulunabilir.)

## Including header files from other directories

For VS Code users

In your _tasks.json_ configuration file, add a new line in the _“Args”_ section:  
`"-I/source/includes",`

Sonuncusu ve önemli bir parçası Header dosyalarını dökümante edin ne işe yaradıklarını.



