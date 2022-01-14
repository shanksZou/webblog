# 前言
写一手精简的代码，不仅仅能够增加代码的可读性，而且还能够提示代码的运行效率。本文主要总结各大佬写代码的风格，通过“站在巨人的肩膀上”来提升自己的编码风格。
本文主要从JavaScript编码风格、css编码风格、vue代码风格三个方面入手。

## JavaScript编码风格

### 1.判断相关

#### 多或判断

如下代码

```js
<script>
	let str="vue"
	if(str==='vue'||str==='anguler'||str === 'react'){
		console.log(str);
	}
	</script>
```

这段的代码的”||“符号是不是很多，这是三种情况的，如果是超过三种情况的时候，这段代码就看起来很别扭了，我们可以通过一个数组来存放可能的情况，在用includes来判断该字符是否存在

1.1.数组includes方法

```js
<script>
	let str2 = "vue"
	let arr = ['vue', 'anguler', 'react']
	if (arr.includes(str2)) {
		console.log(str2);
	}
</script>
```

这样的代码是不是可读性就高了，这种方法还可以使用在vue中绑定class或者v-if判断中

```vue
<div :class="{'active' : ['Home', 'Gallery', 'Profile'].includes($route.name)}"></div>
```

```vue
<div v-if="['Home', 'Gallery', 'Profile'].includes(routeName)"></div>
```



#### 多if

给出以下代码：

```js
let str = "vue"
if (str === 'vue') {
	console.log('vue');
}
if (str === 'anguler') {
	console.log('anguler');
}
if (str === 'react') {
	console.log('react');
}
```

根据不同的控制条件执行不同的代码，如果使用if...if....if，导致太多的if语气导致读起来别扭，解决方案有，将if内的代码都提取出来封装成一个方法，在if语气内引用，这可以使得if内代码不会太多，读起来页比较方便，但是还是不太理想，if太多了......

如下：

使用map封装

```js
<script>
	let str3 = "vue"
	let fn = function () {
		console.log('item');
	}
	let fn2 = function () {
		console.log('item');
	}
	let fn3 = function () {
		console.log('item');
	}
	let map = new Map([
		['vue', (item) => { console.log(item); }],
		['anguler', (item) => { console.log(item); }],
		['react', (item) => { console.log(item); }]
		])
	map.get(str3)(str3)
</script>
```

使用对象法

```js
<script>
	let str='vue'
	let obj={
		'vue':function(item){console.log(item);},
		'js': function (item) { console.log(item); },
		'css': function (item) { console.log(item); },
	}
	obj[str](str)
</script>
```

这样就简单易懂了。

#### 多if-else

实际上用法和多if差不多，只是多一部分判断，如果为空或者undefined的时候不执行或者执行别的代码

使用对象举例：

```js
<script>
	let str='vue'
	let fn=function (){
        console.log("执行else的语气")
    }
	let obj={
		'vue':function(item){console.log(item);},
		'js': function (item) { console.log(item); },
		'css': function (item) { console.log(item); },
	}
	str?obj[str](str):fn()
</script>
```

#### 三目运算符取代if..else

```js
let a='vue'
if (a) {
	console.log('vue');
}else{
	console.log('not vue');
}
```

可以写成：

```js
a? console.log('vue'): console.log('not vue')
```

#### 取代单if

```js
let a ="vue"
if (a==='vue') {
	console.log('vue');
}
```

可写成：

```js
let a='vue'
a==='vue'&& console.log('vue')
```

### 2.循环相关的

#### for循环

平时写for循环的时候我们是这么写的

```javascript
	<script>
		let arr=[1,2,3,4,5]
		for (let index = 0; index < arr.length; index++) {
			console.log(arr[index]);
		}
	</script>
```

我们可以优化为：

```javascript
let arr=[1,2,3,4,5]
for (let index = 0,arrLength= arr.length; index < arrLength; index++) {
	console.log(arr[index]);
}
```

执行的时候，不用每次计算数组的长度，节省算能。

这个是根据数组的索引升循环，我们还可以更加降序循环，减少for循环的条件变量，达到性能优化的目的

```javascript
for (let index = arr.length-1; index >=0; index--) {
	console.log(arr[arr.length-index-1]);
}
```

这个效果和for索引升序的效果一样。



## css编码风格

## vue编码技巧

