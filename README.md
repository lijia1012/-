<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<meta name="viewport" content="width=device-width,user-scalable=no" />
		<title></title>
		<style>
			#test{
				width: 200px;
				height: 200px;
				margin: 100px auto;
				background: deeppink;
			}
		</style>
	</head>
	<body>
		<div id="test"></div>
	</body>
	<script>
		document.addEventListener("touchstart",function(ev){
			ev.preventDefault();
		})
		
		window.onload=function(){
			var testNode = document.querySelector("#test");
			
			var callback={
				start:function(){
					testNode.style.background="gray";
				},
				change:function(){
					testNode.innerHTML+="change<br />";
				},
				end:function(){
					testNode.style.background="deeppink";
					testNode.innerHTML="";
				}
			}
			
			gesTure(testNode,callback);
		}
		
//			touches 当前屏幕上的手指列表
//			targetTouches 当前元素上的手指列表
//			changedTouches 触发当前事件的手指列表
		function gesTure(el,callback){
			var flag = false;
			el.addEventListener("touchstart",function(ev){
				if(ev.touches.length>=2){
					flag=true;
					if(callback&&callback.start){
						callback.start();
					}
				}
			})
			
			el.addEventListener("touchmove",function(ev){
				if(ev.touches.length>=2){
					if(callback&&callback.change){
						callback.change();
					}
				}
			})
			
			el.addEventListener("touchend",function(){
				if(flag){
					if(callback&&callback.end){
						callback.end();
					}
					flag = false;
				}
			})
		}
	</script>
</html>
