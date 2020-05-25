

### document和window调用事件处理程序有不同吗？
> 如果事件目标是window对象或者其他一些单独对象(比如XMLHttpRequest)时，浏览器会简单地调用对象上的处理程序响应事件。<br>

>如果事件目标是文档或者文档元素时，会涉及事件冒泡和事件捕获。<br>

> 发生在文档元素上的大部分事件都会冒泡，例外有focus、blur和scroll事件。
```html
<!DOCTYPE html>
<html lang="en">
<head>
     ……
</head>
<body>
<div id="myDiv">clickMe</div>
</body>
 </html>
```
现代浏览器同时支持事件冒泡和事件捕获。<br>
事件冒泡：div—body—html—Document—window<br>
事件捕获：window—Document—html—body—div<br>

- 使用事件委托，注册在document对象和window对象上效果是一样的<br>
    ```javascript
    // 第三个参数false表示冒泡阶段调用事件处理程序
    window.addEventListener('click',function(){……}，false)
    document.addEventListener('click',function(){……}，false)
    ```
    PS：尽管“DOM2级事件”规范要求事件应该从document对象开始传播，但是目前浏览器都是从window对象开始捕获的。不过规范与浏览器实现不一致也是家常便饭了，也许很久很久以后会统一也说不定。
- load事件<br>
    load事件可以冒泡，但该事件会document对象上停止冒泡，直到页面完全加载，才会触发window上的load事件。所以将load事件绑定在window对象上
    ```javascript
    window.onload=function(){……}
    ```
    PS:同样“DOM2级事件”规范，load事件应该在document上触发，但是所有浏览器都在window上实现了该事件，以确保兼容
- DOMContentLoaded事件<br>
    DOMContentLoaded 事件在页面的html加载和解析完毕后触发
    ```js
    //事件目标是document，所以一般都注册在document上
    document.addEventListener('DOMContentLoaded',function(){
        console.log('something');
    });
    ```




