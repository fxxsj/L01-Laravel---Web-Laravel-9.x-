# 第五章 用户模型

### 5.1. 章节说明

1. 本章我们将构建一个基本的用户模型来实现用户数据的存储，并了解 Laravel 如何对模型对象进行增删改查操作。

2. 如果完全借助 Laravel 提供的用户认证系统，我们能够在短短几分钟便完成整个登录注册功能的开发，包括用户数据库的整个构建过程。

3. 用到数据模型 - Model，利用 Laravel 提供的 Eloquent ORM 跟数据库进行交互，实现用户数据的增删改查操作。

4. Active Record 是一种领域模型模式，该模式由 Martin Fowler 在 2003 年出版的《企业应用架构模式》一书中进行了详细叙述并命名。其特点是一个模型类对应关系型数据库中的一个表，模型类的一个实例对应表中的一行记录。Active Record 最大优点是允许我们简单，直观地操作数据层。

###　5.2. 数据库迁移

1. 所有创建的迁移文件都被统一放在 database/migrations 文件夹里。

2. 若要了解更多 $table 的可用方法，可查阅 [官方文档](https://learnku.com/docs/laravel/9.x/migrations#creating-tables)

### 5.3. 查看数据库表

1. 在 Mac 上，我们可以通过安装 `Sequel Ace` 来进行数据库的一些操作，如查阅数据或删除数据。

2. 如果你是使用 Windows 机器进行开发，推荐使用 `HeidiSQL` 。连接信息从上面读取。

3. 运行下面的命令来生成执行迁移，migrate 命令会执行所有未被执行过的迁移

```
php artisan migrate
```

4. 在日常开发中，我们有时候也需要通过下面的方式来回滚到最近一次执行的迁移。回滚执行成功后，两个表都将被删除。

```
php artisan migrate:rollback
```

### 5.4. 模型文件

1. Laravel 默认为我们生成的用户模型中包含了不少代码，我们主要将精力放在用户模型中定义的三个属性 `$casts`, `$fillable`, `$hidden` 上。`$casts` 属性是用来指定数据库字段使用的数据类型，`fillable` 在过滤用户提交的字段，只有包含在该属性中的字段才能够被正常更新;当我们需要对用户密码或其它敏感信息在用户实例通过数组或 JSON 显示时进行隐藏，则可使用 `hidden` 属性.

2. 一般情况下，如果我们要自己手动创建一个模型文件，最简单的方式是通过 `make:model` 来创建。需要注意的一点是，模型类名称使用 单数 形式来命名：

```
php artisan make:model Article
```

3. 如果需要在创建模型的同时顺便创建数据库迁移，则可以使用 `--migration` 或 `-m` 选项

```
php artisan make:model Article -m
```

4. 在Eloquent 数据模型中，Eloquent Article 模型默认情况下会使用类的「下划线命名法」与「复数形式名称」来作为数据表的名称生成规则。

5.  Eloquent 将会假设 Article 模型被存储记录在 articles 数据表中。如果你需要指定自己的数据表，则可以通过 table 属性来定义，如：

```
protected $table = 'my_articles';
```

6. 『约定优于配置』（convention over configuration），也称作按约定编程，这是一种软件设计范式，旨在减少软件开发人员需做决定的数量，获得简单的好处，而又不失灵活性。