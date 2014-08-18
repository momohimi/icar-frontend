
ICT框架
====

ICT框架是适用于PP租车的前端工程化解决方案。

开发：高峰(gaofeng@ppzuche.com)

文档：高静华(gaojinghua@ppzuche.com)

----

依赖 {#depends}
----
**Fat-Free Framework** [<i class="icon-share"></i>官网][1]

一个轻量的PHP框架。

> 因为历史原因使用，ICT封装了F3的模板接口，与F3保持兼容

**FIS** [<i class="icon-share"></i>官网][2]

FIS是专为解决前端开发中自动化工具、性能优化、模块化框架、开发规范、代码部署、开发流程等问题的工具框架。

> FIS有完整的静态资源管理解决方案，若使用grunt需要自己实现。
> 注：第一次使用需安装FIS，安装方法见FIS官网。

----

目录结构 {#dir_stander}
----
标准结构如下：

    -ICT
        - pc
          - common
            - layout
              - base
                  base.html
            + lib
            - widget
              - header
                + images
                  header.html
                  header.css
                  header.js
              + footer
          - user
            - page
              - signup
                - signup.html
            + widget
          fis-conf.js
        + mo
    
说明：

**系统(System)**

> 在ICT目录下，按终端划分为两个独立的系统：pc和mo。 pc对应PC-web业务，mo对应MO-web业务。
> 系统保持自身独立，不互相影响。

> **fis-conf.js**
> 每个系统目录下有一个对应的fis-conf.js文件，用于配置编译和部署。

**模块(module)**
> 按复用性分为分公共模块和普通模块两类
> **公共模块common** 每个系统有且只有一个，用于放置系统内可复用的layout、widget
> **普通模块** 每个系统有N个，按业务逻辑划分，个数和命名不限。

> 模块下有以下几类结构Type：

 - **布局(Layout)**
   > 定义页面的结构，可继承。
   
 - **组件(widget)**
   
       按业务划分的最小功能单元，目录结构如下：
       widgetName
          - images
            - img_a.png
            - img_b.jpg
          - widgetName.html
          - widgetName.css
          - widgetName.js
       
 - **页面(Page)**
   > 业务入口，后承action，前接layout,加载widget实现页面。

----
资源管理 {#resource}
----
**资源路径**

> **System:Module/Type/Name.ext**

> 例：
> mo:common/layout/base
> pc:common/widget/city_switch.js

> 注：如果文件类型是html时,ext可省略

**资源定位**：
> 获取任何开发中所使用资源的线上路径

**内容嵌入**：
> 把一个文件的内容(文本)或者base64编码(图片)嵌入到另一个文件中

**依赖声明**: 
> 在一个文本文件内标记对其他资源的依赖关系

**资源地图**
> map.json

----

API {#API}
----
**PHP**
```
$html = ICT_View::load($path, $data);
参数说明：
    $path: 资源路径
    $data: 自定义数据
```

以下为FIS支持的特性，详见[<i class="icon-share"></i>官网][3] 

**HTML**

```
嵌入资源
给资源加?__inline参数将资源嵌入html中

声明依赖
在注释中声明 @require path
```

**JS**

```
声明JS模块依赖
var mod = require(path);或在注释中@require path

加载资源
var resource = __url(path);

在js中嵌入资源
__inline(path);
    
``` 
    
**CSS**

```  
在CSS中嵌入文件
@import url(path)

嵌入图片
给资源加?__inline参数将资源嵌入

声明依赖
在注释中声明 @require path
```  

----

发布 {#release}
----

线下使用：
> **fis relase -d local**

上线前使用：
> **fis release -pomd local**

----






























  [1]: http://fatfreeframework.com/home
  [2]: http://fis.baidu.com/
  [3]: http://fis.baidu.com/docs/more/fis-standard.html
