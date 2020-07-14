# 实现一个对象的for...of功能



### 思路

实现Symbol.iterrator。

可以是生成器，可以是实现next







### 实现1（生成器）

```js
var myIterable = {}
myIterable[Symbol.iterator] = function* () {
    let keys = Object.keys(this)
	let values = keys.map(key=>this[key])
	for(let i=0; i<values.length; i++){
        yield values[i]
    }
};
[...myIterable] // [1, 2, 3]
```



### 实现2（next）

```js
var myIterable = {}
myIterable[Symbol.iterator] = function(){
    let values = Object.keys(this).map(key=>this[key])
    let i = 0
	return {
        next(){
            if(i<values.length){
                return {
                    done: false,
                    value: values[i++]
                }
			}else{
                return {done: true}
            }
        }
    }
}
```

