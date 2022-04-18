## Validate 插件

基于PHP7.4 + 的Validate实现。基于think-validate修改支持PHP8+的通用数据验证器。

## 安装

```shell
composer require luohonen/validate
```

## 基础用法

~~~php
<?php
namespace app\index\validate;

use Luohonen\Validate\Validate;

class UserValidate extends Validate
{
    protected $rule =   [
        'name'  => 'require|max:25',
        'age'   => 'require|number|between:1,120',
        'email' => 'require|email'
    ];

    protected $message  =   [
        'name.require' => '名称必须',
        'name.max'     => '名称最多不能超过25个字符',
        'age.require'  => '年龄必须是数字',
        'age.number'   => '年龄必须是数字',
        'age.between'  => '年龄只能在1-120之间',
        'email.require'=> '邮箱必须是数字',
        'email.email'  => '邮箱格式错误'
    ];
}
~~~

验证器调用代码如下：
~~~php
$data = [
    'name'  => 'name',
    'age'   => 18,
    'email' => '123@qq.com'
];

$validate = new \app\index\validate\UserValidate;

if (!$validate->check($data)) 
{
    var_dump($validate->getError());
}
~~~

## 助手函数（推荐）

验证器调用代码如下：
```php
$data = [
    'name'  => 'name',
    'age'   => 18,
    'email' => '123@qq.com'
];
validate($data, \app\index\validate\UserValidate::class . '.login');
```
> 验证错误会自动抛出异常

更多用法可以参考6.0完全开发手册的[验证](https://www.kancloud.cn/manual/thinkphp6_0/1037623)章节

