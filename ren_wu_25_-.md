# 任务25-jquery DOM&事件
#### 问答
1.说说库和框架的区别？

* 库： 是把一些可以复用的方法集中封装到一个 library ，并且提供 API 给使用者调用，由于库的内部已经做了各种底层的封装和各种兼容实现，因此可以调用提供的API接口来实现我们需要的功能，而不需要复杂的代码和加工，因此使代码得到优化，效率提高。

* 框架： 框架相当于一个模板，用来搭建一个项目的最基层的部分，框架内部可以根据不同项目的需要填入不同的内容

2.jquery 能做什么？

* 取得文档中的元素
```
 $('div').find('.className');
 ```
* 修改页面的外观
```
$(this).addClass('active').siblings().removeClass('active');
```
* 改变文档内容
```
$(this).clone.append('.ul-list');
```
* 响应用户的交互性
```
$('#btn').on('click', function() {
  $('.hidden-text').show(1000);
});
```
* 为页面添加动态效果
```
$('btn').on('click', function(){
  $(this).animate({
      width: '+=5px'
  }, 1000);
});
```

3.jquery 对象和 DOM 原生对象有什么区别？如何转化？

**区别：**
* jQuery对象：只能使用jQuery自己的属性和方法，通过jQuery选择器获得目标，  jQuery 对象更像是把 DOM 原生对象用一个类数组的形式包裹起来。
* DOM对象：通过原生 JavaScript 获得目标，只能使用 DOM的属性和方法；

**转化：**

* jQuery -> DOM原生：
```
var btn = $('#btn')[0];
```
* DOM原生 -> jQuery:
```
var navi = document.getElementById('navi');
var $navi = $(navi);
```

4.jquery中如何绑定事件？bind、unbind、delegate、live、on、off都有什么作用？推荐使用哪种？使用on绑定事件使用事件代理的写法？
```
$('#btn').on('click', function() {
    // on中, 第一个参数即事件的类型，类型包括click, mouseover等
    // 第二个参数是一个匿名函数，执行给定的操作
});
```
* bind:
找到给定的元素后，用bind将事件绑定到该元素上。
```
$("#btn").bind('click', function() {
    console.log('bind()');
});
```
* unbind:
unbind和bind正好相反，unbind的将绑定在给定元素上的事件给解绑。解绑后原先在该元素上的事件就会失效。
```
$("#btn").unbind();
```
* delegate:
表示事件的代理。给给定元素绑定事件，基于一个指定的根元素的子集，匹配的元素包括那些目前已经匹配到的元素，也包括那些今后可能匹配到的元素。例如新添加的元素是匹配到的元素，但是用了代理以后，不用给这些新匹配的元素添加事件，而用了代理后它们就已经绑定好了事件。
```
$('ul').delegate('li', 'click', function() {
    console.log($(this).text());
});
```
* live:
给匹配到的元素添加事件，现在匹配到的和将来匹配到都添加事件。但是推荐使用delegate或者on来替代。
```
$('#btn').live('click', function() {
    console.log('clicked');
});
```
* on:
在匹配的元素上绑定事件。
```
$('#btn').on('click', function() {
    console.log('clicked');
});
```
* off:
将元素上的用on()绑定的元素给移除。
```
$('btn').off();
```
**推荐使用on()，这个方法可以将以上的各种事件绑定的方法都替代掉。**
* on绑定事件代理：
```
$('ul').on('click', 'li', function() {
    console.log($(this).text());
});
```



5.jquery 如何展示/隐藏元素？

**展示元素**
* 使用show()
 ```
$('#btn').on('click', function() {
  $('.div1').show(1000); // 1000表示以1000ms的速度显示div
});
```
* 使用fadeIn()
 ```
$('#btn').on('click', function() {
  $('.div1').fadeIn(1000);
});
```
* 使用slideDown()
 ```
$('#btn').on('click', function() {
  $('.div1').slideDown(1000);
});
```
**隐藏元素：**

* 使用hide()
```
$('#btn').on('click', function() {
  $('.div1').hide(1000);
});
```
* 使用fadeOut()
```
$('#btn').on('click', function() {
  $('.div1').fadeOut(1000);
});
```
* 使用slideUp()
```
$('#btn').on('click', function() {
  $('.div1').slideUp(1000);
});
```
**demo演示**


6.jquery 动画如何使用？

```
$("#btn").on('click', function() {
    $('.div1').animate({
        width: "200px", // 宽度变为200px
        height: "200px", // 高度变为200px
        left: "100px", // 向左移动
        opacity: '0' // 透明度变化
    }, 1000) // 持续一秒
    animate() {
        // 多个动画
    }; 
});
```
**demo演示**

7.如何设置和获取元素内部 HTML 内容？如何设置和获取元素内部文本？
* 设置和获取元素内部HTML可以使用.html()。
```
console.log($('.div1').html()); // 获取内部html
$('.div1').html('<p>改变html</p>'); // 改变内部html
```
* 设置和获取元素内部文本可以使用.text()。
```
console.log($('.div1').text()); // 获取内部text
$('.div1').text('改变text'); // 改变内部text值
```
**demo演示**

8.如何设置和获取表单用户输入或者选择的内容？如何设置和获取元素属性？

**获取内容使用val()。**
```
console.log($('.text1').val()); // 获得id为text1的元素的内容
```
**设置和获取元素属性可以使用attr()。**
```
console.log($('.text1').attr('title')); // 获得id为text1的元素的title属性
$('.text1').attr('title', 'input-text'); // 设置id为text1的元素的title属性为input-text
```
**demo演示**