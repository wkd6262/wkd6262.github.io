# 😎포트폴리오 제작일지

## 📝 목표

- 📌 사용자의 편의가 우선인, 심플하고 깔끔한 느낌을 주고 싶다.
- 📌 간단해 보이지만 많은 걸 보여줄 수 있는 페이지를 만들고 싶다.
- 📌 원 페이지 구조이므로 심심하지 않게 스크롤 이벤트, 애니메이션 제공.
- 📌 클론이 아닌 나만의 포트폴리오 사이트를 만들자.

## 🗂 디렉토리 구조

| ![디렉토리 구조](https://github.com/wkd6262/wkd6262.github.io/assets/142865132/71a89e0d-c63f-4c29-96ce-721450d98bd2) | ![디렉토리 구조](https://github.com/wkd6262/wkd6262.github.io/assets/142865132/6a01eb64-39b6-42ae-81b1-fd504d0e0d3a) | ![디렉토리 구조](https://github.com/wkd6262/wkd6262.github.io/assets/142865132/2c2e757f-6ac2-42c5-bd05-e7684a61dd11) |
| --- | --- | --- |
| **원 페이지로 깔끔, 심플함을 줌.** | **module.css를 사용해 css겹침 현상 배제.** | **답답해 보이지 않도록 margin으로 여백을 주었음.** |



## 🛠사용 기술

- **REACT ,   JAVASCRIPT ,   CSS3**
- **VSCODE ,   GITHUB ,   FIGMA**

## ✅ 컴포넌트 구성

## **Header**

- ㅇㅈ, 이름의 초성 로고만을 넣어 심플함을 강조
- UseEffect-스크롤 이벤트 - project,stack,more 부분 도달시 글씨 변경
- backdrop-filter 를 사용하여 심심한 디자인에 포인트를 줌
- Positon fixed 사용하여 상단 고정, border-bottom 으로 경계선 표시
- 스크롤 함수
    
    ```jsx
    const handleScroll = () => {
        const projectElement = projectRef.current;
        const stackElement = stackRef.current;
        const moreElement = moreRef.current;
        const scrollY = window.scrollY || window.pageYOffset;
    
        if (projectElement) {
          const projectTop = projectElement.offsetTop;
          const projectBottom = projectTop + projectElement.offsetHeight;
    
          if (scrollY >= projectTop && scrollY <= projectBottom) {
            setIsInProject(true);
          } else {
            setIsInProject(false);
          }
        }
        if (stackElement) {
          const stackTop = stackElement.offsetTop;
          const stackBottom = stackTop + stackElement.offsetHeight;
    
          if (scrollY >= stackTop && scrollY <= stackBottom) {
            setIsInStack(true);
            setIsInProject(false);
          } else {
            setIsInStack(false);
          }
        }
        if (moreElement) {
          const moreTop = moreElement.offsetTop;
          const moreBottom = moreTop + moreElement.offsetHeight;
    
          if (scrollY >= moreTop && scrollY <= moreBottom) {
            setIsInMore(true);
            setIsInStack(false);
            setIsInProject(false);
          } else {
            setIsInMore(false);
          }
        }
      };
    
      useEffect(() => {
        window.addEventListener("scroll", handleScroll);
    
        return () => {
          window.removeEventListener("scroll", handleScroll);
        };
      }, []);
    ```
    

## **Project**

- UseEffect 스크롤 이벤트 나타나는 효과로 심플한 구성에 시각적인 효과를 추가
- 프로젝트 이미지들을 스와이퍼로 나타내어 여러 이미지를 한 곳에 볼 수 있음
- Autoplay를 사용하여 사용자의 클릭 빈도를 줄임
- 제목, 개인(팀),기간, 기술 들을 나타내어 한 눈에 간편히 볼 수 있음
- 자세히 볼 수 있게 링크를 만들어 사용자의 이동 편리성 상승

## **Stack**

- useEffect 스크롤 이벤트를 사용해 시각적 효과 제공
- 제목과 내용의 font-size, 간격, 자간, 등을 차별화하여 가독성 상승 효과

## **More**

- 한 눈에 이야기를 전달 하고 싶어 100vh로 설정
- lettere-space,애니메이션 등을 사용해 시각적 효과 제공
- Link를 제공하므로 사용자의 클릭을 유도

## **Footer**

- 심플함을 강조하고 싶어 기능 요소들을 넣지 않고 이메일만 넣어 기억에 남도록 유도

## 🧰 문제 및 해결

❓ **Scroll 이벤트 문제** 

- 💭 Javascript에서 사용하던 addEvent를 이용해 스크롤 이벤트를 구현하려 했지만 React 특성 상 컴포넌트 연결식이므로 구현에 문제
- ❗**Ref,useEffect를 사용해 구현에 성공**

```jsx
useEffect(() => {
    const handleScroll = () => {
      const scrolled = window.scrollY;
      const offsetTop = projectRef.current.offsetTop;

      setScrollVisible(scrolled > offsetTop - window.innerHeight / 2);
      setScrollVisible2(scrolled > offsetTop - window.innerHeight / 4);
      setScrollVisible3(scrolled > offsetTop + window.innerHeight / 3);
    };

    window.addEventListener("scroll", handleScroll);

    return () => {
      window.removeEventListener("scroll", handleScroll);
    };
  }, [projectRef]);
```

- 💭Header가 각 구간에 맞춰서 글씨가 변경되게 설정하는 스크롤 이벤트 구현을 하고 싶었지만 Ref에 미숙하여 문제 발생
- ❗**블로그,GPT**를 통해 정보를 얻어 각 구간을 설정하는 **App.js**에 **useRef**를 사용해 각 구간을 **ref로 정의**하여 그 **구간에 들어 올 때 글씨가 변경** 되게 {txt} 함수로 설정하여 구현에 성공

```jsx
const handleScroll = () => {
    const projectElement = projectRef.current;
    const stackElement = stackRef.current;
    const moreElement = moreRef.current;
    const scrollY = window.scrollY || window.pageYOffset;

    if (projectElement) {
      const projectTop = projectElement.offsetTop;
      const projectBottom = projectTop + projectElement.offsetHeight;

      if (scrollY >= projectTop && scrollY <= projectBottom) {
        setIsInProject(true);
      } else {
        setIsInProject(false);
      }
    }
    if (stackElement) {
      const stackTop = stackElement.offsetTop;
      const stackBottom = stackTop + stackElement.offsetHeight;

      if (scrollY >= stackTop && scrollY <= stackBottom) {
        setIsInStack(true);
        setIsInProject(false);
      } else {
        setIsInStack(false);
      }
    }
    if (moreElement) {
      const moreTop = moreElement.offsetTop;
      const moreBottom = moreTop + moreElement.offsetHeight;

      if (scrollY >= moreTop && scrollY <= moreBottom) {
        setIsInMore(true);
        setIsInStack(false);
        setIsInProject(false);
      } else {
        setIsInMore(false);
      }
    }
  };

  useEffect(() => {
    window.addEventListener("scroll", handleScroll);

    return () => {
      window.removeEventListener("scroll", handleScroll);
    };
  }, []);

<h3>
        {isInProject
          ? "프로젝트,"
          : isInStack
          ? "기술,"
          : isInMore
          ? "끝이 아닌,"
          : "ㅇㅈ,"}
      </h3>
```

## 📓✏ 일지

### 2023 - 12 - 26

- [**gdweb**](https://www.gdweb.co.kr/sub/list.asp) 사이트에서 UI참고를 위해 목표를 반영하여 하나의 사이트를 선정하여 기획
- 4개의 목표 설정 및 One 페이지 방향으로 기획

### 2023 - 12 - 27

- 참고 사이트를 Figma를 이용해 와이어 프레임을 제작
- 전 세계 프론트엔드, 국내 등 다양한 포트폴리오를 검색하고 찾아보며 정보를 얻음
- 와이어프레임을 제작한 후 포트폴리오의 페이지, 기능적인 구현 디자인 작업 시작

### 2023 - 12 - 28

- 목표 방향에 맞게 디자인 작업 후 완성된 디자인에 대해 고민
- 시간이 부족하다고 판단하여 참고사이트를 많이 클론하게 되었음

### 2023 - 12 - 29

- 클론을 하면 포트폴리오에서 자신의 모습을 담지 못한다고 판단하여 새로운 디자인 구상
- 피드백 → 글자의 크기 및 자간,  글자의 굵기에 따른 가독성, 프로젝트 구간 UI
- 피드백을 수렴하여 디자인을 다시 수정 ~ 1/2 까지 기능구현 계획

### 2024 - 01 - 02

- 피드백 → 스킬 상세 설명, 불필요한 이벤트 제거, 사용자의 클릭 수 빈도를 낮춤
- 피드백을 수렴하여 모바일(390px) 디자인 및 제작 및 제출

### 2024 - 01 - 04 ~ 2024 - 01 - 05

- 2차 제출 후 수정 보완 , 프로젝트 보고서 정리 기록

## 👉  [포트폴리오 바로 가기](https://wkd6262.github.io/)https://wkd6262.github.io/){:target="_blank"}
