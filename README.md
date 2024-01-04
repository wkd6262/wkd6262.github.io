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

<span id="문제해결">문제 해결</span>
1) 스크롤 이벤트 처리
문제:
사용자의 스크롤 위치에 따라 헤더의 스타일을 업데이트하고 싶습니다.

해결:
이미 handleScroll 함수를 통해 문제를 해결하려고 시도하셨습니다. 이 함수를 개선하기 위해 더 간결한 접근 방식을 제안합니다. 뷰포트 내에 요소가 있는지 확인하는 재사용 가능한 isElementInView 도우미 함수를 만들어 사용할 수 있습니다.

jsx
Copy code
import React, { useState, useEffect } from "react";
import headerStyle from "../../styles/header.module.css";

const Header = ({ projectRef, stackRef, moreRef }) => {
  const [activeSection, setActiveSection] = useState(null);

  const isElementInView = (element) => {
    const scrollY = window.scrollY || window.pageYOffset;
    const elementTop = element.offsetTop;
    const elementBottom = elementTop + element.offsetHeight;

    return scrollY >= elementTop && scrollY <= elementBottom;
  };

  const handleScroll = () => {
    if (isElementInView(projectRef.current)) {
      setActiveSection("프로젝트");
    } else if (isElementInView(stackRef.current)) {
      setActiveSection("기술");
    } else if (isElementInView(moreRef.current)) {
      setActiveSection("끝이 아닌");
    } else {
      setActiveSection("ㅇㅈ");
    }
  };

  useEffect(() => {
    window.addEventListener("scroll", handleScroll);

    return () => {
      window.removeEventListener("scroll", handleScroll);
    };
  }, []);

  return (
    <div
      className={`${headerStyle.header} ${
        activeSection === "프로젝트" ? headerStyle.inProject : ""
      }`}
    >
      <h3>
        {activeSection === "프로젝트"
          ? "프로젝트,"
          : activeSection === "기술"
          ? "기술,"
          : activeSection === "끝이 아닌"
          ? "끝이 아닌,"
          : "ㅇㅈ,"}
      </h3>
    </div>
  );
};

export default Header;
위의 코드에서 isElementInView 함수를 사용하여 각 섹션의 가시성을 확인하고, activeSection 상태를 업데이트하여 헤더의 스타일을 동적으로 변경합니다.
