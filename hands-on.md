<a name="FXIom"></a>
#### 表格（虚拟滚动）
可编辑单元格内容更新后，重新渲染卡顿；<br />过多列和行时，虚拟滚动；

```javascript
this.tableData = list.slice(this.startRow, this.endRow);
calcColumns() {this.virtualColumns = this.allColumns.slice(this.startCol, this.endCol);
```



虚拟滚动的核心思想是只渲染用户当前视口中可见的部分数据，而不是一次性渲染所有数据。随着用户滚动，动态地增加或移除数据项，以提高渲染性能和减少内存使用。具体实现思路包括以下几点：

1. **计算可见区域**：通过监听滚动事件，计算当前视口内的可见区域，确定需要渲染的起始索引和结束索引。
- 具体步骤
   - 通过监听滚动容器的scroll事件来捕捉滚动位置的变化。
   - **计算当前滚动位置**：
   - 获取滚动容器的scrollTop属性，这表示容器顶部与内容顶部之间的垂直距离。
   - **确定起始索引和结束索引**：
   - 计算起始索引：通过将scrollTop除以每个数据项的高度（itemHeight），并使用Math.floor向下取整得到起始索引。
   - 计算结束索引：通过起始索引加上视口的高度（height）除以每个数据项的高度，得到结束索引。为了确保缓冲区，通常会增加一些额外的项。

2. **只渲染可见项**：根据计算出的索引，只渲染视口内可见的数据项，而非全部数据。
3. **占位容器**：使用一个容器元素占位，使得滚动条的长度与实际数据长度匹配，从而实现滚动效果。
4. **动态加载和卸载数据**：随着用户的滚动，动态地加载新数据项并卸载不再可见的数据项。
- 具体细节...
- 动态加载和卸载数据的目的是根据计算出的可见区域索引来更新渲染的数据项。这包括：

1. **加载新数据**：
   - 根据计算的起始索引和结束索引，从数据源中获取对应的数据项。
2. **更新渲染数据**：
   - 仅渲染计算得到的可见区域内的数据项，并调整容器的填充来模拟完整列表的高度。
3. **维护填充区域**：
   - 使用顶部填充（topPadding）和底部填充（bottomPadding）来占据未渲染的数据项的位置，使滚动条保持正常工作。

### 代码示例
```javascript
const visibleItems = items.slice(startIndex, endIndex);
const topPadding = startIndex * itemHeight;
const bottomPadding = (items.length - endIndex) * itemHeight;

return (
  <div ref={listRef} style={{ height, overflowY: 'auto' }}>
  <div style={{ height: topPadding }} />
{visibleItems.map((item, index) => (
  <div key={startIndex + index} style={{ height: itemHeight }}>
{item}
</div>
))}
<div style={{ height: bottomPadding }} />
  </div>
);
```

在这个示例中：

- visibleItems：根据起始索引和结束索引截取的数据项。
- topPadding：用来填充列表顶部未渲染项的高度。
- bottomPadding：用来填充列表底部未渲染项的高度。

##### 实战例子

###### 使用React实现虚拟滚动
```javascript
import React, { useState, useRef, useEffect, useCallback } from 'react';

const VirtualList = ({ items, itemHeight, height }) => {
  const [startIndex, setStartIndex] = useState(0);
  const [endIndex, setEndIndex] = useState(10); // 初始渲染10个项目
  const listRef = useRef(null);

  const handleScroll = useCallback(() => {
    const scrollTop = listRef.current.scrollTop;
    const newStartIndex = Math.floor(scrollTop / itemHeight);
    const newEndIndex = newStartIndex + Math.ceil(height / itemHeight);
    setStartIndex(newStartIndex);
    setEndIndex(newEndIndex);
  }, [itemHeight, height]);

  useEffect(() => {
    const listElement = listRef.current;
    listElement.addEventListener('scroll', handleScroll);
    return () => listElement.removeEventListener('scroll', handleScroll);
  }, [handleScroll]);

  const visibleItems = items.slice(startIndex, endIndex);
  const topPadding = startIndex * itemHeight;
  const bottomPadding = (items.length - endIndex) * itemHeight;

  return (
    <div ref={listRef} style={{ height, overflowY: 'auto' }}>
  <div style={{ height: topPadding }} />
{visibleItems.map((item, index) => (
  <div key={startIndex + index} style={{ height: itemHeight }}>
{item}
</div>
))}
<div style={{ height: bottomPadding }} />
  </div>
);
};

// 示例使用
const items = Array.from({ length: 1000 }, (_, i) => `Item ${i + 1}`);

const App = () => (
  <div>
  <h1>Virtual Scroll Example</h1>
  <VirtualList items={items} itemHeight={50} height={500} />
  </div>
);

export default App;
```
###### 使用Vue实现虚拟滚动
```vue
<template>
    <div ref="list" class="virtual-list" @scroll="handleScroll">
      <div :style="{ height: `${topPadding}px` }"></div>
      <div v-for="(item, index) in visibleItems" :key="startIndex + index" class="item">
        {{ item }}
      </div>
      <div :style="{ height: `${bottomPadding}px` }"></div>
    </div>
</template>

<script>
  export default {
    props: {
      items: {
      type: Array,
      required: true,
      },
      itemHeight: {
      type: Number,
      required: true,
      },
      height: {
      type: Number,
      required: true,
      },
    },
    data() {
      return {
      startIndex: 0,
      endIndex: 10, // 初始渲染10个项目
      };
    },
    computed: {
      visibleItems() {
      return this.items.slice(this.startIndex, this.endIndex);
      },
      topPadding() {
      return this.startIndex * this.itemHeight;
      },
      bottomPadding() {
      return (this.items.length - this.endIndex) * this.itemHeight;
      },
    },
    methods: {
      handleScroll() {
      const scrollTop = this.$refs.list.scrollTop;
      this.startIndex = Math.floor(scrollTop / this.itemHeight);
      this.endIndex = this.startIndex + Math.ceil(this.height / this.itemHeight);
      },
    },
    mounted() {
      this.$refs.list.addEventListener('scroll', this.handleScroll);
    },
    beforeDestroy() {
      this.$refs.list.removeEventListener('scroll', this.handleScroll);
    },
  };
</script>

  <style>
  .virtual-list {
    height: 500px;
    overflow-y: auto;
  }
  .item {
    height: 50px;
  }
  </style>
```

##### 优点

- **性能提升**：显著减少浏览器需要渲染的DOM节点数，提升滚动和渲染性能。
- **内存节省**：减少内存消耗，尤其在处理数千甚至数百万条数据时。
<a name="JYyJd"></a>
##### 注意事项

