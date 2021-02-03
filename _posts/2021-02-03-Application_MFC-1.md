---
title: "MFC Fundamentals of Windows 응용"

classes: wide

categories:
  - MFC
tags:
  - MFC
  - Programming
  - Coding
---

# 내용

MFC Fundamentals of Windows에 대한 개념을 공부한 후, 이를 용용하여 20개의 창을 띄워주는 프로그램을 작성함.

Delay를 주지 않았을 경우, 한 번에 20개의 창이 뜨므로,

다음처럼 0.1초의 delay를 줌.

```cpp
Sleep(100);
```

# 코드

```cpp
#include <afxwin.h>
#include <Windows.h>
 
class CMyFrame : public CFrameWnd {
public:
    CMyFrame(POINT p, SIZE s) {
        Create(NULL, _T("MFC Application Tutorial"), NULL, CRect(p, s));
    }
};
 
class CExample : public CWinApp {
    BOOL InitInstance() {
        int x = 0, y = 0;
        int cx = 0, cy = 0;
 
        POINT p;
        SIZE s;
 
        for (int i = 0; i < 20; i++) {
            p.x = (x += 25);
            p.y = (y += 25);
 
            s.cx = (cx += 40);
            s.cy = (cy += 40);
 
            CMyFrame* Frame = new CMyFrame(p, s);
            m_pMainWnd = Frame;
 
            Frame->ShowWindow(SW_NORMAL);
            Frame->UpdateWindow();
 
            Sleep(100);
            
        }
 
        return TRUE;
    }
 
};
 
CExample theApp;
```