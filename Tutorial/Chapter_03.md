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

1.创建应用命令

`composer create-project laravel/laravel weibo --prefer-dist "9.1.*"`

2.getenv 方法的使用

`>>> getenv('APP_ENV')`

3.art tinker（php artisan tinker） 是 Laravel 框架自带的命令，用以调出 Laravel 的交互式

4.Git 代码版本控制

`cd ~/Code/weibo`

`git init`

`git add -A`

`git commit -m "Initial commit"`

### 3.3. 统一代码风格

1.在 Laravel 应用的根目录下修改 .editorconfig 文件

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

2.移除无用视图

```
rm resources/views/welcome.blade.php
```

3.配置路由  

在 Laravel 中我们较为常用的几个基本的 HTTP 操作分别为 GET、POST、PATCH、DELETE。  

GET 常用于页面读取  

POST 常用于数据提交

PATCH 常用于数据更新

DELETE 常用于数据删除

在这四个动作中，PATCH 和 DELETE 是不被浏览器所支持的

4.生成静态页面控制器,Laravel 的控制器命名规范统一使用 `驼峰式大小写` 和复数形式来命名  

```
php artisan make:controller StaticPagesController
```

4.2 `app/Providers/RouteServiceProvider.php` 路由的服务提供者