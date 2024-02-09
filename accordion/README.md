# svelte-accordion

## 💬 설명

이 프로젝트는 확장 가능한 아코디언(`accordion`) UI 구현을 목표로 합니다.
&nbsp;

## 🖥️ 화면 구성

| accordion 활성화 | accordion 비활성화 |
|:-----------:|:-------------:|
| ![image](https://github.com/harblaith7/svelte-crash-course/assets/105186724/67535284-e524-4ee6-bd7a-7a7b9f4cafba) | ![image](https://github.com/harblaith7/svelte-crash-course/assets/105186724/f78b1cd5-cb7f-44fa-a94a-3795ca1b8d57)|

&nbsp;

## 🛠️ 기능 설명

- 각 아코디언 아이템은 제목과 내용으로 구성됩니다.
- 아코디언 아이템의 제목을 클릭하면 해당 아이템의 내용이 확장되거나 축소됩니다.
- 아이템의 내용이 현재 활성화된 상태인지는 버튼의 모양을 변경하여 나타냅니다.
- 한 번에 하나의 아이템만 활성화됩니다. 다른 아이템의 내용이 열리면 이전에 열려있던 아이템의 내용은 자동으로 닫힙니다.

## </> 주요 코드

```ts
let activeIndex: number = -1;

const handleIndex = (index: number): void => {
    activeIndex = activeIndex === index ? -1 : index;
};
```
