# svelte-image-slider

## 💬 설명

이 프로젝트는 웹 페이지에서 간단한 이미지 슬라이드를 구현한 것입니다.

&nbsp;

## 🖥️ 화면 구성

| 초기화면 |
|:----:|
| ![image](https://github.com/kmseunh/svelte-projects/assets/105186724/1db4d52f-a31e-4b50-82e2-ae4e66008eb2) |

&nbsp;

## 🛠️ 기능 설명

- 사용자가 수동으로 이전 이미지와 다음 이미지로 이동할 수 있는 버튼을 제공합니다.
- 자동 슬라이드 기능을 통해 일정 시간마다 자동으로 이미지가 전환됩니다.

&nbsp;

## </> 주요 코드

```ts
const nextImage = (): void => {
    currentIndex = (currentIndex + 1) % images.length;
};

const prevImage = (): void => {
    currentIndex = (currentIndex - 1 + images.length) % images.length;
};

const toggleAutoSlide = (): void => {
    if (autoSlideRunning) {
        clearInterval(interval);
    } else {
        interval = setInterval(nextImage, 5000);
    }
    autoSlideRunning = !autoSlideRunning;
};
```
