# svelte-typing-speed-test

## 💬 설명

이 프로젝트는 사용자의 타자 속도를 측정하고 향상시킬 수 있는 애플리케이션입니다.

&nbsp;

## 🖥️ 화면 구성

| 초기 화면 | 테스트 완료 화면|
|:----:|:----:|
| ![image](https://github.com/kmseunh/svelte-projects/assets/105186724/a99129af-9848-43b7-a50f-0b767c987dc5) | ![image](https://github.com/kmseunh/svelte-projects/assets/105186724/48779b50-e9ab-42d7-bdd4-db0d9dffff2f) |

&nbsp;

## 🛠️ 기능 설명

- 사용자는 주어진 텍스트를 입력할 수 있습니다.
- 텍스트 입력란에서는 엔터 키를 눌러 테스트를 종료할 수 있습니다.
- 사용자가 테스트를 시작하면, 애플리케이션은 사용자가 텍스트를 입력하는 시간을 측정합니다.
- 테스트가 종료되면, 입력된 텍스트의 단어 수를 계산하여 타자 속도를 분당 단어 수로 계산합니다.

&nbsp;

## </> 주요 코드

```ts
const endTest = (): void => {
    if (startTime && text.trim() !== '') {
        elapsedTime = (Date.now() - startTime.getTime()) / 1000;
        wordCount = text.trim().split(/\s+/).length;
        typingSpeed = Math.round(wordCount / (elapsedTime / 60));
        started = false;
    }
};
```
