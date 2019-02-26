
[debouncing和throttling](https://css-tricks.com/debouncing-throttling-explained-examples/)

Debounce是去抖动，在指定时间内某个事件触发多次，但是去抖动后只执行一次，可以指定是前或者后执行。

Throttle是节流操作，限制某个函数在指定时间内执行多次。

`requestAnimationFrame`也是一种限制函数执行频率的方式，类似`_.throttle(dosomething, 16)`。