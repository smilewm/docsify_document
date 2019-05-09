# 异步操作之 Promise 和 Async await 用法进阶

  **首先定义以下三个异步函数：** 
  ```js
  function sleep3000() {
    return new Promise(function (resolve, reject) {
        setTimeout(function () {
            console.log('sleep3000 执行完成');
            resolve(new Date());
        }, 3000);
    })
  };

  function sleep2000() {
      return new Promise(function (resolve, reject) {
          setTimeout(function () {
              console.log('sleep2000 执行完成');
              resolve(new Date());
          }, 2000);
      })
  };
  function sleep4000() {
      return new Promise(function (resolve, reject) {
          setTimeout(function () {
              console.log('sleep4000 执行完成');
              resolve(new Date());
          }, 4000);
      })
  };
  ```  

  1. **使用 `promise` 方法分别执行以上三个函数** 

  ```js  
    console.log('Now：', new Date());

    sleep3000().then((d) => {
        console.log('3000：', d);
    })

    sleep2000().then((d) => {
        console.log('2000：',d);
    })

    sleep4000().then((d) => {
        console.log('2000：',d);
    })

    最终打印结果：

    Now： 2019-04-08T02:29:38.388Z
    sleep2000 执行完成
    2000： 2019-04-08T02:29:40.398Z
    sleep3000 执行完成
    3000： 2019-04-08T02:29:41.398Z
    sleep4000 执行完成
    2000： 2019-04-08T02:29:42.394Z
  ```  

  2. **使用 promise.all() 方法**  

    Promise 的 all() 方法提供了并行执行异步操作的能力，即在所有异步操作执行完后才执行回调， all()里面接收一个数组，数组中每个元素都返回一个 promise 对象。

    all()里面的异步都执行完成后，才会把每个异步结果以数组的形式放入 then 中。

    某些情况下，如果上面sleep3000、sleep200、sleep4000分别代表页面不同模块的加载时间，在页面刚打开时，需要当所有模块加载完成后，清除loading。此时可以作如下处理：

    ```js  
    console.log('Now：', new Date());

    Promise.all([
        sleep2000(),
        sleep3000(),
        sleep4000()
    ]).then((res) => {
        console.log(res)
    })
    最终打印结果：

    Now： 2019-04-08T02:43:07.139Z
    sleep2000 执行完成
    sleep3000 执行完成
    sleep4000 执行完成
    [ 2019-04-08T02:43:09.144Z,
    2019-04-08T02:43:10.145Z,
    2019-04-08T02:43:11.144Z ]
    ```  

    3. **使用 promise.race() 方法**  

       Promise 的 race() 方法 与 all () 相反，即只以执行最快的那个promise为准，一旦race()中的某个promise解决或拒绝，所有返回的 promise就会解决或拒绝。

        ```js   
            console.log('Now：', new Date());

            Promise.race([
                sleep2000(),
                sleep3000(),
                sleep4000()
            ]).then((res) => {
                console.log(res)
            })
        ```
        因为 sleep2000 最先执行完成，所以在2秒后，就会立即进入then。

        最终打印结果：

        ```js
            Now： 2019-04-08T02:44:34.193Z
            sleep2000 执行完成
            2019-04-08T02:44:36.200Z
            sleep3000 执行完成
            sleep4000 执行完成
        ```
        !> `注意：`  
        2秒进入 then 后， sleep3000 和 sleep4000 并没有被停止, 仍会继续走完，只是不会处理resolve或reject。  

        4. **async/await 处理以上三个函数**  

        ```js
        console.log('Now：', new Date());

        async function getDate () {
            let res1 = await sleep3000();
            let res2 = await sleep2000();
            let res3 = await sleep4000();
            console.log('3000：', res1);
            console.log('2000：', res2);
            console.log('4000：', res3);
        }

        getDate();
        最终打印结果：

        Now： 2019-04-08T02:58:23.990Z
        sleep3000 执行完成
        sleep2000 执行完成
        sleep4000 执行完成
        3000： 2019-04-08T02:58:26.996Z
        2000： 2019-04-08T02:58:29.001Z
        4000： 2019-04-08T02:58:33.004Z
        ```  

        通过打印时间，可见，每处理完前一个await，才会处理下一个await，上面所有处理完花费了9秒。

        所以， 只有当处理后面await需要前一个await返回值时，才可以用以上方法。

        5. **async/await 中使用 promise.all 并行处理异步操作**  

        当三个异步相互之间没有关系，需要同时发送时：  
        
        ```js
        console.log('Now：', new Date());

        async function getdate () {
            let res1 = sleep3000();
            let res2 = sleep2000();
            let res3 = sleep4000();
            let res = await Promise.all([res1, res2, res3]);
            console.log(res);
        }

        getdate();
        最终打印结果：

        sleep2000 执行完成
        sleep3000 执行完成
        sleep4000 执行完成
        [ 2019-04-08T03:11:24.280Z,
        2019-04-08T03:11:23.280Z,
        2019-04-08T03:11:25.275Z ]
        ```  
    !>  `注意：`  
        对比 2 和 5 的打印结果，可以看出，二者打印的返回数组里面的顺序是有区别的：  
        * 只用promise.all()时，各个异步是无序的；
        * 在 async/await 中使用 promise.all(), 各个异步是有序的。