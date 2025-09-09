核心思想是**赋予容器改变其项目宽度、高度、顺序的能力，以最佳方式填充可用空间**。


### 一、核心概念：容器 vs. 项目

要使用 Flexbox，首先需要理解两个核心角色：

1. **Flex Container（弹性容器）**：
    
    - 设置了 `display: flex;` 或 `display: inline-flex;` 的元素。
        
    - 它直接包含的所有**直接子元素**都会成为 Flex Items。
        
2. **Flex Items（弹性项目）**：
    
    - 弹性容器内的**直接子元素**。
        
    - 容器外的元素或容器的孙子元素都不受影响。
        

```html
<div class="container"> <!-- Flex Container -->
  <div class="item"></div> <!-- Flex Item -->
  <div class="item"></div> <!-- Flex Item -->
  <div class="item"></div> <!-- Flex Item -->
</div>
```

```css
.container {
  display: flex; /* 或 inline-flex */
}
```

---

### 二、Flex Container（容器）的属性

这些属性设置在容器上，用于定义其内部项目的布局方式。

#### 1. 主轴方向：`flex-direction`

定义主轴的方向（即项目的排列方向）。

- `row` (默认值)：主轴为水平方向，起点在左端。
    
- `row-reverse`：主轴为水平方向，起点在右端。
    
- `column`：主轴为垂直方向，起点在上沿。
    
- `column-reverse`：主轴为垂直方向，起点在下沿。
    

#### 2. 换行：`flex-wrap`

定义项目如果一条轴线排不下，如何换行。

- `nowrap` (默认值)：不换行，项目会收缩以适应单行。
    
- `wrap`：换行，第一行在上方。
    
- `wrap-reverse`：换行，第一行在下方。
    

#### 3. 主轴与换行的简写：`flex-flow`

`flex-direction` 和 `flex-wrap` 的简写形式。

- 语法：`flex-flow: <flex-direction> <flex-wrap>;`
    
- 示例：`flex-flow: row wrap;`
    

#### 4. 主轴对齐：`justify-content`

定义项目在**主轴**上的对齐方式。

- `flex-start` (默认值)：向主轴起点对齐。
    
- `flex-end`：向主轴终点对齐。
    
- `center`：居中对齐。
    
- `space-between`：两端对齐，项目之间的间隔都相等。
    
- `space-around`：每个项目两侧的间隔相等。项目之间的间隔比项目与边框的间隔大一倍。
    
- `space-evenly`：每个项目周围的间隔完全相等。
    

#### 5. 交叉轴对齐：`align-items`

定义项目在**交叉轴**上的对齐方式（单行情况）。

- `stretch` (默认值)：如果项目未设置高度或设为auto，将占满整个容器的高度。
    
- `flex-start`：向交叉轴的起点对齐。
    
- `flex-end`：向交叉轴的终点对齐。
    
- `center`：居中对齐。
    
- `baseline`：项目的第一行文字的基线对齐。
    

#### 6. 多根轴线对齐：`align-content`

定义多根轴线（多行）在**交叉轴**上的对齐方式。**如果项目只有一根轴线，该属性不起作用。**

- `stretch` (默认值)：轴线占满整个交叉轴。
    
- `flex-start`：与交叉轴的起点对齐。
    
- `flex-end`：与交叉轴的终点对齐。
    
- `center`：与交叉轴的中点对齐。
    
- `space-between`：与交叉轴两端对齐，轴线之间的间隔平均分布。
    
- `space-around`：每根轴线两侧的间隔都相等。
    
- `space-evenly`：每根轴线周围的间隔完全相等。
    

---

### 三、Flex Items（项目）的属性

这些属性设置在各个项目上，用于微调单个项目的布局行为。

#### 1. 排序：`order`

定义项目的排列顺序。数值越小，排列越靠前，默认为0。

- 示例：`order: -1;` （该项目会排在最前面）
    

#### 2. 放大比例：`flex-grow`

定义项目的放大比例，默认为0（即如果存在剩余空间，也不放大）。

- 如果所有项目的 `flex-grow` 属性都为1，则它们将等分剩余空间。
    
- 如果一个项目的 `flex-grow` 属性为2，其他项目都为1，则前者占据的剩余空间将比其他项多一倍。
    

#### 3. 缩小比例：`flex-shrink`

定义项目的缩小比例，默认为1（即如果空间不足，该项目将缩小）。

- 如果所有项目的 `flex-shrink` 属性都为1，当空间不足时，都将等比例缩小。
    
- 如果一个项目的 `flex-shrink` 属性为0，其他项目都为1，则空间不足时，前者不缩小。
    

#### 4. 项目基准大小：`flex-basis`

定义在分配多余空间之前，项目占据的主轴空间。浏览器根据这个属性计算是否有多余空间。默认值为 `auto`（即项目的本来大小）。

- 可以设置为一个长度值（如 `200px`, `20%`, `10rem`）。
    

#### 5. 简写属性：`flex`

`flex-grow`, `flex-shrink` 和 `flex-basis` 的简写。**这是最常用的项目属性。**

- 默认值：`flex: 0 1 auto;`
    
- 常用快捷值：
    
    - `flex: initial;` -> `flex: 0 1 auto;` （不放大，可缩小，大小为内容大小）
        
    - `flex: auto;` -> `flex: 1 1 auto;` （可放大，可缩小）
        
    - `flex: none;` -> `flex: 0 0 auto;` （不放大，不缩小，刚性尺寸）
        
    - `flex: 1;` -> `flex: 1 1 0%;` （等分剩余空间）
        

#### 6. 单独对齐：`align-self`

允许单个项目有与其他项目不一样的对齐方式，可覆盖 `align-items` 属性。

- 默认值：`auto`，表示继承父容器的 `align-items` 属性。
    
- 其他值：`stretch`, `flex-start`, `flex-end`, `center`, `baseline`。
    

---

### 总结与记忆技巧

|属性|作用对象|作用|常用值|
|---|---|---|---|
|**`display: flex`**|**容器**|定义Flex容器|`flex`, `inline-flex`|
|**`flex-direction`**|**容器**|**主轴方向**|`row`, `column`|
|**`justify-content`**|**容器**|**主轴**对齐|`center`, `space-between`|
|**`align-items`**|**容器**|**交叉轴**对齐（单行）|`center`, `stretch`|
|**`flex`**|**项目**|**定义项目的弹性**|`1`, `none`, `0 0 200px`|
|**`align-self`**|**项目**|覆盖单个项目的交叉轴对齐|`center`, `flex-start`|

**一句话总结主轴与交叉轴：**

- `flex-direction: row` -> 主轴是X轴，`justify-content` 管左右对齐，`align-items` 管上下对齐。
    
- `flex-direction: column` -> 主轴是Y轴，`justify-content` 管上下对齐，`align-items` 管左右对齐。
    

Flexbox 极大地简化了之前需要靠浮动、定位和 Hack 才能实现的布局，是如今前端开发中**使用最频繁、最重要的布局方案**之一，尤其适合处理组件、导航栏、列表等一维布局场景。