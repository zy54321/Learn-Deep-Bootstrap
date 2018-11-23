[bootstrap中popover.js(弹出框)使用总结+案例](https://www.cnblogs.com/willingtolove/p/4694573.html)

https://www.cnblogs.com/willingtolove/p/4694573.html

*转载请注明出处：

作者：willingtolove；

http://www.cnblogs.com/willingtolove/p/4694573.html

*bootstrap官方说明：http://v3.bootcss.com/javascript/#popovers

### 一. popover常用配置参数：
```
//常用配置参数：
$(document).ready(function() {
    $('#temp').popover(
        {
            trigger:'click', //触发方式
            template: '', //你自定义的模板
            title:"标题",//设置 弹出框 的标题
            html: true, // 为true的话，data-content里就能放html代码了
            content:"",//这里可以直接写字符串，也可以是一个函数，该函数返回一个字符串；
        }
    );
}
//常用方法：
$('#element').popover('show');
$('#element').popover('hide');
$('#element').popover('destroy')
```

### 二. 案例分析：
1. 案例要求：动态产生一个按钮，并给页面中所有具有data-toggle="popover"属性的元素绑定popover(弹出框)效果，触发方式：当鼠标指针放到元素上时弹出弹出框，离开元素时，弹出框消失；弹出框内容要求：一定要包含该触发弹窗元素的文本信息；

2. html代码：（注意引入bootstrap.js和样式）
```
<body>
    <a id="temp1" tabindex="0" class="btn btn-lg btn-danger" role="button" data-toggle="popover"  title="Dismissible popover" >弹出框1</a>
    <a id="temp2" tabindex="0" class="btn btn-lg btn-danger" role="button" data-toggle="popover">弹出框2</a>

    <div id="LinkDIV" style="float:left;width:200px">
    </div>
</body>
```
3. js代码
```
<script>
        $(function () {
            $("#LinkDIV").html('<button type="btn btn-lg btn-primary" data-toggle="popover" id="temp3">弹出框3</button>');
            $('[data-toggle="popover"]').each(function () {
                var element = $(this);
                var id = element.attr('id');
                var txt = element.html();
                element.popover({
                    trigger: 'manual',
                    placement: 'bottom', //top, bottom, left or right
                    title: txt,
                    html: 'true',
                    content: ContentMethod(txt),

                }).on("mouseenter", function () {
                    var _this = this;
                    $(this).popover("show");
                    $(this).siblings(".popover").on("mouseleave", function () {
                        $(_this).popover('hide');
                    });
                }).on("mouseleave", function () {
                    var _this = this;
                    setTimeout(function () {
                        if (!$(".popover:hover").length) {
                            $(_this).popover("hide")
                        }
                    }, 100);
                });
            });
        });
        function ContentMethod(txt) {
            return '<table class="table table-bordered"><tr><td>' + txt + '</td><td>BB</td><td>CC</td><td>DD</td></tr>' +
                    '<tr><td>' + txt + '</td><td>BB</td><td>CC</td><td>DD</td></tr>' +
                    '<tr><td>' + txt + '</td><td>BB</td><td>CC</td><td>DD</td></tr>'+
                    '<tr><td>AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA</td><td>BB</td><td>CC</td><td>DD</td></tr></table>';
        }
    </script>
```

