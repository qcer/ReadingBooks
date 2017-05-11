### **字符串API总结：**
1、字符方法

	str.charAt(ele)
	strcharCodeAt(ele)
2、字符串操作方法

	str.concat()
3、字符串位置方法

	str.indesOf()
	str.lastIndexOf()
4、trim()方法

5、大小写转化方法

	str.toLowerCase()
	str.toLocaleLowerCase()
	str.toUpperCase()
	str.toLocaleUpperCase()
6、模式匹配方法

match()和search()、replace()、split()


1、字符方法:charAt()和 charCodeAt()
两个用于访问字符串中特定字符的方法是： charAt()和 charCodeAt()。这两个方法都接收一个参数，即基于 0 的字符位置。
其中， charAt()方法以单字符字符串的形式返回给定位置的那个字符（ECMAScript 中没有字符类型）。
如果你想得到的不是字符而是字符编码，那么就要像下面这样使用 charCodeAt()了。
第一个就是 concat()，用于将一或多个字符串拼接起来，
返回拼接得到的新字符串。先来看一个例子。

	var stringValue = "hello ";
	var result = stringValue.concat("world");
	alert(result); //"hello world"
	alert(stringValue); //"hello"

2、字符串操作方法：concat()

第一个就是 concat()，用于将一或多个字符串拼接起来，返回拼接得到的新字符串。先来看一个例子。

	var stringValue = "hello ";
	var result = stringValue.concat("world");
	alert(result); //"hello world"
	alert(stringValue); //"hello"

3、字符串位置方法：indexOf()和 lastIndexOf()

有两个可以从字符串中查找子字符串的方法： indexOf()和 lastIndexOf()。这两个方法都是从一个字符串中搜索给定的子字符串，然后返子字符串的位置（如果没有找到该子字符串，则返回-1）。这两个方法的区别在于： indexOf()方法从字符串的开头向后搜索子字符串，而 lastIndexOf()方法是从字符串的末尾向前搜索子字符串。

4、 trim()方法
ECMAScript 5 为所有字符串定义了 trim()方法。这个方法会创建一个字符串的副本，删除前置及后缀的所有空格，然后返回结果。

5、 字符串大小写转换方法：toLowerCase()、 toLocaleLowerCase()、 toUpperCase()和 toLocaleUpperCase()。

接下来我们要介绍的是一组与大小写转换有关的方法。 ECMAScript 中涉及字符串大小写转换的方法有 4 个： toLowerCase()、 toLocaleLowerCase()、 toUpperCase()和 toLocaleUpperCase()。
其中， toLowerCase()和 toUpperCase()是两个经典的方法，借鉴自 java.lang.String 中的同名
方法。而 toLocaleLowerCase()和 toLocaleUpperCase()方法则是针对特定地区的实现。

6、 字符串的模式匹配方法：match()和search()、replace()、split()

第一个方法就是 match()，在字符串上调用这个方法，本质上与调用 RegExp 的 exec()方法相同。 match()方法只接受一个参数，要么是一个正则表达式，要么是一个 RegExp 对象。来看下面的例子。
另一个用于查找模式的方法是 search()。这个方法的唯一参数与 match()方法的参数相同：由字符串或 RegExp 对象指定的一个正则表达式。 search()方法返回字符串中第一个匹配项的索引；如果没有找到匹配项，则返回-1。

ECMAScript 提供了 replace()方法。这个方法接受两个参数：第一个参数可以是一个 RegExp 对象或者一个字符串（这个字符串不会被转换成正则表达式），第二个参
数可以是一个字符串或者一个函数。如果第一个参数是字符串，那么只会替换第一个子字符串。要想替换所有子字符串，唯一的办法就是提供一个正则表达式，而且要指定全局（g）标志.

最后一个与模式匹配有关的方法是 split()，这个方法可以基于指定的分隔符将一个字符串分割成多个子字符串，并将结果放在一个数组中。分隔符可以是字符串，也可以是一个 RegExp 对象（这个方法不会将字符串看成正则表达式）。 split()方法可以接受可选的第二个参数，用于指定数组的大小，以便确保返回的数组不会超过既定大小。


7、转型方法
每个函数继承的 toLocaleString()和 toString()方法始终都返回函数的代码。返回代码的格
式则因浏览器而异——有的返回的代码与源代码中的函数代码一样，而有的则返回函数代码的内部表
示，即由解析器删除了注释并对某些代码作了改动后的代码。由于存在这些差异，我们无法根据这两个
方法返回的结果来实现任何重要功能；不过，这些信息在调试代码时倒是很有用。另外一个继承的
valueOf()方法同样也只返回函数代码。

