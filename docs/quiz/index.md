---
title: 数组去重
nav:
  title: 面试集
  order: 1
group:
  title: JavaScript
  order: 1
---

## 数组去重

> `数组去重` 不仅在面试中经常出现，在工作中，我们也经常会使用到。我们现在就把一些常见的去重方法进行一个整理，方便我们在复习的时候进行查缺补漏。

1. 双重 for 循环

   > 这里主要是利用 双循环 + 索引标记 的一个方法，来实现对数组的去重。

   ```js
   let arr = [1, 2, 3, 1, 3, 2, 1, 5];
   let un_repeat = [];
   for (let i = 0; i < arr.length; i++) {
     let index = 0;
     for (let k = 0; k < un_repeat.length; k++) {
       if (arr[i] === un_repeat[k]) {
         index = index + 1;
       }
     }
     if (index === 0) {
       un_repeat.push(arr[i]);
     }
   }
   console.log(un_repeat); // [1, 2, 3, 5]
   ```

2. 使用对象的特性对数组进行去重

   > 在 js 中，对象的键名是不允许重复的，我们可以把数组中的值作为对象中的键名，这样当遇到重复的数据时，就不会进行创建数据，而是覆盖与这键名相同的数据了。

   ```js
   let arr = [1, 2, 3, 1, 3, 2, 1, 5];
   let un_repeat = [];
   let un_repeat_obj = {};

   for (let i = 0; i < arr.length; i++) {
     un_repeat_obj[arr[i]] = arr[i];
   }
   for (let key in un_repeat_obj) {
     un_repeat.push(un_repeat_obj[key]);
   }
   console.log(un_repeat); // [1, 2, 3, 5]
   ```

3. 利用 Set + 扩展运算符 来进行去重

   > 在 Set 中，所有的元素只会出现一次。

   ```js
   let arr = [1, 2, 3, 1, 3, 2, 1, 5];
   console.log([...new Set(arr.map((item) => item))]); // [1, 2, 3, 5]
   ```

4. 使用 indexOf
   ```js
   let arr = [1, 2, 3, 1, 3, 2, 1, 5];
   let un_repeat = [];
   for (let i = 0; i < arr.length; i++) {
     if (un_repeat.indexOf(arr[i]) === -1) {
       un_repeat.push(arr[i]);
     }
   }
   console.log(un_repeat); // [1, 2, 3, 5]
   ```
5. 使用 reduce + indexOf
   ```js
   let arr = [1, 2, 3, 1, 3, 2, 1, 5];
   let un_repeat = arr.reduce((previousValue, currentValue, currentIndex) => {
     if (previousValue.indexOf(currentValue) === -1) {
       previousValue.push(currentValue);
     }
     return previousValue;
   }, []);
   console.log(un_repeat); // [1, 2, 3, 5]
   ```
