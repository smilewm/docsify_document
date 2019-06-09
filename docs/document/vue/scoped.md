# scoped

## scoped 的作用

防止组件间样式污染，添加 scoped，样式只作用在当前组件范围。

```css
  <style lang="scss" scoped>

  </style>
```

!>`添加 scoped 后，无法修改引入的第三方组件样式，比如修改 element-ui 中 el-input 的样式.`

## scoped 中修改第三方组件样式

```css
<style lang="scss" scoped>
  /deep/ .el-input{
    width: 200px;
  }
  /**或者*/
  .el-input::deep{
    width: 200px;
  }
</style>
```
