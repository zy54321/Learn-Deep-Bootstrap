[toc]
## 零、连接
[bootstrap的JS插件资料连接](http://v3.bootcss.com/javascript/#js-overview)
## 一、概览
### 1、单个还是全部引入
。。。
### 2、data属性
可以只需data属性API就能使用所有的Bootstrap插件，是Bootstrap中一等式，也是首选方式。     

关闭data属性API方法，即解除以 data-api 为命名空间并绑定在文档上的事件。就像下面这样：
```
$(document).off('.data-api')
```
如果针对某个特定插件，只需在 data-api 前面添加那个插件的名称作为命名空间，如下：
```
$(document).off('.alert.data-api')
```

### 3、编程方式的API
。。。
### 4、避免命名空间冲突
某些时候可能需要将 Bootstrap 插件与其他 UI 框架共同使用。在这种情况下，命名空间冲突随时可能发生。如果不幸发生了这种情况，你可以通过调用插件的 .noConflict 方法恢复其原始值。
```
var bootstrapButton = $.fn.button.noConflict() // return $.fn.button to previously assigned value
$.fn.bootstrapBtn = bootstrapButton            // give $().bootstrapBtn the Bootstrap functionality
```

### 5、事件
Bootstrap 为大部分插件所具有的动作提供了自定义事件。一般来说，这些事件都有不定式和过去式两种动词的命名形式，例如，不定式形式的动词（例如 show）表示其在事件开始时被触发；而过去式动词（例如 shown ）表示在动作执行完毕之后被触发。       

从 3.0.0 版本开始，所有 Bootstrap 事件的名称都采用命名空间方式。      

所有以不定式形式的动词命名的事件都提供了 preventDefault 功能。这就赋予你在动作开始执行前将其停止的能力。     

```
$('#myModal').on('show.bs.modal', function (e) {
  if (!data) return e.preventDefault() // 阻止模态框的展示
})
```

### 6、Version numbers
每个 Bootstrap 的 jQuery 插件的版本号都可以通过插件的构造函数上的 VERSION 属性获取到。例如工具提示框（tooltip）插件：
```
$.fn.tooltip.Constructor.VERSION // => "3.3.7"
```
### 7、浏览器的JavaScript被禁用得情况
Bootstrap 插件未对禁用 JavaScript 的浏览器提供补救措施。如果你对这种情况下的用户体验很关心的话，请添加 < noscript> 标签向你的用户进行解释（并告诉他们如何启用 JavaScript），或者按照你自己的方式提供补救措施
### 8、第三方工具库
Bootstrap 官方不提供对第三方 JavaScript 工具库的支持
## 二、过渡效果 transition.js
对于简单的过渡效果，只需将 transition.js 和其它 JS 文件一起引入即可。如果你使用的是编译（或压缩）版的 bootstrap.js 文件，就无需再单独将其引入了。

通过下面的 JavaScript 代码可以在全局范围禁用过渡效果，并且必须将此代码放在 transition.js （或 bootstrap.js 或 bootstrap.min.js）后面，确保在 js 文件加载完毕后再执行下面的代码：
```
$.support.transition = false
```
## 三、模态框 modal.js
1、不支持同时打开多个模态框

千万不要在一个模态框上重叠另一个模态框。要想同时支持多个模态框，需要自己写额外的代码来实现。

2、模态框的 HTML 代码放置的位置

务必将模态框的 HTML 代码放在文档的最高层级内（也就是说，尽量作为 body 标签的直接子元素），以避免其他组件影响模态框的展现和/或功能。

### 1、实例
动态实例：      
点击下面的按钮即可通过 JavaScript 启动一个模态框。此模态框将从上到下、逐渐浮现到页面前。
```
<!-- Button trigger modal -->
<button type="button" class="btn btn-primary btn-lg" data-toggle="modal" data-target="#myModal">
  Launch demo modal
</button>

<!-- Modal -->
<div class="modal fade" id="myModal" tabindex="-1" role="dialog" aria-labelledby="myModalLabel">
  <div class="modal-dialog" role="document">
    <div class="modal-content">
      <div class="modal-header">
        <button type="button" class="close" data-dismiss="modal" aria-label="Close"><span aria-hidden="true">&times;</span></button>
        <h4 class="modal-title" id="myModalLabel">Modal title</h4>
      </div>
      <div class="modal-body">
        ...
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-default" data-dismiss="modal">Close</button>
        <button type="button" class="btn btn-primary">Save changes</button>
      </div>
    </div>
  </div>
</div>
```

注意：      

增强模态框的可访问性

务必为 .modal 添加 role="dialog" 和 aria-labelledby="..." 属性，用于指向模态框的标题栏；为 .modal-dialog 添加 aria-hidden="true" 属性。

另外，你还应该通过 aria-describedby 属性为模态框 .modal 添加描述性信息。

### 2、可选尺寸 .bs-example-modal-lg/sm
```
<!-- 大 Large modal -->
<button type="button" class="btn btn-primary" data-toggle="modal" data-target=".bs-example-modal-lg">Large modal</button>

<div class="modal fade bs-example-modal-lg" tabindex="-1" role="dialog" aria-labelledby="myLargeModalLabel">
  <div class="modal-dialog modal-lg" role="document">
    <div class="modal-content">
      ...
    </div>
  </div>
</div>

<!-- 小 Small modal -->
<button type="button" class="btn btn-primary" data-toggle="modal" data-target=".bs-example-modal-sm">Small modal</button>

<div class="modal fade bs-example-modal-sm" tabindex="-1" role="dialog" aria-labelledby="mySmallModalLabel">
  <div class="modal-dialog modal-sm" role="document">
    <div class="modal-content">
      ...
    </div>
  </div>
</div>
```
### 3、禁止动画
不需要模态框弹出时的动画效果（淡入淡出效果），删掉 .fade 类即可。

```
<div class="modal" tabindex="-1" role="dialog" aria-labelledby="...">
  ...
</div>
```
### 4、使用栅格系统
要利用模式内的Bootstrap网格系统，只需在.modal-body内嵌套.rows，然后使用正常的网格系统类。
```
<div class="modal fade" tabindex="-1" role="dialog" aria-labelledby="gridSystemModalLabel">
  <div class="modal-dialog" role="document">
    <div class="modal-content">
      <div class="modal-header">
        <button type="button" class="close" data-dismiss="modal" aria-label="Close"><span aria-hidden="true">&times;</span></button>
        <h4 class="modal-title" id="gridSystemModalLabel">Modal title</h4>
      </div>
      <div class="modal-body">
        <div class="row">
          <div class="col-md-4">.col-md-4</div>
          <div class="col-md-4 col-md-offset-4">.col-md-4 .col-md-offset-4</div>
        </div>
        <div class="row">
          <div class="col-md-3 col-md-offset-3">.col-md-3 .col-md-offset-3</div>
          <div class="col-md-2 col-md-offset-4">.col-md-2 .col-md-offset-4</div>
        </div>
        <div class="row">
          <div class="col-md-6 col-md-offset-3">.col-md-6 .col-md-offset-3</div>
        </div>
        <div class="row">
          <div class="col-sm-9">
            Level 1: .col-sm-9
            <div class="row">
              <div class="col-xs-8 col-sm-6">
                Level 2: .col-xs-8 .col-sm-6
              </div>
              <div class="col-xs-4 col-sm-6">
                Level 2: .col-xs-4 .col-sm-6
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-default" data-dismiss="modal">Close</button>
        <button type="button" class="btn btn-primary">Save changes</button>
      </div>
    </div><!-- /.modal-content -->
  </div><!-- /.modal-dialog -->
</div><!-- /.modal -->
```
### 5、根据触发器按钮改变模态内容
有一堆按钮都触发相同的模式，只是内容稍有不同？ 使用event.relatedTarget和HTML data- *属性（可能通过jQuery）根据点击哪个按钮来改变模式的内容。 有关relatedTarget的详细信息，请参阅模态事件文档，
```
<button type="button" class="btn btn-primary" data-toggle="modal" data-target="#exampleModal" data-whatever="@mdo">Open modal for @mdo</button>
<button type="button" class="btn btn-primary" data-toggle="modal" data-target="#exampleModal" data-whatever="@fat">Open modal for @fat</button>
<button type="button" class="btn btn-primary" data-toggle="modal" data-target="#exampleModal" data-whatever="@getbootstrap">Open modal for @getbootstrap</button>
...more buttons...

<div class="modal fade" id="exampleModal" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel">
  <div class="modal-dialog" role="document">
    <div class="modal-content">
      <div class="modal-header">
        <button type="button" class="close" data-dismiss="modal" aria-label="Close"><span aria-hidden="true">&times;</span></button>
        <h4 class="modal-title" id="exampleModalLabel">New message</h4>
      </div>
      <div class="modal-body">
        <form>
          <div class="form-group">
            <label for="recipient-name" class="control-label">Recipient:</label>
            <input type="text" class="form-control" id="recipient-name">
          </div>
          <div class="form-group">
            <label for="message-text" class="control-label">Message:</label>
            <textarea class="form-control" id="message-text"></textarea>
          </div>
        </form>
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-default" data-dismiss="modal">Close</button>
        <button type="button" class="btn btn-primary">Send message</button>
      </div>
    </div>
  </div>
</div>
```
```
$('#exampleModal').on('show.bs.modal', function (event) {
  var button = $(event.relatedTarget) // Button that triggered the modal
  var recipient = button.data('whatever') // Extract info from data-* attributes
  // 如果有必要，你可以在这里发起一个AJAX请求（然后在回调中进行更新）。
  // 更新模态的内容。 我们将在这里使用jQuery，但您可以使用数据绑定库或其他方法。
  var modal = $(this)
  modal.find('.modal-title').text('New message to ' + recipient)
  modal.find('.modal-body input').val(recipient)
})
```
### 6、用法
通过 data 属性或 JavaScript 调用模态框插件，可以根据需要动态展示隐藏的内容。模态框弹出时还会为 < body> 元素添加 .modal-open 类，从而覆盖页面默认的滚动行为，并且还会自动生成一个 .modal-backdrop 元素用于提供一个可点击的区域，点击此区域就即可关闭模态框。

1、通过data属性     
不需写 JavaScript 代码也可激活模态框。通过在一个起控制器作用的元素（例如：按钮）上添加 data-toggle="modal" 属性，或者 data-target="#foo" 属性，再或者 href="#foo" 属性，用于指向被控制的模态框。
```
<button type="button" data-toggle="modal" data-target="#myModal">Launch modal</button>
```

2、通过JavaScript调用       
只需一行 JavaScript 代码，即可通过元素的 id myModal 调用模态框：
```
$('#myModal').modal(options)
```

### 7、参数
相关资料点击链接进入查阅：              
[参数设置](http://v3.bootcss.com/javascript/#modals-options)

### 8、方法
1、.modal(options)

将页面中的某块内容作为模态框激活。接受可选参数 object。
```
$('#myModal').modal({
  keyboard: false
})
```
2、.modal('toggle')

手动打开或关闭模态框。在模态框显示或隐藏之前返回到主调函数中（也就是，在触发 shown.bs.modal 或 hidden.bs.modal 事件之前）。
```
$('#myModal').modal('toggle')
```
3、.modal('show')

手动打开模态框。在模态框显示之前返回到主调函数中 （也就是，在触发 shown.bs.modal 事件之前）。
```
$('#myModal').modal('show')
```
4、.modal('hide')

手动隐藏模态框。在模态框隐藏之前返回到主调函数中 （也就是，在触发 hidden.bs.modal 事件之前）。
```
$('#myModal').modal('hide')
```
5、.modal('handleUpdate')

重新调整模式的位置以对抗滚动条，以防出现滚动条，这会使模式跳转到左侧。      
只有当模态的高度在打开时发生变化时才需要。
```
$('#myModal').modal('handleUpdate')
```
### 9、事件
Bootstrap 的模态框类提供了一些事件用于监听并执行你自己的代码        
所有的模态事件都是在模态本身触发的（即在< div class =“modal”>）。

事  件  类  型 | 描述
---|---
show.bs.modal | show 方法调用之后立即触发该事件。如果是通过点击某个作为触发器的元素，则此元素可以通过事件的 relatedTarget 属性进行访问。
shown.bs.modal |  	此事件在模态框已经显示出来（并且同时在 CSS 过渡效果完成）之后被触发。如果是通过点击某个作为触发器的元素，则此元素可以通过事件的 relatedTarget 属性进行访问。
hide.bs.modal | hide 方法调用之后立即触发该事件。
hidden.bs.modal | 此事件在模态框被隐藏（并且同时在 CSS 过渡效果完成）之后被触发。
loaded.bs.modal |  	从远端的数据源加载完数据之后触发该事件。

```
$('#myModal').on('hidden.bs.modal', function (e) {
  // do something...
})
```

## 四、下拉菜单 dropdown.js
### 1、实例
用这个简单的插件将下拉菜单添加到几乎所有的东西中，包括导航条、标签和药片。      
分为两种，一个是在普通导航栏中的下拉菜单，一个是药片形状导航栏中的下拉菜单

### 2、用法
通过数据属性或JavaScript，下拉插件通过切换父列表项上的.open类来切换隐藏内容（下拉菜单）。

在移动设备上，打开下拉菜单时，会添加一个.dropdown-backdrop作为点击区域，以便在菜单之外点击时关闭下拉菜单，这是获得iOS支持的必要条件。 这意味着从打开的下拉菜单切换到不同的下拉菜单需要额外的移动点击。

注意：data-toggle =“dropdown”属性依赖于在应用程序级别关闭下拉菜单，所以始终使用它是个好主意。

1、通过data属性         
将data-toggle="dropdown"添加到链接或按钮以切换下拉菜单。        
```
<div class="dropdown">
  <button id="dLabel" type="button" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
    Dropdown trigger
    <span class="caret"></span>
  </button>
  <ul class="dropdown-menu" aria-labelledby="dLabel">
    ...
  </ul>
</div>
```
要使链接按钮保持不变，请使用data-target属性而不是href =“＃”。
```
<div class="dropdown">
  <a id="dLabel" data-target="#" href="http://example.com" data-toggle="dropdown" role="button" aria-haspopup="true" aria-expanded="false">
    Dropdown trigger
    <span class="caret"></span>
  </a>

  <ul class="dropdown-menu" aria-labelledby="dLabel">
    ...
  </ul>
</div>
```

2、通过JavaScript       
通过JavaScript调用下拉菜单：        
```
$('.dropdown-toggle').dropdown()
```
data-toggle =“dropdown”仍然是必需的

无论您是通过JavaScript调用下拉菜单，还是使用data-api，data-toggle =“dropdown”总是需要存在于下拉的触发元素上。

### 3、方法
$().dropdown('toggle')

切换给定导航栏或标签导航的下拉菜单。

### 4、事件
所有的下拉菜单都会在.dropdown菜单的父元素上触发。

所有下拉事件都有一个relatedTarget属性，其值是切换锚点元素。


事  件  类  型 | 描述
---|---
show.bs.dropdown | 当show instance方法被调用时，此事件立即触发。
shown.bs.dropdown | 当下拉菜单对用户可见时会触发此事件（等待CSS转换完成）。
hide.bs.dropdown | 当调用隐藏实例方法时立即触发此事件。
hidden.bs.dropdown | 当下拉菜单完成对用户隐藏时会触发此事件（等待CSS转换完成）。

```
$('#myDropdown').on('show.bs.dropdown', function () {
  // do something…
})
```

## 五、滚动监听 scrollspy.js
### 1、实例
滚动监听插件是用来根据滚动条所处的位置来自动更新导航项的。滚动导航条下面的区域并关注导航项的变化。下拉菜单中的条目也会自动高亮显示。

### 2、用法

**依赖 Bootstrap 的导航组件**       
滚动监听插件依赖 Bootstrap 的导航组件 用于高亮显示当前激活的链接。        
**需要可解析的ID目标**      
导航栏链接必须具有可解析的ID目标。 例如，<a href="#home">主页</a>必须对应于DOM中的某些内容，例如<div id =“home”> </ div>。      
**非::visible 目标元素被忽略**      
根据jQuery不可见的目标元素将被忽略，并且其相应的导航项不会突出显示。

1、需要相对定位（relative positioning）     
无论何种实现方式，滚动监听都需要被监听的组件是 position: relative; 即相对定位方式。大多数时候是监听 <body> 元素。无论何种实现方式，滚动监听都需要被监听的组件是position：relative; 即相对定位方式。大多数时候是监听<body>元素。当滚动到<body>以外的元素时，一定要有高度设置和overflow-y：scroll;应用。     

2、通过data属性调用     
为了方便地将滚动行为添加到顶栏导航中，请将data-spy =“scroll”添加到您想要窥探的元素（最典型的情况是<body>）。 然后将data-target属性与任何Bootstrap .nav组件的父元素的ID或类相加。
```
body {
  position: relative;
}
```
```
<body data-spy="scroll" data-target="#navbar-example">
  ...
  <div id="navbar-example">
    <ul class="nav nav-tabs" role="tablist">
      ...
    </ul>
  </div>
  ...
</body>
```

3、通过 JavaScript 调用
在 CSS 中添加 position: relative; 之后，通过 JavaScript 代码启动滚动监听插件：
```
$('body').scrollspy({ target: '#navbar-example' })
```

### 3、方法
.scrollspy('refresh')

当使用滚动监听插件的同时在 DOM 中添加或删除元素后，你需要像下面这样调用此刷新（ refresh） 方法：
```
$('[data-spy="scroll"]').each(function () {
  var $spy = $(this).scrollspy('refresh')
})
```

### 4、参数
可以通过 data 属性或 JavaScript 传递参数。对于 data 属性，其名称是将参数名附着到 data- 后面组成，例如 data-offset=""。

名称 | 类型 | 默认值 | 描述
---|--- | --- | ---
offset | number | 10 | 计算滚动位置时相对于顶部的偏移量（像素数）。

### 5、事件

事件类型 | 描述
---|---
activate.bs.scrollspy | 每当一个新条目被激活后都将由滚动监听插件触发此事件。

## 六、标签页 tab.js
### 1、实例
添加快速、动态的选项卡功能，可以通过本地内容的窗格进行转换，甚至可以通过下拉菜单进行转换。不支持嵌套制表符。

```
扩展选项卡式导航

此插件扩展了选项卡式导航组件以添加可列表区域。
```
### 2、用法
通过JavaScript启用可制表选项卡(每个选项卡需要单独激活):
```
$('#myTabs a').click(function (e) {
  e.preventDefault()
  $(this).tab('show')
})
```
您可以通过以下几种方式激活各个选项卡:
```
$('#myTabs a[href="#profile"]').tab('show') // 选择选项卡的名字
$('#myTabs a:first').tab('show') // 选择第一个选项卡
$('#myTabs a:last').tab('show') // 选择最后一个标签
$('#myTabs li:eq(2) a').tab('show') // 选择第三个选项卡（0-indexed）
```
1、标记
只需在元素上指定data-toggle =“tab”或data-toggle =“pill”，即可激活选项卡或药丸导航而无需编写任何JavaScript。 将nav和nav-tabs类添加到选项卡ul将应用Bootstrap选项卡样式，而添加nav和nav-pills类将应用丸样式。
```
<div>

  <!-- Nav tabs -->
  <ul class="nav nav-tabs" role="tablist">
    <li role="presentation" class="active"><a href="#home" aria-controls="home" role="tab" data-toggle="tab">Home</a></li>
    <li role="presentation"><a href="#profile" aria-controls="profile" role="tab" data-toggle="tab">Profile</a></li>
    <li role="presentation"><a href="#messages" aria-controls="messages" role="tab" data-toggle="tab">Messages</a></li>
    <li role="presentation"><a href="#settings" aria-controls="settings" role="tab" data-toggle="tab">Settings</a></li>
  </ul>

  <!-- Tab panes -->
  <div class="tab-content">
    <div role="tabpanel" class="tab-pane active" id="home">...</div>
    <div role="tabpanel" class="tab-pane" id="profile">...</div>
    <div role="tabpanel" class="tab-pane" id="messages">...</div>
    <div role="tabpanel" class="tab-pane" id="settings">...</div>
  </div>

</div>
```
2、淡化效果
要使标签淡入，请将.fade添加到每个.tab-pane。 第一个选项卡窗格还必须具有.in以使初始内容可见。
```
<div class="tab-content">
  <div role="tabpanel" class="tab-pane fade in active" id="home">...</div>
  <div role="tabpanel" class="tab-pane fade" id="profile">...</div>
  <div role="tabpanel" class="tab-pane fade" id="messages">...</div>
  <div role="tabpanel" class="tab-pane fade" id="settings">...</div>
</div>
```
### 3、方法
1、$().tab

激活制表符元素和内容容器。 选项卡应具有数据目标或针对DOM中容器节点的href。 在上面的示例中，选项卡是带有data-toggle =“tab”属性的<a>。

2、.tab('show')
选择给定的选项卡并显示其相关内容。先前选中的任何其他选项卡都将被取消选中，其相关内容将被隐藏。返回到实际显示选项卡窗格之前的调用者(即在shown.bs之前)。选项卡事件发生)。
```
$('#someTab').tab('show')
```

### 4、事件
当显示新选项卡时，事件按以下顺序触发:
```

    1、hide.bs.tab (在当前活动选项卡上)
    2、show.bs.tab (在待显示的标签上)
    3、hidden.bs.tab (在上一个活动选项卡上，与hide.bs.tab事件相同)
    4、shown.bs.tab (在刚刚显示的新活动选项卡上，与show.bs.tab事件相同)
```
如果没有选项卡已处于活动状态，则不会触发hide.bs.tab和hidden.bs.tab事件。

事件类型 | 描述
--- |---
show.bs.tab | 此事件在选项卡显示时触发，但在显示新选项卡之前。       使用event.target和event.relatedTarget分别定位活动选项卡和上一个活动选项卡（如果可用）。
shown.bs.tab | 显示选项卡后，此事件将在选项卡显示中触发。        使用event.target和event.relatedTarget分别定位活动选项卡和上一个活动选项卡（如果可用）。
hide.bs.tab | 当要显示新选项卡时将触发此事件（因此将隐藏先前的活动选项卡）。       使用event.target和event.relatedTarget分别定位当前活动选项卡和新的即将激活的选项卡。
hidden.bs.tab | 显示新选项卡后将触发此事件（因此隐藏了上一个活动选项卡）。         使用event.target和event.relatedTarget分别定位上一个活动选项卡和新活动选项卡。

```
$('a[data-toggle="tab"]').on('shown.bs.tab', function (e) {
  e.target // newly activated tab
  e.relatedTarget // previous active tab
})
```

## 七、工具提示 tooltip.js
受到Jason Frame编写的优秀jQuery.tipsy插件的启发; 工具提示是一个更新版本，不依赖于图像，使用CSS3进行动画处理，使用数据属性进行本地标题存储。

永远不会显示具有零长度标题的工具提示。

### 1、实例
将鼠标悬停在下面的链接上可查看工具提示：        
[实例](https://v3.bootcss.com/javascript/#tooltips-examples)

1、静态工具提示
有四种选择：顶部，右侧，底部和左侧对齐。

2、四个方向
```
<button type="button" class="btn btn-default" data-toggle="tooltip" data-placement="left" title="Tooltip on left">Tooltip on left</button>

<button type="button" class="btn btn-default" data-toggle="tooltip" data-placement="top" title="Tooltip on top">Tooltip on top</button>

<button type="button" class="btn btn-default" data-toggle="tooltip" data-placement="bottom" title="Tooltip on bottom">Tooltip on bottom</button>

<button type="button" class="btn btn-default" data-toggle="tooltip" data-placement="right" title="Tooltip on right">Tooltip on right</button>
```

3、可选功能
出于性能原因，Tooltip和Popover data-apis是选择加入的，这意味着您必须自己初始化它们。

初始化页面上所有工具提示的一种方法是通过数据切换属性选择它们：
```
$(function () {
  $('[data-toggle="tooltip"]').tooltip()
})
```
### 2、用法
工具提示插件会根据需要生成内容和标记，默认情况下会在触发元素后面放置工具提示。

通过JavaScript触发工具提示：
```
$('#example').tooltip(options)
```
1、标记
工具提示所需的标记只是您希望获得工具提示的HTML元素上的数据属性和标题。 生成的工具提示标记相当简单，但它确实需要一个位置（默认情况下，由插件设置为顶部）。
```
<!-- HTML to write -->
<a href="#" data-toggle="tooltip" title="Some tooltip text!">Hover over me</a>

<!-- Generated markup by the plugin -->
<div class="tooltip top" role="tooltip">
  <div class="tooltip-arrow"></div>
  <div class="tooltip-inner">
    Some tooltip text!
  </div>
</div>
```
多行链接

    有时您想要将工具提示添加到包含多行的超链接。 工具提示插件的默认行为是水平和垂直居中。 添加 white-space: nowrap; 到你的锚点避免这种情况。

按钮组，输入组和表中的工具提示需要特殊设置

    在.btn-group或.input-group中的元素或与表相关的元素（<td>，<th>，<tr>，<thead>，<tbody>，<tfoot>）上使用工具提示时， 你必须指定选项container: 'body'（下面记录）以避免不必要的副作用（例如当触发工具提示时元素变宽和/或失去圆角）。
    
不要试图在隐藏元素上显示工具提示

    当目标元素为display：none时，调用$（...）。tooltip（'show'）; 将导致工具提示错误定位。
    
用于键盘和辅助技术用户的可访问工具提示

    对于使用键盘导航的用户，特别是辅助技术的用户，您应该只将工具提示添加到键盘可聚焦的元素，例如链接，表单控件或任何具有tabindex =“0”;属性的任意元素。
    
禁用元素上的工具提示需要包装元素

    要向禁用或.disabled元素添加工具提示，请将元素放在<div>中，然后将工具提示应用于该<div>。
    
### 3、参数
选项可以通过数据属性或JavaScript传递。 对于数据属性，将选项名称附加到data-，如data-animation =“”。


名称 | 类型 | 默认 | 描述
---|--- | --- | ---
animation |	boolean | true | 将CSS淡入淡出过渡应用于工具提示
container |	string | false | 将工具提示附加到特定元素。 示例：container：'body'。 此选项特别有用，因为它允许您将工具提示放置在触发元素附近的文档流中 - 这将防止工具提示在窗口调整大小期间从触发元素浮动。
delay |	number / object | 0 | 延迟显示和隐藏工具提示（ms） - 不适用于手动触发类型，如果提供了数字，则延迟将应用于隐藏/显示，对象结构是：delay：{“show”：500，“hide”：100}
html |	boolean | false | 将HTML插入工具提示。 如果为false，则使用jQuery的文本方法将内容插入DOM。 如果您担心XSS攻击，请使用文本。
placement |	string / function | 'top' | 如何定位工具提示 - 顶部 \| 底部 \| 左侧 \| 右侧 \| 自动。指定“auto”时，它将动态重新定向工具提示。例如，如果展示位置为“自动离开”，则工具提示会尽可能显示在左侧，否则它将显示正确。当使用函数确定放置时，将使用工具提示DOM节点作为其第一个参数并将触发元素DOM节点作为其第二个参数来调用它。 this上下文设置为工具提示实例。
selector |	string | false | 如果提供了选择器，则工具提示对象将委派给指定的目标。 实际上，这用于使动态HTML内容添加工具提示。 看到this和an informative example。
template | string |	``` '<div class="tooltip" role="tooltip"><div class="tooltip-arrow"></div><div class="tooltip-inner"></div></div>' ``` | 创建工具提示时使用的基本HTML。工具提示的标题将被注入.tooltip-inner。.tooltip-arrow将成为工具提示的箭头。最外层的包装元素应该具有.tooltip类。
title |	string \| function |'' | 如果title属性不存在，则为默认title值。如果给出了一个函数，它将被调用，其this引用设置为工具提示所附加的元素。
trigger | string |'hover focus' | 如何触发工具提示 - click \| hover \| focus \| manual.。 你可以传递多个触发器; 用空格隔开它们。 manual不能与任何其他触发器结合使用。
viewport | string \| object \| function | { selector: 'body', padding: 0 } | 将工具提示保持在此元素的范围内。 示例：viewport：'＃viewport'或{“selector”：“＃viewport”，“padding”：0}如果给出了一个函数，则使用触发元素DOM节点作为其唯一参数调用它。 此上下文设置为工具提示实例。

    各个工具提示的数据属性

    如上所述，可以通过使用数据属性来指定单个工具提示的选项。
    
### 4、方法
$().tooltip(options)        
将工具提示处理程序附加到元素集合。

.tooltip('show')        
显示元素的工具提示。 **在实际显示工具提示之前**（即在shown.bs.tooltip事件发生之前）返回到调用者。 这被认为是工具提示的“手动”触发。 永远不会显示具有零长度标题的工具提示。
```
$('#element').tooltip('show')
```

.tooltip('hide')        
隐藏元素的工具提示。 **在实际隐藏工具提示之前**（即在hidden.bs.tooltip事件发生之前）返回调用者。 这被认为是工具提示的“triggering ”触发。
```
$('#element').tooltip('hide')
```

.tooltip('destroy')     
隐藏和销毁元素的工具提示。 使用委托（使用the selector option）的工具提示不能在后代触发器元素上单独销毁。
```
$('#element').tooltip('destroy')
```

### 5、事件

事件类型 | 描述
---|---
show.bs.tooltip | 调用show实例方法时会立即触发此事件。
shown.bs.tooltip | 当工具提示对用户可见时将触发此事件（将等待CSS转换完成）。
hide.bs.tooltip | 调用hide实例方法时会立即触发此事件。
hidden.bs.tooltip | 当工具提示完成对用户的隐藏时将触发此事件（将等待CSS转换完成）。
inserted.bs.tooltip | 将工具提示模板添加到DOM后，在show.bs.tooltip事件之后触发此事件。

```
$('#myTooltip').on('hidden.bs.tooltip', function () {
  // do something…
})
```
## 八、弹出框 popover.js
为任意元素添加一小块浮层，就像 iPad 上一样，用于存放非主要信息。

弹出框的标题和内容的长度都是零的话将永远不会被显示出来。

    
**插件依赖**        
弹出框依赖 工具提示插件 ，因此，如果你定制了 Bootstrap，一定要注意将依赖的插件编译进去。

**初始化**      
由于性能的原因，工具提示和弹出框的 data 编程接口（data api）是必须要手动初始化的。      
在一个页面上一次性初始化所有弹出框的方式是通过 data-toggle 属性选中他们：
```
$(function () {
  $('[data-toggle="popover"]').popover()
})
```

**按钮组，输入组和表中的弹出窗口需要特殊设置**      
在.btn-group或.input-group中的元素或表相关元素（\<td>，\<th>，\<tr>，\<thead>，\<tbody>，\<tfoot>）上使用弹出窗口时， 你必须指定选项 container: 'body';（下面记录）以避免不必要的副作用（例如元素在触发弹出窗口时变宽和/或失去圆角）。

**不要试图在隐藏元素上显示弹出窗口**        
当目标元素为display：none时，nvoking $（...）。popover（'show'）; 将导致弹出窗口错误定位。

**禁用元素上的弹出窗口需要包装元素**        
要将弹出框添加到disabled 或.disabled元素，请将元素放在\<div>中，然后将弹出框应用于该\<div>。

**多行链接**        
有时您想要将popover添加到包含多行的超链接。 弹出窗口插件的默认行为是水平和垂直居中。 添加 white-space: nowrap; 到你的锚点避免这种情况。

### 1、实例
#### 1、静态弹出框

4个可能的弹出方向：顶部、右侧、底部和左侧。

#### 2、实例演示
```
<button type="button" class="btn btn-lg btn-danger" data-toggle="popover" title="Popover title" data-content="And here's some amazing content. It's very engaging. Right?">点我弹出/隐藏弹出框</button>
```
1、4个弹出方向
```
<button type="button" class="btn btn-default" data-container="body" data-toggle="popover" data-placement="left" data-content="Vivamus sagittis lacus vel augue laoreet rutrum faucibus.">
  Popover on 左侧
</button>

<button type="button" class="btn btn-default" data-container="body" data-toggle="popover" data-placement="top" data-content="Vivamus sagittis lacus vel augue laoreet rutrum faucibus.">
  Popover on 顶部
</button>

<button type="button" class="btn btn-default" data-container="body" data-toggle="popover" data-placement="bottom" data-content="Vivamus
sagittis lacus vel augue laoreet rutrum faucibus.">
  Popover on 底部
</button>

<button type="button" class="btn btn-default" data-container="body" data-toggle="popover" data-placement="right" data-content="Vivamus sagittis lacus vel augue laoreet rutrum faucibus.">
  Popover on 右侧
</button>
```

2、点击并让弹出框消失

通过使用 focus 触发器可以在用户点击弹出框是让其消失。

    实现“点击并让弹出框消失”的效果需要一些额外的代码

    为了更好的跨浏览器和跨平台效果，你必须使用 <a> 标签，不能使用 <button> 标签，并且，还必须包含 role="button" 和 tabindex 属性。

```
<a tabindex="0" class="btn btn-lg btn-danger" role="button" data-toggle="popover" data-trigger="focus" title="Dismissible popover" data-content="And here's some amazing content. It's very engaging. Right?">可消失的弹出框</a>
```
### 2、用法
通过 JavaScript 代码启动弹出框：

    $('#example').popover(options)
### 3、参数
可以通过 data 属性或 JavaScript 传递参数。对于 data 属性，将参数名附着到 data- 后面，例如 data-animation=""。

选项名称 | 类型/默认值 | Data 属性名称 | 描述
---|--- | --- | ---
row 1 col 1 | row 1 col 2
animation | boolean </br> 默认值：true | data-animation | 向弹出框应用 CSS 褪色过渡效果。
html | boolean </br> 默认值：false	| data-html | 向弹出框插入 HTML。如果为 false，jQuery 的 text 方法将被用于向 dom 插入内容。如果您担心 XSS 攻击，请使用 text。
placement | string \|function </br> 默认值：top | data-placement | 规定如何定位弹出框（即 top \| bottom \| left \| right \| auto）。当指定为 auto 时，会动态调整弹出框。例如，如果 placement 是 "auto left"，弹出框将会尽可能显示在左边，在情况不允许的情况下它才会显示在右边。
selector | string </br> 默认值：false | data-selector | 如果提供了一个选择器，弹出框对象将被委派到指定的目标。
title | string \| function </br> 默认值：'' | data-title | 如果未指定 title 属性，则 title 选项是默认的 title 值。
trigger	| string </br> 默认值：'hover focus' | data-trigger | 定义如何触发弹出框： click \| hover \| focus \| manual。您可以传递多个触发器，每个触发器之间用空格分隔。
delay | number \| object </br> 默认值：0 | data-delay | 延迟显示和隐藏弹出框的毫秒数 - 对 manual 手动触发类型不适用。如果提供的是一个数字，那么延迟将会应用于显示和隐藏。如果提供的是对象，结构如下所示：``` delay: { show: 500, hide: 100 } ```
container | string \| false </br> 默认值：false | data-container | 向指定元素追加弹出框。实例： container: 'body'

### 4、方法
**$().popover(options)**        
初始化元素集合的弹出窗口。

**.popover('show')**        
显示元素的弹出窗口。 在实际显示弹出窗口之前（即在 shown.bs.bs.popover事件发生之前）返回到调用者。 这被认为是弹出窗口的“手动”触发器。 永远不会显示标题和内容都为零长度的弹出窗口。

    $('#element').popover('show')

**.popover('hide')**        
隐藏元素的弹出窗口。 在实际隐藏弹出窗口之前（即在hidden.bs.popover事件发生之前）返回调用者。 这被认为是弹出窗口的“手动”触发器。

    $('#element').popover('hide')
    
**.popover('toggle')**      
切换元素的弹出窗口。 在实际显示或隐藏弹出框之前（即在显示的.bs.popover或hidden.bs.popover事件发生之前）返回到调用者。 这被认为是弹出窗口的“手动”触发器。

    $('#element').popover('toggle')
    
**.popover('destroy')**     
隐藏和摧毁元素的弹出窗口。 使用委托（使用选择器selector创建）的弹出窗口不能在后代触发器元素上单独销毁。

    $('#element').popover('destroy')
    

### 5、事件
下表列出了弹出框（Popover）插件中要用到的事件。这些事件可在函数中当钩子使用。       
事件 | 描述 | 实例
--- | --- | ---
show.bs.popover	| 当调用 show 实例方法时立即触发该事件。 | 	``` $('#mypopover').on('show.bs.popover', function () {// 执行一些动作...})  ```
shown.bs.popover | 当弹出框对用户可见时触发该事件（将等待 CSS 过渡效果完成）。 | ``` $('#mypopover').on('shown.bs.popover', function () {// 执行一些动作...}) ```
hide.bs.popover	| 当调用 hide 实例方法时立即触发该事件。| ``` $('#mypopover').on('hide.bs.popover', function () {// 执行一些动作...}) ``` 
hidden.bs.popover | 当工具提示对用户隐藏时触发该事件（将等待 CSS 过渡效果完成）。| ``` $('#mypopover').on('hidden.bs.popover', function () {// 执行一些动作...}) ```

## 九、警告框 alert.js
### 1、警告框实例
通过此插件可以为警告信息添加点击并消失的功能。

当使用 .close 按钮时，它必须是 .alert-dismissible 的第一个子元素，并且在它之前不能有任何文本内容。
### 2、用法
为关闭按钮添加 data-dismiss="alert" 属性就可以使其自动为警告框赋予关闭功能。关闭警告框也就是将其从 DOM 中删除。

```
<button type="button" class="close" data-dismiss="alert" aria-label="Close">
  <span aria-hidden="true">&times;</span>
</button>
```

为了让警告框在关闭时表现出动画效果，请确保为其添加了 .fade 和 .in 类。

### 3、方法
**$().alert()**     
让警告框监听具有 data-dismiss="alert" 属性的后裔元素的点击（click）事件。（如果是通过 data 属性进行的初始化则无需使用）

**$().alert('close') **     
关闭警告框并从 DOM 中将其删除。如果警告框被赋予了 .fade 和 .in 类，那么，警告框在淡出之后才会被删除。

### 4、事件
Bootstrap 的警告框插件对外暴露了一些可以被监听的事件。
事件类型 | 描述
--- | ---
close.bs.alert | 当 close 方法被调用后立即触发此事件。
closed.bs.alert | 当警告框被关闭后（也即 CSS 过渡效果完毕之后）立即触发此事件。

```
$('#myAlert').on('closed.bs.alert', function () {
  // do something…
})
```
## 十、按钮 button.js
按钮的功能很丰富。通过控制按钮的状态或创建一组按钮并形成一些新的组件，例如工具条。
```

跨浏览器兼容性

在页面多次加载之间，Firefox 仍然保持表单控件的状态（禁用状态和选择状态）。一个解决办法是设置 autocomplete="off"。参见 Mozilla bug #654072。

```
### 1、状态
通过添加 data-loading-text="Loading..." 可以为按钮设置正在加载的状态。

**从 v3.3.5 版本开始，此特性不再建议使用，并且已经在 v4 版本中删除了。**
```
<button type="button" id="myButton" data-loading-text="Loading..." class="btn btn-primary" autocomplete="off">
  Loading state
</button>

<script>
  $('#myButton').on('click', function () {
    var $btn = $(this).button('loading')
    // business logic...
    $btn.button('reset')
  })
</script>
```
### 2、单切换
添加data-toggle =“button”以激活单个按钮的切换。
```
** 预切换按钮需要.active和aria-pressed =“true” **

对于预切换按钮，您必须自己将.active类和aria-pressed =“true”属性添加到按钮。
```

```
<button type="button" class="btn btn-primary" data-toggle="button" aria-pressed="false" autocomplete="off">
  Single toggle
</button>
```
### 3、复选和单选
将data-toggle =“buttons”添加到包含复选框或无线电输入的.btn-group中，以便能够切换各自的样式。
```
预选选项需要.active

对于预选选项，您必须自己将.active类添加到输入label中。
```

```
视觉检查状态仅在单击时更新

如果更新复选框按钮的选中状态而未触发按钮上的click事件（例如，通过<input type =“reset”>或通过设置输入的checked属性），则需要切换.active类 输入的label自己。
```

**复选按钮实例：**
```
<div class="btn-group" data-toggle="buttons">
  <label class="btn btn-primary active">
    <input type="checkbox" autocomplete="off" checked> Checkbox 1 (pre-checked)
  </label>
  <label class="btn btn-primary">
    <input type="checkbox" autocomplete="off"> Checkbox 2
  </label>
  <label class="btn btn-primary">
    <input type="checkbox" autocomplete="off"> Checkbox 3
  </label>
</div>
```

**单选按钮实例：**
```
<div class="btn-group" data-toggle="buttons">
  <label class="btn btn-primary active">
    <input type="radio" name="options" id="option1" autocomplete="off" checked> Radio 1 (preselected)
  </label>
  <label class="btn btn-primary">
    <input type="radio" name="options" id="option2" autocomplete="off"> Radio 2
  </label>
  <label class="btn btn-primary">
    <input type="radio" name="options" id="option3" autocomplete="off"> Radio 3
  </label>
</div>
```
### 4、方法
**$().button('toggle')**        
切换推送状态。 为按钮提供已激活的外观。

**$().button('reset')**     
重置按钮状态 - 将按钮上的文本还原回原始的内容。此为异步方法，此方法在内容被重置完成之前即返回。

**$().button(string)**      
将文本交换到任何数据定义的文本状态。

```
<button type="button" id="myStateButton" data-complete-text="finished!" class="btn btn-primary" autocomplete="off">
  ...
</button>

<script>
  $('#myStateButton').on('click', function () {
    $(this).button('complete') // button text will be "finished!"
  })
</script>
```