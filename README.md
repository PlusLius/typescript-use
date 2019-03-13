# typescript-use

## 基本数据类型

```ts

//基本套路 A:类型 = 类型 ？值 : 报错
//函数类型 function 函数名(参数:类型):返回值类型
//数组  变量:Array<类型> = [值，...]

//布尔类型
let a:boolean = false

//数字类型
let b:number = 10

//字符串
let c:string = '123'

//数组类型
let arr1:number[] = [4,5,6]
let arr2:Array<number> = [7,8,9]

//元组类型
let tuple:[string,number] = ['123',5]

//枚举
enum Cat {
    miao='miao',
    mu='mu'
}
console.log(Cat.mu)

//任意类型
let ok:any = 123

//null or undefined
let x:number
x = 1
x = undefined
x = null

//void类型
function test(obj:string):void{
    console.log(obj)
}

test('123')

//never类型 表示不会出现的值
function test2(obj:string):never{
    throw new Error(obj)
}

//联合类型
let d:string | number
d = '21'
d = 123


```
