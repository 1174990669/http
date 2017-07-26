<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
	<style>
		ul{margin:0; padding: 0;width: 660px;height: 660px;position:relative;}
		li{width: 200px;height: 200px;margin:10px;list-style:none;float: left;text-align: center;line-height: 200px;font-size:40px;color:red; }
		img{width: 200px;height: 200px;}
		/* li:nth-of-type(1){background:url(img/t1.jpg);background-size: 100% 100%}
		li:nth-of-type(2){background:url(img/t2.jpg);background-size: 100% 100%}
		li:nth-of-type(3){background:url(img/t3.jpg);background-size: 100% 100%}
		li:nth-of-type(4){background:url(img/t3.jpg);background-size: 100% 100%}
		li:nth-of-type(5){background:url(img/t1.jpg);background-size: 100% 100%}
		li:nth-of-type(6){background:url(img/t2.jpg);background-size: 100% 100%}
		li:nth-of-type(7){background:url(img/t1.jpg);background-size: 100% 100%}
		li:nth-of-type(8){background:url(img/t2.jpg);background-size: 100% 100%}
		li:nth-of-type(9){background:url(img/t3.jpg);background-size: 100% 100%} */
	</style>

	<script>
		window.onload=function(){
			var aLi=document.getElementsByTagName('li');
			var zindex=1;
			var fon=[];
			for (var i = 0; i < aLi.length; i++) {
				fon.push([aLi[i].offsetLeft,aLi[i].offsetTop]);//获取所在的位置
			}
			for (var i = 0; i < aLi.length; i++) {
				aLi[i].style.position='absolute';//直接定位到获取的位置
				aLi[i].style.left = fon[i][0]+'px';
				aLi[i].style.top = fon[i][1]+'px';
				aLi[i].abc = i;
				fim(aLi[i]);


			}
			function fim(obj){
				// console.log(aLi[i].abc)
				obj.onmousedown=function(ev){

					var disX=0;
					var disY=0;
					var ev=ev||window.event;
					disX=ev.clientX-obj.offsetLeft;
					disY=ev.clientY-obj.offsetTop;
					// console.log(obj.style.zIndex)
					document.onmousemove=function(ev){
						var ev=ev||window.event;
						obj.style.zIndex=zindex++;
						obj.style.left=ev.clientX-disX+'px';
						obj.style.top=ev.clientY-disY+'px';
						// console.log(obj.style.left)
						for (var i = 0; i < aLi.length; i++) {
							aLi[i].style.border='';
							if (findc(obj)) {
								findc(obj).style.border='4px solid red';
								// console.log(aLi[i].style.border)
							}
						}
					}
					document.onmouseup=function(){
						document.onmousemove=null;
						document.onmouseup=null;
						var fc=findc(obj);
						var tmp = 0;
						if(fc){	
							fc.style.left = fon[obj.abc][0] + 'px';
							fc.style.top =  fon[obj.abc][1] + 'px';
							obj.style.left = fon[fc.abc][0] + 'px';
							obj.style.top = fon[fc.abc][1] + 'px';
							// console.log(findc(obj))
							tmp = obj.abc;
							obj.abc = fc.abc;
							fc.abc = tmp;

						}
						
					}
						return false;
				}
			}

		    function fun(obj1,obj2){//判断四边的大小
		    	var T1=obj1.offsetTop;
		    	var L1=obj1.offsetLeft;
		    	var R1=obj1.offsetLeft+obj1.offsetWidth;
		    	var B1=obj1.offsetTop+obj1.offsetHeight; 

		    	var T2=obj2.offsetTop;
		    	var L2=obj2.offsetLeft;
		    	var R2=obj2.offsetLeft+obj2.offsetWidth;
		    	var B2=obj2.offsetTop+obj2.offsetHeight; 

		    	if(T1>B2||L1>R2||R1<L2||B1<T2){
		    		return false
		    	}else{
		    		return true
		    	}
		    }
			function gou(obj1,obj2){
				var a=obj1.offsetLeft-obj2.offsetLeft;
				var b=obj2.offsetTop-obj1.offsetTop;
				var c = Math.sqrt(a*a+b*b);//勾股定理取最短值

				return c;
			}
			function findc(obj){
				var value = 9999;
				var index = -1;
				for (var i = 0; i < aLi.length; i++) {
					if( fun(obj,aLi[i]) && obj != aLi[i] ){
						// console.log(1)
						var lc = gou(obj,aLi[i]);
						// console.log(lc)
						if ( lc < value ) {
							value = lc;
							index = i;
						}
					}
				}
				if (index != -1) {
					return aLi[index];
				}
			}
		}
	</script>
</head>
<body>
	<!-- <div> -->
		<ul id="ul1">
			<li><img src="img/t1.jpg" alt=""></li>
			<li><img src="img/t2.jpg" alt=""></li>
			<li><img src="img/t3.jpg" alt=""></li>
			<li><img src="img/t1.jpg" alt=""></li>
			<li><img src="img/t2.jpg" alt=""></li>
			<li><img src="img/t3.jpg" alt=""></li>
			<li><img src="img/t1.jpg" alt=""></li>
			<li><img src="img/t2.jpg" alt=""></li>
			<li><img src="img/t3.jpg" alt=""></li>
		</ul>
	<!-- </div> -->
</body>
</html>
