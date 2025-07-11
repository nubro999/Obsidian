

---

# MVVM (Model-View-ViewModel) 패턴

MVVM은 **Model-View-ViewModel**의 약자로, 소프트웨어 아키텍처 패턴 중 하나입니다.  
주로 **UI 개발(특히 WPF, Xamarin, React, Android, iOS 등)**에서 사용되며,  
코드의 **유지보수성**과 **테스트 용이성**을 높이고, **UI와 비즈니스 로직의 분리**를 목표로 합니다.

---

## 구성 요소

### 1. Model (모델)
- **정의:**  
  애플리케이션의 핵심 데이터와 비즈니스 로직을 담당합니다.
- **역할:**  
  데이터 구조, 데이터베이스 연동, 네트워크 통신, 비즈니스 규칙 등
- **예시:**  
  사용자 정보, 서버 API 호출, DB 저장 등

---

### 2. View (뷰)
- **정의:**  
  사용자에게 보여지는 UI(화면)입니다.
- **역할:**  
  데이터를 시각적으로 표현하며, 사용자 입력을 받습니다.
- **특징:**  
  View는 직접적으로 데이터를 처리하지 않고, ViewModel에 의존하여 데이터 바인딩만 수행합니다.

---

### 3. ViewModel (뷰모델)
- **정의:**  
  View와 Model 사이에서 중개자 역할을 합니다.
- **역할:**  
  - Model의 데이터를 가공해서 View에 제공
  - View의 명령(이벤트, 입력 등)을 받아서 처리 후 Model에 전달
  - View와 Model을 느슨하게 연결(주로 **데이터 바인딩** 사용)
- **특징:**  
  ViewModel은 UI 요소에 직접 접근하지 않고, Observable, LiveData, State 등으로 View와 소통합니다.

---

## MVVM 구조도

```
[사용자]
   ↓
 [View] ←→ [ViewModel] ←→ [Model]
```
- View는 ViewModel에 바인딩되어 데이터를 표시
- ViewModel은 Model에서 데이터를 가져와 가공
- Model은 실제 데이터와 비즈니스 로직을 담당

---

## MVVM의 장점

- **관심사의 분리**: UI와 비즈니스 로직을 명확히 분리
- **테스트 용이성**: ViewModel과 Model의 단위 테스트가 쉬움
- **유지보수성**: UI 변경 시 비즈니스 로직 영향이 적음
- **재사용성**: ViewModel을 여러 View에서 재사용 가능

---

## MVVM의 단점

- **구현 복잡성**: 소규모 프로젝트에서는 오히려 구조가 복잡해질 수 있음
- **학습 곡선**: 데이터 바인딩, 옵저버블 등 새로운 개념 학습 필요

---

## 실제 적용 예시 (간단한 흐름)

1. **사용자**가 View(화면)에서 버튼 클릭
2. View는 ViewModel에 이벤트 전달
3. ViewModel이 Model에 데이터 요청
4. Model이 데이터를 반환
5. ViewModel이 데이터를 가공해 View에 바인딩
6. View가 데이터 갱신된 내용을 사용자에게 표시

---

추가로,
- **MVVM**은 **MVC**(Model-View-Controller), **MVP**(Model-View-Presenter)와 함께 UI 아키텍처 패턴의 대표적인 예시입니다.
- **React**의 상태 관리, **Android**의 LiveData/ViewModel, **WPF**의 데이터 바인딩 등에서 널리 활용됩니다.
- - **Model(모델):** 데이터와 비즈니스 로직 담당 (MVC와 동일)
- **View(뷰):** UI를 담당 (MVC와 동일)
- **ViewModel(뷰모델):** View와 Model 사이에서 중개자 역할, 데이터 가공 및 상태 관리, **데이터 바인딩** 지원

---
## 예시로 보는 차이

- **MVC:**  
    버튼 클릭 → Controller가 이벤트 처리 → Model 데이터 변경 → View를 새로 그림(코드로 명시적으로 View 갱신)
    
- **MVVM:**  
    버튼 클릭 → ViewModel이 이벤트 처리 → Model 데이터 변경 → ViewModel의 상태가 바뀌면 **자동으로 View가 갱신**(데이터 바인딩)