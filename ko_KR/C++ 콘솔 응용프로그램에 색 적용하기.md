# C++ 콘솔 응용프로그램에 색 적용하기


프로젝트 rang은 Abhinav Gauniyal 이 만든 헤더파일만으로 동작하는 콘솔 텍스트 색 적용하는 오픈소스 라이브러리 입니다.
https://github.com/agauniyal/rang

##### Colors for your Terminal.

<details>
 <summary>Unix-like (리눅스, 유닉스, 맥)</summary>

![rang-demo](https://cloud.githubusercontent.com/assets/7630575/13501282/0bd00074-e18c-11e5-9848-5bd1f20566d9.gif)
</details>

<details>
 <summary>Windows Demo</summary>

![rang-windows-demo](https://cloud.githubusercontent.com/assets/11349690/19836886/8134975e-9ebe-11e6-9ee4-c4657784ff3b.gif)
</details>

## 라이브러리 의존성
rang은 C++ standard library만으로 동작하므로 별도의 추가 라이브러리는 필요하지 않습니다.

## 설치
```sh
$ git clone https://github.com/agauniyal/rang.git 
```
## 내 프로젝트에 적용하기
설치 폴더내 **include/rang.hpp** 파일을 자신의 프로젝트의 적정한 위치에 복사하거나, 설치 폴더의 **include** 폴더를 프로젝트 경로에 추가합니다.


## 다양한 설정 
   
**Text Styles**:

| Code | Linux/Win/Others | Old Win
| ---- | --------- | ------ |
| `rang::style::bold`      | yes   | yes   |
| `rang::style::dim`       | yes   | no    |
| `rang::style::italic`    | yes   | no    |
| `rang::style::underline` | yes   | no    |
| `rang::style::blink`     | no    | no    |
| `rang::style::rblink`    | no    | no    |
| `rang::style::reversed`  | yes   | yes   |
| `rang::style::conceal`   | maybe | yes   |
| `rang::style::crossed`   | yes   | no    |

**Text Color**:

| Code | Linux/Win/Others | Old Win
| ---- | --------- | ------ |
| `rang::fg::black`     | yes | yes |
| `rang::fg::red`       | yes | yes |
| `rang::fg::green`     | yes | yes |
| `rang::fg::yellow`    | yes | yes |
| `rang::fg::blue`      | yes | yes |
| `rang::fg::magenta`   | yes | yes |
| `rang::fg::cyan`      | yes | yes |
| `rang::fg::gray`      | yes | yes |

**Background Color**:

| Code | Linux/Win/Others | Old Win
| ---- | --------- | ------ |
| `rang::bg::black`     | yes | yes |
| `rang::bg::red`       | yes | yes |
| `rang::bg::green`     | yes | yes |
| `rang::bg::yellow`    | yes | yes |
| `rang::bg::blue`      | yes | yes |
| `rang::bg::magenta`   | yes | yes |
| `rang::bg::cyan`      | yes | yes |
| `rang::bg::gray`      | yes | yes |

**Bright Foreground Color**:

| Code | Linux/Win/Others | Old Win
| ---- | --------- | ------ |
| `rang::fgB::black`     | yes | yes |
| `rang::fgB::red`       | yes | yes |
| `rang::fgB::green`     | yes | yes |
| `rang::fgB::yellow`    | yes | yes |
| `rang::fgB::blue`      | yes | yes |
| `rang::fgB::magenta`   | yes | yes |
| `rang::fgB::cyan`      | yes | yes |
| `rang::fgB::gray`      | yes | yes |

**Bright Background Color**:

| Code | Linux/Win/Others | Old Win
| ---- | --------- | ------ |
| `rang::bgB::black`     | yes | yes |
| `rang::bgB::red`       | yes | yes |
| `rang::bgB::green`     | yes | yes |
| `rang::bgB::yellow`    | yes | yes |
| `rang::bgB::blue`      | yes | yes |
| `rang::bgB::magenta`   | yes | yes |
| `rang::bgB::cyan`      | yes | yes |
| `rang::bgB::gray`      | yes | yes |

**Reset Styles/Colors**:

| Code | Linux/Win/Others | Old Win
| ---- | --------- | ------ |
| `rang::style::reset`  | yes   | yes |
| `rang::fg::reset`     | yes   | yes |
| `rang::bg::reset`     | yes   | yes |

## 간단한 sample code
```c++
#include "rang.hpp"

int main()
{
    rang::setControlMode(rang::control::Auto); 
    // 터미널이 색을 지원하는지 자동으로 검출하여 적용여부 결정
    // rang::control::Off : 색 적용기능을 해제
    // rang::control::Force : 터미널 색 지원여부 상관없이 강제 적용
    
    std::cout << "Hello world !!!" 
              << rang::style::bold 
              << "Rang styled text !!!"
              << rang::style::reset << std::endl;
    return 0;
}
```
output :

**Hello world !!!**