【$(this)与this的区别】
相信很多刚接触JQuery的人，很多都会对$(this)和this的区别模糊不清，那么这两者有什么区别呢？
首先来看看JQuery中的  $()  这个符号，实际上这个符号在JQuery中相当于JQuery（）,即$(this)=jquery();也就是说，这样可以返回一个jquery对象。那么，当你在网页中alert($('#id'));时，会弹出一个[object Object ]，这个object对象，也就是jquery对象了。
那么，我们再回过头来说$(this)，这个this是什么呢？假设我们有如下的代码：
```
$("#desktop a img").each(function(index){
          alert($(this));
          alert(this);
}
```
那么，这时候可以看出来：
alert($(this));  弹出的结果是[object Object ]
alert(this);        弹出来的是[object HTMLImageElement]
也就是说，后者返回的是一个html对象(本例中是遍历HTML的img对象，所以为 HTMLImageElement)。很多人在使用jquery的时候，经常this.attr('src');   这时会报错“对象不支持此属性或方法”，这又是为什么呢？其实看明白上面的例子，就知道错在哪里了：
很简单，this操作的是HTML对象，那么，HTML对象中怎么会有val()方法了，所以，在使用中，我们不能直接用this来直接调用jquery的方法或者属性。

【prop与attr的区别】
今天在用JQuery的时候发现一个问题用.attr("checked")获取checkbox的checked属性时选中的时候可以取到值,值为"checked"但没选中获取值就是undefined.
为什么jquery 1.6+增加了.prop()方法，因为在有些浏览器中比如说只要写disabled，checked就可以了，而有的要写成disabled ="disabled"，checked="checked"。所以，从1.6开始，jq提供新的方法“prop”来获取这些属性。
 以前我们使用attr获取checked属性时返回"checked"和"",现在使用prop方法获取属性则统一返回true和false。
看些例子
```
<input type="checkbox"id="test" abc="111" />
$(function(){ 
el = $("#test"); 
console.log(el.attr("style")); //undefined 
console.log(el.prop("style")); //CSSStyleDeclaration对象 
console.log(document.getElementById("test").style);//CSSStyleDeclaration对象 
});
el.attr(“style”)输出undefined，因为attr是获取的这个对象属性节点的值，很显然此时没有这个属性节点，自然输出undefinedel.prop(“style”)输出CSSStyleDeclaration对象，对于一个DOM对象，是具有原生的style对象属性的，所以输出了style对象至于document.getElementById(“test”).style和上面那条一样
接着看：
el.attr("abc","111") 
console.log(el.attr("abc")); //111 
console.log(el.prop("abc")); //undefined
首先用attr方法给这个对象添加abc节点属性，值为111，可以看到html的结构也变了
el.attr(“abc”)输出结果为111，再正常不过了el.prop(“abc”)输出undefined，因为abc是在这个的属性节点中，所以通过prop是取不到的
el.prop("abc", "222"); 
console.log(el.attr("abc")); //111 
console.log(el.prop("abc")); //222
```
我们再用prop方法给这个对象设置了abc属性，值为222，可以看到html的结构是没有变化的。输出的结果就不解释了。
上面已经把原理讲清楚了，什么时候用什么就可以自己把握了。
提一下，在遇到要获取或设置checked,selected,readonly和disabled等属性时，用prop方法显然更好，比如像下面这样：
```
<input type="checkbox"id="test" checked="checked"/>console.log(el.attr("checked")); //checked 
console.log(el.prop("checked")); //true 
console.log(el.attr("disabled")); //undefined 
console.log(el.prop("disabled")); //false
```
显然，布尔值比字符串值让接下来的处理更合理。
PS一下，如果你有JS性能洁癖的话，显然prop的性能更高，因为attr需要访问DOM属性节点，访问DOM是最耗时的。这种情况适用于多选项全选和反选的情况。
大家都知道有的浏览器只要写disabled，checked就可以了，而有的要写成disabled ="disabled"，checked="checked"，比如用attr("checked")获取checkbox的checked属性时选中的时候可以取到值,值为"checked"但没选中获取值就是undefined
jq提供新的方法“prop”来获取这些属性，就是来解决这个问题的，以前我们使用attr获取checked属性时返回"checked"和"",现在使用prop方法获取属性则统一返回true和false。
那么，什么时候使用attr，什么时候使用prop？？
1.添加属性名称该属性就会生效应该使用prop.
2.是有true,false两个属性使用prop.
3.其他则使用attr

用data()获取id的值
```
<a href="javascript:;" class="active J_menuTab" data-id="/travelQRC/qr/basic">首页</a>
alert($(".J_menuTab").data("id"));
```
$(selector).each(function(index,element))
index - 选择器的 index 位置
element - 当前的元素（也可使用 "this" 选择器）

on() 和 click() 的区别:
二者在绑定静态控件时没有区别，但是如果面对动态产生的控件，只有 on() 能成功的绑定到动态控件中。
以下实例中原先的 HTML 元素点击其身后的 Delete 按钮就会被删除。而动态添加的 HTML 元素，使用 click() 这种写法，点击 Delete 按钮无法删除；使用 On() 方式可以。
http://www.runoob.com/jquery/event-on.html

window.location 对象所包含的属性
属性	描述
hash	从井号 (#) 开始的 URL（锚）
host	主机名和当前 URL 的端口号
hostname	当前 URL 的主机名
href	完整的 URL
pathname	当前 URL 的路径部分
port	当前 URL 的端口号
protocol	当前 URL 的协议
search	从问号 (?) 开始的 URL（查询部分）

jquery off() 方法通常用于移除通过 on() 方法添加的事件处理程序。

要注意页面加载顺序！！！

js对象要转成jquery对象才能用jquery的方法

label:点击文本标记之一，就可以触发相关控件

$( " li " ).map( function(  ){
        return  $(this).text(  );   
    } ).get(  ).join("%")   
map()之后还不是真正的数组，要get()一下	

不让浏览器缓存的方法：在src后面加个时间，这样缓存就不起作用了

jcaptcha验证码实现：https://blog.csdn.net/qdqht2009/article/details/50246357

连接mysql要记得安装connector/J，在musql连接的properties里

不是行高line-height与文字高height一样就能让文字居中，而是应该这样理解，字符本来就在行高内垂直居中了，只是行高与文字的盒子高度不等，导致不能在盒子里垂直居中，如果我们把行高line-height与盒子的height设置为一样大，意思就是行高的平行线与盒子的上下边重合了，这时字符当然仍是在行高内垂直居中，但也顺便在盒子内垂直居中。

$('input[name="onecheck"]:not(:checked)')选择未选中的

left是配合position:absolute;用的,当块级元素赋予position:absolute;属性后,left就是相对第一个position:relative;的父层而言的.

复制到剪贴板
```
<script type="text/javascript">
function copyUrl2(){
var Url2=document.getElementById("biao1");
Url2.select(); // 选择对象
document.execCommand("Copy"); // 执行浏览器复制命令
}
</script>
<textarea cols="20" rows="10" id="biao1">用户定义的代码区域</textarea>
<input type="button" onClick="copyUrl2()" value="点击复制代码" />
```