# 响应式原理

defineProperty和proxy的区别

1. vue2的响应式用的defineProperty（属性描述符），vue3的响应式用的proxy（代理），我有去看过MDN的官方文档，defineProperty其实底层调用的是对象的一个内部方法：DefineOwnProperty，这个内部方法的作用是重新定义属性描述符，它能够拦截现有属性的读写，新增属性这些是拦截不到的，针对一个对象的基本操作方法很多，比如得到原型GetOwnProperty、设置原型SetPrototypeOf、还有读取对象设置对象Get、Set，而defineProperty底层调用其实只是对应了一个基本操作，所以vue2的拦截其实是有缺陷的很多东西都拦截不到。但是vue3使用的是proxy，但是proxy的定义就比defineProperty要大的多，它是针对对象的所有内部方法都可以重定义和拦截，不管是函数对象还是普通对象都可以拦截。所以这两个东西其实不应该放在一块去对比，因为他们本来就不在一个层面，proxy比defineProperty要大的多。
2. 还有defineProperty是属性描述符，他其实针对的是对象的属性，实现响应式需要去监听对象和添加副作用函数，所以这里能看到defineProperty的缺陷是Object.defineProperty针对既有对象属性的监听，那么当我们给对象新增一个属性后，就监听不到了，无法监听属性的新增和删除，并且他的监听是针对对象的属性，所以要实现对象的响应式需要使用递归对对象的所有属性进行监听，而递归监听也带来了效率的降低。
3. 所以vue3需要解决上述问题，不再监听对象的属性，而是直接监听整个对象，也不需要遍历，通过new Proxy(obj,{})来实现代理，vue3响应式动的其实是代理对象，而没有动原始对象，vue2监听的是原始对象，所以vue3比vue2好在：由于不需要监听属性了，监听的是整个对象，就不需要递归遍历了。由于监听的是对象，所以对象的属性的新增和删除都可以监听到

vue2使用的是option（选项式的api）而vue3使用的是composition（组合式）的api，支持setup语法糖

# 生命周期不同，函数组件的生命周期呢？

### Vue 2 生命周期钩子

在 Vue 2 中，组件的生命周期钩子包括：

1. **`beforeCreate`**: 实例初始化之后，数据观测和事件配置之前被调用。
2. **`created`**: 实例已创建，数据观测和事件配置完毕，但 DOM 尚未生成。
3. **`beforeMount`**: 在挂载开始之前调用，相关的 render 函数首次被调用。
4. **`mounted`**: 实例被挂载后调用，DOM 结构已生成。
5. **`beforeUpdate`**: 数据更新时调用，发生在虚拟 DOM 重新渲染之前。
6. **`updated`**: 数据变化导致的虚拟 DOM 重新渲染和更新后调用。
7. **`beforeDestroy`**: 实例销毁之前调用，此时实例仍然可用。
8. **`destroyed`**: 实例销毁后调用，所有的事件监听器和子实例都已被移除。

### Vue 3 生命周期钩子

在 Vue 3 中，生命周期钩子与 Vue 2 基本相同，但有一些细微的改进和新钩子的添加。以下是 Vue 3 的钩子：

1. **`beforeCreate`**: 与 Vue 2 相同。
2. **`created`**: 与 Vue 2 相同。
3. **`beforeMount`**: 与 Vue 2 相同。
4. **`mounted`**: 与 Vue 2 相同。
5. **`beforeUpdate`**: 与 Vue 2 相同。
6. **`updated`**: 与 Vue 2 相同。
7. **`beforeUnmount`**: 替代 `beforeDestroy`，在实例销毁之前调用。
8. **`unmounted`**: 替代 `destroyed`，在实例销毁后调用。