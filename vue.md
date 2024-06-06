<a name="ss74U"></a>
### vue组件props，methods，data，computed，watch的加载顺序
props - > methods - > data - > computed - > watch

<a name="syU1z"></a>
### vue3 和 vue2 的区别 
<a name="OsSyk"></a>
#### 总结
**更快的渲染性能**：

- Vue3 相比 Vue2 来说，Vue3 重写了虚拟 Dom 实现，编译模板的优化，更高效的组件初始化。

**更小的体积：**

- 通过 webpack 的 tree-shaking 功能，可以将无用模块“剪辑”，仅打包需要的模块。
- Vue 3 的运行时核心相比 Vue2 更小，这意味着更小的打包体积，减少了前端加载时间。

**更好的 TypeScript 支持：**

- Vue 3 的代码库已经全面采用 TypeScript 重写，提供了更好的类型推断和类型提示。
- 提供了更多的内置类型声明，使得开发时更容易发现代码错误和调试。

**更灵活的组合式 API：**

- Vue 3 引入了组合式 API，使得组件的逻辑可以更好地组织和复用。setup（）
- 组合式 API 提供了更直观、更灵活的方式来组织组件代码，使得代码更易读、易维护。

**更好的响应式系统：**

- Vue 3 使用了ES6的 Proxy 来重写响应式系统，相比 Vue 2 的 Object.defineProperty，更加直观和强大。
- 在 Vue 3 中，可以在更深的层次上追踪响应式变量的变化，使得开发者能够更准确地监听数据变化。

vue2.x 中绝大多数的 API 与特性，在 vue3.x 中同样支持。同时，vue3.x 中还新增了 3.x 所特有的功能、并废弃了某些 2.x 中的旧功能： <br />**新增**： 组合式 API、多根节点组件、更好的兼容TypeScript等 <br />**废弃**： 过滤器、不再支持 $on，$off 和 $once 实例方法等
<a name="zxStE"></a>
#### v3 proxy代替 v2 defineProperty
| Object.defineProperty()  | proxy |
| --- | --- |
| 不能监听数组的变化 | 可以监听数组，不用再去单独的对数组做特异性操作 vue3.x可以检测到数组内部数据的变化 |
| 必须深层遍历嵌套的对象 | 可以省去for in、闭包等内容来提升效率（直接绑定整个对象即可） |
| 必须遍历对象的每个属性 | <br /> |

