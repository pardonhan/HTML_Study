     
## 登录页面回车登录
###  第一种方法
``` html 
<html xmlns="http://www.w3.org/1999/xhtml" >
<head>
  <title>Check Score</title>
    <script language="JavaScript">
    function keyLogin(){
    if (event.keyCode==13)   //回车键的键值为13
        document.getElementByIdx_x("input1").click();  //调用登录按钮的登录事件
    }
    </script>
 </head>
<body onkeydown="keyLogin();">
    <input id="input1" value="登录" type="button" onClick="alert('调用成功！')">
</body>
</html>

```
###  第二种方法
``` html 
<html xmlns="http://www.w3.org/1999/xhtml" >
<head>
    <script>
    function KeyDown()
    {
        if (event.keyCode == 13)
        {
            event.returnValue=false;
            event.cancel = true;
            Form1.btnsubmit.click();
        }
    }
    </script>
</head>    
<body>
    使用方法：
    <form name="Form1" method="">
        用户名:<INPUT TYPE="text" SIZE="20" maxlength = "8" onkeydown="KeyDown()"/>
        密码:<INPUT TYPE="password" SIZE="20" maxlength = "8" onkeydown="KeyDown()"/>
        <input type="submit" name="btnsubmit" value="提交" />
    </form>
</body>
</html>
```