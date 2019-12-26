基本用法

**数据模板中的每个属性由 3 部分构成：属性名、生成规则、属性值：**

```js
// 属性名   name
// 生成规则 rule
// 属性值   value
'name|rule': value
```

**注意：**

- *属性名* 和 *生成规则* 之间用竖线 `|` 分隔。

- *生成规则* 是可选的。

- 生成规则

   

  有 7 种格式：

  1. `'name|min-max': value`
  2. `'name|count': value`
  3. `'name|min-max.dmin-dmax': value`
  4. `'name|min-max.dcount': value`
  5. `'name|count.dmin-dmax': value`
  6. `'name|count.dcount': value`
  7. `'name|+step': value`

- 生成规则的 含义 需要依赖 属性值的类型才能确定。

- *属性值* 中可以含有 `@占位符`。

- *属性值* 还指定了最终值的初始值和类型。

```js
var data = Mock.mock({
    'list|1-10': [{
        'id|+1': 1,
        'range|20-30': 20,
        'count|6': '*',
        'price|10-20.1-2': 10,
        'countd|1': Mock.Random.email(),
        'countReg|1-2': /[a-z][A-Z][0-9]/,
        'array|1-2': [1, 2, 3, 4, 5, 6, 7, 8, 9, 10],
        first: '@FIRST',
        last: '@LAST',
        // text: Mock.Random.paragraph(),
        full: '@first @last @countd @email @color @email',
        paragraph: '@paragraph(2)',
        paragraph2: Mock.Random.paragraph(3)
    }]
})
```





怎么拦截

实现原理

```js
/* global window, document, location, Event, setTimeout */
/*
    ## MockXMLHttpRequest

    期望的功能：
    1. 完整地覆盖原生 XHR 的行为
    2. 完整地模拟原生 XHR 的行为
    3. 在发起请求时，自动检测是否需要拦截
    4. 如果不必拦截，则执行原生 XHR 的行为
    5. 如果需要拦截，则执行虚拟 XHR 的行为
    6. 兼容 XMLHttpRequest 和 ActiveXObject
        new window.XMLHttpRequest()
        new window.ActiveXObject("Microsoft.XMLHTTP")

    关键方法的逻辑：
    * new   此时尚无法确定是否需要拦截，所以创建原生 XHR 对象是必须的。
    * open  此时可以取到 URL，可以决定是否进行拦截。
    * send  此时已经确定了请求方式。

    规范：
    http://xhr.spec.whatwg.org/
    http://www.w3.org/TR/XMLHttpRequest2/

    参考实现：
    https://github.com/philikon/MockHttpRequest/blob/master/lib/mock.js
    https://github.com/trek/FakeXMLHttpRequest/blob/master/fake_xml_http_request.js
    https://github.com/ilinsky/xmlhttprequest/blob/master/XMLHttpRequest.js
    https://github.com/firebug/firebug-lite/blob/master/content/lite/xhr.js
    https://github.com/thx/RAP/blob/master/lab/rap.plugin.xinglie.js

    **需不需要全面重写 XMLHttpRequest？**
        http://xhr.spec.whatwg.org/#interface-xmlhttprequest
        关键属性 readyState、status、statusText、response、responseText、responseXML 是 readonly，所以，试图通过修改这些状态，来模拟响应是不可行的。
        因此，唯一的办法是模拟整个 XMLHttpRequest，就像 jQuery 对事件模型的封装。

    // Event handlers
    onloadstart         loadstart
    onprogress          progress
    onabort             abort
    onerror             error
    onload              load
    ontimeout           timeout
    onloadend           loadend
    onreadystatechange  readystatechange
 */

var Util = require('../util')

// 备份原生 XMLHttpRequest
window._XMLHttpRequest = window.XMLHttpRequest
window._ActiveXObject = window.ActiveXObject
```







fetch？