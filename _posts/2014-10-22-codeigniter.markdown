---
layout: post
title: "codeigniter读书笔记"
date: 2014-10-21 16:00:00
categories: 读书笔记
---

#### codeigniter简介：

#### codeigniter操作流程：
1. index.php提供了前端的控制器载入codeigniter所需的基本资源。

2. Routing检验HTTP request来决定哪些东西需要被处理.

3. 假如cacheing file存在的话，会直接给浏览器，跳过正常的处理。

4. Security在应用程序控制器被载入之前都会在security进行过滤。

5. 应用程序控制器负责载入各种不同的request所需要的model，core libraries, 辅助函数（helper），以及其它辅助的资源。

6. 最后view建立出来并送给网页浏览器。

#### CodeIgniter架构目标：
用最小，最轻盈的套件，呈现最大的效能、相容以及弹性。

#### 分段式URI：
example.com/class/function/ID
第一段代表的是控制器的启动的类别。第二段代表的是控制器类别的函数。第三段代表的是Id或者任何准备传给控制器使用的参数。

#### CodeIgniter中的保留字:
1. 控制器名称：`Controller`, `CI_Base`, `_ci_initialize`, `Default`, `index`。

2. 函数：`is_really_writable()`, `load_class()`, `get_config()`, `config_item()`, `show_error()`, `show_404()`, `log_message()`, `_exception_handler()`, `get_instance()`;

3. 变量: `$config`, `$mimes`, `$lang`。

4. 常数: `ENVIRONMENT`, `EXT`, `FCPATH`, `SELF`, `BASEPATH`, `APPPATH`, `CI_VERSION`, `FILE_READ_MODE`, `FILE_WRITE_MODE`, `DIR_READ_MODE`, `DIR_WRITE_MODE`, `FOPEN_READ`, `FOPEN_READ_WRITE`, `FOPEN_WRITE_CREATE_DESTRUCTIVE`, `FOPEN_READ_WRITE_CREATE_DESTRUCTIVE`, `FOPEN_WRITE_CREATE`, `FOPEN_READ_WRITE_CREATE`, `FOPEN_WRITE_CREATE_STRICT`, `FOPEN_READ_WRITE_CREATE_STRICT`。

#### 辅助函数：
如同它的名称，辅助函数协助来处理特定的任务。每个辅助函数都是特定用途函数的集合。
载入辅助函数：`$this->load->helper('name');`
扩充辅助函数：只要在application/helpers/ 中的helper文档使用`MY_`开头就可以增加或者覆盖原有的辅助函数。

#### 程序库：
所有可用的程序库都在system/libraries目录下面。大部分情况可以通过controller来进行载入，也可以建立自己的程序库。需要新建在application/libraries中。
1. 可以建立自己的程序库。
2. 可以继承原有的程序库。
3. 可以取代原有的程序库。
命名规则：文档的第一个字母必须大写。类别声明的第一个字母必须大写。类别声明和文档名称必须相同。

#### 自动载入资源：

#### hooks:
CodeIgniter的Hooks机制提供了一个方法来进入并改变框架的内部作业而不用修改核心文档，
1. 启动Hooks: 可以在`application/config/config.php`档案中设定项目来启动。
2. 自定义一个Hooks: Hooks定义在`application/config/hooks.php`中，定义如下：
```php
$hook['pre_controller'] = array(
    'class'=>'MyClass',
    'function'=>'Myfunction',
    'filename'=>'MyClass.php',
    'filepath'=>'hooks',
    'params'=>'',
    )
```
3. 在同一个hooks中多次呼叫:

4. Hook插入点:`pre_system`, `pre_controller`, `post_controller_constructor`, `post_controller`, `display_override`, `cache_override`, `post_system`。

#### 通用函数：
CodeIgniter使用少许几个全局函数来协助运行。
`is_php('version_number')`, `is_really_writable('path/to/file')`, `config_item('item_key')`, `show_error('message')`, `show_404('page')`, `log_message('level', 'message')`, `set_status_header(code, 'text')`, `remove_invisible_characters($str)`, `html_escape($mixed)`.

#### URI路由：
路由规则设定在application/config/routes.php中。
通配符：`(:num)`:匹配只有数字的一个片段。`(:any)`:匹配含有任何字符的一个片段。
保留的路由：`$route['default_controller']='welcome'`, `$route['404_override'] = '';`

#### cache:
启动cache的方式：`$this->output->cache(n);`