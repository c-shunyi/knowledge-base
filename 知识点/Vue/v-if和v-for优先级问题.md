当它们同时存在于一个节点上时，`v-if` 比 `v-for` 的优先级更高

```vue
<!--
 这会抛出一个错误，因为属性 todo 此时
 没有在该实例上定义
-->
<li v-for="todo in todos" v-if="!todo.isComplete">
  {{ todo.name }}	
</li>
```

在外先包装一层 `<template>` 再在其上使用 `v-for` 可以解决这个问题 (这也更加明显易读)：

```vue
<template v-for="todo in todos">
  <li v-if="!todo.isComplete">
    {{ todo.name }}
  </li>
</template>
```

Tip：

```vue
同时使用 v-if 和 v-for 是不推荐的，因为这样二者的优先级不明显。

两种常见的情况可能导致这种用法：

过滤列表中的项目 (例如，v-for="user in users" v-if="user.isActive")。在这种情况下，可以用一个新的计算属性来替换 users，该属性返回过滤后的列表 (例如 activeUsers)。

避免渲染应该隐藏的列表 (例如 v-for="user in users" v-if="shouldShowUsers")。在这种情况下，将 v-if 移至容器元素 (如 ul、ol)。
```
