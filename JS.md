<a name="e0fb9ab1"></a>
### [https://vue3js.cn/interview/](https://vue3js.cn/interview/)

乱序绝对值之和最小

[https://blog.csdn.net/qq_25753445/article/details/124917801?ops_request_misc=&request_id=&biz_id=102&utm_term=%E4%B9%B1%E5%BA%8F%E6%95%B4%E6%95%B0%E5%BA%8F%E5%88%97%E4%B8%A4%E6%95%B0%E4%B9%8B%E5%92%8C%E7%BB%9D%E5%AF%B9%E5%80%BC%E6%9C%80%E5%B0%8Fjs&utm_medium=distribute.pc_search_result.none-task-blog-2allsobaiduweb~default-0-124917801.142](https://blog.csdn.net/qq_25753445/article/details/124917801?ops_request_misc=&request_id=&biz_id=102&utm_term=%E4%B9%B1%E5%BA%8F%E6%95%B4%E6%95%B0%E5%BA%8F%E5%88%97%E4%B8%A4%E6%95%B0%E4%B9%8B%E5%92%8C%E7%BB%9D%E5%AF%B9%E5%80%BC%E6%9C%80%E5%B0%8Fjs&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-0-124917801.142)v17rank_v33,157v15new_3&spm=1018.2226.3001.4187

分积木[https://www.nowcoder.com/discuss/957454?source_id=profile_create_nctrack&channel=-1](https://www.nowcoder.com/discuss/957454?source_id=profile_create_nctrack&channel=-1)

we are a team

[https://www.nowcoder.com/discuss/934770?type=all&order=recall&pos=&page=1&ncTraceId=&channel=-1&source_id=search_all_nctrack&gio_id=2FD1FCFDF95E5CF9DD2D1FD9E9F1B906-1655541783689](https://www.nowcoder.com/discuss/934770?type=all&order=recall&pos=&page=1&ncTraceId=&channel=-1&source_id=search_all_nctrack&gio_id=2FD1FCFDF95E5CF9DD2D1FD9E9F1B906-1655541783689)

```javascript
class UnionFind {
    constructor(size) {
        this.fa = [];
        this.size = size;
        this.init();
    }
    // 初始化 每个元素的父节点为自身
    init() {
        for(let i = 0; i < this.size; i++) {
            this.fa[i] = i;
        }
    }
    // 递归找到根节点，同时进行路径压缩
    find(x) {
        if(x === this.fa[x]) {
            return x;
        }
        this.fa[x] = this.find(this.fa[x]);
        return this.fa[x];
    }
    // 合并 x, y 直到各自的根节点， 其中一个的指向另一个
    merge(x, y) {
        let fx = this.find(x);
        let fy = this.find(y);
        if(fx !== fy) {
            this.fa[fx] = fy;
        }
    }
    // 获取集合数量
    getCount() {
        let count = 0;
        for(let i = 0; i < this.size; i++) {
            if(this.fa[i] === i) {
                count++;
            }
        }
        return count;
    }
}
```

<a name="215eb3f9"></a>
### java、c++：编译型语言    javascript：解释型语言

-  需要编译器编译成本地可执行程序后才能运行，由开发人员在编写完成后手动实施。用户只使用这些编译好的本地代码 
-  开发语言写好后直接将代码交给用户，用户使用脚本解释器将脚本文件解释执行。对于脚本语言，没有开发人员的编译过程， 
-  对于JavaScript与Java它们还有的不同： 
-  Java语言将源代码编译成字节码，这个同执行阶段是分开的。也就是从源代码到抽象语法树到字节码这段时间的长短是无所谓的； 对于JavaScript，这些都是在网页和JavaScript文件下载后同执行阶段一起在网页的加载和渲染过程中实施的，所以对于它们的处理时间有严格要求。<br />**静态类型VS动态类型** 
-  静态类型，编译的时候就能够知道每个变量的类型，编程的时候也需要给定类型，如C中的整型int，浮点型float等。C、C、Java都属于静态类型语言。 
-  动态类型，运行的时候才知道每个变量的类型，编程的时候无需显示指定类型，如JavaScript中的var、PHP中的$。JavaScript、Ruby、Python都属于动态类型语言。 
-  静态类型还是动态类型对语言的性能有很大影响。 
-  于静态类型，在编译后会大量利用已知类型的优势，如int类型，占用4个字节，编译后的代码就可以用内存地址加偏移量的方法存取变量，而地址加偏移量的算法汇编很容易实现。 
-  而动态类型，会当做字符串通通存下来，之后存取就用字符串匹配。 

<a name="f75c005f"></a>
### JavaScript有哪些数据类型，它们的区别？

<a name="b22b515d"></a>
#### **基本数据类型**
基本数据类型存储在栈中（栈区指内存里的栈内存），占用的内存较小，可以直接操作它们的值，而且是按值传递的，即一个变量的值是直接存储在变量中的，它们的比较也是按值进行的。<br />String<br />Number<br />Boolean<br />undefined<br />Null<br />Symbol （ES6）<br />BigInt （ES10）

<a name="11ffa3f4"></a>
#### **引用数据类型（对象类型Object）**
引用类型的对象存储于堆中，占用的内存较大，不能直接操作它们的值，而是需要通过引用来访问它们的属性和方法，它们的赋值和比较也是按引用进行的，即一个变量的值是一个指向实际对象的引用。<br />数组、函数、日期……不是数据类型，它们都属于对象 Object 。

Object<br />Array<br />Function<br />RegExp<br />Date<br />Math<br />Map<br />Set

<a name="2f94464b"></a>
#### **区别**

> 	两种类型的区别在于存储位置的不同

		基本数据类型直接存储在栈（stack）中的简单数据段，占据空间小、大小固定，属于被频繁使用数据，所以放入栈中存储

		引用数据类型存储在堆（heap）中的对象，占据空间大、大小不固定。如果存储在栈中，将会影响程序运行的性能；引用数据类型在栈中存储了指针，该指针指向堆中该实体的起始地址。当解释器寻找引用值时，会首先检索其在栈中的地址，取得地址后从堆中获得实体


**栈内存的特点：**存取速度快，但是不灵活，同时由于结构简单，在变量使用完成后就可以将其释放，内存回收容易实现**。**

**堆内存的特点：**使用灵活，可以动态增加或删除空间，但是存取比较慢。

栈内存的数据是永久保存的不可修改的。

基本数据：将a重新赋值为1，并不是修改原来的，而是在下面重新存了一次，原来的a还原为1008，但是数据是没清除的，所以有些数据是可以还原的。一般情况下，覆盖了，原来的数据就被删除了。所以栈内存是不可修改的

首先说明：JS的值分为原始值（基本数据类型）和引用值（object，array，function，date，RegExp）

[https://blog.csdn.net/qq_17627195/article/details/110199130](https://blog.csdn.net/qq_17627195/article/details/110199130)

<a name="d726de53"></a>
### typeof的返回值共有七种：

number, boolean, string, undefined, object(对象，数组，null返回object), function,symbol(ES6新增).

<a name="01dd2478"></a>
### 检测数据类型的方式有哪些

<a name="Qt8k0"></a>
##### typeof xxx
<br />	①，检测基本数据类型（除Null外，Null会被检测为object）<br />	②，检测引用数据类型除（除function外，function会被检测为function）会被检测为object<br />	返回结果为字符串类型，且类型第一个字母均为小写
<a name="o9xrl"></a>
##### <br />instanceof & isPrototypeOf()
<br />	只能精准检测引用数据类型<br />	可以正确判断对象的类型，用于检测构造函数的 prototype 属性是否出现在某个实例对象的原型链上，object instanceof constructor，object为实例对象，constructor为构造函数
```javascript
function Car() {}

const auto = new Car();

auto instanceof Car // Car.prototype 是否在 auto 原型链上, true
auto instanceof Object // Object.prototype 是否在 auto 原型链上, true

Car.prototype.isPrototypeOf(auto) // Car.prototype 是否在 auto 原型链上, true
Object.prototype.isPrototypeOf(auto) // Object.prototype 是否在 auto 原型链上, true
```
<a name="WBuii"></a>
##### 	<br />Object.prototype.toString.call()
<br />	适用于所有数据类型<br />	调用该方法，统一返回格式"[object Type]"的字符串

<a name="bjv8S"></a>
##### Constructor
该方式既可以处理 引用数据、又能够处理 基本数据<br />(不同于 instanceof, 不能判断 对象父类)<br />**注意:** null 和 undefined 没有 constructor, 所以它是无法检测 Null undefined
```javascript
(123).constructor === Number // true
(true).constructor === Boolean // true
('bar').constructor === String // true
```
<a name="cICxj"></a>
### 判断是否为数组
```javascript
1.Array.prototype.toString.call(arr)==='[object Array]'；
2.arr.constructor === Array；
3.arr instanceof Array === true；
43.Array.isArray(arr)；
```

<a name="icXez"></a>
### js中0.1+0.2

0.1+0.2 不等于 0.3 ，<br />JS中采用的IEEE 754的**双精度(64位)标准，**JS是不区分整数（int）和浮点数（float）的<br />因为在 0.1+0.2 的计算过程中发生了**两次精度丢失**。<br />0.1 0.2—— 二进制 —— 浮点数（对二进制无限循环的尾数做截断）<br />0.1+0.2—— 二进制浮点数相加 ——小数位相加导致小数位多出了一位，进一位<br />第一次是在 0.1 和 0.2 转成双精度二进制浮点数时，由于二进制浮点数的小数位只能存储52位，导致小数点后第53位的数要进行为1则进1为0则舍去的操作，从而造成一次精度丢失。

第二次在 0.1 和 0.2 转成二进制浮点数后，二进制浮点数相加的过程中，小数位相加导致小数位多出了一位，又要让第53位的数进行为1则进1为0则舍去的操作，又造成一次精度丢失。最终导致 0.1+0.2 不等于0.3


<a name="VX5px"></a>
### object.is(ES6)、==、===
<a name="oAdqY"></a>
#### ==（相等比较）：
①. 如果两个操作数类型相同，执行严格比较。<br />②. 如果两个操作数类型不同，则进行类型转换后再进行比较。规则如下：

如果两者类型不同，则会做类型转换，首先比较是否是null和undefined，如果是，则返回true
```javascript
null == undefind // true
null == null // true
undefind == undefind // true
```
如果不是则会判断两者是否为字符串或者数字，如果是则将字符串转换为数字
```javascript
1 == '1'（后面的1会转换为数字1）
Number('') => 0
```
如果不是字符串或者数字，则会判断是否为boolean，如果是boolean，则将boolean转换为数字判断
```javascript
true == '1' // true
步骤详解
1、Number(true) ==> 1, 此时比较式变为 1 == '1',符合第三条规则，将字符串变为数字
2、Number('1') ===> 1, 此时比较式变为 1 == 1
```
如果是Object，会首先调用对象的valueOf)方法，将对象转化为基本类型，再进行比较。当valueOf(）返回的不是基本类型的时候，才会调用toString(）方法。
```javascript
1. 首先调用数组的valueOf方法 
  [].valueOf() ==> []
2. 调用数组的toString()
  [].toString() ==> ""
3. 此时等式变为 "" == 0，符合第三条
4. Number("") ==> 0, 此时等式变为0==0
```
<a name="qScsW"></a>
#### object.is() & ===
object.is()解决了ES5 NaN不严格等于自身的问题，另外可以区分+0和-0
```javascript
Object.is(NaN, NaN); // true
NaN === NaN;         // false

Object.is(-0, +0); // false 
-0 === +0; // true
```
注：**即使2个对象的属性和值完全相同，它们的值也不同：**
```javascript
const myObject1 = { prop: 'Value' };
const myObject2 = { prop: 'Value' };
console.log(myObject1 === myObject2); // false 
console.log(Object.is(myObject1,myObject2)) // false 
```
<a name="DArLq"></a>
### null和undefined区别
```javascript
1. 相等比较时，二者相等
  null == undefind // true
2. typeof判断时
  console.log(typeof undefined);    // undefined
  console.log(typeof null);         // object
```
<a name="mmsAJ"></a>
### 数组
<a name="l4cHQ"></a>
#### *判断数组的方式有哪些

```javascript
1.xxx instanceof Array
// 返回布尔值

2.Object.prototype.toString.call( )
// 返回“[object Xxx]”的字符串

3.数组.__proto__ === Array.prototype(通过原型链做判断)
// 返回布尔值

4.通过ES6的Array.isArray()做判断
// 返回布尔值

5.通过Array.prototype.isPrototypeOf(数组名）
// 返回布尔值
```

<a name="BPoDJ"></a>
#### *数组去重的方式
<a name="u8OnW"></a>
##### set
```javascript
1.Array.from(new Set(arr);
2.[...new Set(arr)];
```
<a name="Toodj"></a>
##### 遍历
利用创建一个空数组，然后对原数组foreach遍历，使用indexOf判定新数组中是否有该数组元素，若没有，就往新数组中push
```javascript
// 数组去重
function unique(arr) {
    let res = [];
    for (let i = 0; i < arr.length; i++) {
        if (res.indexOf(arr[i]) === -1) {
            res.push(arr[i]);
        }
    }
    return res;
}
console.log(unique([ 2, 3, 3, 4, 5, 5 ])); // [ 2, 3, 4, 5 ]
```
<a name="W24XR"></a>
##### 利用对象属性去重
创建空对象，遍历数组，将数组中的值设为对象的属性，并给该属性赋初始值1，每出现一次，对应的属性值增加1，这样，属性值对应的就是该元素出现的次数了

更多方法：[https://juejin.cn/post/7291595522979397666?searchId=202404091742298F3A365BC0D3FB2CB27F](https://juejin.cn/post/7291595522979397666?searchId=202404091742298F3A365BC0D3FB2CB27F)

<a name="vZz5q"></a>
#### 数组排序

**sort**

**选择排序**

- 先假定数组中的第 0 个就是最小的数字的索引
- 然后遍历数组，只要有一个数字比我小，那么就替换之前记录的索引
- 知道数组遍历结束后，就能找到最小的那个索引，然后让最小的索引换到第 0 个位置
- 再来第二遍遍历，假定第 1 个是最小的数字的索引
- 在遍历一次数组，找到比我小的那个数字索引
- 遍历结束后换个位置
- 以此类推，就能把数组排序好了

```javascript
var arr = [3,1,5,2,4];
console.log('初始数组：',arr);	// 	3,1,5,2,4
for(let i = 0; i< arr.length; i++){
	/*假定第 1 遍数组中的第 0 个是最小数字的索引
	第 2 遍的时候假定第 1 个，即假定第 i 个就行*/
	let minIndex = i;
	/*因为之前已经把最小的放在最前面了，后面的循环
	就不需要判断前面的了，直接从i+1开始*/
	for(let j = i+1; j < arr.length; j++){
		if(arr[j] < arr[minIndex]){
			minIndex = j;
		}
	}
	/*遍历结束后找到最小的索引
	第 1 趟的时候是和第 0 个交换，第 2 趟的时候和
	第 1 个交换，即直接和第 i 个交换就行
	*/
	let tmp = arr[minIndex];
	arr[minIndex] = arr[i];
	arr[i] = tmp;
	console.log('i='+i,arr);
}
console.log('排序结束：',arr);	// 1,2,3,4,5
```

**冒泡排序**

- 先遍历数组，让挨着的两个进行比较，如果前一个比后一个大，那么就把两个换个位置
- 数组遍历一遍以后，那么最后一个数字就是最大的那个了
- 然后进行第二遍的遍历，还是按照之前的规则，第二大的数字就会跑到倒数第二的位置
- 依次类推，最后就会按照顺序把数组排好了

```javascript
var arr = [5,4,3,2,1];
console.log('初始数组：',arr);	// 	5,4,3,2,1
//一次次遍历，有多少个数就遍历多少次
for(var i = 0; i < arr.length; i++){
	//循环两两比较数组中的数字
	for(var j = 0; j < arr.length; j++){
		//if判断，如果数组中的当前一个比后一个大，那么两个交换一下位置
		if(arr[j] > arr[j + 1]){
			var tmp = arr[j];
			arr[j] = arr[j + 1];
			arr[j + 1] = tmp;
			console.log('i='+i,arr);
		}
	}
}
console.log('排序结束：',arr);	// 1,2,3,4,5
```

**插入排序**

- 假设前面 n-1 的元素已经排好序，将第n个元素插入到前面已经排好的序列中。

```javascript
var arr = [5,4,3,2,1];
console.log('初始数组：',arr);	// 	5,4,3,2,1
for(var i = 0; i < arr.length; i++) {	
	for(var n = i; n >= 0; n--) {
		if(arr[n] > arr[n+1]){
			var temp = arr[n];
			arr[n] = arr[n+1];
			arr[n+1] = temp;
			console.log('i='+i,arr);		
		}	
 	}
}
console.log('排序结束：',arr);	// 1,2,3,4,5
```

**快速排序(依托递归函数)**

- 快速排序 ：冒泡排序的改进算法。
- 设定分界值，根据分界值将数组分为左右两部分。其中一部分的所有数据都比另外一部分的所有数据都比另一部分的所有数据小，然后再按此方法对这两部分数据分别进行快速排序，整个排序过程可以递归进行，以此达到整个数据变成有序序列

```javascript
var arr = [3,1,5,2,4];
console.log('初始数组：',arr);	// 	3,1,5,2,4
var sum = 0;
function quickSort (arr) {
    if (arr.length <= 1) {
        return arr;
    }
    var medianIndex = Math.floor(arr.length / 2); // 找分界值索引
    var medianValue = arr.splice(medianIndex, 1); // 把分界值从原数组中取出并删除
    var left = []; 	// 比分界值小的，放左边
    var right = [];	// 比分界值大的，放右边
    for (let i = 0; i < arr.length; i++) {
        if (arr[i] < medianValue) {
            left.push(arr[i])
        } else {
            right.push(arr[i])
        }
        sum++;
    }
    console.log(medianIndex, medianValue, left, right)
    return quickSort(left).concat(medianValue,quickSort(right));	// 最后进行拼接
};
console.log('排序结束：',quickSort(arr));	// 1,2,3,4,5
```

**希尔排序 ：**

- 插入排序的改进算法。
- 把记录按下标的一定增量分组，对每组使用直接插入排序算法排序；随着增量逐渐减少，每组包含的关键词越来越多，当增量减至 1 时，整个数据列恰好被分成一组，算法便终止。

```javascript
var arr = [3,1,5,2,4];
console.log('初始数组：',arr);	// 	3,1,5,2,4
var sum = 0;
// var fraction = Math.floor(arr.length / 2) => 定义间隔区间
// fraction = Math.floor(fraction / 2) => 循环中不断切割区间
for (var fraction = Math.floor(arr.length / 2); fraction > 0; fraction = Math.floor(fraction / 2)) {
	// 以间隔值开始遍历
	for (var i = fraction; i < arr.length; i++) {
		// 如果前面一个大于后面一个
		for (var j = i - fraction; j >= 0 && arr[j] > arr[fraction + j]; j -= fraction) {
			var temp = arr[j];
			arr[j] = arr[fraction + j]; // 后移
			arr[fraction + j] = temp; // 填补
			console.log('i='+i,arr);	
			sum++;
		}
	}
}
console.log('排序结束：',arr);	// 1,2,3,4,5
```

**localeCompare中英合并排序**

<a name="iMjsx"></a>
#### 数组乱序（lc384）
<a name="iwcMa"></a>
##### 1.sort + Math.random
sort 是对数组进行排序，每次从数组里面挑选两个数 进行运算。

如果传入的参数是0，两个数位置不变<br />如果参数小于0，就交换位置<br />如果参数大于0，就不交换位置<br />接下来用刚才的较大数字跟下一个进行比较。这样循环进行排序。<br />我们利用 Math.random-0.5，这个运算的结果要么是大于0,要么是小于0.这样要么交换位置，要么不交换位置。当然大于或者小于0是随即出现的。所以数组就被随即排序了。<br />Math.random()：返回介于 0（包含） ~ 1（不包含） 之间的一个随机数

```javascript
var arr = [4,1,67,12,45,121,3];
arr.sort(() => Math.random() - 0.5);
console.log(arr);
```

随机播放，索引值用index = Math.floor(Math.random() * musics.length);
<a name="g4EBA"></a>
##### 2.洗牌算法
```javascript
function shuffle(a) {
    for (let i = a.length; i; i--) {
        let j = Math.floor(Math.random() * i);
        [a[i - 1], a[j]] = [a[j], a[i - 1]];
    }
    return a;
}
```
<a name="XHR0E"></a>
#### 数组有哪些原生方法？
数组和字符串的转换方法<br />	toString()、toLocalString()、join() 

数组尾部操作的方法<br />	pop() 和 push()，push 方法可以传入多个参数

数组首部操作的方法<br />	shift() 和 unshift()；unshift方法可以传递多个参数，表示在数组开头增加

重排序的方法<br />	reverse() 和 sort()，sort() 方法可以传入一个函数来进行比较，传入前后两个值，如果返回值为正数，则交换两个参数的位置

数组连接的方法<br />	concat() ，返回的是拼接好的数组，不影响原数组

数组截取（浅拷贝）办法<br />	slice(begin【end】)，用于截取数组中的一部分返回，不影响原数组。

数组插入/删除/新增方法<br />	array.splice(start[, deleteCount[, item1[, item2[, ...]]]])，改变原数组

数组归并方法<br />	reduce() 和 reduceRight() 方法<br />数组 扁平化方法：<br /> flat()

<a name="Qf7PO"></a>
#### 数组的遍历方法有哪些

```javascript
1.for...of

不改变原数组

for...of遍历具有Iterator迭代器的对象的属性，返回的是数组的元素、对象的属性值，不能遍历普通的obj对象

2.forEach()

视情况是否改变原数组

没有返回值

3.filter()

不改变原数组

数组方法，不改变原数组，有返回值，返回一个符合筛选规则的新数组

4.every() 和 some()

不改变原数组

数组方法，some()只要有一个是true，便返回true；而every()只要有一个是false，便返回false.

5.map()

不改变原数组

数组方法，不改变原数组，有返回值，生成一个一一对应的新数组

6.find() 和 findIndex()

不改变原数组

数组方法，find()返回的是第一个符合条件的值；findIndex()返回的是第一个返回条件的值的索引值

7.reduce() 和 reduceRight()

不改变原数组

数组方法，reduce()对数组正序操作；reduceRight()对数组逆序操作
```


<a name="C4xc5"></a>
### 数组遍历方法
<a name="v02GE"></a>
#### 总结（是否改变原数组 返回值）
forEach是数组原生方法，所以它无法等待异步操作完成，只会按顺序执行，for of 这些都是在js事件循环机制下工作的，可以正常等待。

| **方法** | **是否改变原数组** | **特点** |
| --- | --- | --- |
| forEach() | 否 | 数组方法，不改变原数组，没有返回值 |
| map() | 否 | 数组方法，不改变原数组，有返回值，可链式调用 |
| filter() | 否 | 数组方法，过滤数组，返回包含符合条件的元素的数组，可链式调用 |
| for...of | 否 | for...of遍历具有Iterator迭代器的对象的属性，返回的是数组的元素、对象的属性值，不能遍历普通的obj对象，将异步循环变成同步循环 |
| every() 和 some() | 否 | 数组方法，some()只要有一个是true，便返回true；而every()只要有一个是false，便返回false. |
| find() 和 findIndex() | 否 | 数组方法，find()返回的是第一个符合条件的值；findIndex()返回的是第一个返回条件的值的索引值 |
| reduce() 和 reduceRight() | 否 | 数组方法，reduce()对数组正序操作；reduceRight()对数组逆序操作 |

<a name="cAPGG"></a>
#### for
这是刚刚入行学习绝对会学习的,就不多介绍了
```javascript
const arr = [1,2,3]
for (let i = 0; i < arr.length; i++) { 
  console.log(arr[i])
}
// 打印结果: 1 2 3
```
以上是入门者经常的写法,不过我建议把长度定义出来
```javascript
const arr = [1,2,3]
const len = arr.length
for (let i = 0; i < len; i++) { 
  console.log(arr[i])
}
// 打印结果: 1 2 3
```
这样可以避免重复去读取数组长度,算是优化的一种方式,数组大的时候会比较明显
<a name="LVYn5"></a>
#### while
如上,也是绝对会学习的,各种语言应该都会有这俩种
```javascript
const arr = [1, 2, 3];
let i = 0;
while (i < arr.length) {
  console.log(arr[i]);
  i += 1;
}
// 打印结果: 1 2 3
```
<a name="GQqR8"></a>
#### for...in...（不适合数组，更适合遍历对象）
for...in...除了遍历对象还能遍历数组<br />注:数组的本质是对象,key默认从0迭代的对象
for...in...用法const arr = [1, 2, 3];<br />const obj = {<br />  key: "value"<br />};<br />// 遍历对象 item的值为对象(键值对)的 key<br />for (const item in obj) {<br />  console.log(item);<br />  console.log(obj[item]);<br />}<br />// 打印结果 key value

// 遍历数组拿到的数组的下标<br />for (const item in arr) {<br />  console.log(item);<br />}<br />//打印结果 0 1 2
<a name="tazE8"></a>
#### for...of...
for...of...遍历数组后拿到的是数组每一项的值, 如果你不会使用index,那么大可代替for<br />**for...of**语句适用于[可迭代对象](https://link.juejin.cn/?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh-CN%2Fdocs%2FWeb%2FJavaScript%2FReference%2FIteration_protocols)（包括 [Array](https://link.juejin.cn/?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh-CN%2Fdocs%2FWeb%2FJavaScript%2FReference%2FGlobal_Objects%2FArray)，[Map](https://link.juejin.cn/?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh-CN%2Fdocs%2FWeb%2FJavaScript%2FReference%2FGlobal_Objects%2FMap)，[Set](https://link.juejin.cn/?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh-CN%2Fdocs%2FWeb%2FJavaScript%2FReference%2FGlobal_Objects%2FSet)，[String](https://link.juejin.cn/?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh-CN%2Fdocs%2FWeb%2FJavaScript%2FReference%2FGlobal_Objects%2FString)，[TypedArray](https://link.juejin.cn/?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh-CN%2Fdocs%2FWeb%2FJavaScript%2FReference%2FGlobal_Objects%2FTypedArray)，[arguments](https://link.juejin.cn/?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh-CN%2Fdocs%2FWeb%2FJavaScript%2FReference%2FFunctions%2Farguments) 对象等等）
```javascript
const arr = [1, 2, 3];
for (const item of arr) {
  console.log(item);
}
//打印结果 1 2 3
```

编码过程中经常使用,非常方便的有以下几种 , 提高编码效率 , 提升逼格 , 以及正常开发者都必须具备的。
<a name="shtfC"></a>
#### forEach
forEach循环一共有内置了3个形参

- item 数组的每一项
- index 数组下标
- arr 数组本身
```javascript
const arr = [1, 2, 3];
arr.forEach((item, index, arr2) => {
  console.log(item);
  console.log(index);
  console.log(arr2);
});
// 打印结果
// 1 0 [1,2,3]
// 2 1 [1,2,3]
// 3 2 [1,2,3]
```
<a name="OPUfO"></a>
#### map
map与forEach循环一致,唯一不同的是map会返回新的数组,你可以进行处理拿到新数组。

- item 数组的每一项
- index 数组下标
- arr 数组本身
```javascript
const arr = [1, 2, 3];
let newArr = arr.map((item,index,arr2) => {
  //...
  return item + 1;
});
console.log(newArr);
// 打印结果 2 3 4
```
当然如果你只是简单处理可以简写
```javascript
const arr = [1, 2, 3];
let newArr = arr.map(item => item + 1);
console.log(newArr);
// 打印结果 2 3 4
```
<a name="i4Tqh"></a>
#### some
some循环, 有一个以上的元素满足条件就返回 true，否则返回 false

- item 数组的每一项
- index 数组下标
- arr 数组本身
```javascript
const arr = [1, 2, 3];
let boolean = arr.some(item => {
  // return item == 1;
  // return item == 2;
  return item == 3;
});
console.log(boolean);
// 打印结果 true
```
```javascript
const arr = [1, 2, 3];
let boolean = arr.some(item => {
  return item == 4;
});
console.log(boolean);
// 打印结果 false
```
如果是对象数组可以使用 , 如果是元素数组我建议使用arr.includes(value),它会比较arr内是否存在value,返回true或false
<a name="KbtiZ"></a>
#### every
every循环, 可以和上一个一起记 ,所有元素满足条件就返回 true，否则返回 false

- item 数组的每一项
- index 数组下标
- arr 数组本身
```javascript
const arr = [1, 2, 3];
let boolean = arr.every(item => {
  return item <= 3;
});
console.log(boolean);
// 打印结果 true
```
```javascript
const arr = [1, 2, 3];
let boolean = arr.every(item => {
  return item < 3;
});
console.log(boolean);
// 打印结果 false
```
<a name="EZ05O"></a>
#### filter
filter循环,将符合条件的循环项组成新数组返回。

- item 数组的每一项
- index 数组下标
- arr 数组本身
```javascript
const arr = [1, 2, 3];
let newArr = arr.filter(item => {
  return item < 3;
});
console.log(newArr);
//打印结果 [1,2]
```
<a name="GjBwo"></a>
#### find
find循环, 找到符合条件的第一项，没找到返回 undefined

- item 数组的每一项
- index 数组下标
- arr 数组本身
```javascript
const arr = [1, 2, 3];
let value = arr.find(item => {
  return item < 3;
});
console.log(value);
//打印结果 1
```
```javascript
const arr = [1, 2, 3];
let value = arr.find(item => {
  return item > 3;
});
console.log(value);
//打印结果 undefined
```
<a name="P5TVw"></a>
#### fiendIndex
fiendIndex循环,看名字就知道和上面的区别了, 找到符合条件的第一项下标，没找到返回 -1

- item 数组的每一项
- index 数组下标
- arr 数组本身
```javascript
const arr = [1, 2, 3];
let value = arr.fiendIndex(item => {
  return item < 3;
});
console.log(value);
//打印结果 0
```
```javascript
const arr = [1, 2, 3];
let value = arr.fiendIndex(item => {
  return item > 3;
});
console.log(value);
//打印结果 -1
```
<a name="GWoce"></a>
#### reduce
reduce循环,一般用于累加,可以传入初始值,不传为0

- init 初始值
- item 数组的每一项
- index 数组下标
- arr 数组本身
```javascript
const arr = [1, 2, 3];
// 没指定初始值的情况下
let value = arr.reduce((init, item) => {
  return init + item; 
});
console.log(value);
//打印结果 6

// 给了初始值之后
let value2 = arr.reduce((init, item) => {
  return init + item;
}, 10);
console.log(value2);
//打印结果 16
```
<a name="PNEJn"></a>
#### reduceRight
reduceRight循环,和 reduce一样,不过它是从数组末尾开始,就不做示例了，看上文。

<a name="6ec5f85271cfda703fba1bc4255ea8b2"></a>
### 数组有哪些原生方法？
<a name="hSist"></a>
#### 改变原数组的数组方法
 

| 方法 | 用途 |
| --- | --- |
| pop() | 删除数组最后一个元素，并返回被删除的元素 |
| shift() | 删除数组首个元素，并返回被删除的元素 |
| push() | 数组末尾添加元素，并返回修改后的数组长度 |
| unshift() | 数组头部添加元素，并返回修改后的数组长度 |
| reverse() | 反转数组，并返回反转后数组 |
| sort() | 数组排序方法 |
| splice() | 插入或删除元素， 并返回删除的数据所组成的数组 |

<a name="Wdgg9"></a>
#### 常用方法

- 数组和字符串的转换方法：toString()、toLocalString()、join() 其中 join() 方法可以指定转换为字符串时的分隔符。
- 数组尾部操作的方法 pop() 和 push()，push 方法可以传入多个参数。
- 数组首部操作的方法 shift() 和 unshift() 
- 重排序的方法 reverse() 和 sort()，sort() 方法可以传入一个函数来进行比较，传入前后两个值，如果返回值为正数，则交换两个参数的位置。
- 数组连接的方法 concat() ，返回的是拼接好的数组，不影响原数组。
- 数组截取办法 slice()，用于截取数组中的一部分返回，不影响原数组。
- 数组插入方法 splice()，影响原数组
- 查找特定项的索引的方法，indexOf() 和 lastIndexOf() 
- 迭代方法 every()、some()、filter()、map() 和 forEach() 方法
- 数组归并方法 reduce() 和 reduceRight() 方法
- 数组 扁平化方法： flat()

<a name="PxzeU"></a>
### MAP
Map通过value获取key
```javascript
const valueToFind = 1;
// ①
let res;
map.forEach((i, k) => {
    if(i === valueToFind) {
      res = k;
    }
});

// ②
const keys = [...myMap.entries()]
  .filter(([key, value]) => value === valueToFind)
  .map(([key]) => key);
```

<a name="qpFRW"></a>
### 深浅拷贝
<a name="DN7eZ"></a>
#### 浅拷贝方法
常见的方法比较多：Object.create(x)、Object.assign({}, x)、concat、slice、数组解构、 arr.toReversed().reverse()。
<a name="ZFeG5"></a>
##### 1. Object.create(x)
```javascript
let a = { name: '小明' }
let b = Object.create(a)
```
Object.create() 是对象身上自带的方法。可以创建一个空对象b，且b对象能隐式的继承到a对象的属性。
<a name="hdbsi"></a>
##### 2. Object.assign({}, x)
```javascript
let a = { name: '小明' }
let b = Object.assign({}, a)
```
Object.assign() 是对象身上自带的方法。对象b将对象a的属性复制下来。
<a name="E9Hew"></a>
##### 3. concat
```javascript
let arr = [1,2,3,{a: 10}]
let newArr = [].concat(arr)
```
该方法是数组身上的一个方法，可以合并新老数组。
<a name="rWJOi"></a>
##### 4. slice
```javascript
let arr = [1,2,3,{a: 10}]
let newArr = arr.slice(0)
```
该方法是数组身上的一个方法，可以切割老数组达到浅拷贝的效果。
<a name="I5Fim"></a>
##### 5. 数组解构（扩展运算符）
```javascript
let arr = [1,2,3,{a: 10}]
let newArr = [...arr]
```
<a name="DPlaL"></a>
##### 6. arr.toReversed().reverse()
```javascript
let arr = [1,2,3,{a: 10}]
let newArr = arr.toReversed().reverse()
```
<a name="SgV4t"></a>
##### 手写浅拷贝
代码：
```javascript
function shalldowCopy(obj) {
  if (typeof obj !== 'object' || obj === null) return //只拷贝引用类型
  let objCopy = obj instanceof Array ? [] : {}
  for (let key in obj) {
    if(obj.hasOwnProperty(key)) {
      objCopy[key] = obj[key]
    }
  }
  return objCopy
}
```
浅拷贝的核心是**只要复制了对象的一层，而不是递归地复制所有嵌套的子对象**。所以只要把原对象(原数组)的引用地址赋给新对象。拷贝前判断原数据的类型，如果不是引用类型直接返回。再通过三元运算符初始化新对象的类型。最后通过for...in来遍历对象，但是该方法可能会**遍历原对象原型链上的属性**，所以拷贝前用JS自带的hasOwnProperty方法判断一下。


<a name="QjOfn"></a>
#### 深拷贝方法
<a name="WhUap"></a>
##### 1.JSON.parse(JSON.stringify( ))
**1. 无法拷贝某些数据类型**<br />该方法无法拷贝**函数、正则表达式、日期对象、Map、Set等特殊对象，undefined、Symbol类型也不行。**<br />**2. 无法拷贝对象中的循环引用**
<a name="ZXd7G"></a>
##### 2.Lodash提供的_.cloneDeep

<a name="y9QU3"></a>
### Map 和 Object 的性能
频繁切换选中（*批量选中/反选）Map的性能更好

相关优化：选择器内部数据结构优化  object/Array -> Map (delete和set速度更快)；

**共同点**<br />存储键值对信息

**区别**

|  | **Object** | **Map** |
| --- | --- | --- |
| 创建方式 | 字面量和构造函数（new Object() ）、Object.create() | 构造函数（new Map() ） |
| 键(key)的形式 | 字符串/ symbol | 任何类型的值 |
| key的顺序 | 与插入顺序无关 | 会保持数据的插入顺序 |
| 迭代属性 | /  | map.keys(),map.values() ,map.entries() |


<a name="408657c1"></a>
### *ES6有哪些新增？

新增了变量的声明方式、解构赋值、模板字符串、简化对象写法、箭头函数、函数形参默认值、rest参数、拓展运算符、新增数据类型（Set、Map、Symbol、BigInt）、promise、async/await<br />1.新增了块级作用域（let，const）

2.提供了定义类的语法糖（class）

3.新增了一种基本数据类型（Symbol）

4.新增了变量的解构赋值

5.函数参数允许设置默认值，引入了rest参数，新增了箭头函数。

6.数组新增了一些API，如isArray / from / of 方法；数组实例新增了 entries()，keys() 和 values() 等方法。

7.对象和数组新增了扩展运算符

8.ES6新增了模块化（import / export）

9.ES6新增了Set和Map数据结构。

10.ES6原生提供Proxy构造函数，用来生成Proxy实例

11.ES6新增了生成器（Generator）和遍历器（Iterator）

[https://blog.csdn.net/weixin_47592687/article/details/109601845](https://blog.csdn.net/weixin_47592687/article/details/109601845)

<a name="b4154cc2"></a>
#### 扩展运算符

<a name="67dae8e2"></a>
#### 解构赋值
**一、数组的解构赋值**<br />1.同时赋值多个变量<br />2.解构嵌套数组<br />3.相同“模式”的不完全解构<br />4.解构的默认值

**二、对象的解构赋值**<br />1.根据属性解构对象

**三、函数参数的解构赋值**

1.解构对象类型参数<br />2.解构数组类型参数<br />3.为参数设定默认值

<a name="5e27ae9b"></a>
#### *let、const、var的区别

```javascript
区别主要体现在七个方面

1.是否有块级作用域

块作用域由 { }包括，let和const具有块级作用域，var不存在块级作用域。块级作用域解决了ES5中的两个问题：

内层变量可能覆盖外层变量

用来计数的循环变量泄露为全局变量

2.是否存在变量提升

var存在变量提升

let、const不存在变量提升，即变量只能在声明之后使用，否在会报错

3.是否添加全局属性

浏览器的全局对象是window，Node的全局对象是global。var声明的变量为全局变量，并且会将该变量添加为全局对象的属性，但是let和const不会。

4.能否重复声明变量

var可以重复声明变量，后声明的同名变量会覆盖之前声明的变量

const和let不允许重复声明变量

5.是否存在暂时性死区

在使用let、const命令声明变量之前，该变量都是不可用的。这在语法上，称为暂时性死区 let a = a/const a = a（会报错）

使用var声明的变量不存在暂时性死区：var a = a（不会报错）

6.是否必须设置初始值

var和let不需要赋初始值，只声明就可以

const声明时必须赋初始值，否则会报错

7.能否改变指针指向（重复赋值）

let创建的变量是可以更改指针指向（可以重新赋值）

const声明的变量是不允许改变指针的指向
```

<a name="1786cbd8"></a>
#### let 和 const 的区别

**1.重新赋值**<br />let创建的变量是可以更改指针指向（可以重新赋值）<br />const声明的变量是不允许改变指针的指向

**2.初始值**<br />let不需要赋初始值，只声明就可以<br />const声明时必须赋初始值，否则会报错

<a name="e2f0200a"></a>
#### *const对象的属性可以修改吗
const保证的并不是变量的值不能改动，而是变量指向的那个内存地址不能改动。对于基本类型的数据（数值、字符串、布尔值），其值就保存在变量指向的那个内存地址，因此等同于常量；但对于引用类型的数据（主要是对象和数组）来说，变量指向数据的内存地址，保存的只是一个指针，const只能保证这个指针是固定不变的，至于它指向的数据结构是不是可变的，就完全不能控制了。

<a name="c74c8853"></a>
#### *箭头函数与普通函数的区别

箭头函数比普通函数更加简洁<br />	如果只有一个参数，可以省去参数的括号<br />	如果函数体的返回值只有一句，可以省略大括号，且必须省略return

箭头函数没有自己的this<br />	箭头函数不会创建自己的this， 所以它没有自己的this，它只会在自己作用域的上一层继承this。所以箭头函数中this的指向在它在定义时已经确定了，之后不会改变。

call()、apply()、bind()等方法不能改变箭头函数中this的指向

	箭头函数的this指向要么是window，要么是他的外层<br />箭头函数不能作为构造函数使用

	箭头函数是ES6中的提出来的，它没有prototype，也没有自己的this指向，更不可以使用arguments参数，所以不能New一个箭头函数；new操作符的实现步骤如下：<br />		1. 创建一个对象<br />		2. 将构造函数的作用域赋给新对象（也就是将对象的__proto__属性指向构造函数的prototype属性）<br />		3. 指向构造函数中的代码，构造函数中的this指向该对象（也就是为这个对象添加属性和方法）<br />		4. 返回新的对象                                                                                               <br />所以，上面的第二、三步，箭头函数都是没有办法执行的。<br />箭头函数没有自己的arguments<br />	箭头函数没有自己的arguments对象。在箭头函数中访问arguments实际上获得的是它外层函数的arguments值。<br />箭头函数没有prototype<br />箭头函数不能用作Generator函数，不能使用yield关键字

<a name="cf9e18ed"></a>
#### *箭头函数的this指向哪⾥？

```javascript
箭头函数不同于传统JavaScript中的函数，箭头函数并没有属于⾃⼰的this，它所谓的this是捕获其所在上下⽂的 this 值，作为⾃⼰的 this 值，并且由于没有属于⾃⼰的this，所以是不会被new调⽤的，这个所谓的this也不会被改变。箭头函数的this指向外层函数的this
```

<a name="3c3c98ca"></a>
#### *对Promise的理解

Promise本身是同步的立即执行函数，当在executor中执行resolve（）或者reject（）的时候, 此时是异步操作，也就是说promise中函数体内部的非异步操作正常顺序执行，resolve（）和reject（）异步操作为promise实例对象的返回结果，这个返回结果后面的then或者catch需要用，所以then和catch要放到异步任务中等待所有同步任务执行完毕之后再按顺序（或者如果有定时器，需要遵循定时器的时间）执行。

Promise是异步编程的一种解决方案，它是一个对象，可以获取异步操作的消息，他的出现大大改善了异步编程的困境，避免了地狱回调，它比传统的解决方案回调函数和事件更合理和更强大。所谓Promise，简单说就是一个容器，里面保存着某个未来才会结束的事件（通常是一个异步操作）的结果。从语法上说，Promise 是一个对象，从它可以获取异步操作的消息。Promise 提供统一的 API，各种异步操作都可以用同样的方法进行处理

Promise的实例有三个状态<br />	Pending（进行中）<br />	Resolved（已完成）<br />	Rejected（已拒绝）

Promise的实例有两个过程<br />	pending -> fulfilled : Resolved（已完成）<br />	pending -> rejected：Rejected（已拒绝）

Promise的特点<br />	对象的状态不受外界影响。promise对象代表一个异步操作，有三种状态，pending（进行中）、fulfilled（已成功）、rejected（已失败）。只有异步操作的结果，可以决定当前是哪一种状态，任何其他操作都无法改变这个状态，这也是promise这个名字的由来——“承诺”<br />	一旦状态改变就不会再变，任何时候都可以得到这个结果。promise对象的状态改变，只有两种可能：从pending变为fulfilled，从pending变为rejected。这时就称为resolved（已定型）。如果改变已经发生了，你再对promise对象添加回调函数，也会立即得到这个结果。这与事件（event）完全不同，事件的特点是：如果你错过了它，再去监听是得不到结果的

Promise的缺点

	无法取消Promise，一旦新建它就会立即执行，无法中途取消<br />	如果不设置回调函数，Promise内部抛出的错误，不会反应到外部<br />	当处于pending状态时，无法得知目前进展到哪一个阶段（刚刚开始还是即将完成）

总结<br />	Promise 对象是异步编程的一种解决方案，最早由社区提出。Promise 是一个构造函数，接收一个函数作为参数，返回一个 Promise 实例。一个 Promise 实例有三种状态，分别是pending、resolved 和 rejected，分别代表了进行中、已成功和已失败。实例的状态只能由 pending 转变 resolved 或者rejected 状态，并且状态一经改变，就凝固了，无法再被改变了。状态的改变是通过 resolve() 和 reject() 函数来实现的，可以在异步操作结束后调用这两个函数改变 Promise 实例的状态，它的原型上定义了一个 then 方法，使用这个 then 方法可以为两个状态的改变注册回调函数。这个回调函数属于微任务，会在本轮事件循环的末尾执行

<a name="39af91cf"></a>
#### *对async/await 的理解
async/await其实是Generator 的语法糖，它能实现的效果都能用then链来实现，它是为优化then链而开发出来的。从字面上来看，async是“异步”的简写，await则为等待，所以很好理解async 用于申明一个 function 是异步的，而 await 用于等待一个异步方法执行完成。

async函数返回的是一个Promise 对象，如果在函数中 return 一个直接量，async 会把这个直接量通过 Promise.resolve() 封装成 Promise 对象，async 函数返回的是一个 Promise 对象，所以在最外层不能用 await 获取其返回值的情况下，当然应该用原来的方式：then() 链来处理这个 Promise 对象<br />	async函数返回的是一个promise对象<br />	可以用then（）方法或者catch（）方法来处理async函数（promise对象）

对promise/then、async/await 的理解<br />	async函数实际上就是promise对象，promise是同步的立即执行函数，所以aysnc函数也是立即执行函数，也就是说含有async或者promise（下面还有普通函数，或者console.log（...))会按照代码的顺序进行执行（若async函数中有await需要重新考虑执行顺序，具体看下面的tip）<br />	promise（async函数）异步任务只针对promise（async函数）中调用的then（）方法或者catch（）方法等里面的函数执行，promise（async函数）中的同步任务正常执行，不会阻塞，此时then或者catch方法里面的代码会放到异步任务队列中，待页面所有同步任务完成后再按照顺序（或时间顺序）执行<br />	没有await的async函数也是立即执行函数，会正常执行async函数里面的代码

	tip：有await的async函数，会暂时阻碍await下面所有代码的执行，在async函数中并且在await前面的代码（以及await紧跟着的那个异步函数也会正常运行）会正常运行，待await等待到他后面异步函数的结果之后，再执行await下面的代码。注意：await在没有等待到它后面的异步函数的结果时只是阻碍async函数中且在await下面的代码的执行，async函数中且在await前面、await后面紧跟着的那个异步任务的代码，以及async函数之后的代码不会受到影响，会正常运行

<a name="4bdc543b"></a>
### 函数的声明与函数[表达式](https://so.csdn.net/so/search?q=%E8%A1%A8%E8%BE%BE%E5%BC%8F&spm=1001.2101.3001.7020)区别

**函数表达式和函数声明的区别在于，函数表达式在使用前必须先赋值。**

关于函数声明，它最重要的一个特征就是函数声明提升，意思是执行代码之前先读取函数声明。不管函数声明写在前面，还是后面，都会出现**函数声明的提升**。

函数表达式中，创建的函数叫做匿名函数，因为function关键字后面没有标识符。

先说两者的显著区别:

- 第一种声明方式也就是var声明方式, 函数只有在var语句声明之后才能被调用，函数表达式是在函数运行阶段才赋值给变量h
- 第二种声明方式也就是function声明方式, 函数可以在function声明之前被调用，代码解析阶段已经赋值给标识符h

```javascript
// 函数表达式(function expression) 
var h = function() {
  // h
}
// 函数声明(function declaration) 
function h() {
  // h
}
```

<a name="d423df61"></a>
### *new操作符的实现原理

```javascript
new操作符的执行过程：

（1）首先创建了一个新的空对象(创建一个新的内存空间）

                （2）设置原型，将对象的原型设置为函数的 prototype 对象。

（3）让函数的 this 指向这个对象，执行构造函数的代码（为这个新对象添加属性）

（4）返回新对象（所以构造函数不需要return）
```

<a name="d770692e"></a>
### *如何实现深拷贝？

```javascript
JSON.stringify()



● JSON.parse(JSON.stringify(obj))是目前比较常用的深拷贝方法之一，它的原理就是利用JSON.stringify 将js对象序列化（JSON字符串），再使用JSON.parse来反序列化(还原)js对象。

● 这个方法可以简单粗暴的实现深拷贝，但是还存在问题，拷贝的对象中如果有函数，undefined，symbol，当使用过JSON.stringify()进行处理之后，都会消失。

函数库lodash的_.cloneDeep方法



手写实现深拷贝函数
```

<a name="1d0084dc"></a>
### *对原型、原型链的理解

在JavaScript中是使用构造函数来初始化一个对象的，每一个构造函数的内部都有一个 prototype（原型对象） 属性，它的属性值是一个对象，这个对象包含了可以由该构造函数的所有实例共享的属性和方法。当使用构造函数新建一个对象后，在这个对象的内部将包含一个指针，这个指针指向构造函数的 prototype 属性对应的值，在 ES5 中这个指针被称为对象的原型。一般来说不应该能够获取到这个值的，但是现在浏览器中都实现了 __proto__ 属性来访问这个属性（prototype原型对象），但是最好不要使用这个属性，因为它不是规范中规定的。ES5 中新增了一个 Object.getPrototypeOf() 方法，可以通过这个方法来获取对象的原型。当访问一个对象的属性时，如果这个对象内部不存在这个属性，那么它就会去它的原型对象里找这个属性，这个原型对象又会有自己的原型，于是就这样一直找下去，也就是原型链的概念。原型链的尽头一般来说都是 Object.prototype（除null外）

<a name="0121a713"></a>
### *Event Loop（JS执行机制）

JS执行机制--Event Loop

JS是单线程，也就是说，同一时间只能做一件事。

-  先执行执行栈中的同步代码，宏任务； 
-  异步任务（回调函数）放入任务队列中； 
-  一旦执行栈中的所有同步任务执行完毕，(执行栈为空）系统会按次序取任务队列中的异步任务，于是被读取的异步任务结束等待状态，进入执行栈，开始执行。 
-  当执行完所有微任务后，如有必要会渲染页面 
-  执行任务队列中所有宏任务<br />**异步任务有三种类型：** 
```javascript
普通事件，如click、resize等

资源加载，如load、error等

定时器，包括setTimeout、setInterval等。
```
<br />JS是单线程，也就是说，同一时间只能做一件事。 
```javascript
同步（按顺序来）

同步任务：同步任务都在主流程上执行，形成一个执行栈。（宏任务）

异步（同时进行）
```
 

当执行完所有同步代码后，执行栈为空，查询是否有异步代码需要执行

```javascript
异步任务：JS的异步是通过回调函数实现的。异步任务相关回调函数添加到任务队列中（任务队列也称消息队列）。一般而言，异步任务有三种类型：

普通事件，如click、resize等

资源加载，如load、error等

定时器，包括setTimeout、setInterval等。

JS执行机制--Event Loop

先执行执行栈中的同步任务；

异步任务（回调函数）放入任务队列中；

一旦执行栈中的所有同步任务执行完毕，系统会按次序取任务队列中的异步任务，于是被读取的异步任务结束等待状态，进入执行栈，开始执行。
```

<a name="6f517a36"></a>
### *什么是回调函数？回调函数有什么缺点？如何解决回调地狱问题？

```javascript
回调函数概念

回调函数是一个作为变量传递给另一个函数的函数，它在主体函数执行完之后再执行

回调函数特点

你定义的

你没有调用

但是最终执行了

缺点

回调函数有一个致命的弱点，就是容易写出回调地狱（Callback hell）

嵌套函数存在耦合性，一旦有所改动，就会牵一发而动全身

嵌套函数一多，就很难处理错误

不能使用 try catch 捕获错误

不能直接 return

常见的回调函数

DOM事件回调函数

定时器回调函数

ajax请求回调函数

生命周期回调函数

如何解决回调函数

promise

async/await

  generator
```

<a name="abe1d678"></a>
### *对闭包的理解

**定义**：闭包让你可以在一个内层函数中访问到其外层函数的作用域，

创建闭包的最常见的方式就是在一个函数内创建另一个函数，创建的函数可以访问到当前函数的局部变量。

比如，函数 A 内部有一个函数 B，函数 B 可以访问到函数 A 中的变量，那么函数 B 就是闭包。

（必须要先调用A，B才可以访问到A里面的变量）

**作用**：

- **创建私有变量**
- **延长变量的生命周期，被闭包引用的变量，不会被销毁**<br />使函数外部能够调用函数内部定义的变量（可以使用这种方法来创建私有变量）

闭包的另一个用途是使已经运行结束的函数上下文中的变量对象继续留在内存中，因为闭包函数保留了这个变量对象的引用，所以这个变量对象不会被回收。

- 闭包就是能够读取其他函数内部变量的函数
- 闭包基本上就是一个函数内部返回一个函数
- 好处 
   - 可以读取函数内部的变量
   - 将变量始终保持在内存中
   - 可以封装对象的私有属性和私有方法
- 坏处 
   - 比较耗费内存、使用不当会造成内存溢出的问题

经典面试题：循环中使用闭包解决 var 定义函数的问题

```javascript
for(var i=0;i<10;i++){
  setTimeout(console.log(i),0);
}
//输出结果：0，1，2，3，4，5，6，7，8，9
for (var i = 0; i <10; i++) {
  setTimeout(function() {
    console.log(i);
  }, 0);
}
//连续的10个10

for(var i=0;i<10;i++){
  setTimeout("console.log(i)",1000);//连续的10个10
}
```

[https://blog.csdn.net/mikibiubiu/article/details/95985542](https://blog.csdn.net/mikibiubiu/article/details/95985542)<br />首先因为 setTimeout 是个异步函数，所以会先把循环全部执行完毕，这时候 i 就是 6 了，所以会输出一堆 6。解决办法

第一种是使用闭包的方式+立即执行函数

在上述代码中，首先使用了立即执行函数将 i 传入函数内部，这个时候值就被固定在了参数 j 上面不会改变，当下次执行 timer 这个闭包的时候，就可以使用外部函数的变量 j，从而达到目的

第二种：使用 setTimeout 的第三个参数，这个参数会被当成 timer 函数的参数传入

第三种用let替换var

  [[详情。。。](https://floweryu.blog.csdn.net/article/details/108272874?spm=1001.2101.3001.6661.1&utm_medium=distribute.pc_relevant_t0.none-task-blog-2%7Edefault%7ECTRLIST%7Edefault-1-108272874-blog-95985542.pc_relevant_scanpaymentv1&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-2%7Edefault%7ECTRLIST%7Edefault-1-108272874-blog-95985542.pc_relevant_scanpaymentv1&utm_relevant_index=1](https://floweryu.blog.csdn.net/article/details/108272874?spm=1001.2101.3001.6661.1&utm_medium=distribute.pc_relevant_t0.none-task-blog-2%7Edefault%7ECTRLIST%7Edefault-1-108272874-blog-95985542.pc_relevant_scanpaymentv1&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-2%7Edefault%7ECTRLIST%7Edefault-1-108272874-blog-95985542.pc_relevant_scanpaymentv1&utm_relevant_index=1))


<a name="9a19b58a"></a>
### *对作用域、作用域链的理解

作用域

<a name="GATYC"></a>
#### 全局作用域

最外层函数和最外层函数外面定义的变量拥有全局作用域（函数本身也是一个特殊的变量，其名字就是函数名字）

所有未定义直接赋值的变量自动声明为全局作用域

所有window对象的属性拥有全局作用域

<a name="iHDQw"></a>
#### 局部作用域

声明在函数内部的变量，一般只有固定的代码片段可以访问到

作用域是分层的，内层作用域可以访问外层作用域，反之不行

<a name="dSzPh"></a>
#### 块级作用域

使用ES6中新增的let和const指令可以声明块级作用域，块级作用域可以在函数中创建也可以在一个代码块中的创建（由{ }包裹的代码片段）

let和const声明的变量不会有变量提升，也不可以重复声明

在循环中比较适合绑定块级作用域，这样就可以把声明的计数器变量限制在循环内部

<a name="FKpwe"></a>
#### 作用域链

概念

在当前作用域中查找所需变量，如果在自己作用域找不到该变量就去父级作用域查找，依次向上级作用域查找，直到访问到window对象就被终止，这一层层的关系就是作用域链。

作用

保证对执行环境有权访问的所有变量和函数的有序访问，通过作用域链，可以访问到外层环境的变量和函数。

本质

一个指向变量对象的指针列表。变量对象是一个包含了执行环境中所有变量和函数的对象。作用域链的前端始终都是当前执行上下文的变量对象。全局执行上下文的变量对象（也就是全局对象）始终是作用域链的最后一个对象
<a name="eaee1474"></a>
### *this指向
全局作用域或者普通函数this指向window

对象方法中的this指向方法的调用者

构造函数或构造函数的原型对象中的this指向实例对象

箭头函数中的this指向外层函数中的this

<a name="c1ee48e5940320be836e28e9319be88c"></a>
### 常见的DOM操作有哪些
<a name="7a1835ac914473ff1d341590e7845cbd"></a>
#### 1）DOM 节点的获取
DOM 节点的获取的API及使用：
```javascript
getElementById // 按照 id 查询
getElementsByTagName // 按照标签名查询
getElementsByClassName // 按照类名查询
querySelectorAll // 按照 css 选择器查询

// 按照 id 查询
var imooc = document.getElementById('imooc') // 查询到 id 为 imooc 的元素
// 按照标签名查询
var pList = document.getElementsByTagName('p')  // 查询到标签为 p 的集合
console.log(divList.length)
console.log(divList[0])
// 按照类名查询
var moocList = document.getElementsByClassName('mooc') // 查询到类名为 mooc 的集合
// 按照 css 选择器查询
var pList = document.querySelectorAll('.mooc') // 查询到类名为 mooc 的集合
```
<a name="38d35b494114b03aa8c95164f2439e1a"></a>
#### 2）DOM 节点的创建
<a name="d7jAW"></a>
#### createElement
<a name="CBgtv"></a>
#### createTextNode
<a name="qAphp"></a>
#### createAttribute
innerHTML + appendChild

```javascript
// 要求添加一个有内容的 span 节点到 id 为 title 的节点后面，做法就是：
// 首先获取父节点
var container = document.getElementById('container')
// 创建新节点
var targetSpan = document.createElement('span')
// 设置 span 节点的内容
targetSpan.innerHTML = 'hello world'
// 把新创建的元素塞进父节点里去
container.appendChild(targetSpan)
```
<a name="d134a2bb3c9b795984f739d88a04d72c"></a>
#### 3）DOM 节点的删除
删除一个节点，首先要获得该节点本身以及它的父节点，然后，调用父节点的removeChild把自己删掉
```javascript
// 拿到待删除节点:
const self = document.getElementById('to-be-removed');
// 拿到父节点:
const parent = self.parentElement;
// 删除:
const removed = parent.removeChild(self);
removed === self; // true
```
删除后的节点虽然不在文档树中了，但其实它还在内存中，可以随时再次被添加到别的位置
<a name="4d48d4dbe713414629192da70fa50f19"></a>
#### 4）修改 DOM 元素
修改 DOM 元素这个动作可以分很多维度，比如说移动 DOM 元素的位置，修改 DOM 元素的属性等。

**将指定的两个 DOM 元素交换位置，**已知的 HTML 结构如下：
```javascript
<html>
  <head>
    <title>DEMO</title>
  </head>
  <body>
    <div id="container"> 
      <h1 id="title">我是标题</h1>
      <p id="content">我是内容</p>
    </div>   
  </body>
</html>
```
现在需要调换 title 和 content 的位置，可以考虑 insertBefore 或者 appendChild：
```javascript
// 获取父元素
var container = document.getElementById('container')   
 
// 获取两个需要被交换的元素
var title = document.getElementById('title')
var content = document.getElementById('content')
// 交换两个元素，把 content 置于 title 前面
container.insertBefore(content, title)
```
<a name="77607c31"></a>
### 给一个元素绑定click事件（三种实现方法）

**直接在DOM中绑定**

```javascript
<div id="btn" οnclick="one()"></div> //直接在DOM里绑定事件
  <script>
  function one(){ 
    alert("hello"); 
  }
  </script>
```

**使用JS获取元素并绑定**<br />1.传统方式注册事件 onclick = function(){};

```javascript
<div id="btn"></div>
  <script>
  document.getElementById("btn").onclick = function（）{
  alert("在js中直接绑定");
} //脚本里面绑定
</script>
```

2.绑定事件监听函数 addEventListener

```javascript
<div id='btn'><div>
  <script>
  document.getElementById('btn').addEventListener('click',function() {
    alert('绑定事件监听函数')
  })
  </script>
```

**使用JQuery**

```javascript
$("button").click(function(){});
```

<a name="URL"></a>
### URL

**URL(Uniform Resource Locator) ，统一资源定位符，能够对因特网的资源进行定位。**

URL一般有四部分组成：

**<协议>://<主机>:<端口>/<路径>?<查询字符串>#<片段>**

://:/?#

[https://www.baidu.com/path/s?id=1&age=13#new](https://www.baidu.com/path/s?id=1&age=13#new)

scheme：协议，常用的协议是http

host 主机，服务器（计算机）域名系统（DNS），主机名或IP地址

port 端口 整数，可选，省略时是默认端口，如http的默认端口是80

path 路径 网络资源在服务器中的指定路径

parameter 参数 如果要向服务器传入参数，在这部分输入

query 查询字符串 可选，用于给动态网页传递参数，可有多个参数，用“&”号隔开，每个参数的名和值用“=”号隔开。如：id=1

fragment 信息片段，字符串，锚点（如果想访问网页后直接到达指定位置，可以在这部分设置）


<a name="yspha"></a>
### Cookie、LocalStorage、SessionStorage区别
浏览器端常用的存储技术是 cookie 、localStorage 和 sessionStorage。<br />		cookie：其实最开始是服务器端用于记录用户状态的一种方式，由服务器设置，在客户端存储，然后每次发起同源请求时，发送给服务器端。cookie 最多能存储 4 k 数据，它的生存时间由 expires 属性指定，并且 cookie 只能被同源的页面访问共享。<br />		sessionStorage：html5 提供的一种浏览器本地存储的方法，它借鉴了服务器端 session 的概念，代表的是一次会话中所保存的数据。它一般能够存储 5M 或者更大的数据，它在当前窗口关闭后就失效了，并且 sessionStorage 只能被同一个窗口的同源页面所访问共享。<br />		localStorage：html5 提供的一种浏览器本地存储的方法，它一般也能够存储 5M 或者更大的数据。它和 sessionStorage 不同的是，除非手动删除它，否则它不会失效，并且 localStorage 也只能被同源页面所访问共享<br />注<br />		上面三种方式都是存储少量数据的时候的存储方式，当需要在本地存储大量数据的时候，我们可以使用浏览器的 indexDB 这是浏览器提供的一种本地的数据库存储机制。它不是关系型数据库，它内部采用对象仓库的形式存储数据，它更接近 NoSQL 数据库。<br />	Web Storage 和 cookie 的区别<br />		● Web Storage是为了更大容量存储设计的。Cookie 的大小是受限的，并且每次你请求一个新的页面的时候 Cookie 都会被发送过去，这样无形中浪费了带宽；<br />		● cookie 需要指定作用域，不可以跨域调用；<br />		● Web Storage 拥有 setItem,getItem,removeItem,clear 等方法，不像 cookie 需要前端开发者自己封装 setCookie，getCookie；<br />		● Cookie 也是不可以或缺的：Cookie 的作用是与服务器进行交互，作为 HTTP 规范的一部分而存在 ，而 Web Storage 仅仅是为了在本地“存储”数据而生。

<a name="1c3afb0c"></a>
### 跨域

<a name="929cd6e9"></a>
#### 什么是同源策略

```javascript
跨域问题其实就是浏览器的同源策略造成的。同源策略限制了从同一个源加载的文档或脚本如何与另一个源的资源进行交互。这是浏览器的一个用于隔离潜在恶意文件的重要的安全机制。同源指的是：协议、端口号、域名必须一致。同源策略：protocol（协议）、domain（域名）、port（端口）三者必须一致。同源政策的目的主要是为了保证用户的信息安全，它只是对 js 脚本的一种限制，并不是对浏览器的限制，对于一般的 img、或者script 脚本请求都不会有跨域的限制，这是因为这些操作都不会通过响应结果来进行可能出现安全问题的操作。同源政策主要限制了三个方面

● 当前域下的 js 脚本不能够访问其他域下的 cookie、LocalStorage、SessionStorage 和 indexDB。

● 当前域下的 js 脚本不能够操作访问操作其他域下的 DOM。

● 当前域下 ajax 无法发送跨域请求。
```

<a name="de8b50de"></a>
#### 如何解决跨越问题
CORS

跨域资源共享(CORS) 是一种机制，它使用额外的 HTTP 头来告诉浏览器  让运行在一个 origin (domain)上的Web应用被准许访问来自不同源服务器上的指定的资源。当一个资源从与该资源本身所在的服务器不同的域、协议或端口请求一个资源时，资源会发起一个跨域HTTP 请求。CORS需要浏览器和服务器同时支持，整个CORS过程都是浏览器完成的，无需用户参与。因此实现CORS的关键就是服务器，只要服务器实现了CORS请求，就可以跨源通信了。

JSONP

jsonp的原理就是利用<script>标签没有跨域限制，通过<script>标签src属性，发送带有callback参数的GET请求，服务端将接口返回数据拼凑到callback函数中，返回给浏览器，浏览器解析执行，从而前端拿到callback函数返回的数据。

缺点<br />● 具有局限性， 仅支持get方法<br />● 不安全，可能会遭受XSS攻击

postMessage 跨域

解决问题

● 页面和其打开的新窗口的数据传递

● 多窗口之间消息传递

● 页面与嵌套的iframe消息传递

● 上面三个场景的跨域数据传递

用法

postMessage(data,origin)方法接受两个参数

● data： html5规范支持任意基本类型或可复制的对象，但部分浏览器只支持字符串，所以传参时最好用JSON.stringify()序列化。

● origin： 协议+主机+端口号，也可以设置为"*"，表示可以传递给任意窗口，如果要指定和当前窗口同源的话设置为"/"。

nginx代理跨域

nginx代理跨域，实质和CORS跨域原理一样，通过配置文件设置请求响应头Access-Control-Allow-Origin…等字段。

跨域问题：同源策略仅是针对浏览器的安全策略。服务器端调用HTTP接口只是使用HTTP协议，不需要同源策略，也就不存在跨域问题。

nodejs 中间件代理跨域

node中间件实现跨域代理，原理大致与nginx相同，都是通过启一个代理服务器，实现数据的转发，也可以通过设置cookieDomainRewrite参数修改响应头中cookie中域名，实现当前域的cookie写入，方便接口登录认证。

document.domain + iframe跨域

此方案仅限主域相同，子域不同的跨域应用场景。实现原理：两个页面都通过js强制设置document.domain为基础主域，就实现了同域。

location.hash + iframe跨域

实现原理：a欲与b跨域相互通信，通过中间页c来实现。 三个页面，不同域之间利用iframe的location.hash传值，相同域之间直接js访问来通信。

window.name + iframe跨域

WebSocket协议跨域

WebSocket protocol是HTML5一种新的协议。它实现了浏览器与服务器全双工通信，同时允许跨域通讯，是server push技术的一种很好的实现。

<a name="58a8451b"></a>
#### 浏览器的垃圾回收机制

> 垃圾回收的概念

垃圾回收：JavaScript代码运行时，需要分配内存空间来储存变量和值。当变量不在参与运行时，就需要系统收回被占用的内存空间，这就是垃圾回收。

回收机制

Javascript 具有自动垃圾回收机制，会定期对那些不再使用的变量、对象所占用的内存进行释放，原理就是找到不再使用的变量，然后释放掉其占用的内存。

JavaScript中存在两种变量：局部变量和全局变量。全局变量的生命周期会持续要页面卸载；而局部变量声明在函数中，它的生命周期从函数执行开始，直到函数执行结束，在这个过程中，局部变量会在堆或栈中存储它们的值，当函数执行结束后，这些局部变量不再被使用，它们所占有的空间就会被释放。

当局部变量被外部函数使用时，其中一种情况就是闭包，在函数执行结束后，函数外部的变量依然指向函数内部的局部变量，此时局部变量依然在被使用，所以不会回收。

垃圾回收的方式

标记清除

标记清除是浏览器常见的垃圾回收方式，当变量进入执行环境时，就标记这个变量“进入环境”，被标记为“进入环境”的变量是不能被回收的，因为他们正在被使用。当变量离开环境时，就会被标记为“离开环境”，被标记为“离开环境”的变量会被内存释放。

垃圾收集器在运行的时候会给存储在内存中的所有变量都加上标记。然后，它会去掉环境中的变量以及被环境中的变量引用的标记。而在此之后再被加上标记的变量将被视为准备删除的变量，原因是环境中的变量已经无法访问到这些变量了。最后。垃圾收集器完成内存清除工作，销毁那些带标记的值，并回收他们所占用的内存空间。

引用计数

另外一种垃圾回收机制就是引用计数，这个用的相对较少。引用计数就是跟踪记录每个值被引用的次数。当声明了一个变量并将一个引用类型赋值给该变量时，则这个值的引用次数就是1。相反，如果包含对这个值引用的变量又取得了另外一个值，则这个值的引用次数就减1。当这个引用次数变为0时，说明这个变量已经没有价值，因此，在在机回收期下次再运行时，这个变量所占有的内存空间就会被释放出来

这种方法会引起循环引用的问题：例如： obj1和obj2通过属性进行相互引用，两个对象的引用次数都是2。当使用循环计数时，由于函数执行完后，两个对象都离开作用域，函数执行结束，obj1和obj2还将会继续存在，因此它们的引用次数永远不会是0，就会引起循环引用


js中的垃圾回收机制。js中的垃圾回收机制比较常见的是标记清除和引用计数。

标记清除是指：一开始为每个变量都做了一个标记。当变量进入某个环境或被环境中的变量引用时，它会去掉该变量身上的标记。最后仍有标记的变量就应该被回收。因为它已经无法被访问到了。

引用计数是指：跟踪记录每个值被引用的次数。当声明了一个变量并将一个引用类型赋给该变量时，则这个值的引用次数就是1。如果同一个值又被赋给另一个值，则引用次数加1。相反，如果包含对这个值的引用的变量又取得了另一个值，则引用次数减一。当引用次数变成0时，说明可以将其回收。这种机制有一中循环引用的问题，感兴趣的同学可以自己去查找相关资料，我就不详细说了，所以实际上还是第一种用的比较多。


原文链接：[https://blog.csdn.net/qq_38164763/article/details/94330129](https://blog.csdn.net/qq_38164763/article/details/94330129)

> 减少垃圾回收

对数组进行优化

在清空一个数组时，最简单的方法就是给其赋值为[ ]，但是与此同时会创建一个新的空对象，可以将数组的长度设置为0，以此来达到清空数组的目的

  对object进行优化

对象尽量复用，对于不再使用的对象，就将其设置为null，尽快被回收

对函数进行优化

在循环中的函数表达式，如果可以复用，尽量放在函数的外面


<a name="Xss"></a>
### Xss

盗取Cookie(用的最频繁的)

获取内网ip

获取浏览器保存的明文密码

截取网页屏幕

网页上的键盘记录

[https://blog.csdn.net/weixin_46601374/article/details/123146245?ops_request_misc=&request_id=&biz_id=102&utm_term=xss&utm_medium=distribute.pc_search_result.none-task-blog-2allsobaiduweb~default-1-123146245.142](https://blog.csdn.net/weixin_46601374/article/details/123146245?ops_request_misc=&request_id=&biz_id=102&utm_term=xss&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-1-123146245.142)v17rank_v33,157v15new_3&spm=1018.2226.3001.4187

<a name="fbd34afc"></a>
### 单元测试（unit testing）

是指对软件中的最小可测试单元进行检查和验证

sum.js

```javascript
function sum(a, b) {
  return a + b;
}
 
module.exports = sum;
```

sum.test.js

```javascript
const sum = require('./sum');
 
describe('sum function test', () => {
  it('sum(1, 2) === 3', () => {
    expect(sum(1, 2)).toBe(3);
  });
  
  // 这里 test 和 it 没有明显区别，
  //it 是指:it should xxx, test 是指 test xxx
  test('sum(1, 2) === 3', () => {
    expect(sum(1, 2)).toBe(3);
  });
})



//简易
const sum = require('../sum');
 
test('adds 1 + 2 to equal 3', () => {
  expect(sum(1, 2)).toBe(3);
});
```

<a name="49a55367"></a>
#### 为什么要做单元测试

- 必要性：JavaScript 缺少类型检查，编译期间无法定位到错误，单元测试可以帮助你测试多种异常情况。
- 正确性：测试可以验证代码的正确性，在上线前做到心里有底。
- 自动化：通过 console 虽然可以打印出内部信息，但是这是一次性的事情，下次测试还需要从头来过，效率不能得到保证。通过编写测试用例，可以做到一次编写，多次运行。
- 保证重构：互联网行业产品迭代速度很快，迭代后必然存在代码重构的过程，那怎么才能保证重构后代码的质量呢？有测试用例做后盾，就可以大胆的进行重构。

<a name="710190a3"></a>
#### 两个常用的单元测试方法论：

TDD（Test-driven development）：测试驱动开发

BDD（Behavior-driven development）：行为驱动开发

<a name="6efc948e"></a>
#### 覆盖率（jest）

Jest 还提供了生成测试覆盖率报告的命令，只需要添加上 --coverage 这个参数即可生成，再加上–colors 可根据覆盖率生成不同颜色的报告（<50%红色，50%~80%黄色， ≥80%绿色）

% Stmts 是语句覆盖率（statement coverage）：是否每个语句都执行了

% Branch 分支覆盖率（branch coverage）：是否每个分支代码块都执行了（if, ||, ? : ）

% Funcs 函数覆盖率（function coverage）：是否每个函数都调用了

% Lines 行覆盖率（line coverage）：是否每一行都执行了

<a name="0ce4430c"></a>
#### 模拟函数

Mock 函数允许你测试代码之间的连接——实现方式包括：擦除函数的实际实现、捕获对函数的调用（以及在这些调用中传递的参数）、在使用 new 实例化时捕获构造函数的实例、允许测试时配置返回值。

两种方法可以模拟函数：1.在测试代码中创建一个 mock 函数，2.编写一个手动 mock 来覆盖模块依赖

**mock 函数**

```javascript
const mockCallback = jest.fn((x) => 42 + x);
forEach([0, 1], mockCallback);

// 此 mock 函数被调用了两次
expect(mockCallback.mock.calls.length).toBe(2);

// 第一次调用函数时的第一个参数是 0
expect(mockCallback.mock.calls[0][0]).toBe(0);

// 第二次调用函数时的第一个参数是 1
expect(mockCallback.mock.calls[1][0]).toBe(1);

// 第一次函数调用的返回值是 42
expect(mockCallback.mock.results[0].value).toBe(42);
```

**.mock 属性**<br />所有的 mokc 函数都有这个特殊的.mock 属性，它保存了关于此函数如何被调用、调用时的返回值的信息。.mock 属性还追踪每次调用时的 this 的值，所以我们同样可以检查 this

```javascript
// 这个函数被实例化两次
expect(someMockFunction.mock.instances.length).toBe(2);

// 这个函数被第一次实例化返回的对象中，有一个 name 属性，且被设置为了 'test’
expect(someMockFunction.mock.instances[0].name).toEqual(‘test’);
复制代码
Mock 的返回值
const myMock = jest.fn();
console.log(myMock());
// > undefined

myMock.mockReturnValueOnce(10).mockReturnValueOnce(‘x’).mockReturnValue(true);

console.log(myMock(), myMock(), myMock(), myMock());
// > 10, ‘x’, true, true
复制代码
模拟模块
可以 用 jest.mock(…)函数自动模拟 axios 模块，一旦模拟模块，我们可为.get 提供一个 mockResolveValue，它会返回假数据用于测试
// users.test.js
import axios from ‘axios’;
import Users from ‘./users’;

jest.mock(‘axios’);

test(‘should fetch users’, () => {
const users = [{ name: ‘Bob’ }];
const resp = { data: users };
axios.get.mockResolvedValue(resp);

// or you could use the following depending on your use case:
// axios.get.mockImplementation(() => Promise.resolve(resp))

return Users.all().then((data) => expect(data).toEqual(users));
});
```

**Mock 实现**<br />用 mock 函数替换指定返回值：jest.fn(cb => cb(null, true))

用 mockImplementation 根据别的模块定义默认的 mock 函数实现：jest.mock(’…/foo’); const foo = require(’…/foo’);foo.mockImplementation(() => 42);

当你需要模拟某个函数调用返回不同结果时，请使用 mockImplementationOnce 方法

.mockReturnThis()函数来支持链式调用

```javascript
const myMockFn = jest
  .fn()
  .mockReturnValue('default')
  .mockImplementation((scalar) => 42 + scalar)
  .mockName('add42');
```

**Mock 名称**

可以为你的 Mock 函数命名，该名字会替代 jest.fn() 在单元测试的错误输出中出现。 用这个方法你就可以在单元测试输出日志中快速找到你定义的 Mock 函数

<a name="c2f42bd2"></a>
### 性能优化

<a name="fb6b7084"></a>
#### 怎么样从web前端方面优化性能？至少列举5点？

1) HTML部分

-  语义化HTML：好处在于可以使代码简洁清晰，支持不同设备，利于搜索引擎，便于团队开发； 
-  减少DOM节点：加速页面渲染； 
-  给图片加上正确的宽高值：这可以减少页面重绘，同时防止图片缩放； 
-  防止src属性和link的href属性为空：当值为空时，浏览器很可能会把当前页面当成其属性值加载； 
-  正确的闭合标签：如避免使用 
-  链接为目录或首页的地址后面加”/”，如[http://www.5icool.org/](http://www.5icool.org/)； 
-  用LINK而不用@import方式导入样式； 
-  样式放在页头，JS放在页尾； 
-  缩小favicon.ico并缓存；<br />2）CSS部分 
-  避免使用CSS Expressions(CSS表达式)： 
-  如background color:expression((newDate()).getHours()%2 ? “#B8D4FF” : “#F08A00″ ) ; 
-  避免使用CSS Filter（CSS滤镜）； 
-  使用CSS缩写，减少代码量； 
-  通过CSSSprites把同类图片合成一张，减少图片请求； 
-  减少查询层级：如.header .logo要好过.header .top .logo； 
-  减少查询范围：如.header>li要好过.header li； 
-  避免TAG标签与CLASS或ID并存：如a.top、button#submit； 
-  删除重复的CSS；<br />3)  Javscript部分 
-  尽量少用全局变量； 
-  使用事件代理绑定事件，如将事件绑定在body上进行代理； 
-  避免频繁操作DOM节点； 
-  不使用EVAL； 
-  减少对象查找，如a.b.c.d这种查找方式非常耗性能，尽可能把它定义在变量里； 
-  类型转换：把数字转换成字符串使用”” + 1，浮点数转换成整型使用Math.floor()或者Math.round()； 
-  对字符串进行循环操作，譬如替换、查找，应使用正则表达式； 
-  删除重复的JS；<br />4)  服务器部分 
-  尽量合并CSS、JS文件，或将其直接写在页面上，减少HTTP请求； 
-  压缩CSS、JS文件，缩短文件传输时间； 
-  避免404错误：特别要避免给404指定一个停摆页面，否则所有404错误都将会加载一次页面； 
-  一般要求减少DNS查询次数，如同一个页面的请求资源尽量少的使用不同的主机名，这可以减少网站并行下载的数量，但很多网站为了加速下载资源其实是特意用了多个主机名，这里要做一个权衡； 
-  使用CDN加速，使用户从离自己最近的服务器下载文件； 
-  减少Cookie的大小，使用无cookie的域，客户端请求静态文件的时候，减少 Cookie 的反复传输对主域名的影响； 
-  为文件头指定Expires，使内容具有缓存性； 
-  使用gzip压缩内容； 

<a name="d41d8cd9"></a>
#### 

<a name="038978fa"></a>
#### 性能优化方法

<a name="CDN"></a>
#### CDN

<a name="9ff4713f"></a>
#### 懒加载

```
		懒加载也叫做延迟加载、按需加载，指的是在长网页中延迟加载图片数据，是一种较好的网页性能优化的方式。在比较长的网页或应用中，如果图片很多，所有的图片都被加载出来，而用户只能看到可视窗口的那一部分图片数据，这样就浪费了性能。如果使用图片的懒加载就可以解决以上问题。在滚动屏幕之前，可视化区域之外的图片不会进行加载，在滚动屏幕时才加载。这样使得网页的加载速度更快，减少了服务器的负载。懒加载适用于图片较多，页面列表较长（长列表）的场景中。
```

<a name="e2d03cae"></a>
#### 节流与防抖

对节流与防抖的理解

防抖

概念

```
	函数防抖是指在事件被触发 n 秒后再执行回调，如果在这 n 秒内事件又被触发，则重新计时。这可以使用在一些点击请求的事件上，避免因为用户的多次点击向后端发送多次请求。
```

应用场景

```
	按钮提交场景：防⽌多次提交按钮，只执⾏最后提交的⼀次 

	服务端验证场景：表单验证需要服务端配合，只执⾏⼀段连续的输⼊事件的最后⼀次，还有搜索联想词功能类似⽣存环境请⽤lodash.debounce
```

节流

概念

```
	函数节流是指规定一个单位时间，在这个单位时间内，只能有一次触发事件的回调函数执行，如果在同一个单位时间内某事件被触发多次，只有一次能生效。节流可以使用在 scroll 函数的事件监听上，通过事件节流来降低事件调用的频率。
```

应用场景

拖拽场景：固定时间内只执⾏⼀次，防⽌超⾼频次触发位置变动

缩放场景：监控浏览器resize

动画场景：避免短时间内多次触发动画引起性能问题

实现节流函数和防抖函数

函数防抖实现

函数节流实现

<a name="cfcbbe39"></a>
#### 减少回流与重绘

回流与重绘的概念及触发条件

<a name="fHrbl"></a>
##### 回流/重排

概念<br />当渲染树中部分或者全部元素的尺寸、结构或者属性发生变化时，浏览器会重新渲染部分或者全部文档的过程就称为回流。


触发条件<br />● 页面的首次渲染<br />	● 浏览器的窗口大小发生变化<br />	● 元素的内容发生变化<br />	● 元素的尺寸或者位置发生变化<br />	● 元素的字体大小发生变化<br />	● 激活CSS伪类<br />	● 查询某些属性或者调用某些方法<br />	● 添加或者删除可见的DOM元素

<a name="eCCSS"></a>
##### 重绘

概念<br />当页面中某些元素的样式发生变化，但是不会影响其在文档流中的位置时，浏览器就会对元素进行重新绘制，这个过程就是重绘。

触发条件<br />● color、background 相关属性：background-color、background-image 等<br />	● outline 相关属性：outline-color、outline-width 、text-decoration<br />	● border-radius、visibility、box-shadow

<a name="Q3ReT"></a>
##### 如何避免回流与重绘

CSS

避免设置多层内联样式。

如果需要设置动画效果，最好使用absolute或者fixed，使元素脱离文档流，这样他们发生变化就不会影响其他元素。

避免使用CSS表达式（例如：calc()）。

JS

避免频繁操作样式，最好将样式列表定义为class并一次性更改class属性。

避免频繁操作DOM，创建一个documentFragment，在它上面应用所有DOM操作，最后再把它添加到文档中。

可以先为元素设置为不可见：display: none，操作结束后再把它显示出来。因为在display属性为none的元素上进行的DOM操作不会引发回流和重绘。

浏览器针对页面的回流与重绘，进行了自身的优化——渲染队列

浏览器会将所有的回流、重绘的操作放在一个队列中，当队列中的操作到了一定的数量或者到了一定的时间间隔，浏览器就会对队列进行批量处理。这样就会让多次的回流、重绘变成一次回流重绘。

documentFragment是什么？用它跟直接操作DOM的区别是什么？

概念

DocumentFragment，文档片段接口，一个没有父对象的最小文档对象。它被作为一个轻量版的 Document使用，就像标准的document一样，存储由节点（nodes）组成的文档结构。与document相比，最大的区别是DocumentFragment不是真实 DOM 树的一部分，它的变化不会触发 DOM 树的重新渲染，且不会导致性能等问题。

与直接操作 DOM 的区别

由于DocumentFragment不会出现在文档树中，将DocumentFragment插入文档树中，相当于把把他的子孙节点插入到文档树中，在频繁的DOM操作时，我们就可以将DOM元素插入DocumentFragment，之后一次性的将所有的子孙节点插入文档中。和直接操作DOM相比，将DocumentFragment 节点插入DOM树时，仅会触发页面的一次重绘，这样就大大提高了页面的性能。

<a name="4a656b3d"></a>
#### 图片优化

**1.图片压缩**

图片的大小和数量直接影响了页面的加载速度和渲染速度，降低图片大小

**2.减少 Http 请求**

- 精灵图
- 使用SVG图标代替图片(可伸缩矢量图形)<br />XML 格式定义图形、放大或改变尺寸的情况下其图形质量不会有所损失

优点：SVG 图像可被搜索、索引、脚本化或压缩

- 使用html5 canvas绘画图形<br />目前canvas应用很多，它可以使用脚本javascript来绘制各种图表、动画等

点击查看更多[html5 canvas](http://www.w3school.com.cn/html5/html5_canvas.asp)

**3.图片懒加载**

- 对图片先设置默认图片，当图片加载完成时，替换掉默认图片
- 在页面中未出现在可视窗口内的图片先不做加载，等用户滚动到可视区域后再去加载。这和预加载使用原理是相反的。
- 原理<br />将页面中的img标签src指向一张小图片或者src为空，然后定义data-src（可用其他命名）属性指向真实的图片。

src指向一张默认的图片，否则当src为空时也会向服务器发送一次请求。

当载入页面时，先把可视区域内的img标签的data-src属性值负给src，然后监听滚动事件，把用户即将看到的图片加载。这样便实现了懒加载

4.图片Base64压缩

图片的 base64 编码就是可以将一副图片数据编码成一串字符串，使用该字符串代替图像地址。每一个图片都需要消耗Http请求，从服务器将图片下载到本地。若是图片可以随着html文件下载一起下载到本地，则可以减少http请求，加快图片访问速度。

<a name="d0b4c268"></a>
#### webpack优化
如何用webpack优化前端性能？

通过webpack优化前端的手段

代码压缩

JS代码压缩<br />利⽤webpack的 UglifyJsPlugin 和 ParallelUglifyPlugin 来压缩JS⽂件

CSS代码压缩<br />利⽤ cssnano （css-loader?minimize）来压缩css

Html文件代码压缩

使用HtmlWebpackPlugin插件来生成HTML的模板时候，通过配置属性minify进行html优化

文件大小压缩

对文件的大小进行压缩，减少http传输过程中宽带的损耗

图片压缩

Tree Shaking<br />将代码中永远不会⾛到的⽚段删除掉（消除死代码）。可以通过在启动webpack时追加参数 --optimize-minimize 来实现；<br />代码分离

代码按路由维度或者组件分块(chunk),这样做到按需加载,同时可以充分利⽤浏览器缓存<br />提取公共第三⽅库

SplitChunksPlugin插件来进⾏公共模块抽取,利⽤浏览器缓存可以⻓期缓存这些⽆需频繁变动的公共代码 

<a name="cO55M"></a>
##### 如何提高webpack构建速度？

			优化webpack构建的方式有很多，主要可以从优化搜索时间、缩小文件搜索范围、减少不必要的编译等方面入手

				优化loader配置

					在使用loader时，可以通过配置include、exclude、test属性来匹配文件，缩小文件的搜索范围，优化搜索时间

				多⼊⼝情况下，使⽤ CommonsChunkPlugin 来提取公共代码

				通过 externals 配置来提取常⽤库，脱离webpack打包，不被打⼊bundle中，从⽽减少打包时间

				利⽤ DllPlugin 和 DllReferencePlugin 预编译资源模块 通过 DllPlugin 来对那些我们引⽤但是绝对不会修改的npm包来进⾏预编译，再通过 DllReferencePlugin 将预编译的模块加载进来，让⼀些基本不会改动的代码先打包成静态资源，避免反复编译浪费时间  

				使⽤ Happypack 实现多线程加速编译 

				使⽤ webpack-uglify-parallel 来提升 uglifyPlugin 的压缩速度。 原理上 webpack-uglify-parallel 采⽤了多核并⾏压缩来提升压缩速度

				使⽤ Tree-shaking 和 Scope Hoisting 来剔除多余代码 

				利⽤缓存提⾼rebuild效率

		如何减少webpack打包时间？

			优化 Loader

				对于 Loader 来说，影响打包效率首当其冲必属 Babel 了。因为 Babel 会将代码转为字符串生成 AST，然后对 AST 继续进行转变最后再生成新的代码，项目越大，转换代码越多，效率就越低。

					优化 Loader 的文件搜索范围

						对于 Babel 来说，希望只作用在 JS 代码上的，然后 node_modules 中使用的代码都是编译过的，所以完全没有必要再去处理一遍。

					还可以将 Babel 编译过的文件缓存起来，下次只需要编译更改过的代码文件即可，这样可以大幅度加快打包时间

						

			HappyPack

				受限于 Node 是单线程运行的，所以 Webpack 在打包的过程中也是单线程的，特别是在执行 Loader 的时候，长时间编译的任务很多，这样就会导致等待的情况。HappyPack 可以将 Loader 的同步执行转换为并行的，这样就能充分利用系统资源来加快打包效率了

					

			DllPlugin

				DllPlugin 可以将特定的类库提前打包然后引入。这种方式可以极大的减少打包类库的次数，只有当类库更新版本才有需要重新打包，并且也实现了将公共代码抽离成单独文件的优化方案。

					

					然后需要执行这个配置文件生成依赖文件，接下来需要使用 DllReferencePlugin 将依赖文件引入项目中

			代码压缩

				在 Webpack3 中，一般使用 UglifyJS 来压缩代码，但是这个是单线程运行的，为了加快效率，可以使用 webpack-parallel-uglify-plugin 来并行运行 UglifyJS，从而提高效率。在 Webpack4 中，不需要以上这些操作了，只需要将 mode 设置为 production 就可以默认开启以上功能。代码压缩也是我们必做的性能优化方案，当然我们不止可以压缩 JS 代码，还可以压缩 HTML、CSS 代码，并且在压缩 JS 代码的过程中，我们还可以通过配置实现比如删除 console.log 这类代码的功能。

			其他

				resolve.extensions

					用来表明文件后缀列表，默认查找顺序是 ['.js', '.json']，如果你的导入文件没有添加后缀就会按照这个顺序查找文件。我们应该尽可能减少后缀列表长度，然后将出现频率高的后缀排在前面

				resolve.alias

					可以通过别名的方式来映射一个路径，能让 Webpack 更快找到路径

				module.noParse

					如果你确定一个文件下没有其他依赖，就可以使用该属性让 Webpack 不扫描该文件，这种方式对于大型的类库很有帮助

		如何减少webpack打包体积？

			按需加载

				在开发 SPA 项目的时候，项目中都会存在很多路由页面。如果将这些页面全部打包进一个 JS 文件的话，虽然将多个请求合并了，但是同样也加载了很多并不需要的代码，耗费了更长的时间。那么为了首页能更快地呈现给用户，希望首页能加载的文件体积越小越好，这时候就可以使用按需加载，将每个路由页面单独打包为一个文件。当然不仅仅路由可以按需加载，对于 loadash 这种大型类库同样可以使用这个功能。

			Scope Hoisting

				Scope Hoisting 会分析出模块之间的依赖关系，尽可能的把打包出来的模块合并到一个函数中去。这样的打包方式生成的代码明显比之前的少多了。如果在 Webpack4 中你希望开启这个功能，只需要启用 optimization.concatenateModules 就可以了

					

			Tree Shaking

				Tree Shaking 可以实现删除项目中未被引用的代码（死代码）
<a name="WY9r9"></a>
### 发布订阅者模式
[https://vue3js.cn/interview/design/Observer%20%20Pattern.html#%E4%B8%80%E3%80%81%E8%A7%82%E5%AF%9F%E8%80%85%E6%A8%A1%E5%BC%8F](https://vue3js.cn/interview/design/Observer%20%20Pattern.html#%E4%B8%80%E3%80%81%E8%A7%82%E5%AF%9F%E8%80%85%E6%A8%A1%E5%BC%8F)


