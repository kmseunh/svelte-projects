# svelte-star-rating

## 💬 설명

이 프로젝트는 사용자가 별점을 평가할 수 있는 간단한 별점 평가 컴포넌트를 구현한 것입니다.

&nbsp;

## 🖥️ 화면 구성

| 초기화면 | 클릭 시 |
|:----:|:----:|
| ![image](https://github.com/kmseunh/svelte-projects/assets/105186724/0a264a69-569d-45ec-b4ff-e3af411767fd) | ![image](https://github.com/kmseunh/svelte-projects/assets/105186724/eadd3064-1370-4398-87a2-e78f8a61df07)|

&nbsp;

## 🛠️ 기능 설명

- 사용자에게 5개의 별이 표시되며, 각 별은 `hover` 및 클릭 가능합니다.
- 마우스를 이용하여 별을 `hover`하면 해당 별을 기준으로 별점이 설정됩니다. 클릭하면 해당 별까지의 별점이 선택됩니다.

&nbsp;

## </> 주요 코드

```ts
    const setRating = (value: number) => {
        if (!clicked) {
            rating = value;
        }
    };

    const handleClick = (star: number) => {
        clicked = true;
        rating = star;
    };

    const resetRating = (): void => {
        if (!clicked) {
            rating = 0;
        }
    };
```
