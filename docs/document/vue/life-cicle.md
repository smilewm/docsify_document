# vue生命周期
> beforeCreate、created、beforeMount、mounted、beforeUpdate、updated、beforeDestroy、destroyed

- `beforeCreate` : vue中的data和method都无

- `created` : data和method都初始化完，可以使用。 `注意：`此时还没有el选项，挂载阶段还没开始

- `beforeMounte` : 完成了初始化，给vue实例对象添加$el成员，此时代码中的绑定还未替换
< h1>\{\{message\}/}< /h1>  message还未替换

- `mounted` : 完成挂载  < h1>vue挂载< /h1>


- `beforeUpdate和updated` : 当vue发现data中的数据发生了改变，会触发对应组件的重新渲染，先后调用beforeUpdate和updated钩子函数

- `beforeDestroy` : 钩子函数在实例销毁之前调用。在这一步，实例仍然完全可用

- `destroyed` : 钩子函数在Vue 实例销毁后调用。调用后，Vue 实例指示的所有东西都会解绑定，所有的事件监听器会被移除，所有的子实例也会被销毁


!> `因此，初始化部分写在created中，需要进行dom操作的，写在mounted中，`  
`比如：echarts初始化 echart = echarts.init(document.getElementById('id'))`

![](../../_images/vue/vue_live.png)  