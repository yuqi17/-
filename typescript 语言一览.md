#### typescript 的好处, 可以让代码更健壮,更精确, 规范, 很多问题在编译过程中就能给出提示, 可以简化逻辑,可以让代码可读性更高; 它是js的超集, 没有js 轻省, 易用;

对于js 开发者来说, 一般除了图片上红色框需要重点花时间去学习一下, 其他的是比较容易理解的
![image](https://user-images.githubusercontent.com/10356819/212884178-74779586-1b55-4652-aa3a-250f6ed83915.png)

[图片中的学习目录](https://www.tslang.cn/docs/handbook/basic-types.html)


#### typescript 中的一些奇特的符号:

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

type Name = { 
  name: string; 
}
type User = Name & { age: number  };// 多类型叠加,跟interface 不同, interface 用的是extends


//========= 如果要给type 或者 interface 默认值可以这样

// 这种只适合一个参数的情况
function Employee({
  name = 'Alice',
  age = 30,
  country = 'Austria',
}: EmployeeProps) {
  return (
    <div>
      <h2>{name}</h2>
      <h2>{age}</h2>
      <h2>{country}</h2>
    </div>
  );
}

//或者

interface IStyle {
  width: number;
  height: number;
}

function show(style: IStyle = { width: 200, height: 300 }): void {
  console.log(style)
}
```

[type 和 interface 的区别](https://juejin.cn/post/6844903749501059085)

#### typescript 比较新的基本类型
1. 下面的代码可以保证any 类型的编译时期不报警告, object 则不行
```js
let notSure: any = 4;
notSure.ifItExists(); // okay, ifItExists might exist at runtime
notSure.toFixed(); // okay, toFixed exists (but the compiler doesn't check)

let prettySure: Object = 4;
prettySure.toFixed(); // Error: Property 'toFixed' doesn't exist on type 'Object'.
```

2. void 跟 any 正好相反, void 类型变量,只能有undefiend 和 null, 通常不这么设置
3. undefined和null两者各自有自己的类型分别叫做undefined和null。 和 void相似，它们的本身的类型用处不是很大
4. never never类型是任何类型的子类型; 即使 any也不可以赋值给never;
![image](https://user-images.githubusercontent.com/10356819/212883029-b117045c-fbd7-4dca-a2bd-f623a920ac2f.png)

#### [高级类型](https://www.tslang.cn/docs/handbook/advanced-types.html)


