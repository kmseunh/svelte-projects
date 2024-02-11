# svelte-light-dark-mode

## 💬 설명

이 프로젝트는 다크 모드 토글 기능을 구현한 것입니다.

&nbsp;

## 🖥️ 화면 구성

| 초기 화면 | QR CODE 생성 화면
|:----:|:----:|
| ![image](https://github.com/kmseunh/svelte-projects/assets/105186724/2e64c99f-0d6b-484e-9016-f3c6898d5c34) | ![image](https://github.com/kmseunh/svelte-projects/assets/105186724/e5b24299-0753-4a9e-a98a-2c39d06045fe) |

&nbsp;

## 🛠️ 기능 설명

- 사용자가 다크 모드와 라이트 모드 사이를 전환할 수 있습니다.
- 사용자의 설정이 로컬 스토리지에 저장되어 페이지를 새로 고침해도 유지됩니다.

&nbsp;

## </> 주요 코드

```ts
    const toggle = (): void => {
        darkMode = !darkMode;
        document.body.classList.toggle('dark', darkMode);
        localStorage.setItem('darkMode', darkMode ? 'true' : 'false');
        dispatch('toggle', { darkMode });
    };
```
