| 特性       | `v-if`  | `v-show`  |
| -------- | ------- | --------- |
| 是否渲染 DOM | 条件为真才渲染 | 一直渲染，只是隐藏 |
| 初始渲染开销   | 小       | 大         |
| 切换开销     | 大       | 小         |
| 适合场景     | 不频繁切换   | 频繁切换      |

## **1. `v-if` vs `v-show`**

### 📌 **`v-if`**

- **条件渲染**：只有当条件为 `true` 时，元素才会被 **创建并挂载** 到 DOM。条件为 `false` 时，元素会被 **销毁**。
    
- **性能特点**：
    
    - 切换开销大（涉及创建和销毁 DOM 节点）。
        
    - 初始渲染开销小（条件为 `false` 时根本不渲染）。
        
- **适用场景**：适合**不频繁切换**的场景，比如页面级组件、弹窗。
    

`<div v-if="isShow">内容</div>`

---

### 📌 **`v-show`**

- **条件显示**：始终渲染元素，只是通过 `display: none` 控制显示/隐藏。
    
- **性能特点**：
    
    - 切换开销小（只是修改样式）。
        
    - 初始渲染开销大（无论条件如何都会渲染）。
        
- **适用场景**：适合**频繁切换**的场景，比如 Tab 切换、下拉菜单。
    

`<div v-show="isShow">内容</div>`


## `v-for` 与 `v-if`[​](https://cn.vuejs.org/guide/essentials/list.html#v-for-with-v-if)

当它们同时存在于一个节点上时，`v-if` 比 `v-for` 的优先级更高。这意味着 `v-if` 的条件将无法访问到 `v-for` 作用域内定义的变量别名：

template

```
<!--
 这会抛出一个错误，因为属性 todo 此时
 没有在该实例上定义
-->
<li v-for="todo in todos" v-if="!todo.isComplete">
  {{ todo.name }}
</li>
```

在外先包装一层 `<template>` 再在其上使用 `v-for` 可以解决这个问题 (这也更加明显易读)：

template

```
<template v-for="todo in todos">
  <li v-if="!todo.isComplete">
    {{ todo.name }}
  </li>
</template>
```

### 注意

同时使用 `v-if` 和 `v-for` 是**不推荐的**，因为这样二者的优先级不明显。

两种常见的情况可能导致这种用法：

- 过滤列表中的项目 (例如，`v-for="user in users" v-if="user.isActive"`)。在这种情况下，可以用一个新的计算属性来替换 `users`，该属性返回过滤后的列表 (例如 `activeUsers`)。
    
- 避免渲染应该隐藏的列表 (例如 `v-for="user in users" v-if="shouldShowUsers"`)。在这种情况下，将 `v-if` 移至容器元素 (如 `ul`、`ol`)。