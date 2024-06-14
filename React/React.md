#### [https://vue3js.cn/interview/](https://vue3js.cn/interview/)
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

Vuex是直接修改<br />Vue依赖收集，自动优化，数据可变。<br />Vue递归监听data的所有属性,直接修改。<br />当数据改变时，自动找到引用组件重新渲染。<br />Redux每次都是用新的state替换旧的state

- React

Redux每次都是用新的state替换旧的state<br />React基于状态机，手动优化，数据不可变，需要setState驱动新的state替换老的state。当数据改变时，以组件为根目录，默认全部重新渲染, 所以 React 中会需要 shouldComponentUpdate 这个生命周期函数方法来进行控制<br />5.vue api较多 react api较少<br />vue指令 react js要求

- Vue 通过 getter/setter 以及一些函数的劫持，能精确知道数据变化，不需要特别的优化就能达到很好的性能
- React 默认是通过比较引用的方式进行的，如果不优化（PureComponent/shouldComponentUpdate）可能导致大量不必要的DOM的重新渲染 
- Vue 使用的是可变数据，而React更强调数据的不可变。
- Vue默认支持双向绑定，而React从诞生以来就不支持双向绑定，它更强调单向数据流，不过我们使用了Vuex或者Redux这样的单向数据流状态管理框架，就不太能感觉到这方面的区别了
- HOC和Mixins，Vue组合不同功能方式是通过混入，而React使用的是高阶组件，React 最早也是使用 mixins 的，不过后来他们觉得这种方式对组件侵入太强会导致很多问题，就弃用了 mixinx 转而使用 Hoc。由于Vue的组件是一个被包装的函数，因此不太方便使用hoc，而react的组件是一个纯函数，所以使用起hoc就比较容易
- 写法上面的区别，vue是指令式的，而react是编程式的。
- 状态管理上，Redux 使用的是不可变数据，而Vuex的数据是可变的。Redux每次都是用新的state替换旧的state，而Vuex是直接修改
#### 说说对React的理解？有哪些特性？
是什么?<br />React，用于构建用户界面的 JavaScript 库，提供了 UI 层面的解决方案，遵循组件设计模式、声明式编程范式和函数式编程概念，以使前端应用程序更高效，使用虚拟DOM来有效地操作DOM，遵循从高阶组件到低阶组件的单向数据流,帮助我们将界面成了各个独立的小块，每一个块就是组件，这些组件之间可以组合、嵌套，构成整体页面.

**特性**

- JSX语法
- 单向数据绑定
- 虚拟DOM
- 声明式编程
- HOC(higher order component)
- Component(组件化)

**优势**

- 高效灵活
- 声明式的设计，简单使用
- 组件式开发，提高代码复用率
- 单向响应的数据流会比双向绑定的更安全，速度更快
#### 说说对 State 和 Props的理解，有什么区别？
**State**<br />一个组件的显示形态可以由数据状态和外部参数所决定，而数据状态就是state，一般在 constructor 中初始化<br />当需要修改里面的值的状态需要通过调用setState来改变，从而达到更新组件内部数据的作用，并且重新调用组件render方法<br />setState还可以接受第二个参数，它是一个函数，会在setState调用完成并且组件开始重新渲染时被调用，可以用来监听渲染是否完成<br />**Props**<br />React的核心思想就是组件化思想，页面会被切分成一些独立的、可复用的组件，组件从概念上看就是一个函数，可以接受一个参数作为输入值，这个参数就是props，所以可以把props理解为从外部传入组件内部的数据<br />react具有单向数据流的特性，所以他的主要作用是从父组件向子组件中传递数据<br />props除了可以传字符串，数字，还可以传递对象，数组甚至是回调函数<br />在子组件中，props在内部不可变的，如果想要改变它看，只能通过外部组件传入新的props来重新渲染子组件，否则子组件的props和展示形式不会改变

**相同点**<br />两者都是 JavaScript 对象<br />两者都是用于保存信息<br />props 和 state 都能触发渲染更新

