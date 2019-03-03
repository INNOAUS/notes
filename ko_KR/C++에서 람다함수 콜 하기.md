# C++ 에서 Lambda 함수 호출하기

Lamda 혹은 anonymous function 개념은 C++에서는 C++11 부터 추가된 것으로 보통 함수와는 달리 함수명이 없는 특징을 가지고 있다. 

다음은 이러한 익명함수를 호출하는 경험을 간단히 정리한 것이다.


그리고, 다양한 C++ 컴파일러에서 제공하는 C++ 특징을 정리한 것을 https://en.cppreference.com/w/cpp/compiler_support 에서 확인 할 수 있다.


# function pointer를 이용한 익명 함수 호출 예제
```c++
auto a_lamda_function = [](const std::string& msg) {
    std::cout << "function pointer를 이용한 람다함수 호출 예제 : " << msg << std::endl;
}

void (* funcPtr)(int) = a_lamda_function;

funcPtr("Hello World!!!");
```

# C++17 부터 제공되는 std::apply 함수 이용하여 호출
```c++
#include <iostream>
#include <tuple>
#include <utility>
 
int add(int first, int second) { return first + second; }
 
template<typename T>
T add_generic(T first, T second) { return first + second; }
 
auto add_lambda = [](auto first, auto second) { return first + second; };
 
int main()
{
    // OK
    std::cout << std::apply(add, std::make_pair(1, 2)) << '\n';
 
   // Error: can't deduce the function type
   // std::cout << std::apply(add_generic, std::make_pair(2.0f, 3.0f)) << '\n'; 
 
   // OK
   std::cout << std::apply(add_lambda, std::make_pair(2.0f, 3.0f)) << '\n';
}

```