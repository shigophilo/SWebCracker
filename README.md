需要1010端口没被占用(很抱歉,端口写死了)
当前目录下要有chromedriver.exe(很抱歉,也写死了)
无头模式运行( -head)

## 食用方法
```
SWebCracker.exe		显示使用说明

SWebCracker.exe  -u -n -p -s [-h][-e][-head][-nf|-un][-pf|-pw][-se][-rs][-rt][-ru][-t][-ot][-o]

  -e string
        元素标志 id ne(name) tn(TagName) cn(ClassName) lt(ByLinkText) plt(ByPartialLinkText) (default "id")
  -head
        是否无头模式运行
  -n string
        username标志,可以标记用户名输入框的标记
  -nf string
        存放username的文件名,每行一个
  -o string
        存放结果的文件名 (default "out.csv")
  -ot int
        无法匹配到结果时,延时写入 (default 5)
  -p string
        password标志,可以标记密码输入框的标记
        存放password的文件名每行一个
  -pw string
        指定密码,指定单个密码
  -rs string
  -rt string
        匹配的返回title
  -ru string
        匹配的返回结url,用于判断页面请求是否发送完成,页面是否加载完成
  -s string
        提交按钮标志
  -se string
        提交按钮类型 id ne(name) tn(TagName) cn(ClassName) lt(ByLinkText) plt(ByPartialLinkText) (default "id")
  -t int
        每次请求页面间隔时间 (default 1)
  -u string
        要测试的url
  -un string
        指定用户名,指定单个用户名
```

## 食用演示
url : https://shigophilo.github.io/login.html

![image-20230205133928316](imgs/image-20230205133928316.png)

+ 用户名输入框
```
<input name="email" id="email" type="email" class="form-control" placeholder="Email">
```
+ 密码输入框
```
<input name="pass" id="pass" type="password" class="form-control" placeholder="Password">
```
+ 登录按钮
```
<input id="login" type="button" class="btn btn-default" value="登 录" onclick="return check_login();">
```
### 简单食用
+ 使用指定的账号:admin 和密码:123456 爆破
```
SWebCracker.exe -u https://shigophilo.github.io/login.html -n email -p pass -s login -un admin -pw 123456
```
+ 使用 指定账号:admin和密码字典pass.txt破解
```
SWebCracker.exe -u https://shigophilo.github.io/login.html -n email -p pass -s login -un admin -pf pass.txt
```
+ 使用账号字典:user.txt 和密码字典:pass.txt破解
```
SWebCracker.exe -u https://shigophilo.github.io/login.html -n email -p pass -s login -uf user.txt -pf pass.txt
```
### 复杂食用
** 可以通过匹配url,title和页面文字内容来确定**

+ 匹配页面返回内容
如果页面中返回了"登录成功",则表示匹配成功
```
SWebCracker.exe -u https://shigophilo.github.io/login.html -n email -p pass -s login -uf user.txt -pf pass.txt -rs "登录成功"
```
+ 匹配网页title
如:`login.html`页面的title是"登录页面", 数据包提交到`login.php`,logon.php页面的title为"登录中"
```
SWebCracker.exe -u https://shigophilo.github.io/login.html -n email -p pass -s login -uf user.txt -pf pass.txt -rt "登录中"
```
+ 匹配url
如:登录页面的url为:https://shigophilo.github.io/login.html  数据包提交到其它页面
```
SWebCracker.exe -u https://shigophilo.github.io/login.html -n email -p pass -s login -uf user.txt -pf pass.txt -ru https://shigophilo.github.io/login.html
```
