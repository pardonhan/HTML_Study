# 12个非常实用的javascript小技巧

## 1.使用  !!  操作符转换布尔值
对变量实用 ```!!``` 操作符， ```!!variable``` ,只要变量的值为 : ```>=0 , null , ""(空串)，undefined或者NaN```都将返回false,反之返回的是true。
``` javascript
    function Account(cash){
        this.cash = cash;
        this.hasMoney = !!cash;
    }
    var account = new Account(100.50);
    console.log(account.cash);
    console.log(account.hasMoney);
    
    var emptyAccount = new Account(0);
    console.log(emptyAccount.cash);
    console.log(emptyAccount.hasMoney);
```
在这个示例中，只要account.cash的值大于0，那么account.hasMoney返回值就是true;

## 2. 使用 + 将字符串转换成数字
可以将数字字符串转换成数字，在转换非数字字符串时，返回NaN
``` javascript
    function toNumber(strNumber){
        return +strNumber;        
    }
    console.log(toNumber("1234"));//1234
    console.log(toNumber("ABC"));//NaN
```
这个也试用于Date,返回的是数字时间戳
``` javascript
    console.log(+new Date());   //1461288164385
```
## 3. 并条件符  && 
如果你有一段这样的代码:
``` javascript
    if(conected){
        login();
    }
```
可以将变量简写，并且使用 && 和函数连接在一起，比如上面的例子，可以简写成:
``` javascript
    conected && login();
```
如果一些属性或者函数存在于一个对象中，可以简写成这样:
``` javascript
    user && user.login();
```
## 4.使用 || 运算符
在ES6中有 默认参数 这一特性。为了在老版本的浏览器中模拟这一特性，可以使用||操作符，并且将默认值当作第二个参数传入。
如果第一个参数的返回值是false，那么第二个值将会认为是一个默认的值。如下面的这个示例:
``` javascript 
    function User(name,age){
        this.name = name || "Oliver Queen";
        this.age = age || 27;
    }
    var user1 = new User();
    console.log(user1.name);
    console.log(user1.age);
    
    var user2 = new User("Barry Allen",30);
    console.log(user2.name);
    console.log(user2.age);
```
## 5.在循环中缓存 array.length
这个技巧很简单，这个在处理一个很大的数组循环时，对性能影响将是非常大的。
基本上，大家都会写这样一个同步迭代的数组：
``` javascript 
    for(var i=0;i<array.length;i++){
        console.log(array[i]);
    }
```
如果是一个小型的数组，这样做可以，如果是要处理一个非常大的数组，这段代码在每次迭代的时候都会重新计算数组的大小，这将会导致
一些延误。为了避免这种现象的出现，可以将```array.length```做一个缓存：
``` javascript
    var length =array.length;
    for(var i=0;i<lenght;i++){
        console.log(array[i]);
    }
    /// 也可以写成下面这样
    for(var i=0,length = array.length;i<length;i++){
        console.log(array[i]);
    }            
```
## 6.检测对象中的属性
如果想要使用```documnet.querySelector()```来选择一个id，并且能让它兼容ie6浏览器，但是在ie6浏览器中这函数是不存在的，
那么使用这个技巧就可以检测这个函数是否存在：
``` javascript
    if("querySelector" in documnet){
        documnet.querySelector("#id");
    }else{
        documnet.getElementById("id");
    }
````
## 7.获取数组的最后一个参数

函数：``` Array.prototype.slice(begin,end)```，用来获取begin和end之间的数组元素。如果不设置end参数，将会将数组的默认长度当作end值。
此外，这个函数还可以接受负数作为其参数，可以获取其最后几个数组元素:

```javascript
    var array = [1,2,3,4,5,6];
    console.log(array.slice(-1));//6
    console.log(array.slice(-2));//5,6
    console.log(array.slice(-3));//4,5,6
```
## 8.数组截断
这个小技巧主要用来锁定数组的大小，如果用于删除数组中的一些元素来说，是非常有用的。例如，你的数组有10个元素，但你只想只要前五个元素，那么你可以通过array.length=5来截断数组。如下面这个示例：
``` javascript
    var array = [1,2,3,4,5,6];
    console.log(array.length); // 6
    array.length = 3;
    console.log(array.length); // 3
    console.log(array); // [1,2,3]
```
## 9.替换所有
函数```String.replace()```允许你使用字符串或正则表达式来替换字符串，本身这个函数只替换第一次出现的字符串，不过你可以使用正则表达多中的/g来模拟replaceAll()函数功能：
``` javascript 
    var string = "john john";
    console.log(string.replace(/hn/, "ana")); // "joana john"
    console.log(string.replace(/hn/g, "ana")); // "joana joana"
```
## 10.合并数组
如果你要合并两个数组，一般情况之下你都会使用Array.concat()函数：
``` javascript
    var array1 = [1,2,3];
    var array2 = [4,5,6];
    console.log(array1.concat(array2)); // [1,2,3,4,5,6];
```
然后这个函数并不适合用来合并两个大型的数组，因为其将消耗大量的内存来存储新创建的数组。在这种情况之个，可以使用```Array.pus().apply(arr1,arr2)```来替代创建一个新数组。这种方法不是用来创建一个新的数组，其只是将第一个第二个数组合并在一起，同时减少内存的使用：
``` javascript
    var array1 = [1,2,3];
    var array2 = [4,5,6];
    console.log(array1.push.apply(array1, array2)); // [1,2,3,4,5,6];
```
## 11.将NodeList转换成数组
如果你运行```document.querySelectorAll(“p”)```函数时，它可能返回DOM元素的数组，也就是```NodeList```对象。
但这个对象不具有数组的函数功能，比如```sort()、reduce()、map()、filter()```等。
为了让这些原生的数组函数功能也能用于其上面，需要将节点列表转换成数组。
可以使用```[].slice.call(elements)```来实现：
``` javascript
    var elements = document.querySelectorAll("p"); // NodeList
    var arrayElements = [].slice.call(elements); // Now the NodeList is an array
    var arrayElements = Array.from(elements); // This is another way of converting NodeList to Array
```
## 12.数组元素的洗牌
对于数组元素的洗牌，不需要使用任何外部的库，比如Lodash，只要这样做：
``` javascript
    var list = [1,2,3];
    console.log(list.sort(function() { Math.random() - 0.5 })); // [2,1,3]
```