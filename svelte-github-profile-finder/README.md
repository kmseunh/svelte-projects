# svelte-github-profile-finder

## 💬 설명

이 프로젝트는 사용자가 `GitHub` 프로필을 검색하고 해당 사용자에 대한 기본 정보를 볼 수 있는 간단한 웹 애플리케이션입니다.

&nbsp;

## 🖥️ 화면 구성

| 초기 화면 | Profile 검색 화면|
|:----:|:----:|
| ![image](https://github.com/kmseunh/svelte-projects/assets/105186724/cf2a1b51-18d5-4e26-b04e-434f64f2a896) | ![image](https://github.com/kmseunh/svelte-projects/assets/105186724/73f9135e-8106-48f4-9c9b-62235ed1afe8) |

&nbsp;

## 🛠️ 기능 설명

- 사용자는 제공된 텍스트 필드에 `GitHub` 사용자 이름을 입력할 수 있습니다.
- 검색 버튼을 클릭하면 애플리케이션은 제공된 사용자 이름을 사용하여 `GitHub API`에서 사용자 데이터를 가져옵니다.
- 사용자 데이터를 성공적으로 가져온 경우, 애플리케이션은 사용자에 대한 다양한 세부 정보를 표시합니다.

&nbsp;

## </> 주요 코드

```ts
const fetchData = async () => {
    try {
        const response = await axios.get<User>(
            `https://api.github.com/users/${userName}`
        );
        user = response.data;
        console.log(user);
    } catch (error) {
        console.log('Error fetching data:', error);
    }
};
```
