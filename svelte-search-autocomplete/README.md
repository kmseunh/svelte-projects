# svelte-search-autocomplete

## 💬 설명

이 프로젝트는 사용자가 포켓몬의 이름을 검색하여 포켓몬의 세부 정보를 확인할 수 있는 웹 어플리케이션입니다.

&nbsp;

## 🖥️ 화면 구성

| 검색 시 화면 | 검색 결과 화면|
|:----:|:----:|
| ![image](https://github.com/kmseunh/svelte-projects/assets/105186724/1d0fc9ed-b745-4e7c-97fb-5f6713186b46) | ![image](https://github.com/kmseunh/svelte-projects/assets/105186724/186decb9-9518-431c-ad0e-1cccf286b6aa) |

&nbsp;

## 🛠️ 기능 설명

- 사용자는 검색 입력란에 포켓몬의 이름을 입력하여 해당 포켓몬을 검색할 수 있습니다.
- 검색한 포켓몬의 세부 정보를 표시합니다.
- 사용자가 포켓몬의 이름을 입력하는 동안 검색 제안 목록을 표시하여 사용자에게 도움을 줍니다.
&nbsp;

## </> 주요 코드

```ts
const search = async () => {
    query = query.trim().toLowerCase();
    if (query !== '') {
        suggestions = (await fetchPokemonList()).filter((pokemon) =>
            pokemon.startsWith(query)
        );
        showSuggestions = true;
    } else {
        suggestions = [];
        showSuggestions = false;
    }
};
```
