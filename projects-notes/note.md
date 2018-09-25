
输入yum install lrzsz下载上传下载文件

classpath：只会到你的class路径中查找文件;
classpath*：不仅包含class路径，还包括jar文件中(class路径)进行查找。

lib和classes同属classpath，两者的访问优先级为: lib>classes。

用sqlSessionFactoryBeanName 后处理，防止dataSource还没加载配置文件

@Resource默认按照名称方式进行bean匹配，@Autowired默认按照类型方式进行bean匹配
@Resource(import javax.annotation.Resource;)是J2EE的注解，
@Autowired(import org.springframework.beans.factory.annotation.Autowired;)是Spring的注解
有多个的话，使用的@Autowired注解，要配上@Qualifier("manImpl")

date.getTime()可以获取long值

1.对对象的统一管理
2.规范的生命周期
3.aop

连接数据库出现权限异常

1.创建数据库
create database test;

2.远程连接数据库时报错：
The specified user/password combination is rejected: 

[28000][1045] Access denied for user 'test'@'%' (using password: YES)

创建完数据库后,用户需要授权.

3.授权命令
grant all on test.* to 'test'@'%' identified by '123456' with grant option;
第一个test是数据库名,第二个test是账户名,123456是密码.
	
Cannot instantiate object of type org.mybatis.generator.plugins.page.PaginationPlugin


JedisConnectionException: java.net.ConnectException: Connection refused
	bind的问题. 把Redis的配置文件redis.conf里
		#bind localhost 	注释掉它.
	注释掉本机,局域网内的所有计算机都能访问.
	band localhost   只能本机访问,局域网内计算机不能访问
	bind  局域网IP    只能局域网内IP的机器访问, 本地localhost都无法访问.
	
			#bind localhost
还要记得把	protected-mode改成 no  !!!!

mybatis的逆向工程时，数据库中的longtext和tinyint(0-255)要手动改成String和Integer，不然会不显示和变成Boolean

(function(){})表示一个匿名函数。function(arg){...}定义了一个参数为arg的匿名函数，然后使用(function(arg){...})(param)来调用这个匿名函数。其中param是传入这个匿名函数的参数。
需要注意与$(function(){})的区别：$(function(){}) 是 $(document).ready(function(){}) 的简写，用来在DOM加载完成之后执行一系列预先定义好的函数。
	
```
$(selector).get(url,data,success(response,status,xhr),dataType)
等同于	$.ajax({
		  url: url,
		  data: data,
		  success: success,
		  dataType: dataType
		});	
```
script不能写成自闭的形式
```
<script/>
	<!ELEMENT img EMPTY>
	<!ATTLIST img   %attrs;
	  src %URI; #REQUIRED
	  alt %Text; #REQUIRED
	  longdesc %URI; #IMPLIED
	  height %Length; #IMPLIED
	  width %Length; #IMPLIED
	  usemap %URI; #IMPLIED
	  ismap (ismap) #IMPLIED
	  >
	这是 img 标签的定义。 ELEMENT 关键字说明它是一个元素， EMPTY 关键字说明它的内容必须是空白。因此，我们可以使用自关闭形式：
	<img src="image.png" alt="some image" />
	留意 ATTLIST 里面声明了两个属性是 #REQUIRED 的，所以必须提供。

	接下来我们再看看 script 标签的定义：
	<!ELEMENT script (#PCDATA)>
	<!ATTLIST script
	  id ID #IMPLIED
	  charset %Charset; #IMPLIED
	  type %ContentType; #REQUIRED
	  language CDATA #IMPLIED
	  src %URI; #IMPLIED
	  defer (defer) #IMPLIED
	  xml:space (preserve) #FIXED 'preserve'
	  >
	可以看到 script 标签通过 (#PCDATA) 声明了它的内部允许包含 CDATA 数据，因此它不是一个带 EMPTY 关键字的标签，也就不可能使用自关闭的写法。	
```
搜索框居中：通过col-md-offset-3前移	
```
	<div class="input-group col-xs-6  col-md-offset-3">
			<input type="text" class="form-control " placeholder="Search for...">
		<span class="input-group-btn">
			<button class="btn btn-default" type="button">Go!</button>
		</span>	
	</div>
```
mybatis中生成的表分包后，记得改spring-dao.xml中的mapper映射的配置	

