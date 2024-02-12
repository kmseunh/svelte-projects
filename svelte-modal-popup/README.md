# svelte-tabs

## 💬 설명

이 프로젝트는 모달 컴포넌트를 구현한 것입니다.

&nbsp;

## 🖥️ 화면 구성

| 기본 화면 | Modal 화면 |
|:----:|:----:|
| ![image](https://github.com/kmseunh/svelte-projects/assets/105186724/1baf60ba-b1c5-44dd-b69d-4faa82eb5f54) | ![image](https://github.com/kmseunh/svelte-projects/assets/105186724/4d15733b-481a-4d34-95c5-17a0baacc94c) |

&nbsp;

## 🛠️ 기능 설명

- 사용자는 `"Toggle Modal"` 버튼을 클릭하여 모달을 열거나 닫을 수 있습니다.
- 모달은 전역 상태로 관리되며, 버튼 클릭에 따라 상태가 변경됩니다.
- 모달의 제목과 내용을 동적으로 변경할 수 있습니다.
- 기본 제목과 내용이 제공되며, 필요에 따라 사용자 정의할 수 있습니다.

&nbsp;

## </> 주요 코드

```ts
export let title: string = 'Default Title';
export let content: string = 'Default Content';
export let isOpen: boolean = false;

const dispatch = createEventDispatcher();

const closeModal = (): void => {
    isOpen = false;
    dispatch('close');
};
```

```html
<Modal bind:isOpen={showModal} title={modalTitle} content={modalContent} />
```
