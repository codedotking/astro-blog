---
author: huala
pubDatetime: 2022-09-23T15:22:00Z
modDatetime: 2023-12-21T09:12:47.400Z
title: JS 开发优化之防抖节流
slug: fang-dou-jie-liu
featured: true
draft: false
tags:
  - 防抖
  - 节流
  - javascript
  - optimize
description: 利用防抖节流来优化操作体验
---

> 防抖（Debouncing）和节流（Throttling）都是优化性能，特别是在事件频繁触发时控制资源消耗的技术。它们通常用于编程和电子学领域，以确保系统的响应性和稳定性。尽管两者的目的相似，它们的实现方式和适用场景有所不同。

## 防抖（Debouncing）

**防抖（Debouncing）** 这个术语来源于电子工程领域，特别是在处理物理开关（如按钮或键盘按键）的信号时。当用户按下一个按钮，由于机械和物理接触的不完美，信号可能会在短时间内迅速地多次开闭，产生抖动（bouncing）。这会导致电路错误地解读多次按压，而实际上用户只进行了一次按压操作。为了解决这个问题，电子工程师会使用防抖电路或软件算法来确保只有一次信号被注册。这种防抖逻辑会等待信号稳定一段时间，只有当没有新的抖动发生时，才会接受信号。

在软件开发中，防抖的概念被借鉴来处理连续的事件触发，比如键盘输入、窗口调整大小、滚动事件等。在这些情况下，事件可能会连续快速地触发，**而我们只关心事件的最终结果** 。通过防抖，我们可以延迟函数的执行直到事件停止触发一段时间后，这样可以避免不必要的函数调用，提高应用程序的性能和用户体验。

因此，防抖在编程中的命名反映了它的功能：在一系列快速连续的事件中，防止函数被多次调用，就像它在电子学中防止信号抖动一样。


**案例 1** 在用户输入时，你可能不希望在每个键盘击键后都进行数据验证或搜索建议的更新。使用防抖，你可以设置一个延迟，比如 300 毫秒，在用户停止输入后才执行验证或更新。


**代码实现**

```js
// 防抖函数
function debounce(func, timeout = 250) {
  let timer;
  return (...args) => {
    clearTimeout(timer);
    timer = setTimeout(() => {
      func.apply(this, args);
    }, timeout);
  };
}
```

<hr/>

## 节流（Throttling）

**节流（Throttling）** 这个术语在电子工程和计算机科学领域中指的是一种控制信号或数据流量的技术。在电子工程领域，节流可以通过限制电流的流动来控制电路中的功率消耗。它可以用来防止电路过热或过载，确保电路的稳定运行。

在计算机科学和软件开发中，节流的概念被应用于事件处理和资源管理。当一个动作或事件（如鼠标滚轮滚动、窗口调整大小、连续的网络请求等）可能触发过于频繁时，如果对每个事件都进行处理，将会导致大量的计算，可能会降低应用程序的性能或者造成不必要的资源消耗。

为了优化性能和避免这种过度处理，节流技术被用来限制函数在一定时间内的调用频率。通过定义一个时间间隔（例如，每 100 毫秒），无论事件触发多少次，关联的函数只会每隔这个时间间隔执行一次。这样，即使事件源源不断地触发，函数的执行次数也被限制在一个可控的范围内。

节流的效果就像是在流水管道中安装了一个阀门，无论水流多么强劲，通过阀门的水流量都被限制在一定的速率。这个比喻适用于软件开发中的节流，因为无论事件触发的频率多高，执行的频率都被限制在预定的阈值内。

节流在编程中的命名反映了其功能：就像控制液体流速的阀门一样，它在一系列连续的事件中限制了函数调用的频率，保证了资源的合理使用和系统的稳定性。


**案例** 调整浏览器窗口大小（resize）会频繁触发事件，如果每次 resize 事件都要重绘页面数据会导致性能问题，因为浏览器需要处理大量不必要的计算和渲染工作。使用节流可以在调整大小过程中以固定的频率更新布局或执行计算，而不是对每次调整都作出响应。


**代码实现**

```js
// 节流函数
function throttle(func, time = 250) {
  let inThrottle;
  return (args)=> {
    if (!inThrottle) {
      func.apply(this, args);
      inThrottle = true;
      setTimeout(() => inThrottle = false, time);
    }
  };
}
```