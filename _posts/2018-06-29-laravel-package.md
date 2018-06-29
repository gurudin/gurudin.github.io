---
layout:     post
title:      Laravel package 扩展包开发 一
subtitle:   扩展包开发
date:       2018-06-29
author:     Gurudin
# header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    - laravel
    - package
    - composer
---

#### 创建目录并初始化
``` mkdir -p packages/gurudin/rms ```
![avatar](/img/2018-06-29/1.png)
1. packages 扩展包存放目录
2. gurudin 作者名称目录，一般是github用户名
3. rms 扩展包具体名称

#### 初始化 composer 配置,在 rms 目录下运行
``` composer init ```

按照指示填写信息即可,成功后在rms目录下会创建出composer.json文件，内容如图：
![avatar](/img/2018-06-29/2.png)

#### 创建逻辑代码存放目录
在rms目录下创建src文件夹
``` mkdir src ```

#### 在laravel项目根目录下的composer.json去声明包的命名空间
![avatar](/img/2018-06-29/3.png)

#### 新建一个Service Provider,将新创建文件从 app/Providers 移动到packages/gurudin/rms/src 目录下（注意修改 namespace）
``` php artisan make:provider RmsServicProvider ```

#### 创建Controller 和 routes 文件
```
# RmsController.php 文件
namespace Gurudin\Rms\Controller;

use App\Http\Controllers\Controller;

class RmsController extends Controller
{

    public function index()
    {
        return view('rms::rms');
    }

}

# routes.php 文件
Route::get('rms', 'Gurudin\Rms\Controller\RmsController@index');
```

#### 创建 view
src 目录下创建 views文件夹，创建文件rms.blade.php 
内容随便写的什么先。

#### 添加 providers 到 config/app.php 的providers数组里面。
``` Gurudin\Rms\RmsServiceProvider::class, ```

#### 最后根目录添加autoload依赖
``` composer dump-autoload ```

#### 访问 http://localhost/rms 查看结果，不报错就是搭建成功。

#### 最终目录结构
![avatar](/img/2018-06-29/4.png)





