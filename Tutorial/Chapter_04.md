# 第四章 优化页面

### 4.1. 章节说明

1. 本章节将针对前面创建的几个静态页面进行样式优化，并在本章节的最后面为接下来的用户注册功能准备好一个注册页面。

### 4.2. 样式美化

1. Bootstrap#

在本书的教学过程中将使用 Bootstrap 来作为演示应用的前端框架。Bootstrap 的 [官方文档](https://getbootstrap.com/)

2. Laravel 项目中使用 Bootstrap 前端框架，需要先执行以下命令：

```
composer require laravel/ui:3.4.5 --dev
```

说明：`composer require` 是用来安装扩展包使用的命令，参数 `--dev` 是指定此扩展包只在开发环境中使用。

上面的命令安装完成后，使用以下命令来引入 Bootstrap ：

```
php artisan ui bootstrap
```

3. 对于NPM 扩展包，我们重点看以下几个：

3.1 bootstrap —— Bootstrap NPM 扩展包；  

3.2 laravel-mix —— 由 Laravel 官方提供的静态资源管理工具。

3.3 由于 NPM 的安装速度，安全性和稳定性等都饱受开发者的诟病。因此我们在教程中改用 Facebook 在 2016 年的 10 月份开源的 Yarn 来作为 NPM 的替代品

3.4 由于国内的网络环境原因，我们在使用 NPM 安装第三方模块时会耗费较长时间，我们可通过淘宝提供的加速镜像来解决该问题

```
npm config set registry=https://registry.npm.taobao.org

yarn config set registry 'https://registry.npm.taobao.org'

```
3.5 使用 `Yarn` 对扩展包进行安装

```
SASS_BINARY_SITE=http://npm.taobao.org/mirrors/node-sass yarn  #在 yarn 命令前添加 SASS_BINARY_SITE=http://npm.taobao.org/mirrors/node-sass 的目的是告诉 yarn 到淘宝的镜像去下载 node-sass 二进制文件。

yarn add cross-env
```

4. 通过下面的命令，在每次检测到 .scss 文件发生更改时，自动将其编译为 .css 文件 

``` npm run watch-poll ```

如果报错，按照指示安装 `resolve-url-loader`

``` yarn add resolve-url-loader@^5.0.0 --dev ```