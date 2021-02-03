---
title: "List의 활용"

classes: wide

categories:
  - Data Structures
tags:
  - Data Structures
  - Programming
  - Coding
---

# 문제

자료구조는 구현도 중요하지만 이에 못지않게 활용도 중요하다.

실제로 이미 구현되어 있는 자료구조를 활용하는 것도 실력이다 !

따라서 다음 헤더파일에 정의된 구조체를 기반으로 List를 활용하는 예제를 작성해보기로 하겠다.

## NameCard.h

```c
#define NAME_LEN 30
#define PHONE_LEN 30

typedef struct __namecard
{
    char name[NAME_LEN];
    char phone[PHONE_LEN];

} NameCard;

// NameCard 구조체 변수의 동적 할당 및 초기화 후 주소 값 반환
NameCard* MakeNameCard(char* name, char* phone);

// NameCard 구조체 변수의 정보 출력
void ShowNameCardInfo(NameCard* pcard);

// 이름이 같으면 0, 다르면 0이 아닌 값 반환
int NameCompare(NameCard* pcard, char* name);

// 전화번호 정보를 변경
void ChangePhoneNum(NameCard* pcard, char* phone);
```

위의 헤더파일에 대응하는 소스파일 NameCard.c를 작성하자 !

그리고 아래에 나열된 순서대로 일을 진행하도록 main 함수를 정의하자.

물론 이를 위해서 앞서 구현한 리스트를 활용해야 한다.

1. 총 3명의 전화번호 정보를, 앞서 우리가 구현한 List에 저장한다.
2. 특정 이름을 대상으로 탐색을 진행하여, 그 사람의 정보를 출력한다.
3. 특정 이름을 대상으로 탐색을 진행하여, 그 사람의 전화번호 정보를 변경한다.
4. 특정 이름을 대상으로 탐색을 진행하여, 그 사람의 정보를 삭제한다.
5. 끝으로 남아있는 모든 사람의 전화번호 정보를 출력한다.

더불어 저장의 형태는 NameCard 구조체 변수의 주소 값이어야 하며, 위에서 언급하는 특정 이름은 임의로 지정하되 서로 다른 이름으로 저장하기로 하자.

## ArrayList.h

```c
#ifndef ArrayList_h
#define ArrayList_h

#include "NameCard.h"

#define TRUE    1   // '참'을 표현하기 위한 매크로 정의
#define FALSE   0   // '거짓'을 표현하기 위한 매크로 정의
#define LIST_LEN    100

typedef NameCard* LData;  // NameCard에 대한 typedef 선언

typedef struct __ArrayList  // 배열기반 리스트를 정의한 구조체
{
    LData arr[LIST_LEN];    // 리스트의 저장소인 배열
    int numOfData;          // 저장된 데이터의 수
    int curPosition;        // 데이터 참조위치를 기록
} ArrayList;

typedef ArrayList List;

void ListInit(List* plist);     // 초기화

void LInsert(List* plist, LData data);      // 데이터 저장

int LFirst(List* plist, LData* pdata);      // 첫 데이터 참조

int LNext(List* plist, LData* pdata);       // 두 번째 이후 데이터 참조

LData LRemove(List* plist);     // 참조한 데이터 삭제

int LCount(List* plist);        // 저장된 데이터의 수 반환

#endif /* ArrayList_h */
```

## ArrayList.c

```c
#include <stdio.h>
#include "ArrayList.h"

void ListInit(List* plist)
{
    (plist->numOfData) = 0;

    (plist->curPosition) = -1;
}

void LInsert(List* plist, LData data)
{
    if(plist->numOfData >= LIST_LEN)
    {
        puts("저장이 불가능합니다.");

        return;

    }
    
    plist->arr[plist->numOfData] = data;

    (plist->numOfData)++;

}

int LFirst(List* plist, LData* pdata)
{
    if(plist->numOfData == 0)
        return FALSE;

    (plist->curPosition) = 0;

    *pdata = plist->arr[0];

    return TRUE;
}

int LNext(List* plist, LData* pdata)
{

    if(plist->curPosition >= (plist->numOfData)-1)
        return FALSE;


    (plist->curPosition)++;

    *pdata = plist->arr[plist->curPosition];

    return TRUE;

}

LData LRemove(List* plist)
{
    int rpos = plist->curPosition;
    int num = plist->numOfData;
    int i;
    LData rdata = plist->arr[rpos];

    for(i=rpos; i<num-1; i++)
        plist->arr[i] = plist->arr[i+1];

    (plist->numOfData)--;
    (plist->curPosition)--;

    return rdata;

}

int LCount(List* plist)
{
    return plist->numOfData;
}
```