**区别**<br />props 是外部传递给组件的，而 state 是在组件内被组件自己管理的，一般在 constructor 中初始化<br />props 在组件内部是不可修改的，但 state 在组件内部可以进行修改<br />state 是多变的、可以修改
#### setState异步
因为 setState 并不是真正的异步函数，它实际上是通过队列延迟执行操作实现的，通过 isBatchingUpdates 来判断 setState 是先存进 state 队列还是直接更新。值为 true 则执行异步操作，false 则直接同步更新。<br />实际上，setState 并不是具备同步这种特性，只是在特定的情境下，它会从 React 的异步管控中“逃脱”掉。<br />[https://blog.csdn.net/qq_42033567/article/details/112005211?utm_medium=distribute.pc_relevant.none-task-blog-2~default~baidujs_baidulandingword~default-1-112005211-blog-79318197.pc_relevant_aa&spm=1001.2101.3001.4242.2&utm_relevant_index=4](https://blog.csdn.net/qq_42033567/article/details/112005211?utm_medium=distribute.pc_relevant.none-task-blog-2~default~baidujs_baidulandingword~default-1-112005211-blog-79318197.pc_relevant_aa&spm=1001.2101.3001.4242.2&utm_relevant_index=4)

#### 说说对React refs 的理解？应用场景？
**是什么？**<br />React 中的 Refs提供了一种方式，允许我们访问 DOM节点或在 render方法中创建的 React元素。<br />本质为ReactDOM.render()返回的组件实例，如果是渲染组件则返回的是组件实例，如果渲染dom则返回的是具体的dom节点。

**如何使用？**<br />传入字符串，使用时通过 this.refs.传入的字符串的格式获取对应的元素<br />传入对象，对象是通过 React.createRef() 方式创建出来，使用时获取到创建的对象中存在 current 属性就是对应的元素<br />传入函数，该函数会在 DOM 被挂载时进行回调，这个函数会传入一个 元素对象，可以自己保存，使用时，直接拿到之前保存的元素对象即可<br />传入hook，hook是通过 useRef() 方式创建，使用时通过生成hook对象的 current 属性就是对应的元素

**应用场景**<br />在某些情况下，我们会通过使用refs来更新组件，但这种方式并不推荐，过多使用refs，会使组件的实例或者是DOM结构暴露，违反组件封装的原则；

**但下面的场景使用refs非常有用**：<br />对Dom元素的焦点控制、内容选择、控制<br />对Dom元素的内容设置及媒体播放<br />对Dom元素的操作和对组件实例的操作<br />集成第三方 DOM 库


#### Component和PureComponent的区别
React.PureComponent 与 React.Component 几乎完全相同，但 React.PureComponent 通过props和state的浅对比来实现 shouldComponentUpate()。

在PureComponent中，如果包含比较复杂的数据结构，可能会因深层的数据不一致而产生错误的否定判断，导致界面得不到更新。

区别点：

1. PureComponent自带通过props和state的浅对比来实现 shouldComponentUpate()，而Component没有。

PureComponent缺点<br />可能会因深层的数据不一致而产生错误的否定判断，从而shouldComponentUpdate结果返回false，界面得不到更新。<br />PureComponent优势<br />不需要开发者自己实现shouldComponentUpdate，就可以进行简单的判断来提升性能。
#### 纯函数 Pure Function
**定义：**一个函数的返回结果只依赖于它的参数，并且在执行的过程中没有副作用，我们就把该函数称作纯函数。<br />**特点**<br />**1. 函数的返回结果只依赖于它的参数。**
```
let foo=(a, b)=>a+b
foo(1,2) //=3
```
**2. 函数执行过程里面没有副作用**<br />什么是副作用<br />除了修改外部的变量，一个函数在执行过程中还有很多方式产生外部可观察的变化，比如说调用 DOM API 修改页面，或者你发送了 Ajax 请求，还有调用 window.reload 刷新浏览器，甚至是 console.log 往控制台打印数据也是副作用。

3.没有额外的状态依赖<br />指方法内的状态都只在方法的生命周期内存活，这意味着不能在方法内使用共享变量，因为会带来不可知因素。

为什么需要纯函数？<br />因为纯函数非常“靠谱”，执行一个纯函数你不用担心它会干什么坏事，它不会产生不可预料的行为，也不会对外部产生影响。不管何时何地，你给它什么它就会乖乖地吐出什么。如果你的应用程序大多数函数都是由纯函数组成，那么你的程序测试、调试起来会非常方便。
#### React 加入 Hooks 的意义是什么？为什么 React 要加入Hooks 这一特性？
为了解决一些component问题：<br />组件之间的逻辑状态难以复用<br />大型复杂的组件很难拆分<br />Class语法的使用不友好<br />比如说：

类组件可以访问生命周期，函数组件不能<br />类组件可以定义维护state(状态)，函数组件不可以<br />类组件中可以获取到实例化后的this,并基于这个this做一些操作，而函数组件不可以<br />mixins:变量作用于来源不清、属性重名、Mixins引入过多会导致顺序冲突<br />HOC（高阶组件）和Render props：组件嵌套过多，不易渲染调试、会劫持props,会有漏洞<br />有了Hooks:

Hooks 就是让你不必写class组件就可以用state和其他的React特性；<br />也可以编写自己的hooks在不同的组件之间复用

**Hooks优点:**<br />没有破坏性改动：完全可选的。 你无需重写任何已有代码就可以在一些组件中尝试 Hook。100% 向后兼容的。 Hook 不包含任何破坏性改动。<br />更容易复用代码：它通过自定义hooks来复用状态，从而解决了类组件逻辑难以复用的问题<br />函数式编程风格：函数式组件、状态保存在运行环境、每个功能都包裹在函数中，整体风格更清爽、优雅<br />代码量少，复用性高<br />更容易拆分

**Hooks缺点(Hoosk有哪些坑):**<br />hooks 是 React 16.8 的新增特性、以前版本的就别想了<br />状态不同步（闭包带来的坑）:函数的运行是独立的，每个函数都有一份独立的闭包作用域。当我们处理复杂逻辑的时候，经常会碰到“引用不是最新”的问题<br />使用useState时候，使用push，pop，splice等直接更改数组对象的坑，demo中使用push直接更改数组无法获取到新值，应该采用析构方式原因：push，pop，splice是直接修改原数组，react会认为state并没有发生变化，无法更新)<br />useState 初始化只初始化一次<br />useEffect 内部不能修改 state<br />useEffect 依赖引用类型会出现死循环<br />不要在循环，条件或嵌套函数中调用Hook，必须始终在React函数的顶层使用Hook。这是因为React需要利用调用顺序来正确更新相应的状态，以及调用相应的钩子函数。一旦在循环或条件分支语句中调用Hook，就容易导致调用顺序的不一致性，从而产生难以预料到的后果
#### 有没有使用过 react hooks，它带来了那些便利？
依我的看法，React hooks 主要解决了状态以及副作用难以复用的场景，除此之外，他对我最大的好处就是在 Console 中不会看到重重叠叠相同名字的组件了(HOC)。<br />1.HOC 嵌套地狱 2.this 3.逻辑复用 3.tree-shaking<br />不用去写生命周期了<br />Hook 是 React 16.8 的新增特性。它可以让你在不编写 class 的情况下使用 state 以及其他的 React 特性，因此，现在的函数组件也可以是有状态的组件，内部也可以维护自身的状态以及做一些逻辑方面的处理；<br />通过对上面的初步认识，可以看到hooks能够更容易解决状态相关的重用的问题：

