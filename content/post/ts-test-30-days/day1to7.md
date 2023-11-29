---
title: "TypeScript练习题：30天LeetCode挑战（day1 to day7）"
date: 2023-02-20T14:08:56+08:00
draft: false # 是否为草稿

tags: ["LeetCode", "TypeScript"]
categories: ["LeetCode"]
---

LeetCode 挑战题目汇总地址： [30 Days of JavaScript Challenge](https://leetcode.com/discuss/study-guide/3458761/Open-to-Registration!-30-Days-of-LC-JavaScript-Challenge)



### DAY1: [Create Hello World Function](https://leetcode.com/problems/create-hello-world-function/)

##### 解题代码：

```typescript
function createHelloWorld() {
	return function(...args): string {
        return "Hello World"
    };
};
```

**官方解題說明**

[https://leetcode.com/problems/create-hello-world-function/editorial/](https://leetcode.com/problems/create-hello-world-function/editorial/?gio_link_id=j9yDnOOo)



### DAY2: [Counter](https://datayi.cn/w/xogkVqBo)

##### 题目说明：

第一次调用 `createCounter` 传值 `n`, 后面每次调用返回都比前一次返回的值加1。

##### 解题思路：

可以用变量和运算符的相对位置来记递增运算符返回的值是计算前还是计算后的值：n++ 的 n 放在 ++ 的前面，所以是运算前的值；++n 是放在 ++ 的后面，所以是运算后的值。

```typescript
function createCounter(n: number): () => number {
    return function() {
		return n++
    }
}
```

**官方解題說明**

https://leetcode.com/problems/counter/editorial/





### DAY3: [Counter II](https://datayi.cn/w/xRxVYOXo)

##### 题目说明：

实现函数 createCounter，可以传一个初始值参数，返回包含三个函数的对象，三个函数分别是 increment()、decrement()、reset()。 

##### 解题思路：

increment()、decrement() 都是返回计算过后的值，变量要放在运算符的后面。reset() 重置初始值，需要额外用变量储存当前计算值，保留初始值 init。

```typescript
type ReturnObj = {
    increment: () => number,
    decrement: () => number,
    reset: () => number,
}

function createCounter(init: number): ReturnObj {
    let currentNum = init
	return {
        increment: () =>  ++currentNum,
        decrement: () => --currentNum,
        reset: () => {
            currentNum = init;
            return currentNum
        },        
    }
};
```



### DAY4: [Apply Transform Over Each Element in Array](https://datayi.cn/w/noqbNOv9)

##### 题目说明：

返回 arr 经过 fn 处理后的结果，不能使用 Array.map()，可以理解成实现一个类似 Array.map 方法的功能。

##### 解题思路：

遍历数组的方式除了 Array.map 还有 for、for...of 与 Array.forEach() 可以用（for...in 是用在 Object），这几个方法都需要一个额外的变量来储存 fn 执行后的结果。

```typescript
function map(arr: number[], fn: (n: number, i: number) => number): number[] {
	let resultArr: number[] = []
    arr.forEach((item, index) => {
        resultArr.push(fn(item, index))
    })

    return resultArr
};
```

**官方解題說明**

https://leetcode.com/problems/apply-transform-over-each-element-in-array/editorial/



### DAY5: [Filter Elements from Array](https://datayi.cn/w/a9a5VZr9)

##### 题目说明：

仅返回 `arr` 经过 `fn` 处理后为真值的元素阵列，不能使用 `Array.filter()` ，一样可以理解成实作一个类似 `Array.filter` 方法的功能。

##### 解题思路：

这题可以看做是DAY4的基础上加上`fn`执行结构是否为true的判断

##### 解题代码：

```typescript
type Fn = (n: number, i: number) => any

function filter(arr: number[], fn: Fn): number[] {
  const newArr: number[] = [];
  for (let i = 0; i < arr.length; i++) {
    if (fn(arr[i], i)) newArr.push(arr[i]);
  }
  return newArr;
};
```

##### 官方解题说明

https://leetcode.com/problems/filter-elements-from-array/editorial/



### DAY6：[Array Reduce Transformation](https://datayi.cn/w/nPN45jD9)

##### 题目说明

按照数组 nums 中元素的顺序，从左至右（第一个到最后一个）逐个通过回调函数 fn 处理初始值 init 和每个元素上，最后将数组缩减成单一值后返回。不能使用 Array.reduce()，同样可以理解成实现类似 Array.reduce() 的方法。

##### 解题方法

由于需要按顺序处理数组中的每个元素，并且每个元素的处理结果都会影响到下一个元素的处理，适合使用循环。在循环中，会需要一个变量来持续追踪当前的处理结果。每次循环结束时，更新这个变量的值，将其设定为当前元素经过缩减函数处理后的结果。这样就能够将前一次循环的结果适当地带入到下一次的处理中。最后循环结束后，只需要返回这个变量的值，即可得到数组经过缩减处理后的结果。

##### 解题代码：

```typescript
type Fn = (accum: number, curr: number) => number;

function reduce(nums: number[], fn: Fn, init: number): number {
  let result = init;
  for (let i = 0; i < nums.length; i++) {
    result = fn(result, nums[i]);
  }
  return result;
}
```

**官方解題說明**

https://leetcode.com/problems/array-reduce-transformation/editorial/



### DAY7: [Function Composition](https://datayi.cn/w/4PY7wZM9)

##### 题目说明

这一题跟昨天的 Array Reduce Function 其实有点像，只是把数组的元素从数字变成函数，可以理解成每次循环使用的回调函数都不同，最后返回的结果虽然变成函数，并且初始值由返回的函数传入的值决定，但函数一样是返回单一值。

##### 解题方法

尝试解题的时候，发现跟 Array Reduce Function 不一样的地方是，函数组合计算顺序是反过来的。可以看题目的举例 [f(x), g(x), h(x)] 组合后的结果是 fn(x) = f(g(h(x))) 所以是 h(x) 的计算结果传给 g(x) 再传给 f(x)。

若要将执行顺序反过来，第一个念头是把数组反转，但用 Array.reverse() 会改变原来的数组，需要先复制一个数组再做处理。不过印象中 reverse 性能没那么好，也可以用 for 循环从最后一个当做执行起始点。

##### 解题代码

```typescript
type F = (x: number) => number;

function compose(functions: F[]): F {
    const reversedFns = functions.reverse()
	return function(x) {
         let result  = x;
        for (const fn of reversedFns) {
            result = fn(result);
        }
        return result
    }
};

```

**官方解題說明**

https://leetcode.com/problems/function-composition/editorial/