# svelte-password-generator

## 💬 설명

이 프로젝트는 사용자가 요구하는 기준에 따라 무작위로 생성된 안전한 암호를 제공하는 패스워드 생성기입니다.

&nbsp;

## 🖥️ 화면 구성

| 초기 화면 | 비밀번호 생성 화면
|:----:|:----:|
| ![image](https://github.com/kmseunh/svelte-projects/assets/105186724/23ecab8d-47c5-4425-93b6-893385f4450c) | ![image](https://github.com/kmseunh/svelte-projects/assets/105186724/361ca86a-ed20-4a4d-af55-077e23099fba) |

&nbsp;

## 🛠️ 기능 설명

- 사용자는 4에서 32 사이의 길이를 선택하여 원하는 암호 길이를 지정할 수 있습니다.
- 사용자는 대문자, 소문자, 숫자, 특수 문자 중 포함할 문자 유형을 선택할 수 있습니다.
- 사용자가 설정한 요구 사항에 따라 프로그램은 무작위로 선택된 문자들로 구성된 암호를 생성합니다.
- 생성된 암호를 사용자가 표시하거나 숨길 수 있는 옵션이 제공됩니다.

&nbsp;

## </> 주요 코드

```ts
if (includeUppercase) charset += uppercaseChars;
if (includeLowercase) charset += lowercaseChars;
if (includeNumbers) charset += numberChars;
if (includeSymbols) charset += symbolChars;

let newPassword: string = '';
for (let i = 0; i < length; i++) {
    const randomIndex = Math.floor(Math.random() * charset.length);
    newPassword += charset[randomIndex];
}
password = newPassword;
```
