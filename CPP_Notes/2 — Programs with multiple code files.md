Configuring **Visual Studio Code** for a project with multiple source files -

Running `Code` (Code Runner extension):

- Go to **Extension Settings**, find **Code-runner: Executor Map**, press **Edit in settings.json** and at line **.cpp** modify it as follows: `"cpp": "cd $dir && g++ -std=c++23 *.cpp -o $fileNameWithoutExt && $dir$fileNameWithoutExt",` where `$fileName` was changed to `*.cpp`.

Running `C/C++ File`:

- Go to **tasks.json** and under args, replace `"${file}",` with `"${fileDirname}\\**.cpp",`.

The above setup is made on Windows. For Unix systems try to replace \\ with /.

Forward declaration başka bir dosyada bulunan fonksiyonun define'ını ile bağdaştırmak için kullanılabilir.

```cpp
#include <iostream>

int add(int x, int y); // needed so main.cpp knows that add() is a function defined elsewhere

int main()
{
    std::cout << "The sum of 3 and 4 is: " << add(3, 4) << '\n';
    return 0;
}
// Bu kod main olarak yer alacaktır.
```

```cpp
int add(int x, int y)
{
    return x + y;
}
//Bu kod ise sadece add ismindi bir dosya olarak yer alacaktır.
```

Yukarıda bulunan kodlar bir araya gelerek compile edilecektir.

```cpp
#include <iostream>

int getInteger()
{
	std::cout << "Enter an integer: ";
	int x{};
	std::cin >> x;
	return x;
}

int main()
{
	int x{ getInteger() };
	int y{ getInteger() };

	std::cout << x << " + " << y << " is " << x + y << '\n';
	return 0;
}
//Bu kodu böyle alıp gruplara dağıtacağız input.cpp ve main.cpp olarak
```

```cpp
#include <iostream> // we need iostream since we use it in this file

int getInteger()
{
	std::cout << "Enter an integer: ";
	int x{};
	std::cin >> x;
	return x;
}
// Bu kısım input.cpp olacak
```

```cpp
#include <iostream> // we need iostream here too since we use it in this file as well

int getInteger(); // forward declaration for function getInteger

int main()
{
	int x{ getInteger() };
	int y{ getInteger() };

	std::cout << x << " + " << y << " is " << x + y << '\n';
	return 0;
}
// Bu kısım ise main.cpp olacak.
```
