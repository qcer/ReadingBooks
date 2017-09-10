### **Array的API汇总**

**总结：**

1、检测数组的方法

	Array.isArray(ary)

2、栈方法：

	ary.pop()//数组尾删除
	ary.push(sth)//数组尾添加
3、队列方法

	ary.shift()//数组首删除
	ary.unshift()//数组首添加
4、重排序

	ary.reverse()
	ary.sort()
5、操作

	ary.concat(sth)
	ary.slice(start,[end=length-1])
	ary.splice()
6、位置方法

	ary.indexOf(ele,[index])
	ary.lastIndexOf(ele,[index])
7、迭代

	ary.every()
	ary.filter()
	ary.forEach()
	ary.map()
	ary.some()
8、归并方法

	ary.reduce()
	ary.reduceRight()
9、转型方法：

	ary.toString()
	ary.toLocalString()
	ary.valueOf() //返回原数组

**ES6新增：**

Array.from():

Array.from方法用于将两类对象转为真正的数组：类似数组的对象（array-like object）和可遍历（iterable）的对象（包括ES6新增的数据结构Set和Map）。

Array.of():用于将一组值，转换为数组。这个方法的主要目的，是弥补数组构造函数Array()的不足。因为参数个数的不同，会导致Array()的行为有差异。

	Array.of(3, 11, 8) // [3,11,8]
	Array.of(3) // [3]
	Array.of(3).length // 1

find()和findIndex():参数为查找条件函数

数组实例的find方法，用于找出第一个符合条件的数组成员。它的参数是一个回调函数，所有数组成员依次执行该回调函数，直到找出第一个返回值为true的成员，然后返回该成员。

find方法的回调函数可以接受三个参数，依次为当前的值、当前的位置和原数组。

	var ary = [3,7,5,9,1];
	console.log(ary.find(function (ele) {
		// body...
		return ele>8;
	})); //9

fill()：

fill方法使用给定值，填充一个数组。

	['a', 'b', 'c'].fill(7)
	// [7, 7, 7]

	new Array(3).fill(7)
	// [7, 7, 7]

entries()，keys()和values():

ES6提供三个新的方法——entries()，keys()和values()——用于遍历数组。它们都返回一个遍历器对象（详见《Iterator》一章），可以用for...of循环进行遍历，唯一的区别是keys()是对键名的遍历、values()是对键值的遍历，entries()是对键值对的遍历。

	var ary = ['a','b','c'];
	for (let i of ary.entries()) {
		console.log(i);
	} 
	// return: //数组是对象这一根本问题
	// [0, "a"]
	// [1, "b"]
	// [2, "c"]

includes():

Array.prototype.includes方法返回一个布尔值，表示某个数组是否包含给定的值，与字符串的includes方法类似。

	var colors = ["red", "blue", "green"]; // 创建一个包含 3 个字符串的数组
	colors[colors.length] = "black"; //（在位置 3）添加一种颜色

1、检测数组

1) instanceof
ary instanceof Array
instanceof 操作符的问题在于，它假定只有一个全局执行环境。如果网页中包含多个框架，
际上就存在两个以上不同的全局执行环境，从而存在两个以上不同版本的 Array 构造函数。如果你从一个框架向另一个框架传入一个数组，那么传入的数组与在第二个框架中原生创建的数组分别具有各自不同的构造函数。

2) Array.isArray()
为了解决这个问题， ECMAScript 5 新增了 Array.isArray()方法。这个方法的目的是最终确定某个值到底是不是数组，而不管它是在哪个全局执行环境中创建的。这个方法的用法如下。

	var ary = [1,2,3];
	if (Array.isArray(ary)){
		//对数组执行某些操作
	}

2、转型方法

所有对象都具有 toLocaleString()、 toString()和 valueOf()方法。其中，调用数组的 toString()方法会返回由数组中每个值的字符串形式拼接而成的一个以逗号分隔的字符串。而调用 valueOf()返回的还是数组。实际上，为了创建这个字符串会调用数组每一项的 toString()方法。来看下面这个例子。

	var colors = ["red", "blue", "green"]; // 创建一个包含 3 个字符串的数组
	console.log(colors.toString()); // red,blue,green
	console.log(colors.valueOf()); // ["red", "blue", "green"]


3、栈方法

CMAScript 为数组专门提供了 push()和 pop()方法，以便实现类似栈的行为。

push()方法可以接收任意数量的参数，把它们逐个添加到数组末尾，并返回修改后数组的长度。而
pop()方法则从数组末尾移除最后一项，减少数组的 length 值，然后返回移除的项。

	var ary = [1,2,3];
	console.log(ary.pop());		//3
	console.log(ary.length);	//2

4、队列方法

队列数据结构的访问规则是 FIFO （First-In-First-Out，先进先出）实现这一操作的数组方法就是 shift()，它能够移除数组中的第一个项并返回该项，同时将数组长度减 1。
ECMAScript 还为数组提供了一个 unshift()方法。顾名思义，unshift()与 shift()的用途相反：它能在数组前端添加任意个项并返回新数组的长度。

**结合使用 push()和shift()方法，可以像使用队列一样使用数组,实现左向队列。**

**结合使用unshift()和pop()可以实现右向队列。**

5、重排序方法

数组中已经存在两个可以直接用来重排序的方法： reverse()和 sort()。

