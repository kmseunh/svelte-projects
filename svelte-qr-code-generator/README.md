# svelte-qr-code-generator

## 💬 설명

이 프로젝트는 입력된 텍스트에 대한 QR 코드가 생성되고 표시되는 QR 코드 생성기입니다.

&nbsp;

## 🖥️ 화면 구성

| 초기 화면 | QR CODE 생성 화면
|:----:|:----:|
| ![image](https://github.com/kmseunh/svelte-projects/assets/105186724/b732ba30-5e48-4426-b56f-084d03fdd12a) | ![image](https://github.com/kmseunh/svelte-projects/assets/105186724/05451e62-b57a-4e39-9897-63133d6a54b5) |

&nbsp;

## 🛠️ 기능 설명

- 사용자가 입력한 텍스트를 기반으로 QR 코드를 생성합니다.
- 버튼을 클릭하면 QR 코드가 생성되며, 입력된 텍스트는 QR 코드의 데이터로 사용됩니다.
- QR 코드가 생성되면 화면에 표시됩니다.
- QR 코드 생성 전에는 아무것도 표시되지 않습니다.

&nbsp;

## </> 주요 코드

```ts
    export let text: string = '';

    const dispatch = createEventDispatcher();

    let inputValue: string = '';
    let isButtonClicked: boolean = false;

    const generateQRCode = () => {
        dispatch('generate', {
            value: inputValue,
        });
        isButtonClicked = true;
    };

    $: {
        text = inputValue;
    }
```