## NameCard.h

```c
#ifndef NameCard_h

#define NameCard_h
#define NAME_LEN    30
#define PHONE_LEN   30

typedef struct __namecard
{
    char name[NAME_LEN];
    char phone[PHONE_LEN];
} NameCard;

NameCard* MakeNameCard(char* name, char* phone);

void ShowNameCardInfo(NameCard* pcard);

int NameCompare(NameCard* pcard, char* name);

void ChangePhoneNum(NameCard* pcard, char* phone);

#endif /* NameCard_h */
```

## NameCard.c

```c
#include "NameCard.h"
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

NameCard* MakeNameCard(char* name, char* phone)
{
    NameCard* nc = (NameCard*)malloc(sizeof(NameCard));

    strcpy(nc->name, name);
    strcpy(nc->phone, phone);

    return nc;
}

void ShowNameCardInfo(NameCard* pcard)
{
    printf("이름: %s\n", pcard->name);
    printf("전화번호: %s\n", pcard->phone);
}

int NameCompare(NameCard* pcard, char* name)
{
    if(!strcmp(pcard->name, name))
        return 0;

    else
        return 1;
}

void ChangePhoneNum(NameCard* pcard, char* phone)
{
    strcpy(pcard->phone, phone);
}
```

## main.c

```c
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#include "NameCard.h"
#include "ArrayList.h"

int main(void)
{
    List list;
    ListInit(&list);
    NameCard* nc1;
    NameCard* nc2;

    nc1 = (NameCard*)malloc(sizeof(NameCard));
    nc2 = (NameCard*)malloc(sizeof(NameCard));

    int i;

    for(i=0; i<3; i++)
    {
        printf("이름 입력: ");
        scanf("%s", nc1->name);

        printf("전화번호 입력: ");
        scanf("%s", nc1->phone);

        LInsert(&list, MakeNameCard(nc1->name, nc1->phone));
    }

    printf("찾고자 하는 사람의 이름: ");
    scanf("%s", nc1->name);

    if(LFirst(&list, &nc2))
    {
        if(!NameCompare(nc2, nc1->name))
            ShowNameCardInfo(nc2);
        else
            while(LNext(&list, &nc2))
                if(!NameCompare(nc2, nc1->name))
                    ShowNameCardInfo(nc2);
    }

    printf("찾고자 하는 사람의 이름: ");
    scanf("%s", nc1->name);

    printf("바꾸고자 하는 전화번호: ");
    scanf("%s", nc1->phone);

    if(LFirst(&list, &nc2))
    {
        if(!NameCompare(nc2, nc1->name))
            ChangePhoneNum(nc2, nc1->phone);
        else
            while(LNext(&list, &nc2))
                if(!NameCompare(nc2, nc1->name))
                    ChangePhoneNum(nc2, nc1->phone);
    }

    printf("찾고자 하는 사람의 이름: ");
    scanf("%s", nc1->name);

    if(LFirst(&list, &nc2))
    {
        if(!NameCompare(nc2, nc1->name))
            LRemove(&list);
        else
        {
            while(LNext(&list, &nc2))
            {
                if(!NameCompare(nc2, nc1->name))
                {
                    LRemove(&list);

                }
            }
        }
    }

    if(LFirst(&list, &nc2))
    {
        ShowNameCardInfo(nc2);

        while(LNext(&list, &nc2))
            ShowNameCardInfo(nc2);
    }

    free(nc1);
    free(nc2);

    return 0;
}
```