每调用useHook一次都会生成一份独立的状态

通过自定义hook能够更好的封装我们的功能

编写hooks为函数式编程，每个功能都包裹在函数中，整体风格更清爽，更优雅

hooks的出现，使函数组件的功能得到了扩充，拥有了类组件相似的功能，在我们日常使用中，使用hooks能够解决大多数问题，并且还拥有代码复用机制，因此优先考虑hooks


最常见的hooks有：useState()、useEffect() 、useRef()<br />hooks的出现，使函数组件的功能得到了扩充，拥有了类组件相似的功能；
```
function List() {
    useEffect(() => {
        console.log(`老弟你来了，List`);  // 这里可以当成 componentDidUpdate 使用，可指定依赖
        return () => {
            console.log(`老弟你走了 List`);   // return 可以当成 componentWillUnmount 使用
        }
    }, []) // 第二个参数为[]可以当成 componentDidMount 使用
    return (
        <div>
            <p>List 页面</p>
        </div>
    )
}
```
#### useState
useState 是 React Hooks 中很基本的一个 API，它的用法主要有这几种：

1. useState 接收一个初始值，返回一个数组，数组里面分别是当前值和修改这个值的方法（类似 state 和 setState）。
2. useState 接收一个函数，返回一个数组。
3. setCount 可以接收新值，也可以接收一个返回新值的函数。
```
const [ count1, setCount1 ] = useState(0);
const [ count2, setCount2 ] = useState(() => 0);
setCount1(1); // 修改 state
```
**和 class state 的区别**<br />虽然函数组件也有了 state，但是 function state 和 class state 还是有一些差异：

