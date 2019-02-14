# thymeleaf学习笔记（常用功能）

## 前言

thymeleaf类似于jsp的模板引擎。结合springboot使用，解决前后端分离问题。

> 1. 使用的版本：`spring-boot-starter-thymeleaf-2.1.2.RELEASE.jar`，对应的maven会自动导入需要的`thymeleaf-3.0.11.RELEASE.jar`和`thymeleaf-spring5-3.0.11.RELEASE.jar`。可在项目底下的`Maven Dependencies`目录下查看。
>
> 2. 如果需要IDE获得代码提示功能则需要在HTML标签加入`xmlns:th="http://www.thymeleaf.org"`
>
>    ```html
>    <!DOCTYPE html>
>    <html xmlns:th="http://www.thymeleaf.org">
>    <head>
>    <meta charset="UTF-8">
>    <title>Insert title here</title>
>    </head>
>    <body>
>        hello thymeleaf!
>    </body>
>    </html>
>    ```
>
> 3. thymeleaf所有的标签元素都是以`th:`开头。除thymeleaf本身所含有的元素外。HTML元素中所有的标签元素都可以用`th:`+`元素名`覆盖。举例：`<a href="" th:href=""></a>`a标签中有`href`属性，便可以使用`th:href`覆盖。**img**标签含有`src`属性，则可以使用`th:src`覆盖代替。
>

###基本属性解释

|      | th:text=""                                                   | th:utext=""                                                  |
| ---- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 区别 | 不会解析HTML标签；${hello<h1>exp<h1>}输出`hello<h1>exp<h1>`  | 会解析HTML标签：输出`helloexp`                               |
|      | [[]]功能和th:text=""相同。区别是th:text=""标签内使用，[[]]标签外使用：如`<a>[[${hello}]]</a>` | [()]功能和th:utext=""相同。区别是th:utext=""标签内使用，[()]标签外使用 |

*例子*

```html
<tr th:each="user:${users}">
    <td th:text="${user.id}"></td>
    <td th:text="${user.username}"></td>
    <td>[[${user.password}]]</td>
    <td>[[${user.danWeiTID}]]</td>
    <td>
		<a class="btn btn-sm btn-primary" th:href="@{/user/}+${user.id}">编辑</a>
		<button th:attr="del_uri=@{/user/}+${user.id}" type="submit" class="btn btn-danger 			deleteBtn">删除</button>
	</td>
</tr>
```



###常用表达式

|        标签        |                  作用                   | 使用举例说明                                                 |
| :----------------: | :-------------------------------------: | ------------------------------------------------------------ |
|     ${example}     | 一般用于获得`变量值相关`。如example的值 | `<p th:text="${example}">value</p>` 说明：如果example存在并且有值，那么便会替代value。 |
| @{/assets/exp.css} | 一般用于链接**地址**，或请求地址使用。  | 1.引入静态资源的地址：`<img th:src="@{/assets/img/img.png}"/>`。其他样式表，脚本等类似。2. 发送请求地址使用：`<form th:action="@{/deleteUser/1001}">` |
| ~{Commons::topbar} |  片段表达式。一般用于引入一段代码片段   | 引入每个页面都需要的导航栏：有一个Commons.html里面包含一个导航栏代码片`<nav th:fragment="topbar"></nav>`。当我们需要引入这一个导航栏代码时，只需要在需要引入的位置使用`<div th:replace="~{commons::topbar}"></div>`引入就好了。语法规则：commons是Commons.html的名字，省略`.html`后缀。代表从哪个模板里边获取。topbar即这个模板底下使用`th:fragment`属性命名的标识。 |

##实用例子

### 1. 公共页面抽取

使用`th:fragment`和`th:replace`属性。

> 举例：有一个Commons.html。里面包含每个页面所需要的顶部导航栏，侧部导航栏等等，即每个页面都含有的公共部分，单独抽取出来放在Commons.html页面里。代码片加上`th:fragment`属性并取一个唯一的名字用作标识。
>

**Commons.html**

