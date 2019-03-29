## 数组克隆  
   
  a1 = [1,2,3];
 - const a2 = a1.concat();  
 - const a2 = JSON.parse(JSON.stringify(a1));
 - const a2 = [...a1];
 - const [...a2] = a1;  

## 数组合并  

  var arr1 = ['a','b','c','d'];  
  var arr2 = ['d'];  
  var arr3 = ['e','f'];  
- var cc = arr1.concat(arr2,arr3);  
- var cc = [...arr1, ...arr2, ...arr3];  

console.log(cc);//["a", "b", "c", "d", "d", "e", "f"]  

## 数组去重  

const newArr = Array.from(new Set(arr));