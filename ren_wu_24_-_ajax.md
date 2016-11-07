# 任务24-ajax
#### 问答

1.ajax 是什么？有什么作用？

2.前后端开发联调需要注意哪些事情？后端接口完成前如何 mock 数据？(npm install -g server-mock) 知识点视频-如何 mock 数据


3.点击按钮，使用 ajax 获取数据，如何在数据到来之前防止重复点击?


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
2.实现如下加载更多的功能。

效果如下： http://jrgzuoye.applinzi.com/作业安排/jscode/JS9-jqueryajax/1.html

3.实现注册表单验证功能

效果如下：http://jrgzuoye.applinzi.com/作业安排/jscode/JS7-ajax/3.html
