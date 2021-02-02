---
title: "C++ IS-A 관계의 상속"

classes: wide

categories:
  - C++
tags:
  - C++
  - Programming
  - Coding
---

# 문제

'책' 을 의미하는 Book 클래스와 '전자 책' 을 의미하는 EBook 클래스를 정의하고자 한다.

그런데 '전자 책'도 '책'의 일종이므로, 다음의 형태로 클래스의 상속 관계를 구성하고자 한다.

(클래스에 선언되어야 할 멤버변수만 제시하였다.)

```cpp
class Book
{
private:
    char* title;
    char * isbn;
    int price;
    ...
};

class EBook : public Book
{
private:    
    char* DRMKey;
    ...
};
```

위의 EBook 클래스에 선언된 멤버 DRMKey는 전자 책에 삽입이 되는 보안관련 키(key)의 정보를 의미한다. 그럼 다음 main 함수와 함께 실행이 가능하도록 위의 클래스를 완성해보자.

## main 함수

```cpp
int main(void)
{
    Book book("좋은 C++", "555-12345-890-0", 20000);
    book.ShowBookInfo();
    cout<<endl;

    EBook ebook("좋은 C++ ebook", "555-12345-890-1", 10000, "fdx9w0i8kiw");
    ebook.ShowEBookInfo();

    return 0;
}
```

## 실행의 예

```shell
제목: 좋은 C++
ISBN: 555-12345-890-0
가격: 20000


제목: 좋은 C++ ebook
ISBN: 555-12345-890-1
가격: 10000
인증키: fdx9w0i9kiw
```

# 해결

## 코드

```cpp
#include <iostream>
#include <cstring>
#include <cstdlib>
 
using namespace std;
 
class Book
{
private:
    char* title;
    char* isbn;
    int price;
 
public:
    Book(char* my_title, char* my_isbn, int my_price) : price(my_price)
    {
        title = new char[strlen(my_title) + 1];
        strcpy(title, my_title);
 
        isbn = new char[strlen(my_isbn) + 1];
        strcpy(isbn, my_isbn);
    }
 
    void ShowBookInfo()
    {
        cout << "제목: " << title << endl;
        cout << "ISBN: " << isbn << endl;
        cout << "가격: " << price << endl;
    }
 
    ~Book()
    {
        delete[]title;
        delete[]isbn;
    }
};
 
class EBook : public Book
{
private:
    char* DRMKey;
    
public:
    EBook(char* my_title, char* my_isbn, int my_price, char* my_drm) : Book(my_title, my_isbn, my_price)
    {
        DRMKey = new char[strlen(my_drm) + 1];
        strcpy(DRMKey, my_drm);
    }
 
    void ShowEBookInfo()
    {
        ShowBookInfo();
        cout << "인증키: " << DRMKey << endl;
        cout << endl;
    }
 
    ~EBook()
    {
        delete[]DRMKey;
    }
};
 
int main(void)
{
 
    Book book("좋은 C++", "555-12345-890-0", 20000);
    book.ShowBookInfo();
    cout << endl;
    cout << endl;
 
    EBook ebook("좋은 C++ ebook", "555-12345-890-1", 10000, "fdx9w0i8kiw");
    ebook.ShowEBookInfo();
 
    return 0;
}
```