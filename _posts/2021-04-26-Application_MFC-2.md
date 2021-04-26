---
title: "MFC & Algorithms: Snowflake"

classes: wide

categories:
  - MFC
  - Algorithms
tags:
  - MFC
  - Algorithms
  - Programming
  - Coding

toc: true
---

# 내용

Nontail Recursion으로 Snowflake를 구현하였으며, 대화상자 위에 뷰(vonKochView)를 올려 해당 뷰에 Snowflake가 그려지게끔 했다.

아래는 Visual Studio에서 기본적으로 생성되는 MFC 프로젝트 내의 파일 중 수정한 부분들과 Snowflake를 구현한 코드이며, 전체 솔루션 파일의 다운로드는 최하단에 별도의 링크로 기재해두었으니 결과물을 확인해보고 싶다면 참고하길 바란다.

# 코드

## vonKoch.h

```cpp
#pragma once

#define _USE_MATH_DEFINES

#include <afxwin.h>
#include <math.h>

class vonKoch {
    public:
    vonKoch(int, int, CDC*);
    void snowflake();

    private:
    double side, angle;
    int level;
    CPoint currPt, pt;
    CDC* pen;

    void right(double x) {
        angle += x;
    }

    void left(double x) {
        angle -= x;
    }

    void drawFourLines(double side, int level);
};

vonKoch::vonKoch(int s, int lvl, CDC* pDC) {
    pen = pDC;
    currPt.x = 200;
    currPt.y = 100;
    pen->MoveTo(currPt);
    angle = 0.0;
    side = s;
    level = lvl;
}

void vonKoch::drawFourLines(double side, int level) {
    if(level == 0) {
        pt.x = int(cos(angle*M_PI / 180)*side) + currPt.x;
        pt.y = int(sin(angle*M_PI / 180)*side) + currPt.y;
        pen->LineTo(pt);
        currPt.x = pt.x;
        currPt.y = pt.y;
    } else {
        drawFourLines(side / 3, level - 1);
        left(60);
        drawFourLines(side / 3, level - 1);
        right(120);
        drawFourLines(side / 3, level - 1);
        left(60);
        drawFourLines(side / 3, level - 1);
    }
}

void vonKoch::snowflake() {
    for(int i=1; i<=4; i++) {
        drawFourLines(side, level);
        right(120);
    }

    drawFourLines(side, level);
}
```

## vonKochView.h

```cpp
#pragma once

class vonKochView : public CView {
    DECLARE_DYNCREATE(vonKochView)

    public:
    vonKochView();      // 기존 protected -> public
    virtual ~vonKochView();     // 기존 protected -> public

    virtual void OnDraw(CDC* pDC);
    #ifdef _DEBUG
    virtual void AssertValid() const;
    #ifndef _WIN32_WCE
    virtual void Dump(CDumpContext& dc) const;
    #endif
    #endif

    protected:
    DECLARE_MESSAGE_MAP()
};
```

## vonKochView.cpp

```cpp
#include "pch.h"
#include "MFCApplication8.h"
#include "vonKochView.h"
#include "vonKoch.h"        // 추가

IMPLEMENT_DYNCREATE(vonKochView, CView)

vonKochView::vonKochView() {

}

vonKochView::~vonKochView() {

}

BEGIN_MESSAGE_MAP(vonKochView, CView)
END_MESSAGE_MAP()

void vonKochView::OnDraw(CDC* pDC) {
    CDocument* pDoc = GetDocument();

    vonKoch(200, 4, pDC).snowflake();   // 추가
}

#ifdef _DEBUG
void vonKochView::AssertValid() const {
    CView::AssertValid();
}

#ifndef _WIN32_WCE
void vonKochView::Dump(CDumpContext& dc) const {
    CView::Dump(dc);
}
#endif
#endif
```

## MFCApplication8Dlg.h

```cpp
#pragma once

#include "vonKochView.h"

class CMFCApplication8Dlg : public CDialog {
    public:
    vonKochView* m_vonKochView;         // 추가
    CMFCApplication8Dlg(CWnd* pParent = nullptr);

    #ifdef AFX_DESIGN_TIME
    enum { IDD = IDD_MFCAPPLICATION8_DIALOG };
    #endif

    protected:
    virtual void DoDataExchange(CDataExchange* pDX);

    protected:
    HICON m_hIcon;

    virtual BOOL OnInitDialog();
    afx_msg void OnSysCommand(UINT nID, LPARAM lParam);
    afx_msg void OnPaint();
    afx_msg void OnDestroy();       // 추가
    afx_msg HCURSOR OnQueryDragIcon();
    DECLARE_MESSAGE_MAP()
};
```

## MFCApplication8Dlg.cpp

