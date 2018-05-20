# axios-example
axios的例子及分析

[axios](https://github.com/axios/axios) 是一个基于 promise 的 HTTP 库，可以用在浏览器和 node.js 中

## axios库的特性

-   从浏览器创建XMLHttpRequest
-   从node.js创建http请求
-   支持Promise API
-   拦截请求与响应
-   转换请求与响应数据
-   取消请求
-   自动转换JSON数据
-   支持客户端XSRF攻击防护

## axios的应用和源码解析

### 实现各种简便调用

-   如何简便使用

既能axios(url, option)
又能axios(url, option)
还能axios.get(url, option)

-   看源码如何实现


### header

-   如何设置

``` javascript

// 设置通用header
axios.defaults.headers.common['X-Requested-With'] = 'XMLHttpRequest'; // xhr标识
axios.defaults.headers.common['withCredentials'] = true; // 跨域携带cookie

// 设置某种请求的header
axios.defaults.headers.post['Content-Type'] = 'application/x-www-form-urlencoded;charset=utf-8'; // 跨域携带cookie

// 设置某次请求的header
axios.get(url, {
  headers: {
    'Authorization': 'whr1',
  },
})

```

-   看源码如何实现

``` javascript

// /lib/core/dispatchRequest.js  -  44行

  config.headers = utils.merge(
    config.headers.common || {},
    config.headers[config.method] || {},
    config.headers || {}
  );

```


### 如何支持Promise

-   xhr篇

-   http篇


### 如何取消请求

-   如何设置

-   看源码如何实现


### 自动转换JSON数据
在默认情况下，axios将会自动的将传入的data对象序列化为JSON字符串，将响应数据中的JSON字符串转换为JavaScript对象

-   看源码如何实现


### 如何监听进度

-   如何设置

-   看源码如何实现


### 超时配置及处理

-   如何设置

```javascript

axios.defaults.timeout = 3000;

```

-   看源码如何实现

```javascript

// /adapters/xhr.js  -  48行
request.timeout = config.timeout;

// /adapters/xhr.js  -  94行
request.ontimeout = function handleTimeout() {
  reject(createError('timeout of ' + config.timeout + 'ms exceeded', 
    config, 'ECONNABORTED', request));
};

```

-   axios库外如何添加超时后的处理

```javascript

axios().catch(error => {
  const { message } = error;
  if (message.indexOf('timeout') > -1){
    // 超时处理
  }
})

```




### 请求失败的错误处理


### 改写验证成功或失败的规则 validateStatus

-   如何设置

-   看源码如何实现


### 如何 拦截请求、响应，并修改请求参数、修改响应数据

-   如何设置

-   看源码如何实现


### 转换请求与响应数据

-   如何设置

-   看源码如何实现

-   备注：但拦截器同样可以实现该功能，且拦截器可取消某个拦截，可异步处理，可对错误进行处理等，管理起来更方便


### 如何支持客户端XSRF攻击防护

-   如何设置

-   看源码如何实现
