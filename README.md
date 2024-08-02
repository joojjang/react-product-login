# FE 카카오 선물하기 5주차 과제: 테스트 코드 작성

## 1단계 구현 사항

- [x] Jest와 React Testing Libaray로 테스트 환경 구축 (CRA로 이미 환경 세팅되어 있었음)
- [x] 단위 테스트
  - [x] CountOptionItem에서 +, - 버튼 클릭 시 수량 조절되는지
- [x] 통합 테스트
  - [x] 상품 상세 페이지 수량 조절 버튼 클릭 시 totalPrice 변경되는지
  - [x] 결제 페이지
    - [x] 현금영수증 Checkbox가 true/false인 경우 폼이 활성화/비활성화되었는지, true인 경우 입력 값이 모두 유효한지
    - [x] form의 validation 로직이 정상 동작하는지
- [ ] MSW를 사용하여 Mock API가 동작하도록 해요. (상세 API / 옵션 API)

## 2단계 구현 사항

- [x] 회원가입 화면 UI와 기능 구현
  - [x] 회원가입을 하면 로그인이 되도록 - 세션 스토리지에 정보 저장
- [x] 위시 기능
  - [x] 상품 상세 페이지에 위시 버튼 추가
  - [x] 버튼을 클릭 했을 때 관심 추가/삭제하는 로직
  - state로만 관리하고 있음. 실제 API 연결 X
  - 관심 등록/삭제 시 Alert 메시지 노출
- [x] **관심 목록 리스트** 구현
  - [x] 내비게이션 바 추가하고 그 안에 위시 탭 추가, 위시 페이지 생성
  - [ ] 관심 목록 API는 [카카오테크 선물하기 API 노션](https://www.notion.so/c78c990bf1264a5a91c4421e125a28c8?pvs=21)의 response 데이터를 사용해요.
  - [x] **관심 목록 리스트에서 관심 삭제가 가능하게** 해요. → 목록에서 사라지게는 아직 미구현 (API 구현 후 구현할 예정)

## 3단계 질의응답

### 질문 1.

Test code를 작성해보면서 좋았던 점과 아쉬웠던 점에 대해 말해주세요.

---

가능한 모든 테스트 시나리오를 하나하나 생각하는 것이 어려웠지만, 테스트 코드를 작성함으로써 유저가 겪을 수 있는 버그를 미리 확인할 수 있다는 점에서 테스트 코드 작성의 필요성을 느꼈습니다.  
Jest가 axios 구문을 파싱하지 못한다는 오류를 접했는데, 이를 해결하기 위해 Jest가 ESM을 파싱할 수 있도록 바벨 설정을 커스텀하여 ESM을 CommonJS로 변환하려 했지만 해결되지 않아서 비동기 통신이 필요한 테스트들이 제대로 수행되지 않은 점이 아쉽습니다.

### 질문 2.

스스로 생각했을 때 좋은 컴포넌트란 무엇인지 본인만의 기준을 세우고 설명해 주세요.

---

처음 보는 사람도 디렉토리 구조를 한눈에 이해할 수 있도록 컴포넌트를 구성해야 하고, 컴포넌트명은 해당 컴포넌트가 수행하는 기능을 알아볼 수 있게 잘 지어야 합니다.  
이를 위해서는 너무 많거나 복잡한 기능을 한 컴포넌트에 넣어서는 안 됩니다.  
또 변수는 외부에서 받아와서 사용해야 독립성을 유지하고 재사용성을 높일 수 있습니다.

재사용이 되지 않더라도 분리해야 하는 경우가 있다면 하나의 컴포넌트 안에 너무 많은 기능이나 또 다른 컴포넌트가 들어가 있는 경우입니다.  
예를 들어보면, 어떤 한 페이지를 하나의 컴포넌트로 만들면 너무 거대해지기도 하고 에러 발생 시 추적과 해결이 어려워집니다.  
이런 경우에는 가독성 및 유지보수성을 위해 페이지 레이아웃에 따라 (사이드바와 콘텐츠 등의) 영역을 구분하여 별개의 컴포넌트로 분리하는 것이 좋습니다.

### 질문 3.

스스로 생각했을 때 공통 컴포넌트를 만들 때 가장 중요한 요소 2개를 선택하고 이유와 함께 설명해주세요.

---

공통 컴포넌트를 만들 때 재사용성 및 관심사 분리를 가장 중요한 요소로 꼽겠습니다.  
공통 컴포넌트는 여러 군데에서 중복 사용되는 코드를 줄이는 데 의미가 있습니다.  
따라서 재사용성 및 독립성을 고려해서 컴포넌트를 작성하는 것이 필요합니다.

그런데 "중복"에만 집중하여 UI가 같다고 같은 컴포넌트를 쓰도록 만들게 되면 오히려 재사용성이 떨어지는 상황이 발생합니다.  
컴포넌트에 넣어야 할 기능이 너무 많아 자꾸 prop을 추가해야 하고, 예외 사항에 대한 분기 처리를 해야 합니다.  
따라서 관심사 분리를 통해 UI와 비즈니스 로직을 분리하여 컴포넌트를 작성하는 것이 중요합니다.