<c:forEach var="sk" items="${list}">记得list也要加el表达式！！！

Cannot build Artifact 'XXX:war exploded' because it is included into a circular dependency
rebuild project     build artifacts

热部署:
	第1种：修改服务器配置，使得IDEA窗口失去焦点时，更新类和资源
		菜单Run -> EditConfiguration , 然后配置指定服务器下，右侧server标签下on frame deactivation = Update classes and resource。
	第2种：使用springloaded jar包
		a. 下载jar包，github：https://github.com/spring-projects/spring-loaded
		b. 启动应用时添加VM启动参数：-javaagent:/home/lkqm/.m2/repository/org/springframework/springloaded/1.2.7.RELEASE/springloaded-1.2.7.RELEASE.jar -noverify
	第3种：使用spring-boot-devtools提供的开发者工具
		spring-boot项目中引入如下依赖
		<dependency>
				<groupId>org.springframework.boot</groupId>
				<artifactId>spring-boot-devtools</artifactId>
		 </dependency>
	第4种：使用Jrebel插件实现热部署(该插件14天免费试用)
		在线安装：菜单File -> Setting -> Plugin, 点击右侧底部 Browse repositories, 弹出框顶部输入:JReble for Intellij， 选中安装即可。
	IDEA开启项目自动编译，进入设置，Build,Execut, Deployment -> Compiler 勾选中左侧的Build Project automatically
	IDEA开启项目运行时自动make, ctrl + shift + a搜索命令：registry -> 勾选compiler.automake.allow.when.app.running

搜索查询时：入参为：名称，其他条件（如是否可用），页号
			返回值为：分页对象（结果集，分页（当前页，每页条数，总条数））

pagination里面有个cpn静态方法，如果传入的数是小于等于0，就返回1		
pagination的构造函数参数（pageNo,pageSize,totalCount），
productQueryDto中的pageRow只有在查结果集的时候有用，是做出来方便计算，省的拿到sql中计算

分页回显的时候：pagination中的方法pageView(url，params)传入跳转的地址和参数值
	
搜索用模糊查询 ：name like "%" #{name} "%"

mybatis 的<when>中and写在前面

mybatis如果是类的话就不用把这个类的名字写在#{}中了，直接写它的变量就行了

COUNT(1)这两个中间不能有空格

传到controller层的参数要记得回显

<nav style="text-align: center">组件居中的方法

1.如果只要提交在表单中信息，直接表单action地址，method就行，获取的值就是各个元素的name的值
2.要提交表单外的东西，要写一个函数，拼接地址和参数
```
function submit_a(){
    //获取用户输入的值
    var username = document.getElementById("id_user").value;
    var password = document.getElementById("id_pwd").value;
    //拼接url
    var url = "servlet/TestServlet?";
    url += "username="+username+"&password="+password;
    //重新定位url
    window.location = url;//$.get(url);
}
```
3.也可以直接在a href=""中加入地址和参数

