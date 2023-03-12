`W3C盒子模型(标准盒子模型)`  
`IE盒子模型(怪异盒子模型)`  


**标准盒子模型**   
元素内容占据的空间由width属性设置，而内容周围的padding和border值是另外计算的，即盒子实际内容的width、height为我们设置的width、height。   

`盒子总宽/高 = width/height + padding + margin + border`  

盒子内容宽高`不包含`padding、border、margin值，`设置的width/height是多少，内容宽高就是多少`   

<div style="color:#38d8f0">box-sizing:content-box;</div>
  
<div class="mt"></div>

**怪异盒子模型**  
width/height属性不是内容的宽高，而是内容、padding和border的总和。  

`盒子的宽高 + padding + border = 我们设置的width/height`  

<div style="color:#38d8f0">box-sizing:border-box;</div>