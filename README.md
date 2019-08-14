## 节流（throttle）
如果一个函数持续的，频繁地触发，那么让它在一定的时间间隔后再触发。
```
function throttle (fn, delay) {
   let  timer    = null,
        remaining   = 0,
        previous = new Date();

    return function () {
        let now = new Date(),
        remaining = now - previous,
        args = arguments,
        context = this;

        if (remaining >= delay) {
            if (timer) {
                clearTimeout(timer);
            }

            fn.apply(context, args);
            previous = now;
        } else {
            if (!timer) {
                timer = setTimeout(function () {
                    fn.apply(context, args);
                    previous = new Date();
                }, delay - remaining);
            }
        }
    };
}
```

## 消抖（debounce）
如果一个函数持续地触发，那么只在它结束后过一段时间只执行一次。
```
function debounce (fn, delay) {
    let timer   = null;

    return function () {
    let args = arguments;
    let context = this;

        if (timer) {
            clearTimeout(timer);

            timer = setTimeout(function () {
                fn.apply(context, args);
            }, delay);
        } else {
            timer = setTimeout(function () {
                fn.apply(context, args);
            }, delay);
        }
    }
}
```
