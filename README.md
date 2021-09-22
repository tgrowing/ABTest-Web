---------------

TAB云实验平台web sdk

## Installation

1. import script

```html
<!-- 使用灯塔sdk上报实验事件 -->
<script src="https://beaconcdn.qq.com/sdk/3.1.42/beacon_web.min.js"></script> 
<!-- 实验SDK -->
<script src="https://res.abtest.qq.com/tabc_saas/tabc_sdk.min.js"></script>
```

## Usage

### 1. 集成SDK:

```js
tabc.init(  // 只能初始化一次
{ 
  appkey: "申请的appkey", 
  guid: "用户的唯一id", // 传人一个用户身份，用来做分流标识
  // isTest: true, // 使用测试环境
  // timeout: 1, // http超时设置，单位秒。 默认2s
  // profiles: {'sexy':'male'}, // 用户属性，可以用来做标签实验
  // antiFlicker: true,   // 打开防闪烁开关，原理是先隐藏原有页面，待sdk init完成后将页面显示出来
  // antiFlickerTimeout: 500, //防闪烁超时时间，超过此时间无论sdk是否完成init都会将隐藏的页面放出来，防止异常情况下页面一直白。默认500毫秒。
  onInit: function(data) { // 初始化完成，加载完本地缓存策略
    console.log('init fniish');
  }, 
  onNetData: function (data) { // 加载完成网络策略
    console.log('net fniish');
  }
});
```

### 2. 相关API:
web实验支持可视化编辑和下发配置，一般不需要代码实验。
如果需要一定的参数逻辑，可以使用下面的API

`getExpByName(**)`
``` json
{
  grayId: 123, params:{...}
}
```
> 通过实验名称获取实验 

`reportExpExpose(exp)`

> 上报一次实验曝光

`reportExpEvent('someclick', exp)`

> 上报一次实验事件

`getAllParams()`
``` json
[{
    grayId: ***, param: { key: val, key2: val2 ...}
}, ...]
```
> 返回所有命中的实验id及其对应的参数 

`getParam(paramKey)`
``` json
{
    grayId: ***, value: ***
}
```
> 返回所命中实验里面对应paramKey的参数值及其对应的实验id


`forceUpdate()`
> 此api的作用是强制更新实验样式，在页面有二次刷新导致实验效果被覆盖的情况下使用（如ssr的页面直出后应用了实验效果，但异步加载数据又覆盖了实验效果）。

### License
ISC
