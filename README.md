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

# 포트폴리오 제작일지

## 📝 목표

<aside>
📌 사용자의 편의가 우선인, 심플하고 깔끔한 느낌을 주고 싶다.

</aside>

<aside>
📌 간단해 보이지만 많은 걸 보여줄 수 있는 페이지를 만들고 싶다.

</aside>

<aside>
📌 원 페이지 구조이므로 심심하지 않게 스크롤 이벤트, 애니메이션 제공.

</aside>

<aside>
📌 클론이 아닌 나만의 포트폴리오 사이트를 만들자.

</aside>

## 🗂 디렉토리 구조

![주석 2024-01-04 123150.png](%E1%84%91%E1%85%A9%E1%84%90%E1%85%B3%E1%84%91%E1%85%A9%E1%86%AF%E1%84%85%E1%85%B5%E1%84%8B%E1%85%A9%20%E1%84%8C%E1%85%A6%E1%84%8C%E1%85%A1%E1%86%A8%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%8C%E1%85%B5%205f0e2dbe337a4e64a79ad03137938228/%25EC%25A3%25BC%25EC%2584%259D_2024-01-04_123150.png)

원 페이지로 깔끔,심플함을 줌.

![주석 2024-01-04 123237.png](%E1%84%91%E1%85%A9%E1%84%90%E1%85%B3%E1%84%91%E1%85%A9%E1%86%AF%E1%84%85%E1%85%B5%E1%84%8B%E1%85%A9%20%E1%84%8C%E1%85%A6%E1%84%8C%E1%85%A1%E1%86%A8%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%8C%E1%85%B5%205f0e2dbe337a4e64a79ad03137938228/%25EC%25A3%25BC%25EC%2584%259D_2024-01-04_123237.png)

module.css를 사용해 css겹침 현상 배제.

![주석 2024-01-04 123252.png](%E1%84%91%E1%85%A9%E1%84%90%E1%85%B3%E1%84%91%E1%85%A9%E1%86%AF%E1%84%85%E1%85%B5%E1%84%8B%E1%85%A9%20%E1%84%8C%E1%85%A6%E1%84%8C%E1%85%A1%E1%86%A8%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%8C%E1%85%B5%205f0e2dbe337a4e64a79ad03137938228/%25EC%25A3%25BC%25EC%2584%259D_2024-01-04_123252.png)

답답해 보이지 않도록 margin으로 여백을 주었음.

## 🛠사용 기술

## **REACT    JAVASCRIPT    CSS3**

## **VSCODE    GITHUB    FIGMA**

## ✅ 컴포넌트 구성

<aside>
1️⃣ **Header**

ㅇㅈ, 이름의 초성 로고만을 넣어 심플함을 강조

UseEffect-스크롤 이벤트 - project,stack,more 부분 도달시 글씨 변경

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
    

backdrop-filter 를 사용하여 심심한 디자인에 포인트를 줌

Positon fixed 사용하여 상단 고정, border-bottom 으로 경계선 표시

</aside>

<aside>
2️⃣ **Project**

UseEffect 스크롤 이벤트 나타나는 효과로 심플한 구성에 시각적인 효과를 추가

프로젝트 이미지들을 스와이퍼로 나타내어 여러 이미지를 한 곳에 볼 수 있음

Autoplay를 사용하여 사용자의 클릭 빈도를 줄임

제목, 개인(팀),기간, 기술 들을 나타내어 한 눈에 간편히 볼 수 있음

자세히 볼 수 있게 링크를 만들어 사용자의 이동 편리성 상승

</aside>

<aside>
3️⃣ **Stack**

useEffect 스크롤 이벤트를 사용해 시각적 효과 제공

제목과 내용의 font-size, 간격, 자간, 등을 차별화하여 가독성 상승 효과

</aside>

<aside>
4️⃣ **More**

한 눈에 이야기를 전달 하고 싶어 100vh로 설정

lettere-space,애니메이션 등을 사용해 시각적 효과 제공

Link를 제공하므로 사용자의 클릭을 유도

</aside>

<aside>
5️⃣ **Footer**

이메일을 적었습니다.

</aside>

## 🧰 문제 및 해결

❓ **Scroll 이벤트 문제** 

<aside>
💭 Javascript에서 사용하던 addEvent를 이용해 스크롤 이벤트를 구현하려 했지만 React 특성 상 컴포넌트 연결식이므로 구현에 문제

</aside>

❗**Ref,useEffect를 사용해 구현에 성공**

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

<aside>
💭 **Header**가 각 **구간에 맞춰서 글씨가 변경**되게 설정하는 **스크롤 이벤트 구현**을 하고 싶었지만 **Ref에 미숙하여 문제** 발생

</aside>

❗**블로그,GPT**를 통해 정보를 얻어 각 구간을 설정하는 **App.js**에 **useRef**를 사용해 각 구간을 **ref로 정의**하여 그 **구간에 들어 올 때 글씨가 변경** 되게 {txt} 함수로 설정하여 구현에 성공

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

## ↗  포트폴리오 바로 가기
