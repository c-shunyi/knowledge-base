### 一、基础选择器

这是最基础、最常用的选择器类型。

|选择器|示例|描述|
|---|---|---|
|**通配选择器**|`*`|选择**所有**元素。|
|**元素选择器**|`div`、`p`、`h1`|选择所有指定**标签**的元素。|
|**类选择器**|`.class-name`|选择所有具有指定 **`class`** 属性的元素（最常用）。|
|**ID选择器**|`#id-name`|选择具有指定 **`id`** 属性的元素（优先级最高）。|
|**属性选择器**|`[type="text"]`|选择具有指定属性的元素。|

**示例：**

```css
* { margin: 0; padding: 0; } /* 重置所有元素的内外边距 */
  
div { color: blue; } /* 所有div文字蓝色 */

.header { background: #fff; } /* class="header"的元素 */

#main-content { width: 80%; } /* id="main-content"的元素 */

input[type="submit"] { cursor: pointer; } /* 类型为submit的input按钮 */
```



---

### 二、组合器（Combinators）

组合器用于解释选择器之间的关系，将它们组合起来以选择更具体的元素。

|选择器|示例|描述|
|---|---|---|
|**后代选择器** (空格)|`div p`|选择**所有**在`div`元素**内部的**`p`元素（无论嵌套多深）。|
|**子选择器** (`>`)|`div > p`|选择**直接**是`div`元素**子元素**的`p`元素（仅一代）。|
|**相邻兄弟选择器** (`+`)|`h1 + p`|选择**紧接**在`h1`元素**之后**的第一个**同级**`p`元素。|
|**通用兄弟选择器** (`~`)|`h1 ~ p`|选择在`h1`元素**之后**的**所有**同级`p`元素。|

**示例：**

```html
<article>
  <h1>标题</h1>
  <p>这段落会被 h1 + p 和 h1 ~ p 选中。</p> <!-- 紧挨着h1的p -->
  <div>
    <p>这个p是div的后代，是article的后代。会被article p选中。</p>
  </div>
  <p>这段落会被 h1 ~ p 选中。</p> <!-- h1之后的所有p -->
</article>
```

```css
article p { color: gray; } /* 文章内所有p */

article > p { border: 1px solid; } /* 仅文章的直接子p（第一个和最后一个） */

h1 + p { font-weight: bold; } /* 紧接h1后的第一个p */

h1 ~ p { margin-left: 20px; } /* h1之后的所有同级p */
```

---

### 三、伪类（Pseudo-classes）

用于选择处于**特定状态**的元素。

|选择器|示例|描述|
|---|---|---|
|**动态伪类**|`:hover`, `:active`, `:focus`|用户交互状态（鼠标悬停、点击、聚焦）。|
|**结构伪类**|`:first-child`, `:last-child`|基于元素在父元素中的位置选择。|
||`:nth-child(n)`|选择第n个子元素（`even`, `odd`, `2n+1` 公式强大）。|
||`:not(selector)`|**否定伪类**，选择不匹配内部选择器的元素。|
|**表单伪类**|`:checked`, `:disabled`|选择被选中或禁用的表单元素。|

**示例：**

```css
a:hover { color: red; } /* 鼠标悬停时变红 */

tr:nth-child(odd) { background: #f5f5f5; } /* 表格斑马纹 */

li:not(.special) { color: blue; } /* 选择没有class="special"的li */

input:focus { outline: 2px solid blue; } /* 输入框聚焦时高亮 */
```

---

### 四、伪元素（Pseudo-elements）

用于样式化元素的**特定部分**或**插入虚拟内容**。

|选择器|示例|描述|
|---|---|---|
|`::before`|`p::before { content: "♥"; }`|在元素**内容前**插入内容。|
|`::after`|`p::after { content: "!"; }`|在元素**内容后**插入内容。|
|`::first-line`|`p::first-line`|选择元素**第一行**文本（仅用于块级元素）。|
|`::first-letter`|`p::first-letter`|选择元素内容的**第一个字母**。|
|`::selection`|`::selection`|改变用户**选中文本**的样式。|

**示例：**

```css
.clearfix::after { /* 经典清除浮动 hack */
  content: "";
  display: table;
  clear: both;
}
p::first-letter { font-size: 2em; } /* 首字母下沉 */
::selection { background: yellow; color: black; } /* 选中文本样式 */
```

---

### 五、选择器优先级（Specificity - 权重计算）

当多条规则作用于同一元素时，浏览器通过一套优先级规则决定应用哪条样式。

**计算规则（从高到低）：**

1. **内联样式** (`style="..."`) - **1000**
    
2. **ID选择器** (`#id`) - **0100**
    
3. **类选择器** (`.class`)、**属性选择器** (`[type="text"]`)、**伪类** (`:hover`) - **0010**
    
4. **元素选择器** (`div`)、**伪元素** (`::before`) - **0001**
    
5. **通配选择器** (`*`)、**组合器** (`>`, `+`, `~`)、**否定伪类** (`:not`) **不影响优先级**（但`:not()`内部的选择器会影响）。
    

**比较规则**：从左到右逐位比较，数值大的优先级高。**`!important`** 是最高优先级，但应尽量避免使用，因为它难以覆盖。