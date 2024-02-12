# svelte-tabs

## 💬 설명

이 프로젝트는 외부 API에서 사용자 데이터를 가져와서 표시하는 간단한 웹 애플리케이션입니다.

&nbsp;

## 🖥️ 화면 구성

| 메인 화면 |
|:----:|
| ![image](https://github.com/kmseunh/svelte-projects/assets/105186724/fd22ecdb-94ca-4f90-8be0-2495b71b19dd) |

&nbsp;

## 🛠️ 기능 설명

- 외부 API에서 가져온 사용자 데이터를 사용하여 사용자 목록을 표시합니다.
- 사용자를 클릭하여 해당 사용자의 정보를 표시합니다.
- 선택한 사용자의 정보를 동적으로 표시합니다.

&nbsp;

## </> 주요 코드

```ts
const setActiveTab = (tabNumber: number): void => {
    activeTab = tabNumber;
};

const fetchData = async () => {
    try {
        const response = await axios.get<User[]>(
            'https://jsonplaceholder.typicode.com/users'
        );
        users = response.data;
    } catch (error) {
        console.log('Error fetching data:', error);
    }
};
```
