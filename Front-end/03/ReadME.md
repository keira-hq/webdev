
```

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>login</title>
    <style>
        * {
            margin: 0;
            padding: 0;
        }
         
        html {
            height: 100%;
            width: 100%;
            overflow: hidden;
            margin: 0;
            padding: 0;
            background: url(Desert.jpg) no-repeat 0px 0px;
            background-repeat: no-repeat;
            background-size: 100% 100%;
            -moz-background-size: 100% 100%;
        }
         
        body {
            display: flex;
            align-items: center;
            justify-content: center;
            height: 100%;
        }
         
        #loginDiv {
            width: 37%;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 300px;
            background-color: rgba(75, 81, 95, 0.3);
            box-shadow: 7px 7px 17px rgba(52, 56, 66, 0.5);
            border-radius: 5px;
        }
         
        #name_trip {
            margin-left: 50px;
            color: red;
        }
         
        p {
            margin-top: 30px;
            margin-left: 20px;
            color: azure;
        }
         
        input {
            margin-left: 15px;
            border-radius: 5px;
            border-style: hidden;
            height: 30px;
            width: 140px;
            background-color: rgba(216, 191, 216, 0.5);
            outline: none;
            color: #f0edf3;
            padding-left: 10px;
        }
         
        .button {
            border-color: cornsilk;
            background-color: rgba(100, 149, 237, .7);
            color: aliceblue;
            border-style: hidden;
            border-radius: 5px;
            width: 100px;
            height: 31px;
            font-size: 16px;
        }
    </style>
</head>
 
<body>
    <div id="loginDiv">
        <form action="" id="form">
            <h1 style="text-align: center;color: aliceblue;">LOGIN  IN</h1>
            <p>User Name:<input id="userNname" type="text"><label id="name_trip"></label></p>
 
            <p>Password:  <input id="password" type="password"><label id="password_trip"></label></p>
 
            <div style="text-align: center;margin-top: 30px;">
                <input type="submit" class="button" value="login up">
                <input type="reset" class="button" value="reset">
            </div>
        </form>
    </div>
 
</body>
</html>

```

参考站点： https://blog.csdn.net/m0_37634735/article/details/107043971