- **高度一致性**：通常适用于高度一致的列表项，对于高度不一致的项需要复杂的处理逻辑。
- **滚动跳动**：由于动态加载和卸载数据，可能会导致滚动条跳动，需要额外处理保持滚动平滑。
<a name="Km30U"></a>
#### 选择器
性能问题的表象：1.多选且选项数据量大时，通过js切换批量数据的选中状态（通过key/value选中, 查找数据，展示label），耗时严重；<br />**Map的增删查性能会优于Object**<br />相关优化：选择器内部数据结构优化  object/Array -> Map (delete和set速度更快)；<br />不仅在大数据量情况下，缩短了切换数据选中的耗时；<br />选项配置(禁用等功能）的更新，使用搜索功能后，视图的响应速度更快；

深挖：<br />频繁操作键值对时使用Map比Object性能更优

- 当key为有序连续的整数时，Object的性能优于Map；（V8对Object在键为有序连续正整数时做了优化）
1. 数据量大，频繁写入用**Map**
2. 对写入顺序有要求使用**Map**
- **Map是一个纯哈希结构，而Object不是（它拥有自己的内部逻辑）**。使用delete对Object的属性进行删除操作存在很多性能问题。所以，**针对于存在大量增删操作的场景，使用Map更合适**。
- 不同于Object，**Map会保留所有元素的顺序。Map结构是在基于可迭代的基础上构建的，所以如果考虑到元素迭代或顺序，使用Map更好，它能够确保在所有浏览器中的迭代性能**。
- Map在存储大量数据的场景下表现更好，尤其是在key为未知状态，并且所有key和所有value分别为相同类型的情况下。

[详细探讨....](https://cloud.tencent.com/developer/article/2281713)


### 卡顿该怎么优化
在前端开发中，树形结构节点拖拽时的卡顿问题通常是由于大量的 DOM 操作和频繁的状态更新引起的。以下是一些常见的优化策略，可以帮助你减少卡顿，提高性能：

#### 1. 减少不必要的重渲染
确保只有必要的组件重新渲染。可以使用 React.memo / shouldComponentUpdate来避免无关节点的重新渲染。

```javascript
import React from 'react';

const TreeNode = React.memo(({ node, onDrag }) => {
  // 渲染树节点的代码
});
```
在Vue中，也有类似于React中React.memo或者shouldComponentUpdate的方法来减少不必要的更新和渲染。以下是一些具体的手段：

- **使用v-once指令**；
- **使用计算属性（Computed Properties）**，只有在依赖项变化时才重新计算和渲染
- **使用watch监听**，从而有选择地更新组件。
- **使用v-memo指令**，Vue 3.2 引入了v-memo指令，这个指令可以缓存一个条件为真的元素或组件的渲染结果
- **使用<KeepAlive>组件**，<KeepAlive>组件用于缓存动态组件，避免不必要的重新渲染。
- ** 使用shallowReactive和shallowRef，**这些API可以创建浅层响应的对象和引用，避免深层次的数据变化导致不必要的渲染。
- ** 优化组件的更新逻辑，**beforeUpdate中进行条件判断
- ** 使用renderTracked和renderTriggered钩子**
详情...**1. 使用v-once指令**<br />v-once指令可以确保元素或组件只渲染一次，不会因为数据变化而重新渲染。
```javascript

<div v-once>
  {{ message }}
</div>
```
**2. 使用计算属性（Computed Properties）**<br />计算属性会基于其依赖项缓存结果，只有在依赖项变化时才重新计算和渲染。
```javascript
computed: {
  computedMessage() {
    return this.message.split('').reverse().join('');
  }
}
```
**3. 使用watch监听**<br />watch可以精确地监听数据变化，从而有选择地更新组件。
```javascript
watch: {
  someData(newValue, oldValue) {
    // 只有在需要时才更新
    if (newValue !== oldValue) {
      this.updateComponent();
    }
  }
}
```
**4. 使用v-memo指令**<br />Vue 3.2 引入了v-memo指令，这个指令可以缓存一个条件为真的元素或组件的渲染结果。这个指令非常类似于React中的React.memo。
```html
<div v-memo="[condition]">
  {{ message }}
</div>
```
**5. 使用<KeepAlive>组件**<br /><KeepAlive>组件用于缓存动态组件，避免不必要的重新渲染。
```html
<keep-alive>
  <component :is="currentComponent"></component>
</keep-alive>
```
**6. 使用shallowReactive和shallowRef**<br />这些API可以创建浅层响应的对象和引用，避免深层次的数据变化导致不必要的渲染。
```javascript
import { shallowReactive, shallowRef } from 'vue';

const state = shallowReactive({
  user: {
    name: 'John',
    age: 30
  }
});

const userRef = shallowRef({
  name: 'John',
  age: 30
});
```
**7. 优化组件的更新逻辑，beforeUpdate中进行条件判断**<br />可以在组件的生命周期钩子中手动控制更新逻辑，例如在beforeUpdate中进行条件判断。
```javascript
export default {
  beforeUpdate() {
    if (this.shouldUpdate()) {
      // 执行更新逻辑
    } else {
      // 阻止更新
      this.$vnode.elm._leaveCb = null;
    }
  },
  methods: {
    shouldUpdate() {
      // 自定义更新条件
      return this.someData !== this.oldData;
    }
  }
}
```
**8. 使用renderTracked和renderTriggered钩子**<br />Vue 3 提供了renderTracked和renderTriggered钩子，可以用来调试和优化渲染过程。
```javascript
export default {
  renderTracked(e) {
    console.log('Tracked:', e);
  },
  renderTriggered(e) {
    console.log('Triggered
```
<a name="I1kyR"></a>
#### <br />
<a name="ELd2F"></a>
#### 2. 优化状态管理
使用局部状态而不是全局状态来管理树节点的状态变化，减少状态更新的范围。
<a name="jwSGy"></a>
#### 3. 虚拟化
对于包含大量节点的树结构，可以使用虚拟化技术，只渲染可见区域的节点。React 中可以使用 react-virtualized 或 react-window 库。

```javascript
import { FixedSizeTree } from 'react-vtree';

const MyTree = ({ treeData }) => (
  <FixedSizeTree
treeWalker={myTreeWalker(treeData)}
itemSize={30}
height={500}
width={300}
  >
  {({ style, node }) => (
    <div style={style}>
  {node.name}
  </div>
)}
  </FixedSizeTree>
);
```
<a name="YQUOe"></a>
#### 4. 防抖和节流
对于拖拽事件，使用防抖或节流技术减少事件处理的频率。Lodash 提供了便捷的 debounce 和 throttle 函数。
```javascript
import { throttle } from 'lodash';

const handleDrag = throttle((event) => {
  // 处理拖拽事件
}, 100);  // 调整节流间隔
```
<a name="KNT39"></a>
#### 5. CSS 过渡和动画
使用 CSS 过渡和动画来处理拖拽的视觉效果，减少 JavaScript 对 DOM 的直接操作。

```css
.tree-node {
  transition: transform 0.2s ease;
}
```
<a name="OLBIH"></a>
#### 6. 分离拖拽逻辑
将拖拽逻辑与渲染逻辑分离。例如，使用 react-dnd 库来管理拖拽行为，可以减少不必要的 DOM 操作。

```javascript
import { useDrag, useDrop } from 'react-dnd';

const DraggableTreeNode = ({ node, onDrop }) => {
  const [, ref] = useDrag({
    type: 'TREE_NODE',
    item: { id: node.id }
  });

  const [, drop] = useDrop({
    accept: 'TREE_NODE',
    drop: (item, monitor) => {
      onDrop(item.id, node.id);
    }
  });

  return (
    <div ref={(node) => ref(drop(node))}>
    {node.name}
    </div>
  );
};
```
<a name="EaVrq"></a>
#### 7. 优化 DOM 操作
在拖拽过程中，避免频繁的 DOM 操作。可以使用 requestAnimationFrame 来优化频繁的 DOM 更新。

```javascript
const handleDrag = (event) => {
  requestAnimationFrame(() => {
    // 更新 DOM 操作
  });
};
```
<a name="ALFpz"></a>
#### 8. 批量更新
在可能的情况下，尽量批量处理状态更新和 DOM 操作。例如，在 React 中，可以使用 unstable_batchedUpdates 来批量更新。

```javascript
import { unstable_batchedUpdates } from 'react-dom';

const handleMultipleUpdates = (updates) => {
  unstable_batchedUpdates(() => {
    updates.forEach(update => update());
  });
};
```
通过以上策略，可以显著提高树形结构节点在拖拽过程中的性能，减少卡顿现象。根据具体情况，选择合适的优化方法组合使用，能达到最佳的性能提升效果。

树形结构查找深层子节点节点过程中卡顿该怎么办<br />在树形结构中查找深层子节点时，卡顿通常是由于大量的递归操作和深度遍历造成的。以下是几种优化策略，可以帮助你提高查找性能，减少卡顿：
<a name="W0kuh"></a>
#### 1. 使用迭代代替递归
递归操作容易造成栈溢出，特别是在处理深层嵌套的树形结构时。可以使用迭代方法代替递归。

```javascript
function findNodeIterative(tree, targetId) {
  const stack = [...tree];

  while (stack.length) {
    const node = stack.pop();
    if (node.id === targetId) {
      return node;
    }
    if (node.children) {
      stack.push(...node.children);
    }
  }

  return null;
}
```
<a name="SYgrz"></a>
#### 2. 索引节点
在树结构初始化时，预先构建一个节点索引（哈希表），将节点的 id 映射到节点对象。查找节点时可以通过查找索引直接获取节点，减少遍历次数。
构建索引哈希表```javascript
function buildNodeIndex(tree) {
  const nodeIndex = {};

  function traverse(node) {
    nodeIndex[node.id] = node;
    if (node.children) {
      node.children.forEach(child => traverse(child));
    }
  }

  tree.forEach(node => traverse(node));
  return nodeIndex;
}

const nodeIndex = buildNodeIndex(tree);
const findNodeById = (id) => nodeIndex[id];
```
<a name="U9ehy"></a>
#### 3. *树的扁平化
将树形结构扁平化为数组或其他线性数据结构，便于快速查找。扁平化过程中可以保留节点的层级信息。

```javascript
function flattenTree(tree) {
  const result = [];

  function traverse(node, level = 0) {
    result.push({ ...node, level });
    if (node.children) {
      node.children.forEach(child => traverse(child, level + 1));
    }
  }

  tree.forEach(node => traverse(node));
  return result;
}

const flatTree = flattenTree(tree);
const findNodeById = (id) => flatTree.find(node => node.id === id);
```
<a name="kFDax"></a>
#### 4. 减少不必要的计算
在查找过程中，尽量避免重复计算。如果某些节点的子树已经被查找过，可以缓存结果。
利用Map缓存```javascript
const cache = new Map();

function findNodeWithCache(tree, targetId) {
  if (cache.has(targetId)) {
    return cache.get(targetId);
  }

  const node = findNodeIterative(tree, targetId);
  cache.set(targetId, node);
  return node;
}
```
<a name="nTau3"></a>
#### 5. 使用 Web Worker
对于非常大的树形结构，可以使用 Web Worker 在后台线程中执行查找操作，避免阻塞主线程。

```javascript
// worker.js
self.onmessage = function(e) {
  const { tree, targetId } = e.data;
  const result = findNodeIterative(tree, targetId);
  self.postMessage(result);
};

// main.js
const worker = new Worker('worker.js');

worker.onmessage = function(e) {
  const node = e.data;
  console.log('Found node:', node);
};

worker.postMessage({ tree, targetId });
```
<a name="JGYIE"></a>
#### 6. 分批处理
对于超大树形结构，可以分批处理节点查找，避免长时间阻塞主线程。
分批处理节点查找```javascript
function findNodeInBatches(tree, targetId, batchSize = 100) {
  const stack = [...tree];
  let index = 0;

  function processBatch() {
    const batch = stack.splice(0, batchSize);
    for (const node of batch) {
      if (node.id === targetId) {
        return node;
      }
      if (node.children) {
        stack.push(...node.children);
      }
    }
    if (stack.length) {
      index++;
      if (index < 5) {  // 控制执行次数，避免死循环
        setTimeout(processBatch, 0); // 使用 setTimeout 将任务分批执行
      }
    }
    return null;
  }

  return processBatch();
}
```
通过上述优化策略，可以显著提高树形结构查找深层子节点的性能，减少卡顿现象。根据具体需求和场景选择合适的策略组合使用，能达到最佳的性能优化效果。
<a name="MR2Gj"></a>
### 大数据量的情况下卡顿怎么办？
在大数据量的情况下，节点拖拽卡顿是一个常见的问题。为了优化拖拽性能，可以从以下几个方面进行优化：
<a name="Cocid"></a>
#### 1. 虚拟化渲染
**Virtual Scrolling** 是一种只渲染视口内节点的技术，通过限制渲染的节点数来提升性能。常用的库如 react-virtualized、react-window 和 vue-virtual-scroller 都能帮助实现这一点。
**React 和 Vue 示例：****React 示例：**
```jsx
import { FixedSizeList as List } from 'react-window';

const Row = ({ index, style }) => (
  <div style={style}>
    Row {index}
  </div>
);

const Example = ({ data }) => (
  <List
    height={150}
    itemCount={data.length}
    itemSize={35}
    width={300}
    >
    {Row}
  </List>
);
```
**Vue 示例：**
```vue
<template>
  <RecycleScroller
    :items="items"
    :item-size="50"
    >
    <template #default="{ item, index }">
      <div class="item">
        {{ item }}
      </div>
    </template>
                 </RecycleScroller>
                   </template>

                   <script>
                   import { RecycleScroller } from 'vue-virtual-scroller';

      export default {
        components: {
          RecycleScroller
        },
        data() {
          return {
            items: Array.from({ length: 10000 }).map((_, index) => `Item ${index}`)
          };
        }
      };
    </script>

<style>
  .item {
    height: 50px;
  }
</style>
```
<a name="KMuLq"></a>
#### 2. 减少重排和重绘
拖拽过程中频繁的 DOM 操作会导致页面的重排和重绘，进而影响性能。尽量减少不必要的 DOM 操作和样式变更。<br />**优化技巧：**

- **减少不必要的样式计算**：使用 will-change 预告浏览器要进行的样式变化，减少重排和重绘。
- **利用 CSS 动画**：使用 CSS 动画代替 JavaScript 动画，减少 JavaScript 的计算负担。
<a name="sbGrt"></a>
#### 3. 节流与防抖
在拖拽事件中使用节流（throttling）或防抖（debouncing）技术，限制事件处理的频率。
**节流示例：**```javascript
function throttle(func, limit) {
  let inThrottle;
  return function() {
    const args = arguments;
    const context = this;
    if (!inThrottle) {
      func.apply(context, args);
      inThrottle = true;
      setTimeout(() => inThrottle = false, limit);
    }
  }
}

const handleDrag = throttle((event) => {
  // 处理拖拽逻辑
}, 100);

element.addEventListener('drag', handleDrag);
```
<a name="NxX3i"></a>
#### 4. 使用 Web Workers
将繁重的计算任务（例如碰撞检测）移到 Web Worker 中，避免阻塞主线程。
**示例：**```javascript
// worker.js
self.onmessage = function(e) {
  const result = performHeavyComputation(e.data);
  self.postMessage(result);
};

function performHeavyComputation(data) {
  // 繁重的计算任务
  return data;
}

// main.js
const worker = new Worker('worker.js');
worker.onmessage = function(e) {
  console.log('Worker result:', e.data);
};

worker.postMessage(data);
```
<a name="qBJ3n"></a>
#### 5. 优化数据结构和算法
使用高效的数据结构和算法来处理树节点和拖拽操作，例如使用平衡树或自平衡二叉树来管理节点。
<a name="GV2PF"></a>
#### 6. 预计算和缓存
预先计算和缓存一些结果，避免每次拖拽都重新计算。例如，可以缓存节点的布局信息，拖拽过程中直接使用缓存的数据。
<a name="KBBAW"></a>
#### 7. 简化拖拽区域
在拖拽过程中，仅更新必要的区域，避免整个树的重绘。例如，使用“占位符”节点来简化视觉反馈，而不实际移动大量节点。
<a name="D5QkZ"></a>
#### 8. 分批次渲染
如果节点数量过多，可以将渲染分成多个批次，每次渲染一部分节点，减少一次性渲染的压力。
**示例：**```javascript
function renderNodesInBatches(nodes, batchSize) {
  let index = 0;
  function renderBatch() {
    const batch = nodes.slice(index, index + batchSize);
    // 渲染 batch 中的节点
    index += batchSize;
    if (index < nodes.length) {
      requestAnimationFrame(renderBatch);
    }
  }
  renderBatch();
}

const nodes = generateNodes(10000);
renderNodesInBatches(nodes, 100);
```
通过综合运用这些优化策略，可以显著提高树形结构中大数据量节点拖拽的性能，减少卡顿现象。<br /> 可以展开说下
<a name="z5pGd"></a>
### 如何优化数据结构和算法
优化数据结构和算法是提升大数据量情况下拖拽性能的关键。下面是一些具体的方法和示例，帮助你优化树形结构和拖拽操作：
<a name="CM5f8"></a>
#### 1. 使用高效的数据结构
**平衡二叉树 (Balanced Binary Tree)** 或 **B树 (B-Tree)** 是管理大量节点的理想选择，它们能保证在最坏情况下的操作时间复杂度较低。
平衡二叉树示例```javascript
class TreeNode {
  constructor(value) {
    this.value = value;
    this.left = null;
    this.right = null;
  }
}

class AVLTree {
  constructor() {
    this.root = null;
  }

  // 插入节点
  insert(value) {
    this.root = this._insert(this.root, value);
  }

  _insert(node, value) {
    if (!node) return new TreeNode(value);

    if (value < node.value) {
      node.left = this._insert(node.left, value);
    } else if (value > node.value) {
      node.right = this._insert(node.right, value);
    } else {
      return node; // 重复值不处理
    }

    // 更新高度并平衡树
    node = this._balance(node);

    return node;
  }

  // 平衡节点
  _balance(node) {
    // 实现平衡逻辑，如旋转操作
    return node; // 这里需添加平衡逻辑
  }

  // 查找节点
  find(value) {
    return this._find(this.root, value);
  }

  _find(node, value) {
    if (!node) return null;
    if (value < node.value) return this._find(node.left, value);
    if (value > node.value) return this._find(node.right, value);
    return node;
  }
}
```
<a name="xEWGz"></a>
#### 2. 优化查找和插入操作
**哈希表 (Hash Table)** 或 **字典树 (Trie)** 可以用于快速查找节点，减少时间复杂度。
哈希表示例```javascript
class HashTable {
  constructor() {
    this.table = new Map();
  }

  // 插入节点
  insert(key, value) {
    this.table.set(key, value);
  }

  // 查找节点
  find(key) {
    return this.table.get(key);
  }

  // 删除节点
  remove(key) {
    this.table.delete(key);
  }
}
```
<a name="QQFKa"></a>
#### 3. 减少树的深度
**多叉树 (Multi-way Tree)** 或 **扁平化结构 (Flat Structure)** 可以减少树的深度，提升查找和操作性能。
多叉树示例```javascript
class MultiWayTreeNode {
  constructor(value) {
    this.value = value;
    this.children = [];
  }

  // 添加子节点
  addChild(node) {
    this.children.push(node);
  }

  // 查找子节点
  findChild(value) {
    return this.children.find(child => child.value === value);
  }
}

class MultiWayTree {
  constructor() {
    this.root = new MultiWayTreeNode(null);
  }

  // 插入节点
  insert(path, value) {
    let currentNode = this.root;
    for (let segment of path) {
      let child = currentNode.findChild(segment);
      if (!child) {
        child = new MultiWayTreeNode(segment);
        currentNode.addChild(child);
      }
      currentNode = child;
    }
    currentNode.addChild(new MultiWayTreeNode(value));
  }
}
```
<a name="TAVli"></a>
#### 4. 批量操作
**批量插入 (Batch Insertion)** 和 **批量删除 (Batch Deletion)** 可以减少单次操作的开销，提升性能。
批量插入示例```javascript
class Tree {
  constructor() {
    this.nodes = [];
  }

  // 批量插入节点
  batchInsert(values) {
    for (let value of values) {
      this.nodes.push(value);
    }
    // 假设这里有平衡或排序操作
  }
}

const tree = new Tree();
const values = [1, 2, 3, 4, 5];
tree.batchInsert(values);
```
<a name="SaHl6"></a>
#### 5. 缓存机制
**缓存 (Caching)** 是提高性能的重要手段，特别是在频繁操作的情况下，可以缓存中间结果，避免重复计算。
缓存示例```javascript
class TreeWithCache {
  constructor() {
    this.nodes = [];
    this.cache = new Map();
  }

  // 插入节点
  insert(value) {
    this.nodes.push(value);
    this.cache.clear(); // 插入后清除缓存
  }

  // 查找节点
  find(value) {
    if (this.cache.has(value)) {
      return this.cache.get(value);
    }
    const node = this.nodes.find(node => node === value);
    if (node) {
      this.cache.set(value, node);
    }
    return node;
  }
}

const tree = new TreeWithCache();
tree.insert(1);
tree.insert(2);
console.log(tree.find(1)); // 缓存查找
```
<a name="rHOgr"></a>
#### 6. 优化遍历
在遍历大数据量时，可以采用 **深度优先搜索 (DFS)** 或 **广度优先搜索 (BFS)**，并且避免递归过深导致的栈溢出问题。
<a name="EiKXe"></a>
##### 深度优先搜索示例

```javascript
function dfs(node) {
  const stack = [node];
  while (stack.length > 0) {
    const currentNode = stack.pop();
    console.log(currentNode.value);
    for (let child of currentNode.children) {
      stack.push(child);
    }
  }
}
```
<a name="CHdYd"></a>
##### 广度优先搜索示例

```javascript
function bfs(node) {
  const queue = [node];
  while (queue.length > 0) {
    const currentNode = queue.shift();
    console.log(currentNode.value);
    for (let child of currentNode.children) {
      queue.push(child);
    }
  }
}
```

通过上述方法优化数据结构和算法，可以显著提升大数据量情况下树形结构的拖拽性能，减少卡顿现象。
<a name="UMUes"></a>
### 新组件的开发：
<a name="vQOe8"></a>
#### 标签组（tag-group）
**props**：color、size、effect、type、tagMaxWidth、modelValue(tag列表 | [])、tagProps（label: 'label',）、collapseTagCount、collapseTagTip、closable、creatable<br />**Event：**'remove', 'add',  'focus',  'selected-change'

**主要功能：**<br />1.通过绑定列表数据驱动控制标签渲染<br />2.多个标签可折叠，并且控制其最大展示数量<br />3.通过鼠标框选选中进行批量操作：复制、删除<br />4.键盘功能：复制，删除，切换当前选中，退格选中<br />5.creatable可创建标签；也包括展示的配置功能：颜色、主题、大小等

重难点 （交互细节）

- 组件的焦点状态的捕获：（点击事件的处理）有焦点状态的元素和非焦点元素组合使用，tabIndex转化为可聚焦元素；
- 键盘功能：退格选中和复制（实现自定义复制内容+es6的键盘api不能支持http环境);
- 框选指令和右键菜单指令；
<a name="ATFnN"></a>
#### 固钉组件(Affix)
当页面滚动时，这个 Vue 组件会检测指定元素（或者默认为窗口）的滚动位置。根据设置的偏移量，如果滚动位置达到了固定定位的条件，组件就会将自身固定在页面上方或下方。通过监听滚动事件和窗口大小改变事件，实时更新状态并调整样式，以确保固定定位的效果。<br />props：  offsetTop，offsetBottom，target<br />method： update()<br />核心逻辑： 监听绑定滚动事件和窗口大小改变事件来计算根元素和目标元素的位置关系，并根据情况判断是否需要固定定位来通过js动态操作css属性： position: 'fixed', top/bottom 

该组件实现了一个固定定位的效果。当页面滚动到一定位置时，该组件的内容会固定在页面上方或下方，直到页面滚动到另一个阈值位置。<br />这个组件有一些 props 和一些内部状态：

- **offsetTop**：指定在顶部偏移多少像素时触发固定定位，默认为0。
- **offsetBottom**：指定在底部偏移多少像素时触发固定定位，默认为 **undefined**。
- **target**：指定滚动的目标元素，默认为 **window**。
- **affixStyle**：用于存储固定定位时的样式。
- **isFixed**：表示当前是否处于固定状态。
- **targetElement**：存储目标元素的引用。
- **initialRootStyle**：存储初始的根元素样式。

这个组件主要功能包括：

1. 在 **mounted** 钩子中初始化目标元素，绑定滚动事件和窗口大小改变事件。
2. 在 **update** 方法中计算根元素和目标元素的位置关系，并根据情况判断是否需要固定定位。
3. 根据固定定位的情况更新 **affixStyle**。
4. 通过 **throttle** 函数控制滚动事件的触发频率。

这个组件的实现比较复杂，主要逻辑在 **update** 方法中，它根据页面滚动位置和 props 中的偏移值来判断是否需要固定定位，然后更新样式。

<a name="UhFCz"></a>
### 优化css样式结构
<a name="RAQFu"></a>
#### 样式隔离（组件库和用户、组件之间）；
line-height等继承属性影响：BFC；<br />**避免缩放导致位置差异：**<br />**flex布局**
<a name="V2ynp"></a>
#### 步骤条：
原方案：<br />利用伪元素绘制三角形在浏览器缩放时会造成其位置和大小发生变化  ；两个三角形的堆叠横向位为一差来构成箭头

1. **子像素渲染问题**：
   - 尽管 **px** 是固定单位，但在缩放时，像素值可能会转化为非整数（子像素）。浏览器在渲染子像素时处理方式可能不一致，从而导致位置和大小的偏移。
2. **缩放算法差异**：
   - 不同浏览器或同一浏览器的不同版本在缩放时可能采用不同的算法。这些算法在处理小数像素值时可能有所不同，导致图形在缩放时表现不一致。
3. **抗锯齿处理**：
   - 浏览器在渲染图形时会进行抗锯齿处理，这在缩放时可能会导致边缘模糊或位置略有偏移。不同的缩放级别可能会触发不同的抗锯齿算法，导致图形显示不稳定

优化后：正方形旋转45度+ z-index， 用border绘制箭头，
<a name="AAfZs"></a>
#### table-border：
原方案细节：```css
background-image: 
linear-gradient(-90deg,$--table-border-color,$--table-border-color),
linear-gradient(-180deg,$--table-border-color,$--table-border-color);
background-repeat: no-repeat;
background-size: 0 100%,100% 1px; 
background-position: 100% 0,100% 100%;
```
主要区别有:

1. border-bottom 只会设置元素的下边框。而 background declarations 实现了下边框和右边框的效果。
2. border-bottom 的样式可以直接通过 $--table-border 变量设置。background 需要两个颜色变体来区分边框和背景。
3. border-bottom 不需要考虑背景平铺、大小、位置等设置。
4. border-bottom 会参与元素的盒模型,可能会影响布局。而 background 设置的边框只是视觉效果。
5. border-bottom 很易于理解和设置样式。background declarations 则较为复杂。
6. border-bottom 在低版本浏览器支持会更好。

所以从实现效果来说,background declarations 可以视觉上模拟出 border-bottom 的样式。<br />但两者本质上还是有区别的,需要根据实际需求选择合适的实现。如果仅需下边框,推荐还是使用 border-bottom 的方式。<br />这是使用 CSS 的 linear-gradient 函数来生成两个叠加的线性渐变作为 background-image 的一种写法。  让两个线性渐变背景互相垂直<br />使用向上(-90度)和向左(-180度)两个方向的 $--table-border-color 线性渐变叠加作为背景图片。<br />这可以创建一个类似双条纹的背景效果。<br />其目的是使用渐变来生成条纹背景,这样可以避免使用重复的背景图片资源。<br />-90deg 和 -180deg 的角度是为了让两个渐变方向互相垂直,实现清晰的条纹效果。<br />使用 background-image 创建线性背景来实现 border 时, 在浏览器缩放时可能出现边框消失的问题,主要原因有:

1. background-size 使用了固定单位值

background-size 设置为 0 100% 和 100% 1px,当浏览器缩放时,这两个固定大小的值不会改变,但元素尺寸会缩小,导致边框显示区域不足,显示不全或消失。

2. background-position 使用了 100% 定位

右边和下边的位置是基于 100% 定位,在元素缩小时也不会调整,无法自适应。

3. 浏览器缩放可能导致子像素渲染变化

一些浏览器不支持子像素渲染,缩放导致像素对齐发生变化,从而使边框消失。

4. zoom 缩放和整体布局缩放有细微差异

但 zoom 缩放同时也会影响背景图像的大小和位置。<br />解决方法是: 

1. 使用边框 CSS 属性直接设置边框样式，浏览器上的稳定性更强 —— box-shadow不会参与元素的盒模型, 缩放过程中和其他css结构的缩放比例一致，能够做到自适应；并且改动范围小 
2. background-size 使用百分比或 em 单位
3. background-position 使用具体数值调整位置
4. 考虑不同缩放情况下的容错性
5. 适当补充多余空间避免直接缩放消失
<a name="ttjQr"></a>
#### 分页器，dissociates
在复杂场景下会受到所在父组件的样式影响；（layout和dissociates都能完成左右分离结构，但共同使用时会样式冲突；）<br />通过display构建形成BFC；


<a name="qCeZy"></a>
### 样式隔离

1. **命名约定**：
   - 命名约定是指在编写CSS时，遵循一定的命名规范来确保样式的唯一性。例如，BEM（Block Element Modifier）是一种常见的命名约定，它将样式类名分为块（Block）、元素（Element）和修饰符（Modifier），通过特定的命名规则来定义样式类名，从而确保样式的唯一性。
   - 例如，在BEM中，一个按钮的样式类名可以是.button，它的子元素可以是.button__icon，表示按钮内部的图标，而修改按钮样式的修饰符可以是.button--primary，表示按钮的主要样式。
   - 使用命名约定可以减少样式的冲突，提高代码的可读性和可维护性。
2. **CSS Modules**：
   - CSS Modules是一种在Webpack等打包工具中使用的技术，它通过在构建过程中为每个模块中的类名添加唯一的标识符，从而实现了样式的局部作用域。
   - 样式表文件中的类名被编译成一串独一无二的 hash 值，同时从控制台进行元素审查能够发现 HTML 元素的类名也变成了相应的 hash 值，因此不同组件中使用相同的类名也就不会产生冲突。
   - 在使用CSS Modules时，每个CSS文件被视为一个模块，导出的类名会被重命名，然后在JavaScript文件中引用。这样就避免了全局样式的冲突，只有在当前模块中才能访问到对应的样式。
   - 使用CSS Modules可以有效地实现样式隔离，但需要配合Webpack等构建工具使用。
3. **Scoped CSS**：
   - Scoped CSS是Vue框架提供的一种样式隔离方案，它通过在<style>标签中添加scoped属性，使得样式仅对当前组件有效。
   - 在使用Scoped CSS时，Vue会自动生成一个唯一的属性选择器，将样式应用到当前组件的DOM元素上，从而实现了样式的隔离。
   - Scoped CSS适用于Vue单文件组件中，可以有效地解决组件之间样式的冲突问题。
4. **CSS-in-JS**：
   - CSS-in-JS是一种将CSS写入JavaScript文件中的解决方案，它通过在组件中动态生成样式， 样式直接与组件相关联，使得组件的样式与组件本身紧密结合，从而实现了样式与组件的强耦合，避免了全局污染。
   - 常见的CSS-in-JS库包括Styled-components、Emotion等，它们提供了一种直观的方式来编写样式，并且可以根据组件的状态和属性动态生成样式。
5. **Shadow DOM**：
   - Shadow DOM是Web标准的一部分，它允许将DOM树和样式封装在一个独立的作用域中，从而实现了真正的样式隔离。
   - 在使用Web组件时，可以通过Shadow DOM来隔离组件的样式，防止与外部样式冲突。每个Shadow DOM都有自己的作用域，样式只会应用到当前Shadow DOM内部的DOM元素上。

这些方案各有优劣，可以根据具体项目的需求和技术栈来选择合适的方案。样式隔离是前端开发中非常重要的一环，它可以帮助我们管理复杂的样式结构，提高代码的可维护性和可重用性。
<a name="KP0Sf"></a>
### vue2-vue3升级过程中遇到的问题 如何解决
 三方依赖包的版本不匹配<br /> Vue 3引入了Composition API和其他新的语法，同时移除了一些旧的API。  <br />模板指令与插槽不同

      - 组件上 v-model 用法已更改。
      - <template v-for> 和 非 v-for 节点上 key 用法已更改。
      - 在同一元素上使用的 v-if 和 v-for 优先级已更改。 * v-bind="object" 现在排序敏感。
      - v-for 中的 ref 不再注册 ref 数组 。
      - vue2中使用slot可以**直接使用slot，**vue3中必须使用**v-slot的形式，<template>。**

移除api

      - vue3中移除keyCode作为v-on的修饰符，当然也不支持config.keyCodes；vue3中**移除v-on.native修饰符**；vue3中**移除过滤器filter**。
      - keyCode 支持作为 v-on 的修饰符。
      - $on，$off 和 $once 实例方法。
      - 过滤器 filter 。
      - 内联模板 attribute 。
      - $destroy 实例方法。用户不应再手动管理单个 Vue 组件的生命周期。

 生命周期钩子变化  
<a name="PA7sQ"></a>
### 打包优化
<a name="JUEeG"></a>
#### 代码层面的优化

1. **代码压缩 (Minification)**
- 目的：减少文件大小，提高传输速度。
- 工具：Terser, UglifyJS。
- 示例：
```javascript
// Webpack 配置
optimization: {
  minimize: true,
    minimizer: [new TerserPlugin()],
    }
```

2. **Tree Shaking**：利用Tree Shaking技术去除未使用的代码，通过ES6的模块系统和工具（如Webpack、Rollup等）来实现。
- 目的：移除未使用的代码。
- 工具：Webpack 内置支持，使用 ES6 模块语法。
- 示例：
```javascript
// 确保使用 ES6 模块
import { usedFunction } from './module';

usedFunction();
```

3. **代码拆分（Code Splitting）**：将代码拆分成多个小块，按需加载。通过动态导入（Dynamic Import）或使用Webpack等打包工具的SplitChunksPlugin来实现。
- 目的：减少初始加载时间，按需加载代码。
- 工具：Webpack 的 import() 动态导入功能。
- 示例：
```javascript
// 在需要的地方使用动态导入
import('./module').then(module => {
  // 使用导入的模块
});
```

4. **懒加载（Lazy Loading）**：延迟加载不是首次加载所需的代码，特别是对于大型应用程序中的一些页面或组件。例如，Vue和React都提供了懒加载组件的支持。
- 目的：减少初始页面加载时间，将不立即需要的资源推迟加载。
- 工具：React 的 React.lazy 和 Vue 的 defineAsyncComponent。
- 示例：
```
// React
const LazyComponent = React.lazy(() => import('./LazyComponent'));

// Vue
const LazyComponent = defineAsyncComponent(() => import('./LazyComponent.vue'));
```
<a name="NgQ4a"></a>
#### 资源优化

1. **图片优化 (Image Optimization)**：压缩图片、选择合适的图片格式（如WebP格式）、使用CSS Sprites、将小图标转换成字体图标或SVG等。
- 目的：减少图片大小，加快加载速度。
- 工具：imagemin, image-webpack-loader。
- 示例：
```javascript
// Webpack 配置
module: {
  rules: [
    {
      test: /\.(png|jpe?g|gif)$/i,
      use: [
        {
          loader: 'file-loader',
        },
        {
          loader: 'image-webpack-loader',
          options: {
            mozjpeg: {
              progressive: true,
            },
            optipng: {
              enabled: false,
            },
            pngquant: {
              quality: [0.65, 0.90],
              speed: 4,
            },
          },
        },
      ],
    },
  ],
    }
```

2. **字体优化**：只包含项目中使用的字体字符、选择合适的字体格式（如woff2）和加载方式（如异步加载）。
3. **减少第三方库的体积**：仅导入项目中使用到的功能，或者考虑替代方案以减小第三方库的体积。
<a name="qwiku"></a>
#### 缓存优化

1. **浏览器缓存(Caching)**：利用浏览器缓存机制（如强缓存和协商缓存）来缓存静态资源，减少重复下载。
- 目的：利用浏览器缓存，加快重复访问的加载速度。
- 工具：Webpack 的 [contenthash]。
- 示例：
```javascript
// Webpack 配置
output: {
  filename: '[name].[contenthash].js',
    }
```

2. **CDN 加速**：将静态资源部署到 CDN 上，提高资源加载速度和并发请求的处理能力。
<a name="hpCUf"></a>
#### 构建工具优化

1. **优化 Webpack 配置**：合理配置 Webpack，使用合适的插件和 loader，开启生产模式下的优化特性（如代码压缩、Scope Hoisting等）。
2. **缓存和持久化**：利用构建工具的缓存功能，避免重复编译。例如，Webpack的cache-loader和hard-source-webpack-plugin。
3. **模块分析**：通过工具分析模块的依赖关系和体积，找出体积较大的模块，并采取相应的优化措施。

<a name="d4xrd"></a>
#### HTTP/网络优化

1. **减少请求次数**：合并和打包静态资源，减少HTTP请求次数。
2. **使用 HTTP/2**：HTTP/2 支持多路复用和头部压缩，提高资源加载速度。
3. **预加载和预解析**：使用<link rel="preload">和<link rel="dns-prefetch">等标签，预加载重要资源和预解析域名。
<a name="m86HB"></a>
#### 其他优化策略

1. **减少框架和库的使用**：合理选择框架和库，避免过度依赖，尽量使用轻量级的解决方案。
2. **持续优化和监控**：定期审查和优化代码，监控网站性能指标，及时发现和解决问题。
3. **服务端渲染（SSR）**：使用服务端渲染技术提高首屏加载速度和SEO效果。

综上所述，前端打包优化是一个综合性的工作，需要结合代码、资源、构建工具、网络等多个方面进行优化，以提供更快、更流畅的用户体验。在实际项目中，需要根据具体情况选择合适的优化策略，并持续进行优化和监控。

<a name="s68ut"></a>
### Vite 打包优化
Vite 是一个新兴的构建工具，因其快速的开发和构建速度而备受欢迎。以下是一些优化 Vite 打包的策略：
<a name="lDRDe"></a>
#### 1. **合理配置 Rollup 插件**
Vite 使用 Rollup 进行打包，可以通过配置 Rollup 插件来进行优化。下面是如何配置 Terser 进行代码压缩和 Visualizer 进行包体积分析的具体步骤。
```
javascript
复制代码
// vite.config.js
import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'
import { terser } from 'rollup-plugin-terser'
import visualizer from 'rollup-plugin-visualizer'

export default defineConfig({
  plugins: [
    vue(),
    {
      ...terser(),
      apply: 'build' // 只在构建时应用 Terser 插件
    },
    visualizer({
      open: true // 构建后自动打开包体积分析报告
    })
  ],
  build: {
    rollupOptions: {
      // 可以在这里配置其他 Rollup 选项
    }
  }
})
```
<a name="Z8i7X"></a>
#### 2. **代码分割**
通过手动配置代码分割，确保将第三方库和应用代码分离，减少主包体积，提高加载速度。
```
javascript
复制代码
// vite.config.js
export default {
  build: {
    rollupOptions: {
      output: {
        manualChunks(id) {
          if (id.includes('node_modules')) {
            return id.toString().split('node_modules/')[1].split('/')[0].toString();
          }
        }
      }
    }
  }
}
```
<a name="f4OlZ"></a>
#### 3. **静态资源优化**
通过插件优化图片资源，使用 modern 格式如 WebP，可以进一步减少图片体积。
```
javascript
复制代码
// vite.config.js
import image from '@rollup/plugin-image'

export default {
  plugins: [
    image()
  ]
}
```
<a name="uUYsJ"></a>
#### 4. **依赖预构建**
通过配置 **optimizeDeps** 来指定需要预构建的依赖，减少首次启动时间。
```
javascript
复制代码
// vite.config.js
export default {
  optimizeDeps: {
    include: ['lodash', 'axios'], // 将 lodash 和 axios 预构建
  }
}
```
<a name="RHN4p"></a>
### Webpack 打包优化
<a name="o3Wq2"></a>
#### 1. **开启生产模式**
在生产模式下，Webpack 会自动进行很多优化，比如代码压缩和去除开发工具。
```
// webpack.config.js
module.exports = {
  mode: 'production',
  // 其他配置
}
```
<a name="tiDqR"></a>
#### 2. **代码分割**
Webpack 的代码分割可以显著减少初始加载时间。
```
javascript
复制代码
// webpack.config.js
module.exports = {
  optimization: {
    splitChunks: {
      chunks: 'all', // 对所有的模块进行分割
      cacheGroups: {
        vendors: {
          test: /[\\/]node_modules[\\/]/,
          name: 'vendors',
          chunks: 'all'
        },
        default: {
          minChunks: 2,
          priority: -20,
          reuseExistingChunk: true
        }
      }
    },
  },
};
```
<a name="pYUXr"></a>
#### 3. **Tree Shaking**
确保使用 ES6 模块语法，以便 Webpack 进行 Tree Shaking，移除未使用的代码。
```
javascript
复制代码
// webpack.config.js
module.exports = {
  optimization: {
    usedExports: true,
  },
};
```
<a name="kQDaC"></a>
#### 4. **压缩代码**
使用 TerserPlugin 压缩 JavaScript 代码，使用 css-minimizer-webpack-plugin 压缩 CSS。
```
javascript
复制代码
// webpack.config.js
const TerserPlugin = require('terser-webpack-plugin');
const CssMinimizerPlugin = require('css-minimizer-webpack-plugin');

module.exports = {
  optimization: {
    minimize: true,
    minimizer: [
      new TerserPlugin({
        terserOptions: {
          compress: {
            drop_console: true, // 移除 console 语句
          },
        },
      }),
      new CssMinimizerPlugin(), // 压缩 CSS
    ],
  },
};
```
<a name="AuKCo"></a>
#### 5. **缓存和持久化缓存**
利用缓存可以加速后续的构建速度。
```
javascript
复制代码
// webpack.config.js
module.exports = {
  cache: {
    type: 'filesystem', // 启用文件系统缓存
  },
};
```
<a name="w5V9O"></a>
#### 6. **图片优化**
使用 image-webpack-loader 优化图片资源。
```
javascript
复制代码
// webpack.config.js
const ImageMinimizerPlugin = require('image-minimizer-webpack-plugin');

module.exports = {
  module: {
    rules: [
      {
        test: /\.(jpe?g|png|gif|svg)$/i,
        use: [
          {
            loader: 'file-loader',
          },
          {
            loader: 'image-webpack-loader',
            options: {
              mozjpeg: { progressive: true, quality: 65 },
              optipng: { enabled: false },
              pngquant: { quality: [0.65, 0.90], speed: 4 },
              gifsicle: { interlaced: false },
              webp: { quality: 75 },
            },
          },
        ],
      },
    ],
  },
};
```
[前端性能优化——包体积压缩82%、打包速度提升65%](https://juejin.cn/post/7186315052465520698)<br />[vue2项目dist瘦身——打包体积压缩73%、速度提升90%](https://juejin.cn/post/7218763788605440056)<br />[让你的vue项目体积更小点，打包速度更快点](https://juejin.cn/post/6919638463168020488)<br />[Vue项目优化打包——前端加分项](https://juejin.cn/post/7004045635620405278)<br />![image.png](https://cdn.nlark.com/yuque/0/2024/png/43022426/1713490173505-9613948a-f13e-45e1-af05-8ea2f9b544cd.png#averageHue=%23fefdfc&clientId=ua05b3679-0809-4&from=paste&height=143&id=u5d681836&originHeight=197&originWidth=244&originalType=binary&ratio=1.375&rotation=0&showTitle=false&size=9436&status=done&style=none&taskId=ufd433e24-ec0f-4d02-a0e6-41d9fa6f1ca&title=&width=177.45454545454547)<br />prod环境去掉sourceMap<br />打包去除console.log、注释（可以使用 UglifyJSWebpackPlugin 插件，它可以压缩、混淆代码，包括删除注释。）<br />[sourceMap](https://juejin.cn/post/6969748500938489892?searchId=20240419093253E748662549E1A0581206)

<a name="Jpwg3"></a>
### Vite 构建速度优化
<a name="twDGZ"></a>
#### 1. **懒加载**
通过动态 **import** 实现懒加载，按需加载模块，减少初始加载时间。

```javascript
// Example.vue
<template>
  <div>
  <button @click="loadComponent">Load Component</button>
  <component :is="asyncComponent"></component>
  </div>
  </template>

  <script>
  export default {
    data() {
      return {
        asyncComponent: null,
      };
    },
    methods: {
      async loadComponent() {
        const { default: Component } = await import('./MyComponent.vue');
        this.asyncComponent = Component;
      },
    },
  };
</script>
```
<a name="nKNni"></a>
#### 2. **热更新 (HMR)**
Vite 默认支持热模块替换（HMR），可以大大提升开发效率。确保 Vite 配置开启 HMR。

```javascript
// vite.config.js
export default {
  server: {
    hmr: true, // 确保开启 HMR
  },
};
```
<a name="OJfxi"></a>
#### 3. **优化依赖预构建**
Vite 会自动预构建依赖，可以通过 **optimizeDeps** 手动指定需要预构建的依赖，以加快开发服务器的启动时间。

```javascript
// vite.config.js
export default {
  optimizeDeps: {
    include: ['lodash', 'axios'], // 手动指定预构建的依赖
  },
};
```
<a name="DMqES"></a>
#### 4. **使用 Vite 插件**
一些 Vite 插件可以帮助提高构建速度，比如 Vite 的快速刷新插件。

```javascript
// vite.config.js
import reactRefresh from '@vitejs/plugin-react-refresh'

export default {
  plugins: [reactRefresh()],
};
```
<a name="gi4BK"></a>
### Webpack 构建速度优化
<a name="iqsqi"></a>
#### 1. **懒加载**
通过动态 **import** 实现懒加载，按需加载模块，减少初始加载时间。

```javascript
// Example.vue
<template>
  <div>
  <button @click="loadComponent">Load Component</button>
  <component :is="asyncComponent"></component>
  </div>
  </template>

  <script>
  export default {
    data() {
      return {
        asyncComponent: null,
      };
    },
    methods: {
      async loadComponent() {
        const { default: Component } = await import('./MyComponent.vue');
        this.asyncComponent = Component;
      },
    },
  };
</script>
```
<a name="Sspn0"></a>
#### 2. **热更新 (HMR)**
Webpack 的 **webpack-dev-server** 和 **HotModuleReplacementPlugin** 支持热模块替换。

```javascript
// webpack.config.js
const webpack = require('webpack');

module.exports = {
  // ...
  devServer: {
    hot: true, // 启用 HMR
  },
  plugins: [
    new webpack.HotModuleReplacementPlugin(),
  ],
};
```
<a name="SNsFw"></a>
#### 3. **DLL 插件**
使用 **DllPlugin** 和 **DllReferencePlugin** 将第三方库预编译成单独的文件，以加快构建速度。

```javascript
// webpack.dll.config.js
const path = require('path');
const webpack = require('webpack');

module.exports = {
  entry: {
    vendor: ['react', 'react-dom'], // 需要预编译的第三方库
  },
  output: {
    path: path.resolve(__dirname, 'dll'),
    filename: '[name].dll.js',
    library: '[name]_lib',
  },
  plugins: [
    new webpack.DllPlugin({
      name: '[name]_lib',
      path: path.resolve(__dirname, 'dll', '[name]-manifest.json'),
    }),
  ],
};

// webpack.config.js
const path = require('path');
const webpack = require('webpack');

module.exports = {
  // ...
  plugins: [
    new webpack.DllReferencePlugin({
      context: __dirname,
      manifest: require('./dll/vendor-manifest.json'), // 引用预编译的 DLL
    }),
  ],
};
```
<a name="DTSDi"></a>
#### 4. **持久化缓存**
使用持久化缓存（文件系统缓存）加快后续构建速度。

```javascript
// webpack.config.js
module.exports = {
  cache: {
    type: 'filesystem', // 启用文件系统缓存
  },
};
```
<a name="W92Hb"></a>
#### 5. **多线程/多进程构建**
使用 **thread-loader** 和 **parallel-webpack** 等工具进行多线程/多进程构建，提升构建速度。

```javascript
// webpack.config.js
module.exports = {
  module: {
    rules: [
      {
        test: /\.js$/,
        use: [
          'thread-loader', // 使用多线程加载器
          'babel-loader',
        ],
        exclude: /node_modules/,
      },
    ],
  },
};

// 使用 parallel-webpack
const ParallelUglifyPlugin = require('webpack-parallel-uglify-plugin');

module.exports = {
  plugins: [
    new ParallelUglifyPlugin({
      cacheDir: '.cache/', // 启用缓存
      uglifyJS: {
        output: {
          comments: false,
        },
        compress: {
          warnings: false,
        },
      },
    }),
  ],
};
```
<a name="b1dd5"></a>
#### 6. **优化模块解析**
减少模块解析路径，避免不必要的解析。

```javascript
// webpack.config.js
module.exports = {
  resolve: {
    modules: [path.resolve(__dirname, 'src'), 'node_modules'], // 优化模块查找路径
    extensions: ['.js', '.jsx', '.vue'], // 优化文件扩展名查找
    alias: {
      '@': path.resolve(__dirname, 'src'), // 创建路径别名
    },
  },
};
```
<a name="BiTSK"></a>
### 封装组件

1. **工具类型的组件**，与具体的项目无关，例如轮播图组件，element-ui
2. 项目**业务相关的组件**，与具体的项目紧密相关，可能会在项目中使用多次，或者是公司统一系列的项目中使用，比如图片上传组件，凡是涉及到上传或者修改图片的都可以使用
3. 项目**复杂页面的子组件**，不hi使用多次，比如后管系统中员工管理页面，因为页面信息较多，通过组件拆分，比较好管理维护

[https://juejin.cn/post/6952777507162554382](https://juejin.cn/post/6952777507162554382)
<a name="A8juS"></a>
#### 一、前端组件封装的设计思路

1. **单一职责原则（SRP）**： 每个组件应当只负责一项功能，这样可以确保组件的独立性和可维护性。
2. **可复用性**： 组件设计应当尽量通用，避免与具体业务逻辑耦合，从而能够在不同项目或不同场景下复用。
3. **可组合性**： 组件应当设计得可以被其他组件组合使用，类似于乐高积木，这样可以通过组合简单组件来构建复杂组件。
4. **状态管理**： 组件内部应当有清晰的状态管理，明确哪些状态是内部状态（私有状态），哪些是外部传入的状态（公共状态）。
5. **样式隔离**： 使用模块化的CSS或样式解决方案（如CSS Modules, Styled Components等）来确保组件的样式不与外部产生冲突。
<a name="w3J7U"></a>
#### 二、常见的组件封装手段

1. **函数式组件和类组件**： 在React中，可以使用函数式组件（Function Components）和类组件（Class Components）来封装组件。函数式组件更加简洁，而类组件则提供了更多的生命周期方法。
2. **高阶组件（HOC）**： 高阶组件是一种增强组件功能的设计模式。它是一个函数，接受一个组件并返回一个新的组件。常用于逻辑复用和代码重用。
3. **Render Props**： Render Props是一种在React中共享代码的技术。通过将函数作为props传递给组件，从而可以灵活地控制组件的渲染逻辑。
4. **Hooks**： React Hooks提供了一种在函数组件中使用状态和其他React特性的方式，如useState, useEffect, useContext等。它简化了组件逻辑的组织和重用。
5. **Slot/插槽**： 在Vue中，可以使用插槽来实现组件内容的灵活定制。插槽允许父组件在子组件内部插入内容。
6. **组件库和UI框架**： 使用现有的组件库（如Ant Design, Material-UI, Bootstrap等）可以快速构建UI，并可以根据需要进行二次封装以适应具体业务需求。
<a name="KyMvy"></a>
#### 三、前端组件封装的意义

1. **提高开发效率**： 通过封装常用组件，开发人员可以避免重复造轮子，直接复用已有组件，从而大大提升开发效率。
2. **提升代码可维护性**： 封装良好的组件具有清晰的接口和职责分离，可以减少代码耦合，提高代码的可维护性和可读性。
3. **增强一致性和可测试性**： 组件封装可以确保UI的一致性，并且每个组件可以单独测试，从而提高整体系统的稳定性和可靠性。
4. **代码复用**： 封装组件使得代码可以在不同项目中复用，减少了重复劳动，提升了整体的开发效率。
5. **方便团队协作**： 封装好的组件可以作为团队内的共享资源，所有成员都可以使用和贡献，促进了团队的协作和知识共享。
<a name="LDMwT"></a>
#### 四、总结
前端组件封装是现代前端开发的核心实践，通过遵循单一职责原则、关注复用性和组合性，并运用高阶组件、Hooks、插槽等技术手段，可以构建出高效、稳定、可维护的前端系统。封装组件不仅提升了开发效率和代码质量，还促进了团队协作和知识共享，是每个前端开发者都应当掌握的重要技能。

**模块化：** 将一个大的问题或功能分解为多个小的模块，每个模块可以独立地处理一个特定的任务或逻辑。每个组件都可以看作一个模块，处理特定的功能。<br />**抽象：** 组件应该隐藏内部实现细节，只暴露必要的接口和方法供外部使用。这样可以降低使用者的学习成本，减少出错的可能性。<br />**接口设计：** 定义清晰的接口，包括props（用于传递数据和配置）、事件（用于触发动作）和插槽（用于渲染组件内部的内容）。接口设计应该具有直观性和一致性。<br />**高内聚低耦合：** 组件应该具有高内聚性，即组件内部的功能相关性紧密。同时，组件之间应该保持低耦合，减少彼此的依赖。<br />**复用性：** 设计组件时应考虑到它的可复用性。一个好的组件可以在不同的场景中重复使用，避免了重复编写相同的代码。<br />**封装状态和逻辑：** 组件可以封装一些内部状态和逻辑，以提供特定的功能。这有助于隔离组件内部的细节，使其更易于管理。<br />**文档和示例： **提供清晰的文档和使用示例，使其他开发者能够快速了解如何正确地使用你的组件。文档应该涵盖组件的接口、用法和示例代码。<br />**测试性：** 组件应该易于测试，使你能够更轻松地编写单元测试来验证组件的功能和行为。<br />**维护性：** 组件的封装应该有助于提高代码的可维护性。组件内部的逻辑应该被合理地组织，使其易于理解和修改。<br />总的来说，封装组件的基本思想是通过将功能模块化、隐藏实现细节、提供清晰的接口和设计、增加复用性等方式，创造出一个可复用、易维护、易测试的代码单元，从而提高整体代码质量和开发效率。
<a name="TfCvW"></a>
### 代码重构
<a name="kiryG"></a>
#### 重构的意义

1. **提高代码可读性**：更清晰的代码结构和命名可以让团队成员更容易理解和维护代码。
2. **增强代码可维护性**：简化复杂的逻辑，使得代码更容易修改和扩展。
3. **减少重复代码**：通过抽取公共逻辑，减少冗余，提高代码复用性。
4. **优化性能**：通过优化算法和减少不必要的操作，提高代码执行效率。
5. **提高代码可靠性**：更清晰和结构化的代码更容易测试和调试，减少错误的发生。
<a name="BmsLV"></a>
#### 常见的重构方式和思路

1. **提取函数**：将重复或复杂的代码段提取到独立的函数中，提高代码的模块化程度。
detail```javascript
// Before
function renderUser(user) {
  console.log('Name: ' + user.name);
  console.log('Email: ' + user.email);
}

// After
function printDetail(label, detail) {
  console.log(`${label}: ${detail}`);
}

function renderUser(user) {
  printDetail('Name', user.name);
  printDetail('Email', user.email);
}
```

2. **简化条件语句**：通过早返回和卫语句（guard clause）简化嵌套的条件语句。

```javascript
// Before
function getUserType(user) {
  if (user) {
    if (user.isAdmin) {
      return 'Admin';
    } else {
      return 'User';
    }
  } else {
    return 'Guest';
  }
}

// After
function getUserType(user) {
  if (!user) return 'Guest';
  return user.isAdmin ? 'Admin' : 'User';
}
```

3. **消除魔法数字和字符串**：使用常量代替代码中的魔法数字和字符串。

```javascript
// Before
const TAX_RATE = 0.07;
const BASE_SALARY = 50000;

function calculateTax(salary) {
  return salary * TAX_RATE;
}

// After
const TAX_RATE = 0.07;
const BASE_SALARY = 50000;

function calculateTax(salary) {
  return salary * TAX_RATE;
}
```

4. **使用ES6+特性**：利用ES6及以上版本的语法特性，如解构赋值、箭头函数、模板字符串等，使代码更简洁。

```javascript
// Before
function createUser(name, age) {
  return {
    name: name,
    age: age
  };
}

// After
const createUser = (name, age) => ({ name, age });
```

5. **组件化和模块化**：在现代前端框架（如React、Vue、Angular）中，将大块的代码拆分为更小、更独立的组件或模块。
合理的模块拆分```javascript
// Before
function App() {
  return (
    <div>
    <header>
    <h1>My App</h1>
    </header>
    <main>
    <p>Welcome to my app!</p>
    </main>
    <footer>
    <p>Footer content</p>
    </footer>
    </div>
  );
}

// After
function Header() {
  return (
    <header>
    <h1>My App</h1>
    </header>
  );
}

function Main() {
  return (
    <main>
    <p>Welcome to my app!</p>
    </main>
  );
}

function Footer() {
  return (
    <footer>
    <p>Footer content</p>
    </footer>
  );
}

function App() {
  return (
    <div>
    <Header />
    <Main />
    <Footer />
    </div>
  );
}
```

6. **消除副作用**：确保函数和组件是纯粹的，没有不必要的副作用。保证功能单一

```javascript
// Before
let counter = 0;
function incrementCounter() {
  counter += 1;
}

// After
function incrementCounter(counter) {
  return counter + 1;
}
```
<a name="HCDa1"></a>
#### 重构的步骤

1. **识别需要重构的部分**：通过代码审查、性能分析和用户反馈，找出需要重构的代码区域。
2. **编写测试**：在重构之前编写单元测试和集成测试，以确保重构过程不会引入新错误。
3. **小步重构**：逐步进行重构，每次只修改一小部分代码，确保每步重构后代码仍然正常运行。
4. **运行测试**：在每次重构后运行测试，确保修改没有引入错误。
5. **提交和文档**：将重构的代码提交到版本控制系统，并更新相关文档，记录重构的原因和结果。

通过以上方式和思路，可以有效地进行前端代码重构，提高代码质量，使得项目更加易于维护和扩展。
<a name="vgXM7"></a>
### 工作流引擎
<br />在工作流引擎或工作流设计系统中，前端的主要工作涉及到多个方面，以确保用户可以直观地设计、管理和监控工作流。以下是前端的主要工作内容：

1. **用户界面设计（UI/UX）**：
   - **工作流设计器**：创建一个直观的拖放式界面，允许用户设计和修改工作流。设计器应支持流程图的创建，任务节点的添加和连接等。
   - **表单设计**：用户可以创建和编辑表单，用于捕获和显示任务的输入和输出数据。
   - **仪表板和报告**：展示工作流的运行状态、统计数据和分析结果，包括任务的完成情况、瓶颈分析等。
2. **交互功能**：
   - **拖放操作**：支持拖放操作，使用户能够轻松地将不同的工作流组件（如任务节点、决策节点）添加到设计器中。
   - **节点配置**：提供界面让用户配置每个节点的详细属性，包括任务类型、执行条件、数据输入输出等。
   - **版本控制**：允许用户保存、比较和恢复工作流的不同版本。
3. **实时监控和通知**：
   - **实时监控**：展示工作流的实时运行状态，包括正在进行的任务和完成的任务。
   - **通知系统**：在特定事件发生时（如任务失败、任务完成）发送通知给相关用户。
4. **数据绑定和管理**：
   - **数据输入输出**：提供用户接口来定义和绑定任务节点的数据输入和输出。
   - **数据可视化**：展示任务执行结果的数据，以便用户可以轻松理解和分析。
5. **用户管理和权限控制**：
   - **权限设置**：允许管理员配置用户的权限，包括哪些用户可以创建、修改和查看哪些工作流。
   - **用户角色管理**：支持定义和管理不同用户角色，分配相应的权限和任务。
6. **集成和扩展**：
   - **第三方服务集成**：通过前端配置，支持集成第三方API和服务，使工作流能够与外部系统交互。
   - **插件和扩展**：提供接口让开发者可以创建和集成自定义插件，扩展工作流引擎的功能。
7. **性能优化**：
   - **前端性能优化**：确保界面响应速度快，即使在处理复杂和大型工作流时也能流畅运行。
   - **资源管理**：优化资源的加载和管理，减少不必要的资源消耗，提高用户体验。

前端开发者需要与后端开发者密切合作，以确保前端设计的各项功能能够正确调用后端API，并与后端逻辑保持一致。此外，前端还需注重用户体验（UX），确保界面简洁易用，满足用户的需求。
<a name="djf7Z"></a>
### gulp
Gulp是一个基于node的流程管理工具，可以说是一个自动化构建工具，在前端项目开发中常用来进行编译、压缩（css文件、html文件、图片文件）、合并、重命名、代码检查等等一系列操作，让简单的任务更简单，复杂的任务可管理。
```javascript
  // element ui
 "build:theme":
   "node build/bin/gen-cssfile 
     && gulp build --gulpfile packages/theme-chalk/gulpfile.js 
     && cp-cli packages/theme-chalk/lib lib/theme-chalk",
  "gulp": "^4.0.0",
  "gulp-autoprefixer": "^6.0.0", // 自动补全 CSS 前缀
  "gulp-cssmin": "^0.2.0", // 用于压缩 CSS。
  "gulp-sass": "^4.0.2", // 编译 scss，转成 CSS

  // element plus
  "gulp-autoprefixer": "^8.0.0",
  "gulp-rename": "^2.0.0",
  "gulp-sass": "^5.1.0",
```
![image.png](https://cdn.nlark.com/yuque/0/2024/png/43022426/1713349914568-81b19575-7937-451c-8948-ac11cf61845d.png#averageHue=%23f8f7f6&clientId=u3c2aaff8-c0d9-4&from=paste&height=529&id=uae5cf560&originHeight=727&originWidth=332&originalType=binary&ratio=1.375&rotation=0&showTitle=false&size=28271&status=done&style=none&taskId=u8af517fb-1b40-4682-b2af-ecc76104451&title=&width=241.45454545454547)
<a name="q6QbO"></a>
#### 主题切换：
gen-cssfile.js<br />gen-devcssfile.js<br />一套scss文件通过gulp编译成两套index.css文件，

<a name="lDFhS"></a>
### 安全编码
声明变量<br />闭包<br />代码混淆，删除注释(UglifyJsPlugin)<br />攻击：<br />xss：① v-html；②v-bind + js原生事件<br />crsf：

1. 禁止在LocalStorage存储敏感数据。
2. 访问外部对象时， 需要先判断对象是否为空。
3. 功能失效时， 必须彻底删除对应的功能代码。
4. 禁止直接将不可信的数据插入到web页面中。
5. 禁止直接对不可信的JavaScript对象进行序列化。
6. 禁止直接将不可信的数据组装成JSON对象。
7. 禁止将不可信的数据直接组装到JavaScript数组。
8. 禁止未验证的输入作为重定向的URL。
9. 禁止将未验证的输入作为客户端系统的路径。
10. 禁止使用eval()函数来处理来自外部的不可信数据。

[https://blog.csdn.net/2401_83412172/article/details/137169070](https://blog.csdn.net/2401_83412172/article/details/137169070)<br />[安全编码规范](https://segmentfault.com/a/1190000039413063?sort=votes#item-4)
<a name="kndbV"></a>
### playWright怎么用
Playwright 是一个用于 Web 测试自动化的强大工具，它支持多浏览器（Chromium、Firefox 和 WebKit）测试。下面是一个基本的入门指南，介绍如何安装和使用 Playwright 进行测试。<br />安装 Playwright<br />首先，你需要安装 Node.js 和 npm（或 Yarn）。然后，可以通过 npm 安装 Playwright：
```
bash
复制代码
npm install playwright
```
或者使用 Yarn：
```
bash
复制代码
yarn add playwright
```
编写和运行第一个测试<br />接下来，创建一个简单的测试脚本。比如，在你的项目目录下创建一个 example.spec.js 文件：
```javascript
const { chromium } = require('playwright');

(async () => {
  // 启动浏览器
  const browser = await chromium.launch();
  // 创建一个新的页面
  const page = await browser.newPage();
  // 导航到目标页面
  await page.goto('https://example.com');
  // 获取页面标题
  const title = await page.title();
  console.log(`Title: ${title}`);
  // 截图
  await page.screenshot({ path: `example.png` });
  // 关闭浏览器
  await browser.close();
})();
```
运行测试脚本<br />在命令行中运行你的脚本：
```
bash
复制代码
node example.spec.js
```
这将启动 Chromium 浏览器，打开 https://example.com，获取页面标题并打印出来，然后截取屏幕截图并保存为 example.png。<br />使用 Playwright Test Runner<br />Playwright 提供了一个内置的测试运行器，可以更方便地编写和组织测试。你可以使用它来编写更复杂的测试。<br />首先，安装 Playwright 测试运行器：
```
bash
复制代码
npm install @playwright/test
```
然后，创建一个测试文件，比如 example.test.js：
```javascript
const { test, expect } = require('@playwright/test');

test('basic test', async ({ page }) => {
  // 导航到目标页面
  await page.goto('https://example.com');
  // 获取页面标题并断言
  const title = await page.title();
  expect(title).toBe('Example Domain');
});
```
在你的 package.json 中添加一个脚本来运行测试：
```json
{
  "scripts": {
    "test": "playwright test"
  }
}
```
然后在命令行中运行测试：
```bash
npm test
```
更多功能<br />Playwright 提供了许多强大的功能，以下是一些常见的功能示例：<br />1. 表单交互
```javascript
await page.fill('#username', 'myuser');
await page.fill('#password', 'mypassword');
await page.click('button[type="submit"]');
```
2. 截取元素截图
```javascript
const element = await page.$('selector');
await element.screenshot({ path: 'element.png' });
```
3. 断言
```javascript
const element = await page.$('selector');
const text = await element.textContent();
expect(text).toBe('Expected Text');
```
4. 捕获网络请求
```javascript
page.on('request', request => {
  console.log('Request:', request.url());
});
```
5. 多浏览器测试
```javascript
const { chromium, firefox, webkit } = require('playwright');

for (const browserType of [chromium, firefox, webkit]) {
  const browser = await browserType.launch();
  const page = await browser.newPage();
  await page.goto('https://example.com');
  // ... your tests
  await browser.close();
}
```
**Playwright Documentation**<br />Playwright 的文档非常详细，包含了所有的API和示例。可以访问 Playwright Documentation 获取更多信息。<br />通过这个入门指南，你应该能够安装和使用 Playwright 来进行基础的 Web 测试。Playwright 功能强大，支持许多高级用例，你可以深入研究文档以充分利用其功能。
<a name="p0SW1"></a>
### 脚本
shell<br />（npm删包发包，npm-setting，ssl-strict = false）<br />xml<br />（maven发包，下载，配置构建镜像，依赖分析/检查）
<a name="s4PsE"></a>
### 单点登录
SSO的定义是在多个应用系统中，用户只需要登录一次就可以访问所有相互信任的应用系统<br />SSO 一般都需要一个独立的认证中心（passport），子系统的登录均得通过passport，子系统本身将不参与登录操作<br />当一个系统成功登录以后，passport将会颁发一个令牌给各个子系统，子系统可以拿着令牌会获取各自的受保护资源，为了减少频繁认证，各个子系统在被passport授权以后，会建立一个局部会话，在一定时间内可以无需再次向passport发起认证<br />**同域名下的单点登录**<br />cookie的domain属性设置为当前域的父域，并且父域的cookie会被子域所共享。path属性默认为web应用的上下文路径<br />**不同域名下的单点登录**<br />登录服务作为模块抽离出来，前端可以通过构造npm包的来实现<br />[https://vue3js.cn/interview/JavaScript/single_sign.html#%E4%B8%80%E3%80%81%E6%98%AF%E4%BB%80%E4%B9%88](https://vue3js.cn/interview/JavaScript/single_sign.html#%E4%B8%80%E3%80%81%E6%98%AF%E4%BB%80%E4%B9%88)<br />![image.png](https://cdn.nlark.com/yuque/0/2024/png/43022426/1713487594253-cc196b92-b1f1-4cf1-ae1d-d1112cdd71bd.png#averageHue=%23f6f6f6&clientId=ua05b3679-0809-4&from=paste&id=u3017415c&originHeight=246&originWidth=440&originalType=url&ratio=1.375&rotation=0&showTitle=false&size=24072&status=done&style=none&taskId=u308e8bca-9cab-47e9-90bb-68b2edccefb&title=)<br />上图有四个系统，分别是Application1、Application2、Application3、和SSO，当Application1、Application2、Application3需要登录时，将跳到SSO系统，SSO系统完成登录，其他的应用系统也就随之登录了

[前端登录方案大全...](https://juejin.cn/post/6845166891393089544)
<a name="FAAp9"></a>
### 前、后端实现登录有效期
refresh token
<a name="W8mJ6"></a>
#### 前端localStorage
在每次登录的时候记录登录时间（例如：用本地时间戳或向后端请求获取当前时间），并使用 localStorage 记录于本地。<br />每次打开页面时获取当前时间，记录于本地。并且使用当前时间-登录时记录的时间，若大于有效期则清空控制登录状态的相关数据,，跳转到登录页。

```javascript
//每次登录成功则记录登录时间
 window.localStorage.setItem("loginTime", Date.parse(new Date()));
1
2
//七天登录有效期设置
 let loginTime = window.localStorage.getItem("loginTime");
 let nowTime = Date.parse(new Date());
 let intervalTime = nowTime - loginTime;
//时间戳大小-------十秒：10000；一分钟：60000；七天：604800000
 if (intervalTime >= 604800000) {
  //清空控制登录状态的相关数据，并且跳转页面
   window.localStorage.setItem("loginFlag", "");
   this.$store.state.loginFlag = false;
   this.$router.push("/login");
 }
```
<a name="Z3mJ8"></a>
#### 前端可控制token有效期  / 主动退出

1- 在用户每一次登录时，将用户当前登录时时间保存到store中<br />2- 设定一个固定的存在有效时间，<br />3- 在每一次发请求之前，请求拦截器中检验保存在store中的用户登录时保存的时间+有效时间是否大于当前的时间<br />如果大于了当前的时间，则不做任何操作，说明token 没有过期<br />当小于当前时间时，说明token已经过期，则强制用户退出登录<br />退出登录的操作：清除保存的token，强制用户返回登录页面<br />以下为主动退出的代码段

```javascript
代码书写在request.js文件中

// 定义允许token存在的时间
const TOKEN_LIVE_TIME = 6 * 60 * 60 * 1000 //一天
 
// 请求拦截器
service.interceptors.request.use((config) => {
  if (store.getters.token) {
    // 判断用户当前的token是否过期
    // 如果过期了，不允许再发送请求，如果没有过期，则继续
    // 首先获取当前时间
    const LoginTime = parseInt(localStorage.getItem('LoginDate'))
    if (LoginTime + TOKEN_LIVE_TIME < Date.now()) {
      // 此时超时
      // 执行退出操作
      store.dispatch('user/logout')
      Message.error('用户登录已过期，请重新登录')
      return
    }
    config.headers.Authorization = `Bearer ${store.getters.token}`
  }
  return config
})
```
 <br /> 
<a name="GMhKE"></a>
#### 后端控制token有效期 / 被动退出
在响应拦截器中做判断 当用户登录过期时，后端会返回用户登录过期的状态码，前端只需要用if来检测后端返回的数据，如果返回的数据显示当前token已经过期，那么将不返回数据给用户，而是直接进行退出操作，并且强制返回到login页面

1. 和后端协商设置token有效期，并在用户打开页面时设置发送带token的请求接口用于验证token是否有效，若token过期则返回指定错误码。
2. 前端获取到指定错误码后则跳转到登录页。

<a name="kVEeC"></a>
### 