默认情况下，sort()方法会调用每个数组项的 toString()转型方法，然后比较得到的字符串，以
确定如何排序。

sort()可传入比较函数。比较函数接收两个参数，如果第一个参数应该位于第二个之前则返回一个负数，如果两个参数相等
则返回 0，如果第一个参数应该位于第二个之后则返回一个正数。总结来说就是：return v1-v2表示递增排序。


6、操作方法

ECMAScript 为操作已经包含在数组中的项提供了很多方法。其中， concat()方法可以基于当前数组中的所有项创建一个新数组。具体来说，这个方法会**先创建当前数组一个副本，然后将接收到的参数添加到这个副本的末尾，最后返回新构建的数组。**

**但是concat()方法是浅复制：**

	var ary = [6,1,4,9,['red']];
	var ary1 = ary.concat();
	ary[4][0] = ['black'];
	console.log(ary1[4][0]);//black


slice()，它能够基于当前数组中的一或多个项创建一个**新数组**。

 slice()方法可以接受一或两个参数，即要返回项的起始和结束位置。在只有一个参数的情况下， slice()方法返回从该参数指定位置开始到当前数组末尾的所有项。如果有两个参数，该方法返回起始和结束位置之间的项——但不包括结束位置的项。

**注意， slice()方法不会影响原始数组。**

请看下面的例子。

	var colors = ["red", "green", "blue", "yellow", "purple"];
	var colors2 = colors.slice(1);
	var colors3 = colors.slice(1,4);
	alert(colors2); //green,blue,yellow,purple
	alert(colors3); //green,blue,yellow


splice()方法这个方法恐怕要算是最强大的数组方法了，它有很多种用法。

splice()的主要用途是向数组的中部插入项，但使用这种方法的方式则有如下 3 种。
 删除：可以删除任意数量的项，只需指定 2 个参数：要删除的第一项的位置和要删除的项数。
例如， splice(0,2)会删除数组中的前两项。

 插入：可以向指定位置插入任意数量的项，只需提供 3 个参数：起始位置、 0（要删除的项数）
和要插入的项。如果要插入多个项，可以再传入第四、第五，以至任意多个项。例如，
splice(2,0,"red","green")会从当前数组的位置 2 开始插入字符串"red"和"green"。

 替换：可以向指定位置插入任意数量的项，且同时删除任意数量的项，只需指定 3 个参数：起
始位置、要删除的项数和要插入的任意数量的项。插入的项数不必与删除的项数相等。例如，
splice (2,1,"red","green")会删除当前数组位置 2 的项，然后再从位置 2 开始插入字符串
"red"和"green"。

splice()方法始终都会返回一个数组，该数组中包含从原始数组中删除的项（如果没有删除任何
项，则返回一个空数组）


7、位置方法

ECMAScript 5 为数组实例添加了两个位置方法： indexOf()和 lastIndexOf()。

8、迭代方法

ECMAScript 5 为数组定义了 5 个迭代方法。每个方法都接收两个参数：要在每一项上运行的函数和（可选的）运行该函数的作用域对象——影响 this 的值。传入这些方法中的函数会接收三个参数：数组项的值、该项在数组中的位置和数组对象本身。根据使用的方法不同，这个函数执行后的返回值可能会也可能不会影响方法的返回值。以下是这 5 个迭代方法的作用。

 every()：对数组中的每一项运行给定函数，如果该函数对每一项都返回 true，则返回 true。

 filter()：对数组中的每一项运行给定函数，返回该函数会返回 true 的项组成的数组。

 forEach()：对数组中的每一项运行给定函数。这个方法没有返回值。

 map()：对数组中的每一项运行给定函数，返回每次函数调用的结果组成的数组。

 some()：对数组中的每一项运行给定函数，如果该函数对任一项返回 true，则返回 true。

在这些方法中，最相似的是 every()和 some()，它们都用于查询数组中的项是否满足某个条件。对 every()来说，传入的函数必须对每一项都返回 true，这个方法才返回 true；否则，它就返回false。而 some()方法则是只要传入的函数对数组中的某一项返回 true，就会返回 true。

filter()函数，它利用指定的函数确定是否在返回的数组中包含某一项。

map()也返回一个数组，而这个数组的每一项都是在原始数组中的对应项上运行传入函数的结果。

最后一个方法是 forEach()，它只是对数组中的每一项运行传入的函数。这个方法没有返回值，本质上与使用 for 循环迭代数组一样。但是不可break;

9、归并方法

ECMAScript 5 还新增了两个归并数组的方法： reduce()和 reduceRight()。这两个方法都会迭代数组的所有项，然后构建一个最终返回的值。其中， reduce()方法从数组的第一项开始，逐个遍历到最后。而 reduceRight()则从数组的最后一项开始，向前遍历到第一项。

这两个方法都接收两个参数：一个在每一项上调用的函数和（可选的）作为归并基础的初始值。

传给 reduce()和 reduceRight()的函数接收 4 个参数：前一个值、当前值、项的索引和数组对象。这个函数返回的任何值都会作为第一个参数自动传给下一项。第一次迭代发生在数组的第二项上，因此第一个参数是数组的第一项，第二个参数就是数组的第二项。使用 reduce()方法可以执行求数组中所有值之和的操作，比如：

	var values = [1,2,3,4,5];
	var sum = values.reduce(function(prev, cur, index, array){
		return prev + cur;
	});
	alert(sum); //15