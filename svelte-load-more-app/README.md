# svelte-load-more-app

## 💬 설명

 이 프로젝트는 `JSONPlaceholder API`에서 게시물을 가져와 그리드 레이아웃으로 표시합니다. 사용자는 "Load More" 버튼을 클릭하여 더 많은 게시물을 로드할 수 있습니다.

&nbsp;

## 🖥️ 화면 구성

| 초기화면 | 클릭 시 |
|:----:|:----:|
| ![image](https://github.com/kmseunh/svelte-projects/assets/105186724/b9e3fece-0fd6-4094-88eb-89ffb67933c0) | ![image](https://github.com/kmseunh/svelte-projects/assets/105186724/cff086e6-326b-493b-932e-86b223e8738b)|

&nbsp;

## 🛠️ 기능 설명

- `JSONPlaceholder API`에서 초기 데이터를 가져옵니다. 애플리케이션이 시작될 때, 처음 9개의 게시물을 가져와 `Svelte` 스토어에 저장합니다.

- 가져온 게시물은 그리드 레이아웃을 사용하여 화면에 표시됩니다. 각 게시물은 제목과 내용을 포함하고 있습니다.

- 사용자는 "`Load More`" 버튼을 클릭하여 추가 게시물을 가져올 수 있습니다. 버튼 클릭 시 이전 게시물의 `ID`를 기준으로 다음 9개의 게시물을 가져와 기존 게시물 목록에 추가합니다.

- 데이터를 가져오는 동안 사용자에게 로딩 상태를 알려주기 위해 "`Load More`" 버튼 내에 회전하는 로더가 표시됩니다.

&nbsp;

## </> 주요 코드

```ts
    const loadMore = async () => {
        try {
            isLoading = true;
            if ($items.length > 0) {
                const lastItemId = $items[$items.length - 1].id;

                const response = await fetch(
                    `https://jsonplaceholder.typicode.com/posts?_start=${
                        lastItemId + 1
                    }&_limit=9`
                );
                const data = await response.json();
                items.update((existingItems) => [...existingItems, ...data]);
            }
        } catch (error) {
            console.error('Error fetching data:', error);
        } finally {
            isLoading = false;
        }
    };
```
