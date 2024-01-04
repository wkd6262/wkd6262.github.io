# wkd6262.github.io

    if (currentScrollTop > lastScrollTop) {
        // 스크롤이 내려갈 때의 처리
        console.log("스크롤이 내려갑니다.");
        setIsScrolled(true);
      } else {
        // 스크롤이 올라갈 때의 처리
        console.log("스크롤이 올라갑니다.");
        setIsScrolled(false);
      }

# Header Component

## 🚀 기능 구현

### Scroll 이벤트 핸들링
- 섹션 진입 여부를 상태로 관리하는 `useState` 훅을 사용합니다.
- `useEffect` 훅을 활용하여 컴포넌트가 마운트되면 스크롤 이벤트 리스너를 등록하고, 언마운트되면 이를 해제합니다.

### 스크롤 위치 확인
- `handleScroll` 함수를 통해 프로젝트, 기술, 끝이 아닌 섹션의 위치를 확인하고, 스크롤 이벤트에 따라 진입 여부를 갱신합니다.

### 헤더 스타일 변경
- 현재 섹션에 따라 헤더에 다른 스타일을 적용합니다. 이는 조건부 클래스를 사용하여 동적으로 변경됩니다.

### 🌈 미끄러운 스크롤 효과
- 섹션 간 이동 시 미끄러운 스크롤 효과를 부여하여 사용자 경험을 향상시킵니다.
  - `scroll-behavior` CSS 속성을 활용하여 부드러운 스크롤을 적용합니다.

### 🎨 시각적 피드백
- 헤더에 현재 섹션을 나타내는 시각적 피드백을 추가합니다.
  - 현재 섹션에 따라 텍스트나 아이콘 색상을 변경하여 사용자에게 현재 위치를 명확하게 시각적으로 전달합니다.

### 💡 가독성 향상을 위한 스타일링
- `flex` 및 `list-style` 속성을 활용하여 헤더의 가독성을 향상시킵니다.
  - `display: flex`를 사용하여 헤더 요소들을 수평 정렬합니다.
  - `list-style-type: none`를 적용하여 목록 스타일을 제거합니다.

## 🛠 사용된 기술
- React
- `useState`, `useEffect` 훅 활용
- 조건부 클래스 적용
- 부드러운 스크롤 효과 (`scroll-behavior`)
- CSS `flex` 및 `list-style` 속성 활용
