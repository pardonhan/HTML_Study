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
