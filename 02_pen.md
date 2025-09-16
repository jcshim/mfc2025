# SDI 펜 프로그램 실습 안내서 (코드 포함)

## 1. 프로젝트 준비

* Visual Studio에서 **MFC App → SDI** 프로젝트를 생성합니다.
* 예: `MFCApplication1`

---

## 2. Document에 데이터베이스 선언

**MFCApplication1Doc.h**

```cpp
class CMFCApplication1Doc : public CDocument
{
    ...
public:
    CObArray m_oa;   // 선 데이터를 저장할 배열
    ...
};
```

---

## 3. CLine 클래스 만들기

**CLine.h**

```cpp
#pragma once
#include <afx.h>

class CLine : public CObject
{
    DECLARE_SERIAL(CLine)

    CPoint m_From;
    CPoint m_To;

public:
    CLine() {}   // 기본 생성자 필수
    CLine(CPoint From, CPoint To) {
        m_From = From;
        m_To = To;
    }

    void Draw(CDC* pDC) {
        pDC->MoveTo(m_From);
        pDC->LineTo(m_To);
    }

    virtual void Serialize(CArchive& ar);
};
```

**CLine.cpp**

```cpp
#include "pch.h"
#include "CLine.h"

IMPLEMENT_SERIAL(CLine, CObject, 1)

void CLine::Serialize(CArchive& ar)
{
    if (ar.IsStoring())
        ar << m_From << m_To;
    else
        ar >> m_From >> m_To;
}
```

---

## 4. Document::Serialize 연결

**MFCApplication1Doc.cpp**

```cpp
void CMFCApplication1Doc::Serialize(CArchive& ar)
{
    m_oa.Serialize(ar);   // 배열 직렬화
}
```

---

## 5. View 준비

**MFCApplication1View\.h**

```cpp
class CMFCApplication1View : public CView
{
    ...
public:
    CPoint opnt;   // 이전 점 저장
    ...
    afx_msg void OnMouseMove(UINT nFlags, CPoint point);
};
```

---

## 6. OnDraw 함수

**MFCApplication1View\.cpp**

```cpp
void CMFCApplication1View::OnDraw(CDC* pDC)
{
    CMFCApplication1Doc* pDoc = GetDocument();
    ASSERT_VALID(pDoc);
    if (!pDoc) return;

    int n = pDoc->m_oa.GetSize();
    for (int i = 0; i < n; i++) {
        CLine* p = (CLine*)pDoc->m_oa[i];
        p->Draw(pDC);
    }
}
```

---

## 7. 마우스 이동 처리

**MFCApplication1View\.cpp**

```cpp
void CMFCApplication1View::OnMouseMove(UINT nFlags, CPoint point)
{
    if (nFlags == MK_LBUTTON) {
        CLine* p = new CLine(opnt, point);
        GetDocument()->m_oa.Add(p);     // 선 데이터 저장
        Invalidate(FALSE);              // 다시 그리기 요청
    }
    opnt = point;
    CView::OnMouseMove(nFlags, point);
}
```

---

## 8. 새 문서 처리

**MFCApplication1Doc.cpp**

```cpp
BOOL CMFCApplication1Doc::OnNewDocument()
{
    if (!CDocument::OnNewDocument())
        return FALSE;

    m_oa.RemoveAll();   // 새 문서 선택 시 데이터 초기화
    return TRUE;
}
```

---

## 9. 실행 & 확인

1. 프로그램 실행 → 마우스로 드래그하면 선이 그려진다.
2. 창 크기를 줄였다가 복원해도 그림이 유지된다.
3. \[파일 → 새로 만들기] 메뉴 실행 → 그림이 지워진다.
4. \[파일 → 저장] → `.dat` 파일로 저장된다.
5. \[파일 → 열기] → 저장한 그림이 다시 불러와진다.

---

## 10. 심화 확장

* `CLine`에 굵기(`int m_Size`)와 색상(`COLORREF m_Col`) 멤버를 추가
* `Draw`에서 `CPen`을 생성해 적용
* `Serialize`에 굵기와 색상 저장 추가
* **툴바/메뉴**에서 색상·굵기 변경 기능을 연결

---

👉 여기까지 따라하면 학생들이 직접 **펜 프로그램**을 완성할 수 있습니다.
선 그리기 → 저장/불러오기 → 새 문서 초기화 → 색상/굵기 확장까지 단계적으로 학습 가능합니다.
