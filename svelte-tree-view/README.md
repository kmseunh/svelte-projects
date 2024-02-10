# svelte-tree-view

## 💬 설명

이 프로젝트는 트리 구조를 표시하고 사용자가 각 노드를 확장하거나 축소할 수 있는 트리 뷰를 구현한 것입니다.

&nbsp;

## 🖥️ 화면 구성

| 메인 화면 |
|:----:|
| ![image](https://github.com/kmseunh/svelte-projects/assets/105186724/a80dbe54-c696-4b7e-8f81-e78639419a55) |

&nbsp;

## 🛠️ 기능 설명

- 트리의 각 노드는 해당 라벨을 표시하며, 자식 노드가 있는 경우 화살표 아이콘을 통해 확장된 상태를 표시합니다.
- 사용자는 각 노드의 화살표 아이콘을 클릭하여 해당 노드의 자식 노드를 확장하거나 축소할 수 있습니다.

&nbsp;

## </> 주요 코드

```ts
    const toggleExpansion = (label: string): void => {
        expansionState[label] = !expansionState[label];
        expansionState = { ...expansionState };
    };

    const initializeExpansionState = (node: TreeNode): void => {
        if (node.children) {
            expansionState[node.label] = false;
            node.children.forEach(initializeExpansionState);
        }
    };
```
