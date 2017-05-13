1、html5标准中定义了许新的表单输入框类型。

占位文本：placeholder属性

允许输入框设置暂未文本，在设置了占位文本后，会在输入框为空或者失去焦点的时候显示出来。
一旦用户点击了输入框，占位文本就会消失（但是这个地方视乎不同浏览器实现不一样）。

实例：

	<form>
		<input name="username" type="text" placeholder="请输入用户名"></input>
		<input name="password" type="password" placeholder="请输入密码"></input>
		<input type="submit"></input>
	</form>

注：一般来说placeholder属性只支持纯文本的形式。但是有的浏览器做了扩展，可以改变其颜色。


自动聚焦：autofocus属性

很多网站采用js脚本的来实现自动聚焦，但是html5实现了autofocus自动聚焦输入框。
	<form>
		<input name="username" type="text" placeholder="请输入用户名"></input>
		<input name="password" type="password" placeholder="请输入密码" autofocus></input>
		<input type="submit"></input>
	</form>

处于兼容性的考虑，对于不支持自动聚焦的浏览器，采用js脚本来实现聚焦，对于支持html5的浏览器，采用autofocus来实现。
	
	<form>
		<input id="demo" autofocus></input>
		<script type="text/javascript">
			if (!("autofocus" in document.createElement('input'))) {
				document.getElementById('demo').focus();
			}
		</script>
		<input type="submit"></input>
	</form>

注：
window.onload事件会在所有dom元素，js脚本，图片加载完成之后才会触发，这时候在聚焦往往会比较晚。。
可以考虑在$(function(){})中实现脚本自动聚焦。

html4支持的表单输入框类型(7中类型):

	<input name="username" type="text" placeholder="请输入用户名"></input>
	<input name="password" type="password" placeholder="请输入密码" autofocus></input>
	<input type="checkbox"></input>
	<input type="radio"></input>
	<input type="password"></input>
	<select>
		<option value="111">111</option>
		<option value="222">222</option>
	</select>
	<input type="file"></input>
	<input type="submit"></input>

html5新增的表单输入框类型：

	<input type="email"></input>
	<input type="url"></input>
	<input type="number" min="0" max="10" step="2" value="5"></input>
	<input type="range" min="0" max="10" step="2" value="5"></input>
	<input type="date"></input>
	<input type="week"></input>
	<input type="time"></input>
	<input type="search"></input>

注：
如果浏览器暂不支持某种输入框，那么就会以type="text"的类型解释该输入框配型。