- function state 的粒度更细，class state 过于无脑。
- function state 保存的是快照，class state 保存的是最新值。
- 引用类型的情况下，class state 不需要传入新的引用，而 function state 必须保证是个新的引用。

#### useEffect
useEffect 是一个 Effect Hook，常用于一些副作用的操作，在一定程度上可以充当 componentDidMount、componentDidUpdate、componentWillUnmount 这三个生命周期。useEffect 是非常重要的一个方法，可以说是 React Hooks 的灵魂，它<br />用法主要有这么几种：

- useEffect 接收两个参数，分别是要执行的回调函数、依赖数组。
- 如果依赖数组为空数组，那么回调函数会在第一次渲染结束后（componentDidMount）执行，返回的函数会在组件卸载时（componentWillUnmount）执行。
- 如果不传依赖数组，那么回调函数会在每一次渲染结束后（componentDidMount 和 componentDidUpdate）执行。
- 如果依赖数组不为空数组，那么回调函数会在依赖值每次更新渲染结束后（componentDidUpdate）执行，这个依赖值一般是 state 或者 props。

![](https://cdn.nlark.com/yuque/0/2024/png/43022426/1712749438323-fee4c7f4-ebcc-477d-8211-22b5b2bccc8a.png#averageHue=%23f1f0ef&clientId=ufa3f18ac-beac-4&from=paste&id=u592c4973&originHeight=454&originWidth=577&originalType=url&ratio=1.375&rotation=0&showTitle=false&status=done&style=none&taskId=ud1ff2559-b32b-4e3e-9f77-3e798ad2002&title=)

useEffect 比较重要，它主要有这几个作用：

- 代替部分生命周期，如 componentDidMount、componentDidUpdate、componentWillUnmount。
- 更加 reactive，类似 mobx 的 reaction 和 vue 的 watch
- 从命令式变成声明式，不需要再关注应该在哪一步做某些操作，只需要关注依赖数据。
- 通过 useEffect 和 useState 可以编写一系列自定义的 Hook。

#### diff算法
把树形结构按照层级分解，只比较同级元素<br />通过给列表结构的每个单元添加的唯一 key值进行区分同层次的子节点的比较。<br />React 只会匹配相同 class 的 component（这里面的 class 指的是组件的名字）<br />合并操作，调用 component 的 setState 方法的时候, React 将其标记为 dirty. 到每一个事件循环结束, React 检查所有标记 dirty 的 component 重新绘制。<br />选择性渲染。开发人员可以重写 shouldComponentUpdate 提高 diff 的性能。

vue和react的虚拟dom都采用类似的diff算法，核心大概可以归为两点

1. 两个相同的组件产生类似的DOM结构，不同的组件产生不同的DOM结构；
2. 同一层级的一组节点，他们可以通过唯一的id进行区分。

当页面的数据发上变化的时候，Diff算法只会比较同一层级的节点：<br />如果节点类型不同，直接干掉前面的节点，在创建并插入新的节点，不会再比较这个节点以后的子节点了。<br />如果节点类型相同，则会重新设置节点的属性，从而实现节点的更新。<br />当某一层有很多相同的节点时，也就是列表节点时，Diff算法的更新过程默认情况下也是遵循以上的原则。

跟Vue一样，React 也存在diff算法，而元素key属性的作用是用于判断元素是新创建的还是被移动的元素，从而减少不必要的Diff，因此key的值需要为每一个元素赋予一个确定的标识。

如果列表数据渲染中，在数据后面插入一条数据，key作用并不大；前面的元素在diff算法中，前面的元素由于是完全相同的，并不会产生删除创建操作，在最后一个比较的时候，则需要插入到新的DOM树中。因此，在这种情况下，元素有无key属性意义并不大。<br />如果列表数据渲染中，在前面插入数据时，当拥有key的时候，react根据key属性匹配原有树上的子元素以及最新树上的子元素，只需要将元素插入到最前面位置，当没有key的时候，所有的li标签都需要进行修改<br />并不是拥有key值代表性能越高，如果说只是文本内容改变了，不写key反而性能和效率更高，主要是因为不写key是将所有的文本内容替换一下，节点不会发生变化，而写key则涉及到了节点的增和删，发现旧key不存在了，则将其删除，新key在之前没有，则插入，这就增加性能的开销<br />总结

良好使用key属性是性能优化的非常关键的一步，注意事项为：

key 应该是唯一的<br />key不要使用随机值（随机数在下一次 render 时，会重新生成一个数字）<br />避免使用 index 作为 key
#### 什么是高阶组件？
高阶组件就是一个函数，且该函数接受一个组件作为参数，并返回一个新的组件。基本上，这是从React的组成性质派生的一种模式，我们称它们为“纯”组件， 因为它们可以接受任何动态提供的子组件，但它们不会修改或复制其输入组件的任何行为。

高阶组件（HOC）是 React 中用于复用组件逻辑的一种高级技巧<br />高阶组件的参数为一个组件返回一个新的组件<br />组件是将 props 转换为 UI，而高阶组件是将组件转换为另一个组件
#### withrouter的原理
高阶组件中的withrouter 作用是将一个组件包裹Route里面, 然后react-router的三个对象history、location、match就会被放进这个组件的props属性中.<br />使用场景：非路由组件读取路由对象（参数）
```
// withRouter实现原理: 
// 将组件包裹进 Route, 然后返回
// const withRouter = () => {
//     return () => {
//         return <Route component={Nav} />
//     }
// }
 
// 这里是简化版
const withRouter = ( Component ) => () => <Route component={ Component }/>
```
#### 组件间通信
父子组件：父传子：props 子传父：子组件调用父组件的函数并传参 redux<br />兄弟：利用父组件或者Redux<br />所有关系都通用的方法：利用pubsub.js 订阅

#### react 生命周期函数
第一次被创建时，也就是实例化时，以下方法依次被调用：

1. getDefaultProps
2. getInitialState
3. componentWillMount
4. render
5. componentDidMount

当组件已经渲染好后，组件也就进入更新期，在更新期会执行以下函数：

1. componentWillReceiveProps
2. shouldComponentUpdate
3. componentWillUpdate
4. render
5. componentDidUpdate 

最后，每当React使用完一个组件，这个组件必须从 DOM 中卸载后被销毁，此时 componentWillUnmout 会被执行，完成所有的清理和销毁工作，在 componentDidMount 中添加的任务都需要再该方法中撤销，如创建的定时器或事件监听器。
#### 详细解释 React 组件的生命周期方法
componentWillMount() – 在渲染之前执行，在客户端和服务器端都会执行。<br />componentDidMount() – 仅在第一次渲染后在客户端执行。<br />componentWillReceiveProps() – 当从父类接收到 props 并且在调用另一个渲染器之前调用。<br />shouldComponentUpdate() – 根据特定条件返回 true 或 false。如果你希望更新组件，请返回true ，不想更新组件则返回 false就会阻止render渲染。默认情况下，它返回 true。<br />componentWillUpdate() – 在 DOM 中进行渲染之前调用。<br />componentDidUpdate() – 在渲染发生后立即调用。<br />componentWillUnmount() – 从 DOM 卸载组件后调用。用于清理内存空间。
#### react在哪个生命周期做优化
shouldComponentUpdate，这个方法用来判断是否需要调用 render 方法重绘 dom。<br />因为 dom 的描绘非常消耗性能，如果我们能在这个方法中能够写出更优化的 dom diff 算法，可以极大的提高性能。

#### React 中构建组件的方式

- 函数式定义的无状态组件 

无状态组件的创建形式使代码的可读性更好，并且减少了大量冗余的代码，精简至只有一个render方法，大大的增强了编写一个组件的便利，除此之外无状态组件还有以下几个显著的特点：

1. 组件不会被实例化，整体渲染性能得到提升
2. 组件不能访问this对象
3. 组件无法访问生命周期的方法
- es5原生方式React.createClass定义的组件 

React.createClass会自绑定函数方法（不像React.Component只绑定需要关心的函数）导致不必要的性能开销，并且在es6的类组件出现后，已经被废弃

- es6形式的extends React.Component定义的组件

#### 受控组件和非受控组件的区别
受控组件是React控制的组件,input等表单输入框值不存在于 DOM 中，而是以我们的组件状态存在。每当我们想要更新值时，我们就像以前一样调用setState。

不受控制组件是您的表单数据由 DOM 处理，而不是React 组件，Refs 用于获取其当前值；

React组件事件代理的原理<br />和原生HTML定义事件的唯一区别就是JSX采用驼峰写法来描述事件名称，大括号中仍然是标准的JavaScript表达式，返回一个事件处理函数。在JSX中你不需要关心什么时机去移除事件绑定，因为React会在对应的真实DOM节点移除时就自动解除了事件绑定。

React并不会真正的绑定事件到每一个具体的元素上，而是采用事件代理的模式：在根节点document上为每种事件添加唯一的Listener，然后通过事件的target找到真实的触发元素。这样从触发元素到顶层节点之间的所有节点如果有绑定这个事件，React都会触发对应的事件处理函数。这就是所谓的React模拟事件系统。

#### React中的key有什么作用？
跟Vue一样，React 也存在diff算法，而元素key属性的作用是用于判断元素是新创建的还是被移动的元素，从而减少不必要的Diff，因此key的值需要为每一个元素赋予一个确定的标识。

如果列表数据渲染中，在数据后面插入一条数据，key作用并不大；前面的元素在diff算法中，前面的元素由于是完全相同的，并不会产生删除创建操作，在最后一个比较的时候，则需要插入到新的DOM树中。因此，在这种情况下，元素有无key属性意义并不大。<br />如果列表数据渲染中，在前面插入数据时，当拥有key的时候，react根据key属性匹配原有树上的子元素以及最新树上的子元素，只需要将元素插入到最前面位置，当没有key的时候，所有的li标签都需要进行修改<br />并不是拥有key值代表性能越高，如果说只是文本内容改变了，不写key反而性能和效率更高，主要是因为不写key是将所有的文本内容替换一下，节点不会发生变化，而写key则涉及到了节点的增和删，发现旧key不存在了，则将其删除，新key在之前没有，则插入，这就增加性能的开销<br />总结

良好使用key属性是性能优化的非常关键的一步，注意事项为：

key 应该是唯一的<br />key不要使用随机值（随机数在下一次 render 时，会重新生成一个数字）<br />避免使用 index 作为 key
#### Linux
Linux允许多个用户同时使用系统，而且每个用户可以运行多个程序，稳定，安全，高效，是我们开发人员布署应用的首选. 一个操作系统的学习是多方面的，深层次的，可以是一个linux管理员，浅一点只要掌握基本的登录登出，文件/目录的增删改查，
### Redux
#### 说说你对Redux的理解？其工作原理？
redux将所有的状态进行集中管理，当需要更新状态的时候，仅需要对这个管理集中处理，而不用去关心状态是如何分发到每一个组件内部的，redux是一个实现集中管理的容器，遵循三大基本原则：单一数据源、state 是只读的、使用纯函数来执行修改；<br />注意的是，redux并不是只应用在react中，还与其他界面库一起使用，如Vue；

工作原理<br />redux要求我们把数据都放在 store公共存储空间，一个组件改变了 store 里的数据内容，其他组件就能感知到 store的变化，再来取数据，从而间接的实现了这些数据传递的功能

工作流程图如下所示：<br />![](https://cdn.nlark.com/yuque/0/2024/png/43022426/1712749438237-ffc23e95-d990-4d6a-adbd-a856b2fd6287.png#averageHue=%23f9f7f5&clientId=ufa3f18ac-beac-4&from=paste&id=ufb842588&originHeight=494&originWidth=783&originalType=url&ratio=1.375&rotation=0&showTitle=false&status=done&style=none&taskId=u11ee2428-f301-4531-9324-3a68c174c4a&title=)<br />根据流程图，可以想象，React Components 是借书的用户， Action Creactor 是借书时说的话(借什么书)， Store 是图书馆管理员，Reducer 是记录本(借什么书，还什么书，在哪儿，需要查一下)， state 是书籍信息；

整个流程就是借书的用户需要先存在，然后需要借书，需要一句话来描述借什么书，图书馆管理员听到后需要查一下记录本，了解图书的位置，最后图书馆管理员会把这本书给到这个借书人

转换为代码是，React Components 需要获取一些数据, 然后它就告知 Store 需要获取数据，这就是就是 Action Creactor , Store 接收到之后去 Reducer 查一下， Reducer 会告诉 Store 应该给这个组件什么数据

#### Redux遵循的三个原则是什么？
单一事实来源：整个应用的状态存储在单个 store 中的对象/状态树里。单一状态树可以更容易地跟踪随时间的变化，并调试或检查应用程序。<br />状态是只读的：改变状态的唯一方法是去触发一个动作。动作是描述变化的普通 JS 对象。就像 state 是数据的最小表示一样，该操作是对数据更改的最小表示。<br />使用纯函数进行更改：为了指定状态树如何通过操作进行转换，你需要纯函数。纯函数是那些返回值仅取决于其参数值的函数。

#### react-redux的两个最主要功能?
Provider：提供包含store的context<br />connect：连接容器组件和傻瓜组件；connect接收两个参数mapStateToProps和mapDispatchToProps。mapStateToProps把Store上的状态转化为内层傻瓜组件的prop,mapDispatchToProps把内层傻瓜组件中的用户动作转化为派送给Store的动作

#### Redux中异步的请求怎么处理
redux使用redux-thunk中间件处理异步状态管理请求；redux-thunk 允许我们 dispatch 一个包含异步处理逻辑函数（thunk）；我们可以借助这种简单的机制在 redux 中处理异步逻辑；

#### 介绍Redux中间件
什么是中间件：

中间件其实就是一个函数，中间件允许我们扩展redux应用程序 。具体体现在对action的处理能力上，当组件触发一个action后，这个action会优先被中间件处理，当中间件处理完后，中间件再把action传递给reducer，让reducer继续处理这个action

加入中间件的redux工作流程：<br />![](https://cdn.nlark.com/yuque/0/2024/png/43022426/1712749438371-040f27f4-41b2-4c4f-b68d-e3c8b09e7321.png#averageHue=%23475363&clientId=ufa3f18ac-beac-4&from=paste&id=uf7493d8c&originHeight=644&originWidth=1268&originalType=url&ratio=1.375&rotation=0&showTitle=false&status=done&style=none&taskId=u20675908-6568-44fa-8e2a-550974b7c55&title=)<br />常用中间件：

redux-thunk<br />redux-saga<br />redux-actions<br />你在React项目中是如何使用Redux的? 项目结构是如何划分的？<br />在Redux介绍中，我们了解到redux是用于数据状态管理，而react是一个视图层面的库。如果将两者连接在一起，可以使用官方推荐react-redux库，其具有高效且灵活的特性；

#### react-redux将组件分成：

容器组件：存在逻辑处理<br />UI 组件：只负责现显示和交互，内部不处理逻辑，状态由外部控制<br />通过redux将整个应用状态存储到store中，组件可以派发dispatch行为action给store，其他组件通过订阅store中的状态state来更新自身的视图

#### 为什么 React Router 中使用 Switch 关键字 ？
由于router和switch对于路由的渲染策略不同，对router来说，如果有的链接既可以被路由A匹配，又可以被路由B匹配，那么Router会同时渲染它们<br />对于switch来说，它只会渲染符合条件的第一个路径，避免重复匹配
