[bootstrap导航菜单做active判断](https://www.cnblogs.com/jiujian/p/5148668.html)

https://www.cnblogs.com/jiujian/p/5148668.html

先创建2个文件，index 和about，导入bootstrap的css
```
<div class="container">
    <ul class="nav nav-pills">
        <li><a href="index.html">Home</a></li>
        <li><a href="about.html">About</a></li>
    </ul>
    <h1>Home Page</h1>
</div>
```
然后导入jquery，不导入也行，原始JS写法
```
 $('.nav-pills').find('a').each(function () {
    if (this.href == document.location.href || document.location.href.search(this.href) >= 0) {
        $(this).parent().addClass('active'); // this.className = 'active';
    }
});
```