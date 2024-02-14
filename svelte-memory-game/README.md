# svelte-memory-game

## 💬 설명

이 프로젝트는 축구 팀 로고 카드를 뒤집어 짝을 찾는 간단한 메모리 매칭 게임입니다.

&nbsp;

## 🖥️ 화면 구성

| 초기화면 | 진행 화면|
|:----:|:----:|
| ![image](https://github.com/kmseunh/svelte-projects/assets/105186724/4a8f55e7-e688-4fe7-9430-d478333a142a) | ![image](https://github.com/kmseunh/svelte-projects/assets/105186724/78acf7be-638a-4215-83bb-fdd779570d71) |

&nbsp;

## 🛠️ 기능 설명

- 게임 시작 시, 사용자는 뒤집어진 카드를 클릭하여 그림이 표시되는 카드를 선택할 수 있습니다.
- 선택한 두 개의 카드가 같은 그림을 가지고 있다면, 그 카드들은 매치되어 화면에 유지됩니다.
- 선택한 두 개의 카드가 다른 그림을 가지고 있다면, 일정 시간이 지난 후 카드가 다시 뒤집힙니다.
- 게임은 사용자의 턴 수를 추적하여 화면에 표시합니다. 사용자는 가능한 적은 턴으로 모든 카드를 매칭해야 합니다
- 사용자는 `"New Game`" 버튼을 클릭하여 새로운 게임을 시작할 수 있습니다. 이 때 모든 카드는 셔플되어 랜덤한 위치에 나타납니다.

&nbsp;

## </> 주요 코드

```js
const shuffledCards = (): void => {
    const shuffledCards: Card[] = [...cardImages, ...cardImages]
        .sort(() => Math.random() - 0.5)
        .map((card, index) => ({ ...card, id: index }));
    cards = shuffledCards;
    turns = 0;
};

const handleChoice = (card: Card): void => {
    if (disabled) return;
    if (!choiceOne) {
        choiceOne = card;
    } else {
        choiceTwo = card;
        checkMatch();
    }
};
```
