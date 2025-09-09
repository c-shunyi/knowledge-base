###  Scoped CSS（最常用、最省心）

这是Vue单文件组件（SFC）提供的**最核心**的解决方案。通过在 `<style>` 标签上添加 `scoped` 属性，Vue会自动为当前组件中的所有CSS选择器添加一个**唯一的属性选择器**（如 `[data-v-f3f3eg9]`），从而实现样式的私有化。

**原理**：

1. 编译阶段，Vue会为当前组件的**所有DOM元素**添加一个唯一的data属性，例如 `data-v-f3f3eg9`。
    
2. 同时，它会将组件内所有CSS选择器转换为 `原选择器[data-v-f3f3eg9]` 的形式。
    

**示例**：

```vue
<template>
  <div class="my-button">Click me</div>
</template>

<style scoped> /* 关键：scoped属性 */
.my-button {
  background-color: blue;
}
</style>
```
<template>
  <div class="my-button">Click me</div>
</template>

**编译后的结果**：
```html
<!-- DOM元素被添加了唯一属性 -->
<div class="my-button" data-v-f3f3eg9>Click me</div>
```

```css
/* CSS选择器被转换，只对本组件的元素生效 */
.my-button[data-v-f3f3eg9] {
  background-color: blue;
}
```

**优点**：

- **简单高效**：一行属性即可解决大部分冲突。
    
- **自动化**：无需手动管理命名。
    

**缺点与注意事项**：

- **优先级权重**：Scoped后的选择器优先级会更高（多了一个属性选择器），有时覆盖全局样式需要更高优先级。
    
- **对子组件根元素有效**：使用 `scoped` 后，父组件的样式会渗透到子组件的**根元素**上，这是设计如此，便于从父组件布局子组件。
    
- **无法深度作用**：Scoped样式**不会**影响到子组件内部的元素（除根元素外）。如果需要修改子组件深层样式，需要使用 `:deep()`。


### Scoped是对全部dom都添加了属性还是只有根?

### 规则总结

| 场景        | 组件身份                    | Scoped 添加 `data-v-xxx` 属性的规则                            |
| --------- | ----------------------- | ------------------------------------------------------- |
| **作为页面**  | 顶层组件（如 `App.vue` 或路由页面） | 对模板内的**所有**原生DOM元素（根、子、孙级）全部添加。                         |
| **作为子组件** | 被其他组件引用的子组件             | **仅**对自身的**根元素**添加父组件的Scoped属性。其内部的任何元素都**不会**添加父组件的属性。 |

---

### 深度修改组件样式

**深度选择器 `:deep()`**

**深度选择器 `:deep()` 的作用是【打破Scoped添加属性选择器的规则】，它【移除】了深度选择器部分前面的Scoped属性，从而让样式能穿透到子组件内部。**

#### 核心原理对比

让我们看一个例子，假设父组件想修改子组件内部一个 `<button>` 的样式。

#### 1. 没有使用 `:deep()` (失败)

```vue
<!-- 父组件 -->
<style scoped>
/* 编译前 */
.child-container button {
  background-color: red;
}
</style>
```

```vue
<!-- 编译后 -->
<style>
/* 编译后：Vue 会给所有选择器部分都加上 [data-v-parent] */
.child-container[data-v-parent] button[data-v-parent] {
  background-color: red;
}
</style>
```

**结果**：样式无效。因为子组件内部的 `button` 只有它自己的 `data-v-child` 属性，没有父组件的 `data-v-parent` 属性。选择器 `button[data-v-parent]` 匹配不到任何元素。

#### 2. 使用了 `:deep()` (成功)

```vue
<!-- 父组件 -->
<style scoped>
/* 编译前：使用 :deep() 包裹需要穿透的部分 */
.child-container :deep(button) {
  background-color: red;
}
</style>
```

```vue
<!-- 编译后 -->
<style>
/* 编译后：:deep() 内部的 'button' 部分不再添加 [data-v-parent] */
.child-container[data-v-parent] button {
  background-color: red;
}
</style>
```

**结果**：样式生效！因为编译后的选择器是 `.child-container[data-v-parent] button`  它意味着：

1. 找到一个**拥有父组件data属性**的 `.child-container`（这正好是子组件的根元素，它确实有这个属性）
    
2. 然后找到这个容器**内部的任何** `button` 元素（无论它有什么data属性，甚至是第三方库的组件）