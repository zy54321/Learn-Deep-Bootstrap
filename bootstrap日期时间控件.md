[bootstrap日期时间控件](https://blog.csdn.net/nangeali/article/details/71077834)

https://blog.csdn.net/nangeali/article/details/71077834

### datetime控件
Bootstrap的日期时间控件，使用非常的简单。       
![image](https://img-blog.csdn.net/20170502100010466?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvbmFuZ2VhbGk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

首先，添加日期时间控件的引用

```
@*datetime控件*@
    <link href="~/Content/BootStrap/css/bootstrap-datetimepicker.min.css" rel="stylesheet" />
    <script src="~/Content/BootStrap/js/moment-with-locales.js"></script>
    <script src="~/Content/BootStrap/js/bootstrap-datetimepicker.min.js"></script>
    <script src="~/Content/BootStrap/js/bootstrap-datetimepicker.zh-CN.js"></script>
```

链接：http://pan.baidu.com/s/1sl56aw1 密码：jc2y

页面代码
```
<a class='input-group date' id='datetimepicker1' style="float: left; left: 320px;">
                <input type='text' class="form-control" id='nowdate' style="width: 150px; height: 30px;" />
                <span class="input-group-addon" style="float: left; width: 50px; height: 30px;">
                    <span class="glyphicon glyphicon-calendar"></span>
                </span>
            </a>
```

JavaScript代码

```
//设置日期时间控件
function Datetime() {
    $('#datetimepicker1').datetimepicker({
        language: 'zh-CN',//显示中文
        format: 'yyyy-mm-dd',//显示格式
        minView: "month",//设置只显示到月份
        initialDate: new Date(),
        autoclose: true,//选中自动关闭
        todayBtn: true,//显示今日按钮
        locale: moment.locale('zh-cn')
    });
    //默认获取当前日期
    var today = new Date();
    var nowdate = (today.getFullYear()) + "-" + (today.getMonth() + 1) + "-" + today.getDate();
    //对日期格式进行处理
    var date = new Date(nowdate);
    var mon = date.getMonth() + 1;
    var day = date.getDate();
    var mydate = date.getFullYear() + "-" + (mon < 10 ? "0" + mon : mon) + "-" + (day < 10 ? "0" + day : day);
    document.getElementById("nowdate").value = mydate;
}
```
日期时间控件默认值的设置，需要注意的是，在JS中使用的ID是input标签的ID。
```
document.getElementById("nowdate").value = mydate;
```

![image](https://img-blog.csdn.net/20170502100024081?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvbmFuZ2VhbGk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

但是，通过日期时间控件选择之后的日期时间，它的前面是有0的。

![image](https://img-blog.csdn.net/20170502100035481?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvbmFuZ2VhbGk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

解决方法，首先获取当前的日期时间，然后通过格式化处理一下即可。

```
    //默认获取当前日期
    var today = new Date();
    var nowdate = (today.getFullYear()) + "-" + (today.getMonth() + 1) + "-" + today.getDate();
    //对日期格式进行处理
    var date = new Date(nowdate);
    var mon = date.getMonth() + 1;
    var day = date.getDate();
    var mydate = date.getFullYear() + "-" + (mon < 10 ? "0" + mon : mon) + "-" + (day < 10 ? "0" + day : day);
    document.getElementById("nowdate").value = mydate;
```
