### 一、语义化标签

HTML5 引入了一系列新的标签，用更有意义的元素来代替无处不在的 `<div>` 和 `<span>`，让代码结构更清晰，对搜索引擎和可访问性也更友好。

- **布局标签**：
    - `<header>`：页眉或部头。
    - `<nav>`：导航链接。
    - `<main>`：页面主要内容。
    - `<article>`：独立的文章、博客帖子等。
    - `<section>`：文档中的节或段。test
    - `<aside>`：侧边栏、附加内容。
    - `<footer>`：页脚。
- **其他语义标签**：
    - `<figure>` 和 `<figcaption>`：表示图片及其标题。
    - `<mark>`：高亮显示文本。
    - `<time>`：表示日期或时间。
    - `<details>` 和 `<summary>`：可折叠的详情组件。

**好处**：代码可读性更强，SEO（搜索引擎优化）效果更好，屏幕阅读器等辅助技术能更好地理解页面结构

---

### 二、表单功能增强（Forms 2.0）

HTML5 为表单带来了巨大的改进，减少了我们对 JavaScript 验证的依赖。
- **新的输入类型**：`email`, `url`, `tel`, `number`, `range` (滑块), `date`, `time`, `color`, `search`。
    - **作用**：在移动设备上会弹出更合适的键盘，浏览器可以进行基本的格式验证。
- **新的表单属性**：
    - `placeholder`：输入框内的提示文本。
    - `required`：标记字段为必须填写。
    - `autofocus`：页面加载时自动聚焦到该输入框。
    - `pattern`：使用正则表达式定义自定义验证规则。
    - `min`/`max`/`step`：为数字输入框限制范围。

---

### 三、媒体元素（Media）

原生支持音频和视频，不再需要依赖 Flash 等第三方插件。

- `<video>`：嵌入视频文件。支持属性如 `controls`（控制条）, `autoplay`, `loop`, `muted`, `poster`（预览图）。
    
- `<audio>`：嵌入音频文件。同样支持 `controls`, `autoplay`, `loop`。
    
```html
<video src="movie.mp4" controls width="600"></video>
<audio src="music.mp3" controls></audio>
```

---

### 四、图形与动画（Graphics）

- `<canvas>`：**位图画布**。一个可以使用 JavaScript 绘制图形、制作游戏、处理图像的容器。它提供的是像素级的 API，非常适合需要高性能、动态渲染的场景（如图表、游戏）。
    
- **SVG**：**可缩放矢量图形**。虽然 SVG 本身不是 HTML5 新推出的，但 HTML5 将其更深入地集成到标准中。SVG 是基于 XML 的矢量格式，放大不会失真，非常适合图标、Logo 和数据可视化。


### 五、JavaScript API（强大生态的核心）

这才是 HTML5 真正强大的地方，它赋予浏览器前所未有的能力。

1. **本地存储（Web Storage）**：
    
    - `localStorage`：长期存储，数据不会随会话结束而丢失。
        
    - `sessionStorage`：会话级存储，关闭标签页后数据清除。
        
    - （替代了容量小且会随请求发送的 Cookie，用于纯客户端存储）。
        
2. **地理定位（Geolocation API）**：
    
    - 允许网站在用户授权后获取其地理位置信息。
        
    - 常用于地图、本地生活服务应用。
        
3. **拖放 API（Drag and Drop）**：
    
    - 原生支持页面元素之间的拖放操作，大大简化了相关交互的开发。
        
4. **Web Workers**：
    
    - 允许在浏览器后台运行 JavaScript 脚本，**不阻塞主线程（UI线程）**。
        
    - 用于执行计算密集型任务，避免页面卡顿。
        
5. **服务器发送事件（Server-Sent Events, SSE）**：
    
    - 允许服务器主动向客户端推送消息（单向），非常适合实现实时通知、行情更新等。
        
6. **WebSocket**：
    
    - 提供了全双工、双向的实时通信通道。在客户端和服务器之间建立持久连接，非常适合聊天应用、实时游戏等。
        
7. **离线应用（Application Cache -> Service Worker）**：
    
    - 早期的 AppCache 已被更强大的 **Service Worker** 取代。
        
    - Service Worker 是一个可编程的网络代理，可以控制页面发出的请求，是实现 **PWA（渐进式Web应用）** 的核心技术，能实现离线访问、消息推送、后台同步等功能。