web.xml过滤器解决post乱码问题
	<filter>
		<filter-name>encoding</filter-name>
		<filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
		<init-param>
			<param-name>encoding</param-name>
			<param-value>UTF-8</param-value>
		</init-param>
	</filter>
	<filter-mapping>
		<filter-name>encoding</filter-name>
		<url-pattern>/*</url-pattern>
	</filter-mapping>
	
js的常用简写：	
```
	var car = new Object();
	car.colour = 'red';
	car.wheels = 4;
	car.hubcaps = 'spinning';
	car.age = 4;	
	
	var car = {
    colour:'red',
    wheels:4,
    hubcaps:'spinning',
    age:4
	}
```
$("#aa").click(function() {})   而click传入一个参数表示执行click函数
$("#aa").onclick=function(){}	
	click方法 是jQuery实现的方法，为$("#aa")检索到的元素绑定click事件；
	而onclick是js原生的click事件绑定，即使没有加载jQuery库也可以使用。
	需要注意的是：
	$('#aa')返回的是一个包含符合条件的dom的数组，click() 可以为数组中的多个元素（有些选择器可能会返回多个匹配结果）绑定click事件（即，隐式遍历）。
	onclick只能给一个dom元素绑定click事件，所以$("#aa").onclick=function(){}这样的写法会报错，改成 $("#aa").get(0).onclick=function(){} 即表示从jQuery结果集中取出第一个元素为其绑定click事件
	
第一种：$("#click").click(function(){       
　　　　　　alert("Hello World  click");  
  　　});

第二种：$('#clickon').on('click', function(){  
 　　　　alert("Hello World  on");  
　　　　}); 

第三种：$('#clickbind').bind("click", function(){  
 　　　　alert("Hello World  bind");  
　　　　});	
第四种：btn.onclick = function() { （这种多个会覆盖之前的）
		alert(1);
		} 

想要传一些表单没有的信息，可以用type="hidden"增加表单内容
<input type="hidden" id="hiddenid" value="${product.id}">
<input type="hidden" id="hiddenPic" value="${product.imgUrl}"/>		
		
把想要传的值都放在表单里，不想显示的用hidden藏起来，设置多个button按钮，onclick设置函数，这样就可以实现一个表单向不同地址发送，而且不需要去其他地方取值。
input内可以用onchange=一个函数，函数里面用ajaxSubmit
ajaxSubmit，提交后页面不刷新，有返回值:		function pictureUpload() {
												var params ={
												   url : "/editGoods/uploadPic",
												   dataType:"json",
												   type : "post",
												   success : function (data) {
													   $("#hiddenpic").val(data.url);
													   $("#pic").atrr("src",data.url);
												   }
												}
												$("#javaForm").ajaxSubmit(params);
											}

普通submit，提交后就不管了，页面刷新：		function pictureUpload() {
												$("#javaForm").attr("action","servlet/TestServlet");
												$("#javaForm").attr("method","post");
												$("#javaForm").submit();	
											}
		
这里面详细列出了表单提交的方法：https://blog.csdn.net/qq_20128967/article/details/52847518?locationNum=8&fps=1
	
如果ajax返回了地址？
如果普通submit没有返回地址？

pringmvc图片上传
用这个来实现图片上传： 	引入两个jar包	commons-fileupload-1.2.2.jar
										commons-io-2.4.jar
在springmvc.xml配置文件中配置插件	<bean id="multipartResolver" class="org.springframework.web.multipart.commons.CommonsMultipartResolver">
要设置最大上传大小，不然会出错			<property name="maxUploadSize">
											<value>5242880</value>
										</property>
									</bean>
					

hadoop创建文件的时候出现权限拒绝，hadoop fs -chmod 777 /user/a的方法更改要添加文件的文件夹的权限

看test的时候要注意有没有before和after

用multipartfile上传图片的方法:	<form action="fileUpload" method="post" enctype="multipart/form-data">
									选择文件:<input type="file" name="file">
									<input type="submit" value="提交">
								</form>
form中记得加入一个属性enctype="multipart/form-data"	

上传图片过程：点击file后，触发onchange()，把图片传输到文件服务器，返回地址，地址被重新写入<input><imag>里面，点提交后将地址存到数据库

写jason可以用JSONObject来弄，在org.json包里		JSONObject jo = new JSONObject();
												jo.put("url",url);
												response.setContentType("application/json;charset=UTF-8");
												response.getwriter().write(jo.toString());
如果要放对象，那个对象应该重写toString()方法								
								
图片回显：	
```
function pictureUpload() {
    var params ={
       url : "/editGoods/uploadPic",
       dataType:"json",
       type : "post",
       success : function (data) {
           $("#hiddenpic").val(data.url);
           $("#pic").attr("src",data.url);
       }
    }
    $("#javaForm").ajaxSubmit(params);
}
```
Controller方法的返回值可以有以下几种：
1、返回ModelAndView
返回ModelAndView时最常见的一种返回结果。需要在方法结束的时候定义一个ModelAndView对象，并对Model和View分别进行设置。
2、返回String
1）：字符串代表逻辑视图名
真实的访问路径=“前缀”+逻辑视图名+“后缀”
注意：如果返回的String代表逻辑视图名的话，那么Model的返回方式如下：
public String testController(Model model){
model.addAttribute(attrName,attrValue);//相当于ModelAndView的addObject方法
return "逻辑视图名";
   }
2）：代表redirect重定向
redirect的特点和servlet一样，使用redirect进行重定向那么地址栏中的URL会发生变化，同时不会携带上一次的request
案例：
public String testController(Model model){
return "redirect:path";//path代表重定向的地址
}
3）：代表forward转发
通过forward进行转发，地址栏中的URL不会发生改变，同时会将上一次的request携带到写一次请求中去
案例：
public String testController(Model model){
return "forward:path";//path代表转发的地址
}
3、返回void
返回这种结果的时候可以在Controller方法的形参中定义HTTPServletRequest和HTTPServletResponse对象进行请求的接收和响应
1）使用request转发页面
  request.getRequestDispatcher("转发路径").forward(request,response);
2）使用response进行页面重定向
  response.sendRedirect("重定向路径");
3）也可以使用response指定响应结果
  response.setCharacterEncoding("UTF-8");
  response.setContentType("application/json;charset=utf-8");
  response.getWriter.write("json串");
  
JSONObject jo = new JSONObject();  
jo.put("url",url);
response.setContentType("application/json;charset=UTF-8");
response.getwriter().write(jo.toString);
返回void和返回对象(加responseBody)是一样的  


如果你想保留request范围内的数据,那么就需要用转发,如果你不想保留request范围内的数据和请求参数,那么可以重定向.
转发是服务器内部跳转，数据不会丢失，浏览器只提交了一次请求
重定向是客户端二次跳转，数据会丢失，浏览器提交了二次请求
做增、删、改的时候最好用重定向，因为如果不用重定向，每次刷新页面就相当于再请求一次，就可能会做额外的操作，导致数据不对。

弹框是否确定onclick="if(!confirm('您确定删除吗？')) {return false;}

批量删除：一个表单里有多个一样的值，后台接收的是这个类型的数组
parameterType如果是数组或者list等集合，只要写泛型就行

mybatis逆向工程实现分页的插件：https://blog.csdn.net/weixin_35891116/article/details/53734795

file属性加一个multiple="multiple"可以支持批量选文件
同时contrller层得到数组，for循环遍历上传图片

solr搭建的时候有显示需要solr.xml文件，如下配置
	<solr>
	<solrcloud>
	<str name="host">${host:}</str>
	<int name="hostPort">${jetty.port:8983}</int>
	<str name="hostContext">${hostContext:solr}</str>
	<int name="zkClientTimeout">${zkClientTimeout:15000}</int>
	<bool name="genericCoreNodeNames">${genericCoreNodeNames:true}</bool>
	</solrcloud>
	<shardHandlerFactory name="shardHandlerFactory"
	class="HttpShardHandlerFactory">
	<int name="socketTimeout">${socketTimeout:0}</int>
	<int name="connTimeout">${connTimeout:0}</int>
	</shardHandlerFactory>
	</solr>

cp solr-4.10.3.war /usr/share/tomcat/webapps/solr.war 

当我们不知道前端传来的图片的名字时，可以强转request为multipartRequest
							MultipartRequest mr = (MultipartRequest)request;
							Map<String,MultipartRequest> mrmap = mr.getFileMap();再遍历
							
传到数据库里的图片是<imag scr="...." /><imag scr="...." />				

Available parameters are [0, 1, param1, param2]是因为mapper中的参数对不上

获取cookie中id的方法
```
document.cookie="userId=828"; 
document.cookie="userName=hulk"; 
//获取cookie字符串 
var strCookie=document.cookie; 
//将多cookie切割为多个名/值对 
var arrCookie=strCookie.split("; "); 
var userId; 
//遍历cookie数组，处理每个cookie对 
for(var i=0;i<arrCookie.length;i++){ 
var arr=arrCookie[i].split("="); 
//找到名称为userId的cookie，并返回它的值 
if("userId"==arr[0]){ 
userId=arr[1]; 
break; 
} 
} 
alert(userId); 
```
有了request和response就可以让后台来自己取cookie	
	设置cookie要记得设置它的路径
	Cookie cookie = new Cookie("zjuUserName",userName);
	cookie.setPath("/");
	response.addCookie(cookie);
	
重定向不能携带中文，应该提前对它进行转义,encodeURIComponent() 函数可把字符串作为 URI 组件进行编码。
encodeURIComponent(window.location.href)
最后return "redirect:"+returnUrl;

json改成jsonp就实现跨域，再多传一个String callback，再把callback送回去，
			MappingJacksonValue  mjv = new MappingJacksonValue(result);
			mjv.setJsonpFunction(callback);
			
this.form.submit()直接提交这个表单

只显示一张图片，传过来的是数组，如果要显示多张就遍历一下
<img width="50" height="50" src="${product.images[0]}"/></td>

如果要显示多张图片，数据库里的imgUrl是以逗号隔开，就在bean里面多设一个String[] images的项
productProduct.setImages(productProduct.getImgUrl().split(","));(注意排除为空的可能)
jsp页面显示：	
```
<c:forEach items="${pagination.list}" var="product">
    <td align="center" class="">${product.id}</td>
    <c:forEach items="${product.images}" var="image">
        <img width="40" height="40" src="${image}"/>
    </c:forEach>
    <td align="center">${product.name}</td>
</c:forEach>
```
//判断用户是否登陆 
```
$(function(){
    $.ajax({
        url : "/login/singleLogin",
        type : "post",
        dataType : "json",
        success : function(data){
            if(data.result == 1){
                $("#login").hide();
                $("#regist").hide();
            }else{
                $("#logout").hide();
                $("#myOrder").hide();
            }
        }
    });
})	
```
		
普通提交时：无非就是用表单和不用表单		
选择地址的方式：href ,表单的action,document.getElementById('').action=
传参的方式：表单,问号接在后面,ajax时多一项data:{"id":id}		

ajax时：（后面三种貌似比较好）

```
$.ajax(对象) 	$.get('url',{' ': , ' ' : },function(data){})	$.post('url',{' ': , ' ' : },function(data){})	 $("#tf").ajaxSubmit(对象);
	$.ajax({  
        type:'post',      
        url:'Notice_noTipsNotice',  
        data:'k1=v1&k2=v2...',    
        dataType:'json',  
        success:function(data){  
        }  
    });  
```

```
<script>  
	//设置cookie  
	function setCookie(cname, cvalue, exdays) {  
		var d = new Date();  
		d.setTime(d.getTime() + (exdays*24*60*60*1000));  
		var expires = "expires="+d.toUTCString();  
		document.cookie = cname + "=" + cvalue + "; " + expires;  
	}  
	//获取cookie  
	function getCookie(cname) {  
		var name = cname + "=";  
		var ca = document.cookie.split(';');  
		for(var i=0; i<ca.length; i++) {  
			var c = ca[i];  
			while (c.charAt(0)==' ') c = c.substring(1);  
			if (c.indexOf(name) != -1) return c.substring(name.length, c.length);  
		}  
		return "";  
	}  
	//清除cookie    
	function clearCookie(name) {    
		setCookie(name, "", -1);    
	}    
	function checkCookie() {  
		var user = getCookie("username");  
		if (user != "") {  
			alert("Welcome again " + user);  
		} else {  
			user = prompt("Please enter your name:", "");  
			if (user != "" && user != null) {  
				setCookie("username", user, 365);  
			}  
		}  
	}  
	checkCookie();   
</script>  
```

window.prompt参数,有两个, 
第一个参数,显示提示输入框的信息. 
第二个参数,用于显示输入框的默认值. 
返回,用户输入的值.

mybatis里要写INTEGER不能写INT

上传多张图片加一个multiple="multiple"就可以了

img中的标签src的地址是以webapp为根目录开始的

```
<dependency>
	<groupId>net.sf.json-lib</groupId>
	<artifactId>json-lib</artifactId>
	<version>2.4</version>
	<classifier>jdk15</classifier>
</dependency>
```

对象转成json

```
public static void convertObject() {
    Student stu=new Student();
    stu.setName("JSON");
    stu.setAge("23");
    stu.setAddress("北京市西城区");
    //1、使用JSONObject
    JSONObject json = JSONObject.fromObject(stu);
    //2、使用JSONArray
    JSONArray array=JSONArray.fromObject(stu);
    String strJson=json.toString();
    String strArray=array.toString();
    System.out.println("strJson:"+strJson);
    System.out.println("strArray:"+strArray);
}
```
json转成对象	
```
public static void jsonStrToJava(){
    //定义两种不同格式的字符串
    String objectStr="{\"name\":\"JSON\",\"age\":\"24\",\"address\":\"北京市西城区\"}";
    String arrayStr="[{\"name\":\"JSON\",\"age\":\"24\",\"address\":\"北京市西城区\"}]";
    //1、使用JSONObject
    JSONObject jsonObject=JSONObject.fromObject(objectStr);
    Student stu=(Student)JSONObject.toBean(jsonObject, Student.class);
    //2、使用JSONArray
    JSONArray jsonArray=JSONArray.fromObject(arrayStr);
    //获得jsonArray的第一个元素
    Object o=jsonArray.get(0);
    JSONObject jsonObject2=JSONObject.fromObject(o);
    Student stu2=(Student)JSONObject.toBean(jsonObject2, Student.class);
    System.out.println("stu:"+stu);
    System.out.println("stu2:"+stu2);
}	
```
style="display: none"可以隐藏标签

先写一个span，后面再来输入内容
<span id="killPhoneMessage" class="glyphicon"> </span>
$('#killPhoneMessage').hide().html('<label class="label label-danger">手机号错误!</label>').show(300);
html()会将内容改为样式后输出
$("p").text("Hello <b>world!</b>");会将内容直接输出，Hello <b>world!</b>，没用

innerHtml 打印标签之间的内容，包括标签和文本信息
innerText 打印标签之间的纯文本信息，会将标签过滤掉

解决高qps的方法：静态资源用cdn保存，非静态不常变的用redis存（如开始时间，结束时间），常变化的用mysql（如库存）
事务可以用mysql存储过程

redis分布式锁：https://www.cnblogs.com/linjiqin/p/8003838.html
加锁：
```
public class RedisTool {
    private static final String LOCK_SUCCESS = "OK";
    private static final String SET_IF_NOT_EXIST = "NX";
    private static final String SET_WITH_EXPIRE_TIME = "PX";
    /**
     * 尝试获取分布式锁
     * @param jedis Redis客户端
     * @param lockKey 锁
     * @param requestId 请求标识
     * @param expireTime 超期时间
     * @return 是否获取成功
     */
    public static boolean tryGetDistributedLock(Jedis jedis, String lockKey, String requestId, int expireTime) {
        String result = jedis.set(lockKey, requestId, SET_IF_NOT_EXIST, SET_WITH_EXPIRE_TIME, expireTime);//必须一句话搞定，保证原子性
        if (LOCK_SUCCESS.equals(result)) {
            return true;
        }
        return false;
    }
}
```
解锁：
```
public class RedisTool {
    private static final Long RELEASE_SUCCESS = 1L;
    /**
     * 释放分布式锁
     * @param jedis Redis客户端
     * @param lockKey 锁
     * @param requestId 请求标识
     * @return 是否释放成功
     */
    public static boolean releaseDistributedLock(Jedis jedis, String lockKey, String requestId) {
        String script = "if redis.call('get', KEYS[1]) == ARGV[1] then return redis.call('del', KEYS[1]) else return 0 end";
        Object result = jedis.eval(script, Collections.singletonList(lockKey), Collections.singletonList(requestId));//eval方法把语句传给redis服务器执行，并使参数KEYS[1]赋值为lockKey，ARGV[1]赋值为requestId
        if (RELEASE_SUCCESS.equals(result)) {
            return true;
        }
        return false;
    }
}
```
	
错误示例2：
```
public static void wrongReleaseLock2(Jedis jedis, String lockKey, String requestId) {
    // 判断加锁与解锁是不是同一个客户端
    if (requestId.equals(jedis.get(lockKey))) {
        // 若在此时，这把锁突然不是这个客户端的，则会误解锁
        jedis.del(lockKey);
    }
}
```
如代码注释，问题在于如果调用jedis.del()方法的时候，这把锁已经不属于当前客户端的时候会解除他人加的锁。那么是否真的有这种场景？答案是肯定的，比如客户端A加锁，一段时间之后客户端A解锁，在执行jedis.del()之前，锁突然过期了，此时客户端B尝试加锁成功，然后客户端A再执行del()方法，则将客户端B的锁给解除了。
	
Spring缓存注解@Cacheable(第一次执行，后面就往缓存里取)、@CacheEvict(执行完就把它删了)、@CachePut(每次都往里存)	

当你的redis数据库里面本来存的是字符串数据或者你要存取的数据就是字符串类型数据的时候，那么你就使用StringRedisTemplate即可，
但是如果你的数据是复杂的对象类型，而取出的时候又不想做任何的数据转换，直接从Redis里面取出一个对象，那么使用RedisTemplate是
更好的选择。

hutool

IOUtils.write(data, response.getOutputStream());下载：写到输出流

layer.use('upload',function(){...})layer.ui上传



信息安全工程师（Web渗透方向）岗位题目¶

Redis未授权访问漏洞如何入侵利用？5

匿名连接访问，获取敏感数据。 通过set db写入crontab或写入ssh private key提权拿到服务器权限。

**SSRF漏洞原理、利用方式及修复方案？Java和PHP的SSRF区别？7 **

request服务对入参未做限制，导致可以构造非HTTP[S]协议，比如dict造成任意文件读取、gopher探测扫描内网服务等。 协议支持程度不一样。

**宽字节注入漏洞原理、利用方式及修复方案？5 **

编码转换 使用过滤函数mysql_real_escape_string

简述JSONP劫持利用方式及修复方案？5

在恶意网站引入JSONP接口，并骗取用户访问恶意网站即可拿到该用户的官方网站数据。 通过限制Referer缓解，通过对每个JSONP接口增加Token来彻底防止。

CRLF注入原理？3

通过插入CRLF字符可以控制响应头

越权问题如何检测？3

通过递增操作的编号或数据，根据返回结果判断是否能操作，从而达到越权。

黑盒如何检测XSS漏洞？7

通过在payload中引入探测js或图片，并像可能存在的地方发起payload探测。

一句话木马密码是一个不可见的字符，ascii码为9，此时应该如何使用caidao进行连接？5 Chr(35)&chr(37)&chr(09) %23%25%09

有哪几种后门实现方式？10

一句话、大马、Rootkit、Crontab、rc.d、bashrc

webshell检测有什么方法思路？10

代码特征、行为特征、文件特征等

Linux服务器中了木马后，请简述应急思路？10

这个题比较灵活，主要看看能否考虑全面，比如网络隔离、样本留存分析、时候回溯、全面排查等等

遇到新0day(比如Struts2)后，应该如何进行应急响应？10

打补丁、升级，其他参考上一题

简述Python装饰器、迭代器、生成器原理及应用场景？10

通用题

简述Python进程、线程和协程的区别及应用场景？10

通用题

安全开发工程师（Java方向）岗位题目¶
Java虚拟机区域如何划分？6
HashMap和Hashtable区别？8
进程间通信有哪几种方式？6
快速排序的过程和复杂度？6
Java BIO/NIO/AIO是什么？适用哪些场景？8
调试工具及异常排查流程？5
数据库索引结构，什么情况下应该建唯一索引？6
数据库分页语句如何写？6
获取一个入参url，请求url地址的内容时应注意什么？10
参数入库前应该如何过滤？12
过滤器和拦截器原理和应用场景？8
SESSION ID如何不被Javascript读取？4
CSRF的Token如何设计？10
如何实现跨域请求？5

@Configuration
public class ESConfig {

    @Bean
    public TransportClient transportClient() throws UnknownHostException {
 
        InetSocketTransportAddress node = new InetSocketTransportAddress(
                InetAddress.getByName("192.168.171.129"),
                9300
        );
 
        Settings settings = Settings.builder()
                .put("cluster.name", "elasticsearch")
                .build();
 
        TransportClient client = new PreBuiltTransportClient(settings);
        client.addTransportAddress(node);
        return client;
    }

    /**
     * 防止netty的bug
     * java.lang.IllegalStateException: availableProcessors is already set to [4], rejecting [4]
     */
    @PostConstruct
    void init() {
        System.setProperty("es.set.netty.runtime.available.processors", "false");
    }
}

