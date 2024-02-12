# svelte-scroll-indicator

## 💬 설명

이 프로젝트는 사용자에게 페이지 스크롤 위치를 시각적으로 표시하는 간단한 웹 애플리케이션을 구현한 것입니다.

&nbsp;

## 🖥️ 화면 구성

| 초기 화면 | 실행 화면 |
|:----:|:----:|
| ![image](https://github.com/kmseunh/svelte-projects/assets/105186724/15781542-68ff-441f-89ba-e147ecc3b6a1) | ![image](https://github.com/kmseunh/svelte-projects/assets/105186724/6e21fe35-d1cd-4062-b05d-45743c04cde3) |

&nbsp;

## 🛠️ 기능 설명

- 사용자에게 현재 페이지 스크롤 위치를 시각적으로 표시하기 위해 스크롤 인디케이터가 제공됩니다.
- 스크롤 인디케이터는 페이지 상단에 고정되어 있으며, 페이지 스크롤 위치에 따라 크기가 조정됩니다.

&nbsp;

## </> 주요 코드

```ts
const calculateScrollPercentage = () => {
    const scrollableHeight =
        document.documentElement.scrollHeight - window.innerHeight;
    scrollPercentage = (window.scrollY / scrollableHeight) * 100;
};

const handleScroll = () => {
    requestAnimationFrame(calculateScrollPercentage);
};
```
