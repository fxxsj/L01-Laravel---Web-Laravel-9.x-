# 第三章 构建页面

###  3.1. 章节说明

从本章节开始，我们将使用 Laravel 开发一个类似新浪微博的网站。整个网站功能包括：

用户的注册登录

用户个人信息的更改

使用管理员权限删除用户

发布微博

关注用户

查看关注用户的微博动态

### 3.2. 创建应用

1. 创建应用命令

`composer create-project laravel/laravel weibo --prefer-dist "9.1.*"`

2. getenv 方法的使用

`>>> getenv('APP_ENV')`

3. art tinker（php artisan tinker） 是 Laravel 框架自带的命令，用以调出 Laravel 的交互式

4. Git 代码版本控制

`cd ~/Code/weibo`

`git init`

`git add -A`

`git commit -m "Initial commit"`

### 3.3. 统一代码风格

1. 在 Laravel 应用的根目录下修改 .editorconfig 文件

### 3.4. 静态页面

1.1新建分支 首先让我们使用 Git 来新建一个 static-pages 分支。  

```
git checkout master   #代表将当前分支切换到 master 分支上  
git checkout -b static-pages  #创建一个名为 static-pages 的新分支。-b 选项表示创建指定名称的新分支
```

1.2.合并分支示例：
```
git merge fake-branch
```

1.3.删除分支示例：
```
git branch -d fake-branch
```  

2. 移除无用视图

```
rm resources/views/welcome.blade.php
```

3. 配置路由  

在 Laravel 中我们较为常用的几个基本的 HTTP 操作分别为 GET、POST、PATCH、DELETE。  

GET 常用于页面读取  

POST 常用于数据提交

PATCH 常用于数据更新

DELETE 常用于数据删除

在这四个动作中，PATCH 和 DELETE 是不被浏览器所支持的

4. 生成静态页面控制器,Laravel 的控制器命名规范统一使用 `驼峰式大小写` 和复数形式来命名  

```
php artisan make:controller StaticPagesController
```

4.2  `app/Providers/RouteServiceProvider.php` 路由的服务提供者

4.3 添加静态页面视图  

要在控制器中指定渲染某个视图，则需要使用到 `view` 方法，`view` 方法接收两个参数，第一个参数是视图的路径名称，第二个参数是与视图绑定的数据，第二个参数为可选参数。

### 3.5. 模板切分

1. DRY（Don’t repeat yourself）原则

2. Laravel 的 Blade 模板支持继承，这意味多个子视图可以共用父视图提供的视图模板。

2.1 我们使用了 @extends 并通过传参来继承父视图 layouts/default.blade.php 的视图模板。

```
@extends('layouts.default')
```

2.2 使用 @section 和 @stop 代码来填充父视图的 content 区块

```
@section('content')
  <h1>主页</h1>
@stop
```

2.3 `@yield` 区块,两个参数，第一个参数是该区块的变量名称，第二个参数是默认值.

2.4 当 `@section` 传递了第二个参数时，便不需要再通过 `@stop` 标识来告诉 Laravel 填充区块会在具体哪个位置结束。
