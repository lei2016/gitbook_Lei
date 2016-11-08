# 任务24-ajax
#### 问答

1.ajax 是什么？有什么作用？

* Ajax 全称是 ```Asynchronous JavaScript and XML``` ;

* Ajax 作用： JavaScript 可使用她的 ```XMLHttpRequest```对象 来直接与服务器进行异步通信，这样JavaScript可在不重载页面的情况与Web服务器交换数据，然后利用交换的数据修改 DOM 对象，达到无需刷新整个页面，只针对局部进行刷新，会带来良好的用户体验。


2.前后端开发联调需要注意哪些事情？后端接口完成前如何 mock 数据？(npm install -g server-mock) 知识点视频-如何 mock 数据

* 前后端开发联调需要注意事项：

    (1) 约定数据：有哪些需要传输的数据，数据类型是什么；

    (2) 约定接口：确定接口名称及请求和响应的格式，请求的参数名称、响应的数据格式；

    (3)根据这些约定整理成接口文档

* 后端接口完成前mock数据：可以根据接口文档，使用假数据来验证我们制作的页面响应和接口是否正常。可以搭建php本地服务器用，php写脚本提供临时数据；也可使用Mock.js，它能拦截ajax请求并根据请求中的内容来随机生成符合你要求的假数据，模拟后端环境让你完成对页面和接口的测试。



3.点击按钮，使用 ajax 获取数据，如何在数据到来之前防止重复点击?

* 可以加一个状态锁，在触发ajax前先上锁，之后用户再怎么点击都不会触发ajax，直至代码执行完再开锁。
```
var lock = false;
btn.addEventListener("click",function(){
   if(!lock){
       lock = true;
       ajax(XXXX);
       lock = false;
   }
});
```
* [更多方法参考：怎样防止重复发送 Ajax 请求？—知乎](https://www.zhihu.com/question/19805411)


#### 代码

1.封装一个 ajax 函数，能通过如下方式调用
```
function ajax(opts){
    // todo ...
}
document.querySelector('#btn').addEventListener('click', function(){
    ajax({
        url: 'getData.php',   //接口地址
        type: 'get',               // 类型， post 或者 get,
        data: {
            username: 'xiaoming',
            password: 'abcd1234'
        },
        success: function(ret){
            console.log(ret);       // {status: 0}
        },
        error: function(){
           console.log('出错了')
        }
    })
});
```
ajax封装
```
function ajax(opts){
    var xmlhttp =new XMLHttpRequest();
    xmlhttp.onreadystatechange=function(){
    
    if(xmlhttp.readyState == 4 && xmlhttp.status == 200){
    var result =JSON.parse(xmlhttp.responseText);
    opts.success(result);
    }
    if(xmlhttp.readyState == 4 && xmlhttp.status == 404){
    opts.error();
    }
    };
    var tmpArr = [];
    for (var key in opts.data){
    tmpArr.push(key + "=" + opts.data[key]);
    }
    var data = tmpArr.join( '&' );
    
    if(opts.type.toLowerCase() === 'get'){
    xmlhttp.open('get' ,opts.url + '? '+ data);
    xmlhttp.send(null);
    
    }
    
    if(opts.type.toLowerCase() === 'post'){
    xmlhttp.open('get',opts.url);
    xmlhttp.setRequestHeader( 'Content-type' , 'application/x-www-form-urlencoded' );
    xmlhttp.send(data);
    }
}
//document.querySelector( '#btn' ).addEventListener('click', function(){
//   ajax({
//       url: 'getData.php',   //接口地址
//       type: 'get',               // 类型， post 或者 get,
//       data: {
//          username: 'xiaoming',
//          password: 'abcd1234'
// },
//       success: function(ret){
//          console.log(ret);       // {status: 0}
// },
//       error: function(){
//          console.log('出错了')
// }
// });
// });
```
2.实现如下加载更多的功能。

效果如下： http://jrgzuoye.applinzi.com/作业安排/jscode/JS9-jqueryajax/1.html

3.实现注册表单验证功能

效果如下：http://jrgzuoye.applinzi.com/作业安排/jscode/JS7-ajax/3.html
