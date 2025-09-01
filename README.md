## MFC

* 오래된 C++/Win32 기반 프레임워크
* 메시지 맵, GDI로 UI 작성
* **장점**: 기존 코드와 호환성, 빠른 네이티브 성능
* **단점**: 현대적 UI(터치, 다크모드, 애니메이션) 구현 어려움

## WinUI 3

* 최신 Windows App SDK 기반 프레임워크
* XAML + GPU 가속, MVVM 패턴 지원
* **장점**: 현대적 UI/UX, 반응형·테마·고DPI 지원
* **단점**: 학습곡선 있음, 기존 MFC 코드와 직접 호환 어려움

---

👉 정리:

* **기존 프로젝트 유지·확장 → MFC**
* **새 프로젝트, 최신 UX 필요 → WinUI 3**

# Windows App SDK와 WinUI3의 관계

## Windows App SDK = “플랫폼 전체”
→ 앱 라이프사이클, 패키징, API 접근, UI 프레임워크 등 종합 제공

## WinUI 3 = “Windows App SDK 안의 UI 부분”
→ 화면 구성 및 사용자 인터페이스 담당

즉, **Windows App SDK는 큰 틀(앱 개발 생태계)**이고, WinUI 3는 그 안에 포함된 UI 엔진입니다.
