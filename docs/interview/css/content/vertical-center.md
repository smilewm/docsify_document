```html
<div class="view">
  <div class="item">子模块</div>
</div>
```  

1. transform  
```css
.view{
  position: relative;
}
.item{
  position: absolute;
  top:50%;
  left:50%;
  transform: translate(-50%,-50%);
}
```  

2. 已知宽高  
```css
.view{
  position: relative;
}
.item{
  position: absolute;
  width: 200px;
  height: 200px;
  top: 50%;
  left: 50%;
  margin: -100px 0 0 -100px;
}
```  

3. flex  
```css
.view{
  width: 200px;
  height: 200px;
  display: flex;
  align-items: center;
  justify-content: center;
}
```