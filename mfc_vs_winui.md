# **MFC**와 **WinUI 3**를 핵심 개념 한 줄 요약

* **MFC**: *네이티브 C++/Win32 래퍼*. 전통적 데스크톱 앱, 메시지 맵과 GDI 중심.
* **WinUI 3**: *현대 XAML UI + Windows App SDK*. DirectX 기반 렌더링, MVVM 친화, 고DPI·터치·애니메이션 등 최신 UX.

---

## 큰 그림 비교

| 항목                | MFC                                | WinUI 3                                  |
| ----------------- | ---------------------------------- | ---------------------------------------- |
| **앱 모델**          | 순수 Win32 데스크톱(네이티브 C++)            | Windows App SDK(Win32 프로세스 + WinRT/XAML) |
| **언어/런타임**        | C++ (CRT, COM 직접 다룸)               | C++/WinRT, C#(.NET) 모두 가능                |
| **UI 기술**         | GDI/GDI+, 리소스(.rc), 대화상자/메뉴        | XAML(선언형 UI), Composition/DirectX 가속     |
| **패턴**            | 메시지 맵(ON\_WM\_xxx), 문서/뷰(Doc/View) | MVVM 권장(바인딩·Command·DataTemplate)        |
| **디자인/스타일**       | 정적 리소스, 커스텀 난이도↑                   | 템플릿/스타일/리소스 사전으로 유연                      |
| **고DPI/터치/애니메이션** | 수동 대응, 작업량 큼                       | 기본 지원 우수                                 |
| **컨트롤 생태계**       | 성숙하지만 레거시 중심                       | 최신 Fluent 컨트롤, 지속 업데이트                   |
| **그래픽**           | CPU 렌더링 위주(GDI)                    | GPU 가속(Composition/Direct2D/Win2D)       |
| **배포**            | exe/msi, 관리자 권한/레지스트리 의존           | MSIX·Self-Contained(비패키지) 등 현대적 배포       |
| **학습 난이도**        | Win32 지식 필요, 러닝커브 완만하지만 저수준        | XAML/MVVM 학습 필요, 초반 러닝커브↑                |
| **성능/지연**         | 네이티브 콜, 오버헤드 낮음(그래픽 제외)            | UI 가속으로 부드러움, 바인딩 비용 존재                  |
| **장점**            | 기존 코드·장비 호환, 디버깅 단순                | 현대 UX, 반응형/접근성·현지화·테마 용이                 |
| **단점**            | 현대 UX 구현 난이도, 유지보수 비용 ↑            | 기존 MFC/COM 자산과의 직접 통합에 설계 필요             |

---

## 언제 무엇을 선택할까?

* **MFC 선택**

  * 기존 MFC/Win32 코드베이스와의 **재사용**·유지보수가 최우선.
  * 하드웨어 제어·드라이버 도구 등 **네이티브 API 밀접** 작업, UI는 단순.
  * 조직 표준/인증 등으로 기술 스택 변경이 어려움.

* **WinUI 3 선택**

  * **새 프로젝트**로 현대적 UX(다크모드, 애니메이션, 터치, 고DPI)가 중요.
  * **MVVM**로 큰 규모 앱을 구조적으로 개발/테스트하고 싶음.
  * 장기적으로 **Windows App SDK** 생태계(Fluent, WebView2, App Lifecycle)를 활용.

---

## 마이그레이션/혼합 전략

* **XAML Islands**: 기존 MFC 앱에 WinUI 3(XAML) 컨트롤을 “섬”처럼 호스팅해 **부분적 현대화**.
* **모듈별 전환**: 설정 대화상자, 리포트 뷰어, 대시보드 등 UX가치 높은 화면부터 WinUI 3로 교체.
* **공유 계층 분리**: 비즈니스 로직/네이티브 라이브러리는 공용(C++), UI만 단계적 교체.

---

## 학습 포인트 체크리스트

* **MFC**

  * `CWinApp / CFrameWnd / CDialog`, 메시지 맵, Doc/View
  * GDI(Device Context, 펜/브러시), 리소스(.rc), OLE/COM 기초

* **WinUI 3**

  * XAML 레이아웃(Grid/StackPanel), 바인딩/템플릿
  * MVVM(ObservableObject/Command), Navigation
  * Windows App SDK(윈도우 관리, AppLifecycle, WebView2)

---

## 빠른 결론

* **레거시 유지/확장**이 목적이면 **MFC**가 실용적.
* **새로운 앱·현대 UX**가 핵심이면 **WinUI 3**가 정석.
* **현실적 절충**은 *MFC + XAML Islands*로 “핵심 화면만 현대화 → 점진 전환”.

필요하시면, \*\*MFC → WinUI 3 단계별 전환 로드맵(6–8주)\*\*도 바로 만들어 드릴게요.
