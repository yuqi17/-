
#### 特别注意json字符串中的key, value 是用""来包裹的, 不要用单引号'', 这样是解析不出来的.

对于已经有单引号返回的json 字符串,可以先替换后再转换成 json对象:
```js
JSON.parse(value.replace(/\'/g, '"'))
```
