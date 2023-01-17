

typescript 中的一些奇特的符号:

![image](https://user-images.githubusercontent.com/10356819/212843994-422bdfc5-1228-4490-a345-da40a8ef9c33.png)

以下是根据上面图片做的一些代码:
```js
const a = 0;
const b = a || "xxx"
const c = a ?? 'yyy' // 空值合并运算符

console.log(b, '<<<<')// 返回 'xxx'
console.log(c, '<<==')// 返回 0 跟 || 不一样的是它不会把左边的值当作布尔值运算


const d = {
    a:{
        test(){
            console.log('hihi')
        },
        b:1
    }
}

function test(d:any){
    // 非控断言操作符

    console.log(d!.a!.c,'<<<<')
    
    //d!.a!.test1()//方法如果找不到则返回undefined 之后当作函数执行还是会报错
    
    // 可选链
    console.log(d?.a?.c,'===')
    d.a.play?.();// ?. 这种写法比较特殊, 后面可以跟[key]
    d.a.test?.();
}

test(d);

interface Node {
    name?:string;// 可选属性
    prop:string|number;// 多种类型中的一种
    // num:number = 1_2; 接口是不能有默认值
}

type Tree = {
    // branch:string = 'xx'; type 也不能有默认值
}

function render(node:Node){
    console.log(node)
}

render({name:'1x', prop:1} as Node)// 这里用as Node 防止编译器报警告
```
