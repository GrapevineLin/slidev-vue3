---
# try also 'default' to start simple
theme: seriph
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: /images/2.jpg
# apply any windi css classes to the current slide
class: 'text-center'
# https://sli.dev/custom/highlighters.html
highlighter: shiki
# show line numbers in code blocks
lineNumbers: false
# some information about the slides, markdown enabled
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
# persist drawings in exports and build
drawings:
  persist: false
# use UnoCSS (experimental)
css: unocss
---

# Vue3设计与实现

<div class="text-s text-gray-400">简单实现一个MiniVue</div> 
<div class="text-s text-gray-400">介绍CompositionAPI和OptionAPI的区别</div>

<!-- <div class="pt-12">
  <span @click="$slidev.nav.next" class="px-2 py-1 rounded cursor-pointer" hover="bg-white bg-opacity-10">
    Press Space for next page <carbon:arrow-right class="inline"/>
  </span>
</div> -->

<!-- <div class="abs-br m-6 flex gap-2">
  <button @click="$slidev.nav.openInEditor()" title="Open in Editor" class="text-xl icon-btn opacity-50 !border-none !hover:text-white">
    <carbon:edit />
  </button>
  <a href="https://github.com/slidevjs/slidev" target="_blank" alt="GitHub"
    class="text-xl icon-btn opacity-50 !border-none !hover:text-white">
    <carbon-logo-github />
  </a>
</div> -->

<!--
The last comment block of each slide will be treated as slide notes. It will be visible and editable in Presenter Mode along with the slide. [Read more in the docs](https://sli.dev/guide/syntax.html#notes)
-->

<style>
  h1{
        background-color: transparent;

  }
</style>

---

<h1 class="linear">Vue框架特点</h1>

- 一款用于构建用户界面的 JavaScript **响应式** 框架
- 渲染基于虚拟Dom，**声明式**


<div v-click class="opacity-75">

```js
const vnode = {
  tag: 'div',
  props: {
    id: 'hello'
  },
  children: [
    {
      tag:'h1',
      children: 'hello vue'
    }
    /* 更多 vnode */
  ]
}

<div id="hello">
  <h1>hello vue</h1>
</div>
```

</div>


---

<h1 class="linear">Vue内部模块</h1>

<!-- Slidev is a slides maker and presenter designed for developers, consist of the following features -->
<br>
<br>

- 📝 **响应式系统** - 响应式系统会为我们的数据建立响应式的特性
  - **Vue2**：基于 es5 的 Object.defineProperty，劫持 setter、getter 实现数据监听
  - **Vue3**：基于Proxy
<br>
<br>
- 🧑‍💻 **渲染器** - 渲染器会执行渲染函数，得到虚拟dom，开始观测响应式数据。接下来在挂载阶段(mount)，使用虚拟dom创建页面
<br>
<br>
- 🎨 **[编译器](https://vue-next-template-explorer.netlify.app/#eyJzcmMiOiIiLCJvcHRpb25zIjp7ImhvaXN0U3RhdGljIjp0cnVlLCJjYWNoZUhhbmRsZXJzIjp0cnVlfX0=)** - 编译器会为我们的模板转换成一个render函数，它引用了响应式数据
<br>
<br>

<v-click>

<div class="opacity-75">
最后如果被观测的响应对象发生变化，会自动调用渲染函数得到新的vnode，新旧vnode会在path函数中进行对比，最终找到有变化的部分，更新页面。 
</div>

</v-click>

<!--
You can have `style` tag in markdown to override the style for the current page.
Learn more: https://sli.dev/guide/syntax#embedded-styles
-->

---

 
<h1 class="linear">实现一个MiniVue</h1>

- 渲染器
- 响应式系统

<v-click>

<div class="pt-20 opacity-75">
 
## 不同框架的更新粒度

<div class="pt10"></div>

- React：完全依赖vdom，`树级更新`
- Vue2：完全依赖vdom，`组件级更新`
- Svelte：没有vdom，`节点级更新`
- [Vue3](https://vue-next-template-explorer.netlify.app/#eyJzcmMiOiIiLCJvcHRpb25zIjp7ImhvaXN0U3RhdGljIjp0cnVlLCJjYWNoZUhhbmRsZXJzIjp0cnVlfX0=)
：vdom + 模板预编译

 

</div>

</v-click>

---

<h1 class="linear">Composition API（组合式API）</h1>

- 和选项式API有什么区别？

<v-click>

<div class="pt-20">

- 代码组织
- 逻辑复用

</div>

</v-click>


<style>
.footnotes-sep {
  @apply mt-20 opacity-10;
}
.footnotes {
  @apply text-sm opacity-75;
}
.footnote-backref {
  display: none;
}
</style>

---

<h1 class="linear">思路来源</h1>

<img src="/images/vue.jpg" class="m-15 h-60 shadow"  />
