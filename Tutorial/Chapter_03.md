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

