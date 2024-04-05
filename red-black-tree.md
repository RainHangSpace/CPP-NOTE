# 红黑树

当我们按照序列【10, 20, 30, 15】插入节点到红黑树时，这些是应该发生的正确步骤：

1. 插入 `10`：
    - `10` 被插入作为根，重新着色为黑色。

```
黑
10
```

2. 插入 `20`：
    - `20` 被插入作为 `10` 的右子节点，默认为红色。

```
  黑
  10
    \
    红
    20
```

3. 插入 `30`：
    - 这个时候，需要修复因为连续的红色节点 `20` 和 `30` 而违反的红黑树性质。
    - 首先，执行一次左旋转。将 `20` 旋转到根的位置，使 `10` 成为 `20` 的左子节点，`30` 成为 `20` 的右子节点。
    - 然后，我们交换 `20` 和 `10` 的颜色（`20` 变黑色，`10` 变红色）。

```
      黑
      20
     /  \
    红    红
   10    30
```

4. 插入 `15`：
    - `15` 作为 `10` 的右子节点插入，默认为红色。现在我们有红色节点 `15` 作为红色节点 `10` 的子节点，这违反了红黑树的性质。
    - 为了修复，我们需要对 `10` 执行一次左旋转。`15` 成为 `10` 原来位置的新节点，并且 `10` 成为 `15` 的左子节点。

```
      黑
      20
     /  \
    红    红
   15    30
  /
红
10
```

在这个状态下，任何进一步的操作都需要综合考虑树的结构。务必注意，由于插入新节点默认为红色，并且我们只有在保持红黑树所有性质的同时才能着色节点，所以最后树的合法状态需要满足所有红黑树的性质：节点是红色或黑色；根节点是黑色；叶子节点（NIL节点）是黑色；不能有两个连续的红色节点；从任一节点到其每个叶子的所有简单路径都包含相同数目的黑色节点。

现在我们来修复最终状态：

```
      黑
      20
     /  \
    红    红
   15    30
  /
红
10
```

由于15成为红色，并且10也是红色的，我们必须进行一些重新着色来保证红黑树性质：

- 我们可以根据兄弟节点(`30`)的颜色来决定是进行重新着色还是旋转。

假设 `30`（当前15的叔叔节点）是黑色，我们可以通过颜色变换和旋转来修复树：

- 着色 `15` 为黑色，`20` 为红色

最终，树应该看起来像这样：

```
      红
      20
     /  \
    黑    黑
   15    30
  /
红
10
```

然后，为了保证根节点为黑色，我们将20这个根节点再次着色为黑色：

```
      黑
      20
     /  \
    黑    黑
   15    30
  /
红
10
```

这样，该红黑树就符合所有的红黑性质了。

注意：红黑树的修复与旋转步骤可能会很复杂，需要根据插入节点的不同位置和颜色有不同的操作。上面的步骤是基于特定情况的简化版，实际操作可能需要更多的步骤以符合红黑树的性质要求。在实际的程序中，通常有专门的函数用来调整树，以保持红黑树的约束条件。

User: 红黑树可以连续出现黑 但是不能连续出现红对吧

AI: 是的，你的理解是正确的。在红黑树的性质中，连续出现红色节点是不被允许的，因为这违反了红黑树的一个核心性质：每个红色节点必须有两个黑色的子节点。另一种表达这个性质的说法是：红色节点不能有红色的父节点或红色的子节点。

然而，反过来并没有规则禁止黑色节点连续出现。实际上， 从任一节点到其各个叶节点的所有路径上黑色节点的数量必须相同是另外一个红黑树的核心性质，这意味着在某些路径上连续多个黑色节点是允许的，且有时候是必须的。

红黑树的性质可以归纳为以下几点：

1. 每个节点要么是红色要么是黑色。
2. 根节点必须是黑色。
3. 所有叶节点（NIL 或空节点）都是黑色。
4. 红色节点不能有红色的父节点或红色的子节点（也就是说——不能有两个连续的红色节点）。
5. 从任一节点到其每个叶子的所有简单路径都包含相同数目的黑色节点。

由于这些性质，红黑树在进行插入和删除节点的操作后通常需要通过特定的旋转和重新着色等一系列操作来调整，以维持红黑平衡，保证搜索、插入、删除的操作时间复杂度保持在O(log n)。