### link与@import对比

- link属于HTML标签，而@import是CSS提供的

- 页面被加载时，link会同时被加载，而@import引用的css会等到页面被加载完再加载

- link方式的样式的权重高于@import的权重

### 语法  
```html
<link rel="stylesheet" href="xxx.css" />
```

```css
@import url('xxx.css')  
// 或
@import 'xxx.css'
```

### 优先级  
内联样式优先级最高，如style=""；id选择器优先级高于css|伪类|属性等选择器；其次是标签|伪元素选择器。  

内联 > css|伪类|属性 > 标签|伪元素