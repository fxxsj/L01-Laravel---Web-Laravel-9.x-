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

### 4.3. Laravel 前端工作流

1. 搞清楚 Laravel 是如何利用 Sass, NPM, Yarn, Laravel Mix 来构成一套完整的前端工作流。

#### SASS 语法基础

1. Sass 使用 `@import` 来导入其它的样式文件。如：

``` @import '~bootstrap/scss/bootstrap';  #将导入 node_modules/bootstrap/scss/bootstrap.scss 文件 ```

2. Sass 还允许你在代码中加入变量，所有的变量均以 $ 开头。

```
$navbar-color: #3c3e42;    #定义了一个 $navbar-color 颜色变量
.navbar-inverse {
  background-color: $navbar-color;
}
```

3. Sass 还允许你在选择器中进行相互嵌套，以减少代码量。

4. 可以在 Sass 嵌套中使用 & 对父选择器进行引用

#### NPM, Yarn, Laravel Mix

1. 在本教程中，出于安装速度考虑，我们使用更加现代化的 Yarn 来替代 NPM 的包管理功能。然而我们仍然会使用到 NPM 的任务管理功能，如命令 `npm run watch-poll`。

2. Laravel 自带 yarn.lock 文件，此文件的作用与 composer.lock 一致，是为了保证项目依赖代码版本号绝对一致而存在的。

3. 我们可以在 webpack.mix.js 文件中制定一些如资源文件的编译、压缩等任务。Laravel 已默认为我们生成了 webpack.mix.js 文件，并集成了 laravel-mix 模块

4. 使用 Mix 很简单，首先你需要使用以下命令安装 npm 依赖：

```
yarn install
```

安装成功后，运行以下命令即可：

```npm run watch-poll```

### 4.4. 浏览器缓存问题

1. 现代化的浏览器，会对静态文件进行缓存，静态文件在本课程的范畴内，指的是 .css 、.js 后缀的文件。

2. 针对浏览器缓存问题，Laravel Mix 给出的方案是为每一次的文件修改做哈希处理。需要对 webpack.mix.js 稍作修改：

```
const mix = require('laravel-mix');

mix.js('resources/js/app.js', 'public/js')  

   .sass('resources/sass/app.scss', 'public/css').version();

```

修改模板，使其动态加载样式代码：

```
<link rel="stylesheet" href="{{ mix('css/app.css') }}">
```

mix() 方法与 webpack.mix.js 文件里的逻辑遥相呼应。

### 4.5. 局部视图

1. 随着后面顶部导航功能愈加完善，代码量也会越来越多，如果把所有代码都放在默认视图文件中，会让这个文件变得无法维护，这明显不符合 Laravel 项目开发的最佳实践。因此我们需要把顶部导航从 default 视图中分离出来，成为一个单独的头部视图。

2. 在头部视图的文件名前面加了下划线 _，这样做是为了指定该视图文件为局部视图，为局部视图增加前缀下划线是『约定俗成』的做法，方便了其它人快速地理解该文件的实际作用。

3. `@include` 是 Blade 提供的视图引用方法，可通过传参一个具体的文件路径名称来引用视图。

### 4.6. 布局中的链接

1. {{　}} 是在 HTML 中内嵌 PHP 的 Blade 语法标识符，表示包含在该区块内的代码都将使用 PHP 来编译运行。route() 方法由 Laravel 提供，通过传递一个具体的路由名称来生成完整的 URL。

2. 在 Laravel 中，我们可以通过在路由后面链式调用 name 方法来为路由指定名称：

```
Route::get('/help', 'StaticPagesController@help')->name('help');  #在实际开发中养成对路由的命名是一个好习惯，可以帮助我们节省很多工作量，另外也是 Laravel 项目开发的最佳实践。
```