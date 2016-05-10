# 12个非常实用的javascript小技巧

## 1.使用  !!  操作符转换布尔值
对变量实用 !! 操作符， !!variable ,只要变量的值为 :0 , null , ""(空串)，undefined或者NaN都将返回false,反之返回的是true。
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