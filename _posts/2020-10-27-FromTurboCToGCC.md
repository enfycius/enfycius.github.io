---
title: "gotoxy(), clrscr(), getch(), and getche() functions for GCC Linux."

classes: wide

categories:
  - C
tags:
  - Programming

toc: true
---



# gotoxy() for GCC Linux
```c
// gotoxy() function definition
void gotoxy(int x, int y)
{
  printf("%c[%d;%df", 0x1B, y, x);
}
```


```c
#include <stdio.h>

// gotoxy() function definition
void gotoxy(int x, int y)
{
    printf("%c[%d;%df", 0x1B, y, x);
}

int main()
{
    int x=10, y=20;
    gotoxy(x, y); // move cursor position

    printf("Hello World!!!"); // print message
    return 0;
}
```

# clrscr() for GCC Linux

```c
// clrscr() function definition
void clsrscr(void)
{
  system("clear");
}
```

```c
#include <stdio.h>

// clrscr() function definition
void clrscr(void)
{
  system("clear");
}

int main()
{
  clrscr();
  printf("Hello World!!!");

  return 0;
}
```

# getch() and getche() for GCC Linux

```c
#include <termios.h>
#include <stdio.h>

static struct termios old, new;

void initTermios(int echo)
{
  tcgetattr(0, &old);
  new = old;
  new.c_lflag &= ~ICANON;
  new.c_lflag &= echo ? ECHO : ~ECHO;
  tcsetattr(0, TCSANOW, &new);
}

void resetTermios(void)
{
  tcsetattr(0, TCSANOW, &old);
}

char getch_(int echo)
{
  char ch;
  initTermios(echo);
  ch = getchar();
  resetTermios();

  return ch;
}

char getch(void)
{
  return getch_(0);
}

char getche(void)
{
  return getch_(1);
}

int main(void) {
  char c;
  printf("(getche example) Please enter a character: ");
  c = getche();
  printf("\nYou entered: %c\n", c);
  printf("(getch example) Please enter a character: ");
  c = getch();
  printf("\nYou entered: %c\n", c);

  return 0;
}
```

출처: [includehelp][includehelplink]

[includehelplink]: https://www.includehelp.com/c-programs/gotoxy-clrscr-getch-getche-for-gcc-linux.aspx
