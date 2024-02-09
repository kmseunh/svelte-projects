# svelte-random-color-generator

## 💬 설명

이 프로젝트는 랜덤한 색상을 생성하고 화면에 표시하는 간단한 웹 애플리케이션입니다.

&nbsp;

## 🖥️ 화면 구성

| Hex 색상 생성 시 | RGB 색상 생성 시 |
|:----:|:----:|
| ![image](https://github.com/kmseunh/svelte-projects/assets/105186724/bfa8cd5d-a7dc-4e52-8a62-6212a63ae346) | ![image](https://github.com/kmseunh/svelte-projects/assets/105186724/80bdaa81-a2d8-47df-a178-4c3be19d1355)|

&nbsp;

## 🛠️ 기능 설명

- `Create HEX Color` 버튼은 무작위 HEX 색상 코드를 생성합니다.
  - 생성된 HEX 색상 코드는 페이지의 배경색으로 설정되고, 화면의 색상 표시 요소에 텍스트로 표시됩니다.
- `Create RGB Color` 버튼은 무작위 HEX 색상 코드를 생성합니다.
  - 생성된 RGB 색상 코드는 페이지의 배경색으로 설정되고, 화면의 색상 표시 요소에 텍스트로 표시됩니다.
- Generate Random Color 버튼을 클릭하면 무작위로 HEX 또는 RGB 색상 코드를 생성합니다.
  - 생성된 색상 코드는 페이지의 배경색으로 설정되고, 화면의 색상 표시 요소에 텍스트로 표시됩니다.

&nbsp;

## </> 주요 코드

```ts
const createHexColor = (): string => {
    let hexColor: string = '#';
    for (let i = 0; i < 6; i++) {
        hexColor +=
            HEX_VALUES[Math.floor(Math.random() * HEX_VALUES.length)];
    }
    return hexColor;
};
```