<a name="vQhfK"></a>
#### Fragments
**vue2**：**不支持**碎片， 只能有一个根节点<br />**vue3**：**支持Fragments）** ，就是说可以拥有多个根节点。
<a name="wDBIf"></a>
#### 生命周期
![](https://cdn.nlark.com/yuque/0/2024/webp/43022426/1711612097849-205004eb-b387-48af-bf50-f042bb46bb43.webp#averageHue=%23f8f9f7&clientId=u2ffe92cf-fb49-4&from=paste&id=u6385fadf&originHeight=219&originWidth=346&originalType=url&ratio=1.375&rotation=0&showTitle=false&status=done&style=none&taskId=u4c0fa9e6-6aa5-4af2-8c65-eb893345a68&title=)<br />在Vue3中新增的一个组合式API中是没有beforeCreate和created这两个生命周期函数等价于setup函数，但是setup函数是在这两个生命周期函数之前执行的

<a name="eHndm"></a>
#### v-if和v-for的优先级
| vue2 | vue3 |
| --- | --- |
| v-for的优先级高于v-if，可以放在一起使用（不建议） | v-if的优先级高于v-for，一起使用会报错<br />（可以通过在外部添加一个标签，将v-for移到外层） |

在vue2中v-for的优先级高于v-if，可以放在一起使用，但是不建议这么做，会带来性能上的浪费<br />在vue3中v-if的优先级高于v-for，一起使用会报错。可以通过在外部添加一个标签，将v-for移到外层

<a name="PVrFV"></a>
#### 模板指令与插槽不同

- 组件上 v-model 用法已更改。
- <template v-for> 和 非 v-for 节点上 key 用法已更改。
- 在同一元素上使用的 v-if 和 v-for 优先级已更改。 * v-bind="object" 现在排序敏感。
- v-for 中的 ref 不再注册 ref 数组 。
- vue2中使用slot可以**直接使用slot，**vue3中必须使用**v-slot的形式。**
<a name="oUgBp"></a>
#### 移除api

- vue3中移除keyCode作为v-on的修饰符，当然也不支持config.keyCodes；vue3中**移除v-on.native修饰符**；vue3中**移除过滤器filter**。
- keyCode 支持作为 v-on 的修饰符。
- $on，$off 和 $once 实例方法。
- 过滤器 filter 。
- 内联模板 attribute 。
- $destroy 实例方法。用户不应再手动管理单个 Vue 组件的生命周期。
<a name="v2q9Y"></a>
#### diff算法不同
**vue2中的diff算法**<br />遍历每一个虚拟节点，进行虚拟节点对比，并返回一个patch对象，用来存储两个节点不同的地方。用patch记录的消息去更新dom<br />缺点：比较每一个节点，而对于一些不参与更新的元素，进行比较是有点消耗性能的。特点：特别要提一下Vue的patch是即时的，并不是打包所有修改最后一起操作DOM，也就是在vue中边记录变更新。（React则是将更新放入队列后集中处理）。<br />**vue3中的diff算法**<br />在初始化的时候会给每一个虚拟节点添加一个patchFlags，是一种优化的标识。只会比较patchFlags发生变化的节点，进行识图更新。而对于patchFlags没有变化的元素作静态标记，在渲染的时候直接复用。
<a name="ThSOT"></a>
#### Vue3 新增特性

- Vue3 中需要关注的一些新特性：
   - framents
   - Teleport
   - composition
   - createRender
<a name="MZVgq"></a>
### 虚拟DOM
<a name="Hb5Ou"></a>
##### 什么是虚拟DOM
虚拟 DOM（Virtual DOM）本质上是JS 和 DOM 之间的一个映射缓存，它在形态上表现为一个能够描述 DOM 结构及其属性信息的 JS 对象。它主要存储在内存中。主要来说：<br />虚拟dom是一个js对象，存储在内存之中。<br />虚拟dom能够描述真实dom（存在一个对应关系）<br />当数据变化的时候，生成新的DOM，对比新旧虚拟DOM的差异，将差异更新到真实DOM上
<a name="FRDiv"></a>
##### 虚拟DOM的优点
减少 DOM 操作：虚拟 DOM 可以将多次 DOM 操作合并为一次操作<br />研发效率的问题：虚拟 DOM 的出现，为数据驱动视图这一思想提供了高度可用的载体，使得前端开发能够基于函数式 UI 的编程方式实现高效的声明式编程。<br />跨平台的问题：虚拟 DOM 是对真实渲染内容的一层抽象。同一套虚拟 DOM，可以对接不同平台的渲染逻辑，从而实现“一次编码，多端运行”
<a name="Zp89m"></a>
### vue和react的虚拟DOM
Vue与React都使用了 Virtual DOM + Diff算法， 不管是Vue的Template模板+options api/compotion api 写法， 还是React的Class或者Function+JSX写法,  最后都是生成render函数，而render函数执行返回VNode(虚拟DOM的数据结构，本质上是棵树)。<br />当每一次UI更新时，总会根据render重新生成最新的VNode，然后跟以前缓存起来老的VNode进行比对，再使用Diff算法（框架核心）去真正更新真实DOM（虚拟DOM是JS对象结构，同样在JS引擎中，而真实DOM在浏览器渲染引擎中，所以操作虚拟DOM比操作真实DOM开销要小的多）

Vue和React都使用了虚拟DOM（Virtual DOM）的概念，但它们在实现和工作原理上有一些区别。<br />**实现方式：**<br />Vue的虚拟DOM：Vue使用模板编译器将模板转换为渲染函数，然后通过渲染函数创建虚拟DOM树。Vue的虚拟DOM是基于浏览器环境的DOM API来实现的。<br />React的虚拟DOM：React使用JSX语法，在组件中直接编写虚拟DOM结构，然后通过Babel等工具将其转换为JavaScript代码。React的虚拟DOM是用纯JavaScript对象来表示的。

**更新机制：**<br />Vue的虚拟DOM：Vue通过跟踪依赖来确定何时重新渲染组件。当数据发生变化时，Vue会生成新的虚拟DOM树，并通过比较新旧虚拟DOM树的差异，计算出最小的更新代价，然后将变更应用于实际DOM。<br />React的虚拟DOM：React采用全量比较的方式，在组件重新渲染时，会生成新的完整虚拟DOM树，并将其与之前的虚拟DOM树进行比较。React使用diff算法找出两个虚拟DOM树的差异，并且只更新需要变化的部分到实际DOM。

**性能特点：**<br />Vue的虚拟DOM：Vue通过使用异步渲染和组件级别的依赖追踪，可以更好地控制渲染的时机和粒度，从而提供更好的性能。Vue的渲染过程中，通常需要较少的虚拟DOM操作。<br />React的虚拟DOM：React采用了协调更新的策略，将多个状态变更合并为一个更新批处理。React通过一系列的优化手段（例如，批处理更新、虚拟DOM的高效比较算法）来提高性能。React的渲染过程中，可能会执行更多的虚拟DOM操作。所以react为了避免父组件更新而引起不必要的子组件更新， 可以在shouldComponentUpdate做逻辑判断，减少没必要的render， 以及重新生成虚拟dom，做差量对比过程。
<a name="g2slv"></a>
### Monorepo 
Monorepo 是一种项目代码管理方式，指单个仓库中管理多个项目，有助于**简化代码共享、版本控制、构建和部署**等方面的复杂性，并提供更好的可重用性和协作性。

- **代码复用**：因为多个项目共享一个代码库，所以避免了在不同项目中重复编写相同功能代码的问题，提高了开发效率。
- **提升协作效率**：多个项目在同一个代码库中进行开发，可以方便地共享代码和文档，避免不同项目之间的沟通和协调成本。
- **集中管理**：Monorepo 架构中，不同的应用程序都在同一个代码库中，方便管理和监控。这一点非常重要，特别是在需要同时对多个版本进行修改和维护的情况下。
- **统一构建**：Monorepo 的一个重要特点是可以共用一套构建系统和工具链进行构建和部署，提升了构建的效率。
- **可以快速定位问题**：由于所有的代码都在同一个代码库中进行开发，debugger 可以很快找出问题所在的代码文件和行数，便于开发人员调试问题。
- **一个版本**：无需担心因为项目依赖于第三方库的冲突版本而导致的不兼容问题。
<a name="qGn8k"></a>
#### pnpm 是一款快速、高效使用磁盘空间的包管理器。
它具有以下优势：

- 速度快：多数场景下，安装速度是 npm/yarn 的 2 - 3 倍。
- 基于内容寻址：硬链接节约磁盘空间，不会重复安装同一个包，对于同一个包的不同版本采取增量写入新文件的策略。
- 依赖访问安全性强：优化了 node_modules 的扁平结构，提供了限制**依赖的非法访问(幽灵依赖)** 的手段。
- 支持 Monorepo：自身能力就对 Monorepo 工程模式提供了有力的支持。在轻量场景下，无需集成 lerna Turborepo 等工具。
<a name="UwzxF"></a>
#### workspace 模式
pnpm 支持 Monorepo 模式的工作机制叫做 workspace(工作空间)。<br />它要求在代码仓的根目录下存有 pnpm-workspace.yaml 文件指定哪些目录作为独立的工作空间，这个工作空间可以理解为一个子模块或者 npm 包。<br />例如以下的 pnpm-workspace.yaml 文件定义：a 目录、b 目录、c 目录下的所有子目录，都会各自被视为独立的模块。

<a name="OQUQy"></a>
### Watch  WatchEffect
**watch 特点**<br />watch 监听函数可以添加配置项，也可以配置为空，配置项为空的情况下，watch的特点为：

- 有惰性：运行的时候，不会立即执行；
- 更加具体：需要添加监听的属性；
- 可访问属性之前的值：回调函数内会返回最新值和修改之前的值；
- 可配置：配置项可补充 watch 特点上的不足： immediate：配置 watch 属性是否立即执行，值为 true 时，一旦运行就会立即执行，值为 false 时，保持惰性。 deep：配置 watch 是否深度监听，值为 true 时，可以监听对象所有属性，值为 false 时保持更加具体特性，必须指定到具体的属性上。

**watchEffect 特点**

- 非惰性：一旦运行就会立即执行；
- 更加抽象：使用时不需要具体指定监听的谁，回调函数内直接使用就可以；
- 不可访问之前的值：只能访问当前最新的值，访问不到修改之前的值；
<a name="Mnn2t"></a>
### Vue 3 watch 与 Vue 2 watch 对比

- Vue 3 watch 与 Vue 2 的实例方法 vm.watch（也就是this._watch_（也就是_this_. watch ）的基本用法差不多，只不过程序员大多使用 watch 配置项，可能对 $watch 实例方法不太熟。实例方法的一个优势是更灵活，第一个参数可以接受一个函数，等于是接受了一个 getter 函数。
<a name="y93I9"></a>
### ref 和 toRef
[https://juejin.cn/post/6954789258607460359](https://juejin.cn/post/6954789258607460359)<br />ref、toRef、toRefs 都是composition API<br />一般在生命周期函数 setup 中使用

- ref、toRef、toRefs 都可以将某个对象中的属性变成响应式数据
- ref的本质是拷贝，修改响应式数据，不会影响到原始数据，视图会更新
- toRef、toRefs的本质是引用，修改响应式数据，会影响到原始数据，视图会更新
- toRef 一次仅能设置一个数据，接收两个参数，第一个参数是哪个对象，第二个参数是对象的哪个属性
- toRefs接收一个对象作为参数，它会遍历对象身上的所有属性，然后挨个调用toRef执行

[https://blog.csdn.net/qq_54753561/article/details/121351993](https://blog.csdn.net/qq_54753561/article/details/121351993)

<a name="QeeU4"></a>
### vue中nextTick的作用
在Vue中，$nextTick 是一个用于延迟执行代码的方法。它的作用是在当前DOM更新周期结束之后执行指定的回调函数。这个方法通常用于等待Vue实例更新完毕后再进行一些DOM操作或者获取更新后的DOM元素。<br />例如，当你修改了Vue实例的数据后，想要在DOM更新完毕后执行一些操作，可以使用 $nextTick 来确保操作在DOM更新完成后执行，而不是立即执行。
<a name="uxxSm"></a>
## <br />旧vue资料
<a name="WhU22"></a>
#### [https://vue3js.cn/interview/](https://vue3js.cn/interview/)
<a name="WSMNH"></a>
### vue的基本原理
	当一个Vue实例创建时，Vue会遍历data中的属性，用 Object.defineProperty（vue3.0使用proxy ）将每一个属性身上绑定一个 getter和setter，并且在内部追踪相关依赖，在属性被访问和修改时通知变化。 每个组件实例都有相应的 watcher 程序实例，它会在组件渲染的过程中把属性记录为依赖，之后当依赖项的setter被调用时，会通知watcher重新计算，从而致使它关联的组件得以更新。
<a name="ddsnc"></a>
### vue项目的开发思路
搭建项目环境：安装脚手架、项目初始化、安装项目依赖、<br />路由搭建：结构分析、准备组件、
<a name="k2K9y"></a>
### Vue中指令有哪些
条件渲染语句：v-if、v-else-if、v-else、v-show<br />事件指令：v-on(@)<br />属性绑定：v-bind()<br />循环指令：v-for<br />渲染指令：v-html、v-text,{{}}

<a name="g8gfl"></a>
### VUE组件中的data必须是函数
函数类别引用数据类型<br />函数属于Object，是引用数据类型，如果不用function返回，每个组件的data都是内存的同一个地址，一个数据改变了其他也改变了；<br />JavaScript只有函数构成作用域(注意理解作用域，只有**函数{}**构成作用域,对象的{}以及if(){}都不构成作用域),data是一个函数时，每个组件实例都有自己的作用域，每个实例相互独立，不会相互影响。

<a name="i6Gyu"></a>
### 使用 Object.defineProperty() 来进行数据劫持有什么缺点？
	在对一些属性进行操作时，使用这种方法无法拦截，比如通过下标方式修改数组数据或者给对象新增属性，这都不能触发组件的重新渲染，因为 Object.defineProperty 不能拦截到这些操作。更精确的来说，对于数组而言，大部分操作都是拦截不到的，只是 Vue 内部通过重写函数的方式解决了这个问题。<br />	在 Vue3.0 中已经不使用这种方式了，而是通过使用 Proxy 对对象进行代理，从而实现数据劫持。使用Proxy 的好处是它可以完美的监听到任何方式的数据改变，唯一的缺点是兼容性的问题，因为 Proxy 是 ES6 的语法。
<a name="FjBuv"></a>
### 双向数据绑定的原理
[双向绑定的原理是什么](https://vue3js.cn/interview/vue/bind.html#%E4%BA%8C%E3%80%81%E5%8F%8C%E5%90%91%E7%BB%91%E5%AE%9A%E7%9A%84%E5%8E%9F%E7%90%86%E6%98%AF%E4%BB%80%E4%B9%88)<br />[vue2和vue3数据劫持的区别](https://juejin.cn/post/7027424588707397662#heading-7)<br />[vue3响应式原理](https://juejin.cn/post/7334623638115598347?searchId=202405081301308E64A8AEBF9BAB77A939)<br />Vue.js 是采用**数据劫持**结合**发布者-订阅者模式**的方式，通过Object.defineProperty()来劫持各个属性，将data全部属性替换成getter和setter，配合发布者和订阅者模式，每一个组件都有一个watcher实例，当我们对data属性赋值和改变，就会触发setter，setter会通知watcher，从而使它关联的组件进行重新渲染。主要分为以下几个步骤：<br />**数据层（Model）**

1. 需要监听器（Observer）的数据对象进行递归遍历，包括子属性对象的属性，都加上setter和getter这样的话，给这个对象的某个值赋值，就会触发setter，那么就能监听到了数据变化

**视图层（View)**

2. compile解析模板指令，将模板中的变量替换成数据，然后初始化渲染页面视图，并将每个指令对应的节点绑定更新函数，添加监听数据的订阅者，一旦数据有变动，收到通知，更新视图

**ViewModel**<br />主要职责————数据变化后更新视图  & 视图变化后更新数据

3. Watcher订阅者是监听器（Observer）和解析器（Compiler）之间通信的桥梁，主要做的事情是: ①在自身实例化时往属性订阅器(dep)里面添加自己 ②自身必须有一个update()方法 ③待属性变动dep.notice()通知时，能调用自身的update()方法，并触发Compile中绑定的回调，则功成身退。

4. MVVM作为数据绑定的入口，整合Observer、Compile和Watcher三者，通过Observer来监听自己的model数据变化，通过Compile来解析编译模板指令，最终利用Watcher搭起Observer和Compile之间的通信桥梁，达到数据变化 -> 视图更新；视图交互变化(input) -> 数据model变更的双向绑定效果。

![image.png](https://cdn.nlark.com/yuque/0/2024/png/43022426/1715145178758-8bed67fd-dd9c-430b-a52c-03f9816127fe.png#averageHue=%23f8f8f8&clientId=u04211fa2-28af-4&from=paste&id=LC2lu&originHeight=390&originWidth=730&originalType=url&ratio=1.375&rotation=0&showTitle=false&size=37183&status=done&style=none&taskId=u929ff13e-6041-4994-9e21-b9901201a9a&title=)

<a name="AmiKw"></a>
### v-if和v-show的区别
	手段<br />		v-if是动态的向DOM树内添加或者删除DOM元素；v-show是通过设置DOM元素的display样式属性控制显隐<br />	编译过程<br />		v-if切换有一个局部编译/卸载的过程，切换过程中合适地销毁和重建内部的事件监听和子组件；v-show只是简单的基于css切换<br />	编译条件<br />		v-if是惰性的，如果初始条件为假，则什么也不做；只有在条件第一次变为真时才开始局部编译; v-show是在任何条件下，无论首次条件是否为真，都被编译，然后被缓存，而且DOM元素保留<br />	性能消耗
<a name="SEaul"></a>
##### 		v-if有更高的切换消耗；v-show有更高的初始渲染消耗
	使用场景
<a name="EtyRw"></a>
##### 		v-if适合不大可能改变；v-show适合频繁切换

<a name="F0KXj"></a>
### *v-model的数据双向绑定理
	vue中v-model可以实现数据的双向绑定，但是为什么这个指令就可以实现数据的双向绑定呢？其实**v-model是vue的一个语法糖**。即利用v-model绑定数据后，既绑定了数据，又添加了一个input事件监听。<br />		实现原理<br />			● **属性绑定：**v-bind绑定响应数据作为属性<br />				<br />			● **事件绑定：** 触发input事件监听数据<br />v-module双向绑定的底层原理:<br />数据绑定+事件绑定<br />通过v-bind:value=‘msg’,将value属性和msg数据进行绑定,n那么msg的值就会影响value的值;<br />然后通过通过v-on:input=‘msg=$event.target.value’，给文本添加了一个input事件
<a name="aVpWx"></a>
### vue如何监听对象或者数组某个属性的变化
	先判断属性是否原本就存在，若存在，则利用自身的setter和getter实现数据的实时更新<br />	当在项目中直接设置数组的某一项的值，或者直接设置对象的某个属性值，这个时候，你会发现页面并没有更新。这是因为Object.defineProperty()限制，监听不到变化。
<a name="wqioj"></a>
### *Vue的生命周期
	Vue 实例有⼀个完整的⽣命周期，也就是从开始创建、初始化数据、编译模版、挂载Dom -> 渲染、更新 -> 渲染、卸载 等⼀系列过程，称这是Vue的⽣命周期。

beforeCreate( 创建前 )<br />数据观测和初始化事件还未开始，elemnets 和 data 并未初始化，因此无法访问methods， data， computed等上的方法和数据。

created ( 创建后 ）<br />实例创建完成，实例上配置的 options 包括 data、computed、watch、methods 等都配置完成，可以访问data数据以及methods方法，但是此时渲染的节点还未挂载到 DOM，所以不能访问到 $el（vue关联的dom） 属性（vm实例身上）。<br />这是一个常用的生命周期，因为你可以调用methods中的方法，改变data中的数据，并且修改可以通过vue的响应式绑定体现在页面上，获取computed中的计算属性等等，通常我们可以在这里对实例进行预处理，也有一些童鞋喜欢在这里发ajax请求，值得注意的是，这个周期中是没有什么方法来对实例化过程进行拦截的，因此假如有某些数据必须获取才允许进入页面的话，并不适合在这个方法发请求，建议在组件路由钩子beforeRouteEnter中完成

beforeMount<br />在挂载开始之前被调用，相关的render函数首次被调用。实例已完成以下的配置：编译模板，把data里面的数据和模板生成html。此时还没有挂载html到页面上，虚拟DOM生成，此时页面渲染的是未经vue编译的DOM结构

mounted<br />在el被新创建的 vm.$el 替换，并挂载到实例上去之后调用。实例已完成以下的配置：用上面编译好的html内容替换el属性指向的DOM对象。完成模板中的html渲染到html 页面中。<br />此时一般可以做一些ajax操作，mounted只会执行一次。

beforeUpdate<br />响应式数据更新时调用，此时虽然响应式数据更新了，但是对应的真实 DOM 还没有被渲染。<br />可以在该钩子中进一步地更改状态，不会触发附加地重渲染过程

updated（更新后）<br />在由于数据更改导致的虚拟DOM重新渲染和打补丁之后调用。此时 DOM 已经根据响应式数据的变化更新了。调用时，组件 DOM已经更新，所以可以执行依赖于DOM的操作。然而在大多数情况下，应该避免在此期间更改状态，因为这可能会导致更新无限循环。该钩子在服务器端渲染期间不被调用。

beforeDestroy（销毁前）<br />实例销毁之前调用。这一步，实例仍然完全可用，<br />这一步仍可以用this来获取实例，<br />一般在这一步做一些重置的操作，比如清除掉组件中的定时器 和 监听的dom事件

destroyed（销毁后）<br />实例销毁后调用，调用后，（Vue 实例指示的所有东西都会解绑定）所有的事件监听器会被移除，所有的子实例也会被销毁。该钩子在服务端渲染期间不被调用。

另外还有 keep-alive 独有的生命周期，分别为 activated 和 deactivated 。用 keep-alive 包裹的组件在切换时不会进行销毁，而是缓存到内存中并执行 deactivated 钩子函数，缓存渲染后会执行 activated 钩子函数。
<a name="oIk97"></a>
### keep-alive的理解
	keep-alive是vue中的内置组件，能在组件切换过程中将状态保留在内存中，防止重复渲染DOM；设置了 keep-alive 缓存的组件，会多出两个生命周期钩子activated 和deactivated
<a name="A9tRc"></a>
### 父子组件生命周期执行顺序
父组件实例先完成创建、在挂载前——子组件开始创建并完成挂载——父组件完成挂载<br />父组件预备更新(组件数据更新之前调用)，子组件开始并完成更新——父组件完成更新<br />父组件销毁前，子组件开始并完成销毁——父组件完成销毁<br />父beforeCreate -> 父created -> 父beforeMount -> 子beforeCreate -> 子created -> 子beforeMount -> 子mounted -> 父mounted->父beforeUpdate->子beforeUpdate->子updated->父updated->父beforeDestroy->子beforeDestroy->子destroyed->父destroyed
<a name="Gj1a8"></a>
####  
<a name="eDx3i"></a>
### 常用的组件间通信方式有哪些？
**一、组件间通信的方案**<br />整理vue中8种常规的通信方案

1. 通过 props 传递
2. 通过 $emit 触发自定义事件
3. 使用 ref
4. EventBus
5. $parent 或$root
6. attrs 与 listeners
7. Provide 与 Inject
8. Vuex
<a name="pGRsd"></a>
#### [#](https://vue3js.cn/interview/vue/communication.html#props%E4%BC%A0%E9%80%92%E6%95%B0%E6%8D%AE)props传递数据

- 适用场景：父组件传递数据给子组件
- 子组件设置props属性，定义接收父组件传递过来的参数
- 父组件在使用子组件标签中通过字面量来传递值
<a name="Lqexk"></a>
#### [#](https://vue3js.cn/interview/vue/communication.html#emit-%E8%A7%A6%E5%8F%91%E8%87%AA%E5%AE%9A%E4%B9%89%E4%BA%8B%E4%BB%B6)$emit 触发自定义事件

- 适用场景：子组件传递数据给父组件
- 子组件通过$emit触发自定义事件，$emit第二个参数为传递的数值
- 父组件绑定监听器获取到子组件传递过来的参数

Children.vue
```javascript
this.$emit('add', good)
```
Father.vue
<a name="UWkOm"></a>
#### [#](https://vue3js.cn/interview/vue/communication.html#ref)ref

- 父组件在使用子组件的时候设置ref
- 父组件通过设置子组件ref来获取数据

父组件
```javascript
<Children ref="foo" />  

  this.$refs.foo  // 获取子组件实例，通过子组件实例我们就能拿到对应的数据
```
<a name="KoDYv"></a>
#### [#](https://vue3js.cn/interview/vue/communication.html#eventbus)EventBus

- 使用场景：兄弟组件传值
- 创建一个中央事件总线EventBus
- 兄弟组件通过$emit触发自定义事件，$emit第二个参数为传递的数值
- 另一个兄弟组件通过$on监听自定义事件

（将`变量`值存贮在了事件总线中，在其他组件中可以直接访问。事件总线就相当于一个桥梁，不用组件通过它来通信。）<br />_运行机制：EventBus_是一款发布/订阅事件总线框架模式。 将事件的接收者和发送者分开<br />Bus.js
```javascript
// 创建一个中央时间总线类  
class Bus {  
  constructor() {  
    this.callbacks = {};   // 存放事件的名字  
  }  
  $on(name, fn) {  
    this.callbacks[name] = this.callbacks[name] || [];  
    this.callbacks[name].push(fn);  
  }  
  $emit(name, args) {  
    if (this.callbacks[name]) {  
      this.callbacks[name].forEach((cb) => cb(args));  
    }  
  }  
}  

// main.js  
Vue.prototype.$bus = new Bus() // 将$bus挂载到vue实例的原型上  
// 另一种方式  
Vue.prototype.$bus = new Vue() // Vue已经实现了Bus的功能
```
Children1.vue
```
this.$bus.$emit('foo')
```
Children2.vue
```
this.$bus.$on('foo', this.handle)
```
<a name="t30eP"></a>
#### [#](https://vue3js.cn/interview/vue/communication.html#parent-%E6%88%96-root)$parent 或$ root

- 通过共同祖辈$parent或者$root搭建通信桥连

兄弟组件<br />this.$parent.on('add',this.add)<br />另一个兄弟组件<br />this.$parent.emit('add')
<a name="SDTQn"></a>
#### [#](https://vue3js.cn/interview/vue/communication.html#attrs-%E4%B8%8E-listeners)$attrs 与$ listeners

- 适用场景：祖先传递数据给子孙
- 设置批量向下传属性$attrs和 $listeners
- 包含了父级作用域中不作为 prop 被识别 (且获取) 的特性绑定 ( class 和 style 除外)。
- 可以通过 v-bind="$attrs" 传⼊内部组件
```javascript
// child：并未在props中声明foo  
<p>{{$attrs.foo}}</p>  

  // parent  
  <HelloWorld foo="foo"/>
```

```javascript
// 给Grandson隔代传值，communication/index.vue  
<Child2 msg="lalala" @some-event="onSomeEvent"></Child2>  

  // Child2做展开  
  <Grandson v-bind="$attrs" v-on="$listeners"></Grandson>  

  // Grandson使⽤  
  <div @click="$emit('some-event', 'msg from grandson')">  
{{msg}}  
  </div>
```
<a name="Mug2K"></a>
#### [#](https://vue3js.cn/interview/vue/communication.html#provide-%E4%B8%8E-inject)provide 与 inject

- 在祖先（父）组件定义provide属性，返回传递的值
- 在后代（子）组件通过inject接收组件传递过来的值

祖先组件
```
provide(){  
    return {  
        foo:'foo'  
    }  
}
```
后代组件
```
inject:['foo'] // 获取到祖先组件传递过来的值
```
<a name="oq7Ye"></a>
#### [#](https://vue3js.cn/interview/vue/communication.html#vuex)vuex

- 适用场景: 复杂关系的组件数据传递
- Vuex作用相当于一个用来存储共享变量的容器 ![image.png](https://cdn.nlark.com/yuque/0/2024/png/43022426/1715139730300-591cebdb-af98-4f1c-bc9f-1a88b4f0c579.png#averageHue=%23fefdfb&clientId=u76bc55ce-034a-4&from=paste&id=u74a14c99&originHeight=551&originWidth=701&originalType=url&ratio=1.375&rotation=0&showTitle=false&size=30488&status=done&style=none&taskId=u1ec681e1-f9c0-43d3-ab75-9dc83b12dde&title=)
- state用来存放共享变量的地方
- getter，可以增加一个getter派生状态，(相当于store中的计算属性），用来获得共享变量的值
- mutations用来存放修改state的方法。
- actions也是用来存放修改state的方法，不过action是在mutations的基础上进行。常用来做一些异步操作
<a name="FhNvl"></a>
#### [#](https://vue3js.cn/interview/vue/communication.html#%E5%B0%8F%E7%BB%93)小结

- 父子关系的组件数据传递选择 props  与 $emit进行传递，也可选择ref
- 兄弟关系的组件数据传递可选择$bus，其次可以选择$parent进行传递
- 祖先与后代组件数据传递可选择attrs与listeners或者 Provide与 Inject
- 复杂关系的组件数据传递可以通过vuex存放共享的变量

<a name="q9K14"></a>
### Vuex有哪几种属性？
	state => 基本数据(数据源存放地)<br />	getters => 从基本数据派生出来的数据<br />	mutations => 提交更改数据的方法，同步<br />	actions => 像一个装饰器，包裹mutations，使之可以异步。<br />	modules => 模块化Vuex
<a name="zVLOY"></a>
### vue-router：params和query的区别
**用法**

- **query**可以用name和path来引入；接收参数this.$route.query.name；在路由信息配置时路径path不需要占位
- **params**要用name来引入；接收参数this.$route.params.name；在路由信息配置时路径path需要占位

**url地址显示**

- query更加类似于ajax中get传参，在浏览器地址栏中显示参数
- params则类似于post，在浏览器地址栏中不显示参数

**刷新**

- query刷新不会丢失query里面的数据
- params刷新会丢失 params里面的数据（可考虑采取本地存储解决此问题）

<a name="Nk1PD"></a>
### Vue-router 导航守卫有哪些
	全局守卫（前置/后置）：beforeEach、beforeResolve、afterEach<br />	路由独享的守卫：beforeEnter<br />	组件内的守卫：beforeRouteEnter、beforeRouteUpdate、beforeRouteLeave

<a name="mhTD3"></a>
### 对虚拟DOM的理解？
	虚拟DOM就是用来描述真实DOM的javaScript对象，可以将多次修改的DOM一次性渲染到页面上，减少页面的重排重绘，提高渲染性能。 在代码渲染到页面之前，vue会把代码转换成一个对象（虚拟 DOM）。在每次数据发生变化前，虚拟DOM都会缓存一份，变化之时，现在的虚拟DOM会与缓存的虚拟DOM进行比较。在vue内部封装了diff算法，通过这个算法来进行比较，渲染时修改改变的变化，原先没有发生改变的通过原先的数据进行渲染。

<a name="nlON0"></a>
### 虚拟DOM的解析过程
	● 首先对将要插入到文档中的 DOM 树结构进行分析，使用 js 对象将其表示出来并将这个 js 对象树给保存下来，最后再将 DOM 片段插入到文档中。<br />	● 当页面的状态发生改变，需要对页面的 DOM 的结构进行调整的时候，首先根据变更的状态，重新构建起一棵对象树，然后将这棵新的对象树和旧的对象树进行比较，记录下两棵树的的差异。<br />	● 最后将记录的有差异的地方应用到真正的 DOM 树中去，这样视图就更新了。
<a name="ZaH2S"></a>
### DIFF算法的原理
	● 首先，对比节点本身，判断是否为同一节点，如果不为相同节点，则删除该节点重新创建节点进行替换<br />	● 如果为相同节点，进行patchVnode，判断如何对该节点的子节点进行处理，先判断一方有子节点一方没有子节点的情况(如果新的没有子节点，将旧的子节点移除)<br />	● 比较如果都有子节点，则进行updateChildren，判断如何对这些新老节点的子节点进行操作（diff核心）。<br />	● 匹配时，找到相同的子节点，递归比较子节点<br />	● 更新差异，复用节点

<a name="UL5qG"></a>
### Vue中key的作用
把树形结构按照层级分解，只比较同级元素<br />通过给列表结构的每个单元添加的唯一 key值进行区分同层次的子节点的比较。

	第一种情况是 v-if 中使用 key。由于 Vue 会尽可能高效地渲染元素，通常会复用已有元素而不是从头开始渲染。因此当使用 v-if 来实现元素切换的时候，如果切换前后含有相同类型的元素，那么这个元素就会被复用。如果是相同的 input 元素，那么切换前后用户的输入不会被清除掉，这样是不符合需求的。因此可以通过使用 key 来唯一的标识一个元素，这个情况下，使用 key 的元素不会被复用。这个时候 key 的作用是用来标识一个独立的元素。<br />	第二种情况是 v-for 中使用 key。用 v-for 更新已渲染过的元素列表时，它默认使用“就地复用”的策略。如果数据项的顺序发生了改变，Vue 不会移动 DOM 元素来匹配数据项的顺序，而是简单复用此处的每个元素。因此通过为每个列表项提供一个 key 值，来以便 Vue 跟踪元素的身份，从而高效的实现复用。这个时候 key 的作用是为了高效的更新渲染虚拟 DOM。<br />	总结<br />		vue为了更高效的渲染元素，会尽可能的复用元素，而非从头渲染，key可以为节点打标记，而非简单的复用节点。当数据发生变化时，Vue会根据【新数据】生成【新的虚拟DOM】, 随后Vue进行【新虚拟DOM】与【旧虚拟DOM】的差异比较，比较规则<br />旧虚拟DOM中找到了与新虚拟DOM相同的key<br />若虚拟DOM中内容没变, 直接使用之前的真实DOM<br />若虚拟DOM中内容变了, 则生成新的真实DOM，随后替换掉页面中之前的真实DOM<br />旧虚拟DOM中未找到与新虚拟DOM相同的key<br />创建新的真实DOM，随后渲染到到页面

<a name="CyMo6"></a>
### 为什么不建议用index作为key?
	若对数据进行：逆序添加、逆序删除等破坏顺序操作:会产生没有必要的真实DOM更新 ==> 界面效果没问题, 但效率低<br />	如果逆序添加、逆序删除等破坏顺序的操作且结构中还包含输入类的DOM：会产生错误DOM更新 ==> 界面有问题

<a name="SdNBO"></a>
### Computed 和 Watch 的区别
	Computed<br />		它支持缓存，只有依赖的数据发生了变化，才会重新计算<br />		不支持异步，当Computed中有异步操作时，无法监听数据的变化<br />		computed的值会默认走缓存，计算属性是基于它们的响应式依赖进行缓存的，也就是基于data声明过，或者父组件传递过来的props中的数据进行计算的<br />		如果一个属性是由其他属性计算而来的，这个属性依赖其他的属性，一般会使用computed<br />		如果computed属性的属性值是函数，那么默认使用get方法，函数的返回值就是属性的属性值；在computed中，属性有一个get方法和一个set方法，当数据发生变化时，会调用set方法<br />	Watch<br />		它不支持缓存，数据变化时，它就会触发相应的操作<br />		支持异步监听<br />		监听的函数接收两个参数，第一个参数是最新的值，第二个是变化之前的值<br />		当一个属性发生变化时，就需要执行相应的操作<br />		监听数据必须是data中声明的或者父组件传递过来的props中的数据，当发生变化时，会触发其他操作，函数有两个的参数<br />			  immediate：组件加载立即触发回调函数<br />			deep：深度监听，发现数据内部的变化，在复杂数据类型中使用，例如数组中的对象发生变化
<a name="BTah7"></a>
####  
<a name="w46qq"></a>
### Vuex 和 localStorage 的区别
<a name="o4TZg"></a>
##### 	存储位置区别
		● vuex存储在内存中<br />		● localstorage 则以文件的方式存储在本地，只能存储字符串类型的数据，存储对象需要 JSON的stringify和parse方法进行处理。 读取内存比读取硬盘速度要快
<a name="J7WVt"></a>
##### 	应用场景区别
		● Vuex 是一个专为 Vue.js 应用程序开发的状态管理模式。它采用集中式存储管理应用的所有组件的状态，并以相应的规则保证状态以一种可预测的方式发生变化。vuex用于组件之间的传值。<br />		● localstorage是本地存储，是将数据存储到浏览器的方法，一般是在跨页面传递数据时使用 。
<a name="mjNTV"></a>
##### 	响应式区别
		Vuex能做到数据的响应式<br />		localstorage不能做到数据的响应式
<a name="PO42S"></a>
##### 	时效区别
		刷新页面时vuex存储的值会丢失<br />		刷新页面时localstorage存储的值不会丢失
<a name="IDO9x"></a>
### Vue data 中某一个属性的值发生改变后，视图会立即同步执行重新渲染吗？
	不会立即同步执行重新渲染。Vue 实现响应式并不是数据发生变化之后 DOM 立即变化，而是按一定的策略进行 DOM 的更新。Vue 在更新 DOM 时是异步执行的。只要侦听到数据变化， Vue 将开启一个队列，并缓冲在同一事件循环中发生的所有数据变更。如果同一个watcher被多次触发，只会被推入到队列中一次。这种在缓冲时去除重复数据对于避免不必要的计算和 DOM 操作是非常重要的。然后，在下一个的事件循环tick中，Vue 刷新队列并执行实际（已去重的）工作。
<a name="YVwBO"></a>
### Vue与react区别
<a name="p8RFZ"></a>
#### 共同点

1. 数据驱动视图
2. 组件化
3. 都使用 Virtual DOM
<a name="wEWwT"></a>
####  区别

1. 核心思想不同
2. 组件写法差异
3. diff算法不同
4. 响应式原理不同

Vue<br />Vue依赖收集，自动优化，数据可变。<br />Vue递归监听data的所有属性,直接修改。<br />当数据改变时，自动找到引用组件重新渲染。<br />React<br />React基于状态机，手动优化，数据不可变，需要setState驱动新的state替换老的state。当数据改变时，以组件为根目录，默认全部重新渲染, 所以 React 中会需要 shouldComponentUpdate 这个生命周期函数方法来进行控制<br />5.vue api较多 react api较少<br />vue指令 react js要求 
<a name="bLhJf"></a>
#### Vue与react区别
**共同点**<br />Vue和React存在着很多的共同点：

- 数据驱动视图

在jquery时代，我们需要频繁的操作DOM来实现页面效果与交互；<br />而Vue和React 解决了这一痛点，采用数据驱动视图方式，隐藏操作DOM的频繁操作。所以我们在开发时，只需要关注数据变化即可

- 组件化

React与Vue都遵循组件化思想

- 都使用 Virtual DOM

Vue与React都使用了 Virtual DOM + Diff算法，当每一次UI更新时，总会根据render重新生成最新的VNode，然后跟以前缓存起来老的VNode进行比对，再使用Diff算法（框架核心）去真正更新真实DOM

**区别**：<br />1. 核心思想不同

- 进行数据拦截/代理，它对侦测数据的变化更敏感、更精确，vue是指令式的
- React推崇函数式编程（纯组件），数据不可变以及单向数据流,当然需要双向的地方也可以手动实现， 比如借助onChange和setState来实现。react是编程式的

2. 组件写法差异

- react的思路是all in js，通过js来生成html，通过js来操作css，
- vue更偏向于html文件的书写规范，

3. 监听数据变化的实现原理不同

- Vue 通过 getter/setter 以及一些函数的劫持，能精确知道数据变化，不需要特别的优化就能达到很好的性能
- React 默认是通过比较引用的方式进行的，如果不优化（PureComponent/shouldComponentUpdate）可能导致大量不必要的DOM的重新渲染 

4. 响应式原理不同

- Vue

Vuex是直接修改<br />Vue依赖收集，自动优化，数据可变。<br />Vue递归监听data的所有属性,直接修改。<br />当数据改变时，自动找到引用组件重新渲染。

- React

Redux每次都是用新的state替换旧的state<br />React基于状态机，手动优化，数据不可变，需要setState驱动新的state替换老的state。当数据改变时，以组件为根目录，默认全部重新渲染, 所以 React 中会需要 shouldComponentUpdate 这个生命周期函数方法来进行控制<br />5.vue api较多 react api较少<br />vue指令 react js要求

- Vue 通过 getter/setter 以及一些函数的劫持，能精确知道数据变化，不需要特别的优化就能达到很好的性能
- React 默认是通过比较引用的方式进行的，如果不优化（PureComponent/shouldComponentUpdate）可能导致大量不必要的DOM的重新渲染 
- Vue 使用的是可变数据，而React更强调数据的不可变。
- Vue默认支持双向绑定，而React从诞生以来就不支持双向绑定，它更强调单向数据流，不过我们使用了Vuex或者Redux这样的单向数据流状态管理框架，就不太能感觉到这方面的区别了
- HOC和Mixins，Vue组合不同功能方式是通过混入，而React使用的是高阶组件，React 最早也是使用 mixins 的，不过后来他们觉得这种方式对组件侵入太强会导致很多问题，就弃用了 mixinx 转而使用 Hoc。由于Vue的组件是一个被包装的函数，因此不太方便使用hoc，而react的组件是一个纯函数，所以使用起hoc就比较容易
- 写法上面的区别，vue是指令式的，而react是编程式的。
- 状态管理上，Redux 使用的是不可变数据，而Vuex的数据是可变的。Redux每次都是用新的state替换旧的state，而Vuex是直接修改
<a name="eVCx9"></a>
### 如何封装一个组件
oop设计原则<br />单一职责<br />接口隔离<br />开闭原则
<a name="JXQ2N"></a>
### 性能优化
<a name="aQ5d4"></a>
## script标签中defer和async的区别
![](https://cdn.nlark.com/yuque/0/2024/png/43022426/1712662914912-8acb0533-175b-4849-b62f-3901c3318283.png#averageHue=%23f5f2ee&clientId=u3fe1dcdc-fce2-4&from=paste&id=uee3cf273&originHeight=593&originWidth=1096&originalType=url&ratio=1.375&rotation=0&showTitle=false&status=done&style=none&taskId=u15a5937c-b26f-4151-9c4b-c269fe761cf&title=)
<a name="c3s8b"></a>
## *性能优化

1. 检查Waterfall瀑布图（Network）
   -  减少资源加载时间
   - 减少请求数量
   - 优化资源请求顺序，加快渲染时间

1. 打包优化

**工具：web-bundle-analyzer**

   - tree shaking
   - 分包/拆包 （按需加载 三方库按需引入）
   - 优化source Map
1. JS性能优化

tool： performance/ recorder

   - FCP(首次内容绘制/最大内容绘制)
   - 并发情况& 并发顺序
   - JS执行情况
1. 性能监视器（F12 -> ctrl + shift +p)
2. CDN

去中心化<br />（静态资源、音频、视频、JS资源、图片）

1. 懒加载、防抖、节流

优化白屏、首屏加载时间<br />表格、选择器性能优化
<a name="zeIKW"></a>
#### 怎么样从web前端方面优化性能？至少列举5点？
1) HTML部分

- 语义化HTML：好处在于可以使代码简洁清晰，支持不同设备，利于搜索引擎，便于团队开发；
- 减少DOM节点：加速页面渲染；
- 给图片加上正确的宽高值：这可以减少页面重绘，同时防止图片缩放；
- 防止src属性和link的href属性为空：当值为空时，浏览器很可能会把当前页面当成其属性值加载；
- 正确的闭合标签：如避免使用<div/>，浏览器会多一个将它解析成<div\></div\>的过程；
- 链接为目录或首页的地址后面加”/”，如[http://www.5icool.org/](http://www.5icool.org/)；
- 用LINK而不用@import方式导入样式；
- 样式放在页头，JS放在页尾；
- 缩小favicon.ico并缓存；

2）CSS部分

- 避免使用CSS Expressions(CSS表达式)：
- 如background color:expression((newDate()).getHours()%2 ? “#B8D4FF” : “#F08A00″ ) ;
- 避免使用CSS Filter（CSS滤镜）；
- 使用CSS缩写，减少代码量；
- 通过CSSSprites把同类图片合成一张，减少图片请求；
- 减少查询层级：如.header .logo要好过.header .top .logo；
- 减少查询范围：如.header>li要好过.header li；
- 避免TAG标签与CLASS或ID并存：如a.top、button#submit；
- 删除重复的CSS；

3)  Javscript部分

- 尽量少用全局变量；
- 使用事件代理绑定事件，如将事件绑定在body上进行代理；
- 避免频繁操作DOM节点；
- 不使用EVAL；
- 减少对象查找，如a.b.c.d这种查找方式非常耗性能，尽可能把它定义在变量里；
- 类型转换：把数字转换成字符串使用”” + 1，浮点数转换成整型使用Math.floor()或者Math.round()；
- 对字符串进行循环操作，譬如替换、查找，应使用正则表达式；
- 删除重复的JS；



4)  服务器部分

- 尽量合并CSS、JS文件，或将其直接写在页面上，减少HTTP请求；
- 压缩CSS、JS文件，缩短文件传输时间；
- 避免404错误：特别要避免给404指定一个停摆页面，否则所有404错误都将会加载一次页面；
- 一般要求减少DNS查询次数，如同一个页面的请求资源尽量少的使用不同的主机名，这可以减少网站并行下载的数量，但很多网站为了加速下载资源其实是特意用了多个主机名，这里要做一个权衡；
- 使用CDN加速，使用户从离自己最近的服务器下载文件；
- 减少Cookie的大小，使用无cookie的域，客户端请求静态文件的时候，减少 Cookie 的反复传输对主域名的影响；
- 为文件头指定Expires，使内容具有缓存性；
- 使用gzip压缩内容；
<a name="l6dWR"></a>
####  
<a name="b1ciW"></a>
#### 性能优化方法
<a name="SYL9Q"></a>
#### CDN
<a name="Y9lcG"></a>
#### 懒加载
			懒加载也叫做延迟加载、按需加载，指的是在长网页中延迟加载图片数据，是一种较好的网页性能优化的方式。在比较长的网页或应用中，如果图片很多，所有的图片都被加载出来，而用户只能看到可视窗口的那一部分图片数据，这样就浪费了性能。如果使用图片的懒加载就可以解决以上问题。在滚动屏幕之前，可视化区域之外的图片不会进行加载，在滚动屏幕时才加载。这样使得网页的加载速度更快，减少了服务器的负载。懒加载适用于图片较多，页面列表较长（长列表）的场景中。
<a name="BAqC0"></a>
#### 节流与防抖
对节流与防抖的理解<br />防抖<br />概念<br />		函数防抖是指在事件被触发 n 秒后再执行回调，如果在这 n 秒内事件又被触发，则重新计时。这可以使用在一些点击请求的事件上，避免因为用户的多次点击向后端发送多次请求。<br />应用场景<br />		按钮提交场景：防⽌多次提交按钮，只执⾏最后提交的⼀次 <br />		服务端验证场景：表单验证需要服务端配合，只执⾏⼀段连续的输⼊事件的最后⼀次，还有搜索联想词功能类似⽣存环境请⽤lodash.debounce<br />节流<br />概念<br />		函数节流是指规定一个单位时间，在这个单位时间内，只能有一次触发事件的回调函数执行，如果在同一个单位时间内某事件被触发多次，只有一次能生效。节流可以使用在 scroll 函数的事件监听上，通过事件节流来降低事件调用的频率。<br />应用场景<br />拖拽场景：固定时间内只执⾏⼀次，防⽌超⾼频次触发位置变动<br />缩放场景：监控浏览器resize <br />动画场景：避免短时间内多次触发动画引起性能问题 <br />实现节流函数和防抖函数<br />函数防抖实现<br />					<br />函数节流实现<br />					
<a name="pQiX4"></a>
#### 减少回流与重绘
回流与重绘的概念及触发条件<br />回流/重排<br />概念<br />		当渲染树中部分或者全部元素的尺寸、结构或者属性发生变化时，浏览器会重新渲染部分或者全部文档的过程就称为回流。<br />触发条件<br />		● 页面的首次渲染<br />		● 浏览器的窗口大小发生变化<br />		● 元素的内容发生变化<br />		● 元素的尺寸或者位置发生变化<br />		● 元素的字体大小发生变化<br />		● 激活CSS伪类<br />		● 查询某些属性或者调用某些方法<br />		● 添加或者删除可见的DOM元素<br />重绘<br />概念<br />		当页面中某些元素的样式发生变化，但是不会影响其在文档流中的位置时，浏览器就会对元素进行重新绘制，这个过程就是重绘。<br />触发条件<br />		● color、background 相关属性：background-color、background-image 等<br />		● outline 相关属性：outline-color、outline-width 、text-decoration<br />		● border-radius、visibility、box-shadow<br />如何避免回流与重绘<br />CSS<br />避免设置多层内联样式。<br />如果需要设置动画效果，最好使用absolute或者fixed，使元素脱离文档流，这样他们发生变化就不会影响其他元素。<br />避免使用CSS表达式（例如：calc()）。<br />JS<br />避免频繁操作样式，最好将样式列表定义为class并一次性更改class属性。<br />避免频繁操作DOM，创建一个documentFragment，在它上面应用所有DOM操作，最后再把它添加到文档中。<br />可以先为元素设置为不可见：display: none，操作结束后再把它显示出来。因为在display属性为none的元素上进行的DOM操作不会引发回流和重绘。<br />浏览器针对页面的回流与重绘，进行了自身的优化——渲染队列<br />浏览器会将所有的回流、重绘的操作放在一个队列中，当队列中的操作到了一定的数量或者到了一定的时间间隔，浏览器就会对队列进行批量处理。这样就会让多次的回流、重绘变成一次回流重绘。<br />documentFragment是什么？用它跟直接操作DOM的区别是什么？<br />概念<br />DocumentFragment，文档片段接口，一个没有父对象的最小文档对象。它被作为一个轻量版的 Document使用，就像标准的document一样，存储由节点（nodes）组成的文档结构。与document相比，最大的区别是DocumentFragment不是真实 DOM 树的一部分，它的变化不会触发 DOM 树的重新渲染，且不会导致性能等问题。<br />与直接操作 DOM 的区别<br />由于DocumentFragment不会出现在文档树中，将DocumentFragment插入文档树中，相当于把把他的子孙节点插入到文档树中，在频繁的DOM操作时，我们就可以将DOM元素插入DocumentFragment，之后一次性的将所有的子孙节点插入文档中。和直接操作DOM相比，将DocumentFragment 节点插入DOM树时，仅会触发页面的一次重绘，这样就大大提高了页面的性能。<br />		
<a name="Dyhk1"></a>
#### 图片优化
<a name="OOnNL"></a>
#### webpack优化
			如何用webpack优化前端性能？<br />				通过webpack优化前端的手段<br />					代码压缩<br />						JS代码压缩<br />							利⽤webpack的 UglifyJsPlugin 和 ParallelUglifyPlugin 来压缩JS⽂件<br />						CSS代码压缩<br />							利⽤ cssnano （css-loader?minimize）来压缩css<br />						Html文件代码压缩<br />							使用HtmlWebpackPlugin插件来生成HTML的模板时候，通过配置属性minify进行html优化<br />					文件大小压缩<br />						对文件的大小进行压缩，减少http传输过程中宽带的损耗<br />					图片压缩<br />					Tree Shaking<br />						将代码中永远不会⾛到的⽚段删除掉（消除死代码）。可以通过在启动webpack时追加参数 --optimize-minimize 来实现；<br />					代码分离<br />						代码按路由维度或者组件分块(chunk),这样做到按需加载,同时可以充分利⽤浏览器缓存<br />					提取公共第三⽅库<br />						SplitChunksPlugin插件来进⾏公共模块抽取,利⽤浏览器缓存可以⻓期缓存这些⽆需频繁变动的公共代码 <br />			如何提高webpack构建速度？<br />				优化webpack构建的方式有很多，主要可以从优化搜索时间、缩小文件搜索范围、减少不必要的编译等方面入手<br />					优化loader配置<br />						在使用loader时，可以通过配置include、exclude、test属性来匹配文件，缩小文件的搜索范围，优化搜索时间<br />					多⼊⼝情况下，使⽤ CommonsChunkPlugin 来提取公共代码<br />					通过 externals 配置来提取常⽤库，脱离webpack打包，不被打⼊bundle中，从⽽减少打包时间<br />					利⽤ DllPlugin 和 DllReferencePlugin 预编译资源模块 通过 DllPlugin 来对那些我们引⽤但是绝对不会修改的npm包来进⾏预编译，再通过 DllReferencePlugin 将预编译的模块加载进来，让⼀些基本不会改动的代码先打包成静态资源，避免反复编译浪费时间  <br />					使⽤ Happypack 实现多线程加速编译 <br />					使⽤ webpack-uglify-parallel 来提升 uglifyPlugin 的压缩速度。 原理上 webpack-uglify-parallel 采⽤了多核并⾏压缩来提升压缩速度<br />					使⽤ Tree-shaking 和 Scope Hoisting 来剔除多余代码 <br />					利⽤缓存提⾼rebuild效率<br />			如何减少webpack打包时间？<br />				优化 Loader<br />					对于 Loader 来说，影响打包效率首当其冲必属 Babel 了。因为 Babel 会将代码转为字符串生成 AST，然后对 AST 继续进行转变最后再生成新的代码，项目越大，转换代码越多，效率就越低。<br />						优化 Loader 的文件搜索范围<br />							对于 Babel 来说，希望只作用在 JS 代码上的，然后 node_modules 中使用的代码都是编译过的，所以完全没有必要再去处理一遍。<br />						还可以将 Babel 编译过的文件缓存起来，下次只需要编译更改过的代码文件即可，这样可以大幅度加快打包时间<br />							<br />				HappyPack<br />					受限于 Node 是单线程运行的，所以 Webpack 在打包的过程中也是单线程的，特别是在执行 Loader 的时候，长时间编译的任务很多，这样就会导致等待的情况。HappyPack 可以将 Loader 的同步执行转换为并行的，这样就能充分利用系统资源来加快打包效率了<br />						<br />				DllPlugin<br />					DllPlugin 可以将特定的类库提前打包然后引入。这种方式可以极大的减少打包类库的次数，只有当类库更新版本才有需要重新打包，并且也实现了将公共代码抽离成单独文件的优化方案。<br />						<br />						然后需要执行这个配置文件生成依赖文件，接下来需要使用 DllReferencePlugin 将依赖文件引入项目中<br />				代码压缩<br />					在 Webpack3 中，一般使用 UglifyJS 来压缩代码，但是这个是单线程运行的，为了加快效率，可以使用 webpack-parallel-uglify-plugin 来并行运行 UglifyJS，从而提高效率。在 Webpack4 中，不需要以上这些操作了，只需要将 mode 设置为 production 就可以默认开启以上功能。代码压缩也是我们必做的性能优化方案，当然我们不止可以压缩 JS 代码，还可以压缩 HTML、CSS 代码，并且在压缩 JS 代码的过程中，我们还可以通过配置实现比如删除 console.log 这类代码的功能。<br />				其他<br />					resolve.extensions<br />						用来表明文件后缀列表，默认查找顺序是 ['.js', '.json']，如果你的导入文件没有添加后缀就会按照这个顺序查找文件。我们应该尽可能减少后缀列表长度，然后将出现频率高的后缀排在前面<br />					resolve.alias<br />						可以通过别名的方式来映射一个路径，能让 Webpack 更快找到路径<br />					module.noParse<br />						如果你确定一个文件下没有其他依赖，就可以使用该属性让 Webpack 不扫描该文件，这种方式对于大型的类库很有帮助<br />			如何减少webpack打包体积？<br />				按需加载<br />					在开发 SPA 项目的时候，项目中都会存在很多路由页面。如果将这些页面全部打包进一个 JS 文件的话，虽然将多个请求合并了，但是同样也加载了很多并不需要的代码，耗费了更长的时间。那么为了首页能更快地呈现给用户，希望首页能加载的文件体积越小越好，这时候就可以使用按需加载，将每个路由页面单独打包为一个文件。当然不仅仅路由可以按需加载，对于 loadash 这种大型类库同样可以使用这个功能。<br />				Scope Hoisting<br />					Scope Hoisting 会分析出模块之间的依赖关系，尽可能的把打包出来的模块合并到一个函数中去。这样的打包方式生成的代码明显比之前的少多了。如果在 Webpack4 中你希望开启这个功能，只需要启用 optimization.concatenateModules 就可以了<br />						<br />				Tree Shaking<br />					Tree Shaking 可以实现删除项目中未被引用的代码（死代码）
