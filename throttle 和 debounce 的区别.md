

[参考](https://segmentfault.com/a/1190000014292298)

简述原理:
```
debounce:第一次触发后，进行倒计wait毫秒，如果倒计时过程中有其他触发，则重置倒计时；否则执行。用它来丢弃一些重复的密集操作，直到流量减慢。
throttle:第一次触发后先执行fn（lodash可以通过{leading: false}来取消），然后wait ms后再次执行，在单位wait毫秒内的所有重复触发都被抛弃。
即如果有连续不断的触发，每wait ms执行fn一次，用在每隔一定间隔执行回调的场景。
```

也就是说, debounce 在wait倒计中没有触发就会在wait后执行一次, 如果倒计时中间还有触发,就清空倒计时. throttle 则是按wait 时间间隔抽样执行,```抽样时间间隔内只能执行一次```.


```js
import React from 'react'
import _ from 'lodash';

export default function App() {
  const handle = () => console.log('clicked');
  const handleThrottle = _.throttle(handle, 3000);
  const handleDebounce = _.debounce(handle, 3000);

  const handleChange = (e) => console.log(e.target.value);
  const handleChangeDebounce = _.debounce(handleChange, 3000);
  const handleChangeThrottle = _.throttle(handleChange, 3000);

  return (
    <div>
      <button onClick={handle}>click me fast</button>
      <button onClick={handleThrottle}>click me throttle</button>
      <button onClick={handleDebounce}>click me debounce</button>
      <p>
        <input onChange={handleChange} placeholder='请输入' /><br />
        <input onChange={handleChangeDebounce} placeholder='请输入debounce' /><br />
        <input onChange={handleChangeThrottle} placeholder='请输入throttle' />
      </p>
    </div>
  )
}

```

使用场景:
- mouse move 时```减少计算次数```：debounce
- ```input 中输入文字自动发送 ajax 请求进行自动补全``： debounce
- ajax 请求合并，```不希望短时间内大量的请求被重复发送```：debounce
- 
- ```resize window 重新计算样式或布局```：debounce 或 throttle
- scroll 时触发操作，如 ```随动效果``` ：throttle 
- 对用户输入的验证，不想停止输入再进行验证，而是```每n秒进行验证```：throttle