```html
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
<!-- 顶部导航栏。我们给导航栏标签最外部加上 th:fragment标签，取名"topbar" -->
    <nav class="navbar navbar-inverse navbar-fixed-top" th:fragment="topbar">
      <div class="container-fluid">
        <div class="navbar-header">
          <button type="button" class="navbar-toggle collapsed" data-toggle="collapse" data-target="#navbar" aria-expanded="false" aria-controls="navbar">
            <span class="sr-only">Toggle navigation</span>
            <span class="icon-bar"></span>
            <span class="icon-bar"></span>
            <span class="icon-bar"></span>
          </button>
          <a class="navbar-brand" href="#" th:text="${session.loginUser}">Project name</a>
        </div>
        <div id="navbar" class="navbar-collapse collapse">
          <ul class="nav navbar-nav navbar-right">
            <li><a href="#">Dashboard</a></li>
            <li><a href="#">设置</a></li>
            <li><a href="#">个人</a></li>
            <li><a href="#">帮助</a></li>
          </ul>
          <form class="navbar-form navbar-right">
            <input type="text" class="form-control" placeholder="Search...">
          </form>
        </div>
      </div>
    </nav>
<!-- 侧边导航栏 。取名"sidebar"-->
        <div class="col-sm-3 col-md-2 sidebar" th:fragment="sidebar">
          <ul class="nav nav-sidebar">
            <li><a href="#">Overview <span class="sr-only">(current)</span></a></li>
            <li><a href="#">Reports</a></li>
            <li><a href="#">Analytics</a></li>
            <li><a href="#">Export</a></li>
          </ul>
          <ul class="nav nav-sidebar">
            <li th:class="${activeUri=='main.html'?'active':''}"><a href="" th:href="@{/main.html}">主页</a></li>
            <li th:class="${activeUri=='users'?'active':''}"><a href="" th:href="@{/users}">员工列表</a></li>
            <li><a href="">One more nav</a></li>
            <li><a href="">Another nav item</a></li>
            <li><a href="">More navigation</a></li>
          </ul>
          <ul class="nav nav-sidebar">
            <li><a href="">Nav item again</a></li>
            <li><a href="">One more nav</a></li>
            <li><a href="">Another nav item</a></li>
          </ul>
        </div>
</body>
</html>
```

![](.\img\thymeleaf_bar.png)

> 假设我们要引入templates/commons/bar.html里面的一个公共片段，且公共片段用`th:fragment`命名。假设为topbar。
>
> 只需要在其他页面需要引入的位置使用`<div th:replace="~{commons/bar::topbar}"></div>`引入就好了
>

### 2.开发小技巧

#### 2.1`th:attr`的使用

##### 需求

当我们需要定义一个HTML本身不含有的属性，并且被thymeleaf所识别，可以被jQuery所获取。

#####举例

一个员工列表，每个员工含一个删除按钮且有每个员工的ID。点击删除按钮，发起submit表单提交请求`@{/user/}+${user.id}`。调用JS执行操作。

![](.\img\userlist.png)

1. 给button按钮的class属性添加一个类名`deleteBtn`。用于jQuery获取：`$(".deleteBtn")`

2. 添加自定义属性`del_uri`

   > 方法：使用   `th:attr`属性添加  `th:attr="del_uri=@{/user/}+${user.id}"`   本例中 `+`用于字符串拼接。如果想定义多个属性,使用`,`隔开，如`th:attr="at1=@{/user/}+${user.id}, at2=xxx, at3=xxx "`

```html
<tr th:each="user:${users}">
    <td th:text="${user.id}"></td>
    <td th:text="${user.username}"></td>
    <td>[[${user.password}]]</td>
    <td>[[${user.danWeiTID}]]</td>
    <td>
		<a class="btn btn-sm btn-primary" th:href="@{/user/}+${user.id}">编辑</a>
		<button th:attr="del_uri=@{/user/}+${user.id}" type="submit" class="btn btn-danger 			deleteBtn">删除</button>
	</td>
</tr>
........

<!--
	1.写一个公用的提交删除请求的form表单，设置id="deleteUserForm"，用于jQuery获取
	2.因为HTML表单请求方法只有"get"和"post"请求。当我们要发起"delete"请求时需要在form表单中指定一个		  name="_method"，value="delete"的input标签。并将它隐藏起来。如果要发起PUT请求，同理只需要修改         value="put"就好了。
-->
<form id="deleteUserForm" method="post">
		<input type="hidden" name="_method" value="delete">
</form>
<script type="text/javascript">
		$(".deleteBtn").click(function(){  //获得button点击事件
             //将表单的“action”属性的值替换成当前点击按钮del_uri属性的值，执行submit方法。
			$("#deleteUserForm").attr("action",$(this).attr("del_uri")).submit();
			return false;
		});
</script>
```





------

指错联系：657835775@qq.com