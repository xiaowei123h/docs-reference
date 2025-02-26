# CSS

## JS获取元素的样式

**使用 element.style 获取内联样式**

element.style 只能获取元素的内联样式（即通过 style 属性直接设置的样式），无法获取外部 CSS 文件或 \<style\> 标签中定义的样式。

```[.js]
const div = document.querySelector('div');
console.log(div.style.backgroundColor); // 获取背景颜色
console.log(div.style.width); // 获取宽度
```

**使用 window.getComputedStyle 获取计算样式**

window.getComputedStyle 可以获取元素最终计算后的样式（包括内联样式、外部 CSS 和 \<style\> 标签中的样式）。

```[.js]
const div = document.querySelector('div');
const computedStyle = window.getComputedStyle(div);
console.log(computedStyle.backgroundColor); // 获取背景颜色
console.log(computedStyle.width); // 获取宽度
```

**获取伪元素的样式**

如果需要获取伪元素（如 ::before 或 ::after）的样式，可以使用 getComputedStyle 的第二个参数指定伪元素。

```[.js]
const div = document.querySelector('div');
const pseudoStyle = window.getComputedStyle(div, '::before');
console.log(pseudoStyle.content); // 获取伪元素的内容
console.log(pseudoStyle.backgroundColor); // 获取伪元素的背景颜色
```

**注意事项**

单位：getComputedStyle 返回的样式值通常带有单位（如 px、rgb() 等）。

性能：频繁调用 getComputedStyle 可能会影响性能，尽量避免在循环中使用。

只读：getComputedStyle 返回的对象是只读的，不能直接修改样式。

**修改样式**

如果需要修改样式，可以直接操作 element.style 或使用 classList 添加/移除类名。

```[.js]
// 直接修改样式
div.style.backgroundColor = 'red';

// 通过类名修改样式
div.classList.add('highlight');
```