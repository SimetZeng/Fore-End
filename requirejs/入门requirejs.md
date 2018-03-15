# 概述
RequireJs是个小巧的Javascript模块载入框架，是AMD规范最后的实现着之一。最新版本的RequireJS压缩后只有14k，非常的轻量。它还可以和其他的框架协同工作，使用RequireHS会使前端代码质量得以提升。

# 优点
优点就是模块化的优点了：
- 作用域污染
- 放在代码暴露可被修改
- 维护成本的提升
- 复用和效率

# 全局配置
requirejs提供了一种‘主数据’的功能--main.js。加载requirejs脚本的script标签加入了data-main属性，此属性指定的js将在加载完require.js后处理，将require.config的配置加到data-main后，就可以让每个页面都使用这个配置，然后界面中就可以直接使用require来加载所有的短模块名。
```
require.config({
  paths: {
    'jquery': ['http://libs/baidu.com/jquery/2.0.3/jquery', 'js/jquery']
  }
})
```