```cpp
#include "pch.h"
#include "framework.h"
#include "MFCApplication8.h"
#include "MFCApplication8Dlg.h"
#include "afxdialogex.h"

#ifdef _DEBUG
#define new DEBUG_NEW
#endif

class CAboutDlg : public CDialogEx {
    public:
    CAboutDlg();

    #ifdef AFX_DESIGN_TIME
        enum { IDD = IDD_ABOUTBOX };
    #endif

    protected:
    virtual void DoDataExchange(CDataExchange* pDX);

    protected:
    DECLARE_MESSAGE_MAP();
};

CAboutDlg::CAboutDlg() : CDialogEx(IDD_ABOUTBOX) {

}

void CAboutDlg::DoDataExchange(CDataExchange* pDX) {
    CDialogEx::DoDataExchange(pDX);
}

BEGIN_MESSAGE_MAP(CAboutDlg, CDialogEx)
END_MESSAGE_MAP()

CMFCApplication8Dlg::CMFCApplication8Dlg(CWnd* pParent) : CDialog(IDD_MFCAPPLICATION8_DIALOG, pParent) {
    m_hIcon = AfxGetApp()->LoadIcon(IDR_MAINFRAME);
}

void CMFCApplication8Dlg::DoDataExchange(CDataExchange* pDX) {
    CDialog::DoDataExchange(pDX);
}

BEGIN_MESSAGE_MAP(CMFCApplication8Dlg, CDialog)
    ON_WM_SYSCOMMAND()
    ON_WM_PAINT()
    ON_WM_QUERYDRAGICON()
END_MESSAGE_MAP()

BOOL CMFCApplication8Dlg::OnInitDialog() {
    CDialog::OnInitDialog();

    m_vonKochView = new vonKochView;        // 추가
    m_vonKochView->Create(NULL, L"", WS_CHILD|WS_BORDER|WS_VISIBLE, CRect(10, 10, 550, 340), this, 50001);          // 추가
    m_vonKochView->OnInitialUpdate();       // 추가

    ASSERT((IDM_ABOUTBOX & 0xFFF0) == IDM_ABOUTBOX);
    ASSERT(IDM_ABOUTBOX < 0xF000);

    CMenu* pSysMenu = GetSystemMenu(FALSE);

    if(pSysMenu != nullptr) {
        BOOL bNameValid;
        CString strAboutMenu;
        bNameValid = strAboutMenu.LoadString(IDS_ABOUTBOX);
        ASSERT(bNameValid);

        if(!strAboutMenu.IsEmpty()) {
            pSysMenu->AppendMenu(MF_SEPARATOR);
            pSysMenu->AppendMenu(MF_STRING, IDM_ABOUTBOX, strAboutMenu);
        }
    }

    SetIcon(m_hIcon, TRUE);
    SetIcon(m_hIcon, FALSE);

    return TRUE;
}

void CMFCApplication8Dlg::OnSysCommand(UINT nID, LPARAM lParam) {
    if((nID & 0xFFF0) == IDM_ABOUTBOX) {
        CAboutDlg dlgAbout;
        dlgAbout.DoModal();
    } else {
        CDialog::OnSysCommand(nID, lParam);
    }
}

void CMFCApplication8Dlg::OnPaint() {
    if(IsIconic()) {
        CPaintDC dc(this);

        SendMessage(WM_ICONERASEBKGND, reinterpret_cast<WPARAM>(dc.GetSafeHdc()), 0);

        int cxIcon = GetSystemMetrics(SM_CXICON);
        int cyIcon = GetSystemMetrics(SM_CYICON);
        CRect rect;
        GetClientRect(&rect);
        int x = (rect.Width() - cxIcon + 1) / 2;
        int y = (rect.Height() - cyIcon + 1) / 2;

        dc.DrawIcon(x, y, m_hIcon);
    } else {
        CDialog::OnPaint();
    }
}

// 추가
void CMFCApplication8Dlg::OnDestroy() {
    delete m_vonKochView;
}

HCURSOR CMFCApplication8Dlg::OnQueryDragIcon() {
    return static_cast<HCURSOR>(m_hIcon);
}
```

# 결과

## level == 1

![Figure](/assets/images/mfc/studying/snowflake/snow-level1.png)

## level == 2

![Figure](/assets/images/mfc/studying/snowflake/snow-level2.png)

## level == 3

![Figure](/assets/images/mfc/studying/snowflake/snow-level3.png)

## level == 4

![Figure](/assets/images/mfc/studying/snowflake/snow-level4.png)

# 참고

## 다운로드

[다운로드](https://github.com/enfycius/Air/raw/main/MFC/von%20Koch/snowflake/snowflake.zip)

