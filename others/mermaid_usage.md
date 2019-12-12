# 使用mermaid
## 安装
- npm或者yarn安装  `yarn add mermaid`/`npm i mermaid `
- CDN--<https://unpkg.com/mermaid/>
## 第一个demo
1、使用script标签引入mermaid框架  
2、在页面中定义图形
```javascript
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8">
</head>
<body>
  <div class="mermaid">
  graph LR
      A --- B
      B-->C[fa:fa-ban forbidden]
      B-->D(fa:fa-spinner);
  </div>
  <script src="./lib/mermaid.min.js"></script>
  <script>mermaid.initialize({startOnLoad:true});</script>
</body>
</html>
```
3、mermaid加载并初始化之后，会寻找网页中`class="mermaid"`的元素，转换为svg图表形式。结果类似下面，id是自动添加的
```javascript
<div class="mermaid" id="mermaidChart0">
    <svg>
        Chart ends up here
    </svg>
</div>
```
4、打开网页，我们就开始了奇幻之旅（不截图了，github总有图片显示不了的问题，动手试试吧）
### 安全选项
securityLevel选项默认是true,禁止点击功能。
```javascript
 mermaidAPI.initialize({
        securityLevel: 'loose'
    });
```
### 注意事项
如果你通过CSS动态加载字体，如谷歌字体，美人鱼应该等待整个页面加载(dom +资产，特别是字体文件)。initialize需要类似下面这样初始化
```javascript
$(document).load(function() {
    mermaid.initialize();
});
```
或者
```javascript
$(document).ready(function() {
    mermaid.initialize();
});
```
### mermaid.init
在页面初始化完成之后，如果再增加图或者需要自己更详细的设置，可以使用
```javascript
mermaid.init({noteMargin: 10}, ".someOtherClass");
```
或者
```javascript
mermaid.init(undefined, $("#someId .yetAnotherClass"));
```
## webpack中使用mermaid
官网提供的[demo](https://github.com/mermaidjs/mermaid-webpack-demo)



