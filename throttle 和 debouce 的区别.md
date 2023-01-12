

debounce(func, wait, options)：创建并返回函数的防反跳版本，将延迟函数的执行（真正的执行）在函数最后一次调用时刻的wait毫秒之后，对于必须在一些输入（多是一些用户操作）停止之后再执行的行为有帮助。将一个连续的调用归为一个，如果连续在wait毫秒内调用，最后只有最后一次会执行
throttle(func, wait, options)：创建并返回一个像节流阀一样的函数，当重复调用函数的时候，最多每隔指定的wait毫秒调用一次该函数；不允许方法在每wait毫秒间执行超过一次，如果连续在wait毫秒内调用，最后执行会均匀分布在大约每wait一次


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
