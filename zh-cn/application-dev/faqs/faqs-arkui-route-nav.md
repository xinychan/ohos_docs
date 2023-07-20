# ArkUI路由/导航开发常见问题(ArkTS)

## router中params无法正常传递class对象

适用于：OpenHarmony 3.2 Beta5 ，API 9 Stage模型

只能传递对象中的属性，无法传递对象中的方法。

## 在Stage模型下，如何通过router实现页面跳转 

适用于：OpenHarmony 3.2 Beta5 ，API 9 Stage模型

1.  对于通过页面路由router实现页面跳转，首先要在main\_pages.json配置文件中将所有跳转的页面加入pages列表；
2.  页面路由需要在页面渲染完成之后才能调用，在onInit和onReady生命周期中页面还处于渲染阶段，禁止调用页面路由方法。

**参考链接：**[页面路由](../reference/apis/js-apis-router.md)

## router通过调用push方法进堆栈的page是否会被回收

适用于：OpenHarmony 3.2 Beta5 ，API 9 Stage模型

调用push进入堆栈的page不回收，调用back方法出栈后可以被回收。

**参考链接：**[Router传递参数](../reference/apis/js-apis-router.md#routergetparams)

