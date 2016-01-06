##jQuery.cookie目录结构说明
>通过一个简单的换颜色的例子来说明jQuery.cookie.js是如何使用的，文件里的jsCookie.html是一个原生js的cookie小例子。对比可以看出：封装后的cookie要比原生的cookie使用方便很多，但了解和研究原生可以有助于更好了解JS底层的东西。

- **CSS：简单的颜色皮肤样式**
- **cookie.html：jQuery.cookie的实例文档**
- **jsCookie.html：原生的cookie小例子**
- **README.md：说明文档**

###cookie.html
``` html
<!doctype html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>cookie的读取和设置</title>
	<link rel="stylesheet" id="skin" href="css/skin0.css"/>
      <!--直接引用的是bootstrap公共库的资源-->
	<script src="http://cdn.bootcss.com/jquery/2.1.4/jquery.js"></script>
    <script src="http://cdn.bootcss.com/jquery-cookie/1.4.1/jquery.cookie.js"></script>
    <style>
		html,body{
			margin: 0;
			padding: 20px;
			font-size: 14px;
		}
		ul{
			margin: 0;
			padding: 0;
			list-style:none;
			float: left;
		}
		ul li{
			float: left;
			margin: 10px;
			padding: 5px 15px;
			border:solid 1px silver;
			cursor:pointer;
			border-radius:5px;

		}

		#skin_view{
			clear:both;
			width: 550px;
			height: 350px;
			border-radius:10px;

		}
    </style>
    <script>
    	$(function(){
    		if($.cookie('pifu')){
    			$("#skin").attr("href","css/"+$.cookie('pifu')+".css");
    		}else{
    			$("#skin").attr("href","css/skin0.css");
    		}
			/*当文档加载完毕，先判断有没有名字为pifu的cookie，如果有就加载它；如果没有就加载默认样式*/
			
    		for(var i=0;i<$("ul li").size();i++){
    			$("ul li").eq(i).click(function(){
    				var style=$(this).attr("class");
    				$("#skin").attr("href","css/"+style+".css");
    				$.cookie('pifu',style,{
    					path:"/",
    					expirse:1
    				})
    			})
    		}
		/*循环遍历里，点击li，更改link里面的href属性*/
		/*style变量保存对应字段，最后使用$.cookie('cookie名','cookie值'，{path:'存储路径',expires:'时间'})*/
    	})
    </script>
</head>
<body>
	<ul>
		<li class="skin0">默认</li>
		<li class="skin1">皮肤1</li>
		<li class="skin2">皮肤2</li>
		<li class="skin3">皮肤3</li>
		<li class="skin4">皮肤4</li>
		<li class="skin5">皮肤5</li>
	</ul>
	<div id="skin_view">
		
	</div>
	
</body>
</html>
```

###jsCookie.html
```html
<!doctype html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>弹窗cookie设置</title>
</head>
<body>
	<button id="btn">cookie判断弹窗</button>
<script>
window.onload=function(){
	var btn=document.getElementById("btn");
	btn.onclick=function(){
		LoadPop();
	}
//文档加载完毕，点击button，执行LoadPop函数
}

//打开新窗口函数
function openWin(){
	var win=window.open('ad.html','new','width=600,height=400');
	win.moveTo((screen.width-600)/2,(screen.height-400)/2);
}

//获取cookie函数
function GetCookie(name){
	var search=name+"=";
	var returnvalue="";
	var offset,end;
	if(document.cookie.length>0){
		offset=document.cookie.indexOf(search);
		if(offset!=-1){
			offset+=search.length;
			end=document.cookie.indexOf(";",offset);
			if(end==-1){end=document.cookie.length};
			returnvalue=unescape(document.cookie.substring(offset,end))
		}
	}
	return returnvalue;
}

//通过是否存在cookie值来判断是否执行打开新窗口函数
function LoadPop(){
	if(GetCookie("pop")==""){
		openWin();
		var today=new Date();
		var time=today.getYear()+"-"+today.getMonth()+"-"+today.getDate();
		document.cookie="pop=yes;expires="+time;
	}
}

</script>
</body>
</html>

```

#`非常简单`
