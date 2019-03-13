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

## 函数

```ts
//函数定义,可选参数和返回类型,剩余参数
function hello(name:string,age?:number,...reset:number[]):void{
    console.log(name)
}
hello('plus')

//函数重载,在Java中的重载，指的在TypeScript中，表现为给同一个函数提供多个函数类型定义
let obj:any = {}
function a1(val:string):void
function a1(val:number):void
function a1(val:any):void{
    if(typeof val === 'number'){
        obj.age = val
    }else {
        obj.name = val
    }
}
a1('plus')
a1(1)
a1(true)
console.log(obj)
```
## 类

```ts
//类,存取器,readonly修饰符
class Person{
    //readonly name:string;
    name:string;
    constructor(name:string){
        this.name = name
    }
    getName():void{
        console.log(this.name)
    }
    get myname() {
        return this.name;
    }
    set myname(value) {
        this.name = value;
    }
}
let p1 = new Person('a')

//继承
class Student extends Person{
    age:number
    constructor(name:string,age:number){
        super(name)
        this.age = age
    }
    getAge():number{
        return this.age
    }
}

let s1 = new Student('plus',24)
console.log(s1.getAge())

//类修饰符,静态属性和静态方法
class Father {
    static className = '1'
    public name: string;  //类里面 子类 其它任何地方外边都可以访问
    protected age: number; //类里面 子类 都可以访问,其它任何地方不能访问
    private money: number; //类里面可以访问， 子类和其它任何地方都不可以访问
    constructor(name:string,age:number,money:number) {//构造函数
        this.name=name;
        this.age=age;
        this.money=money;
    }
    getName():string {
        return this.name;
    }
    setName(name:string): void{
        this.name=name;
    }
}
class Child extends Father{
    constructor(name:string,age:number,money:number) {
        super(name,age,money);
    }
    desc() {
        //console.log(`${this.name} ${this.age} ${this.money}`);
    }
}

let child = new Child('plus',10,1000);
console.log(child.name);
// console.log(child.age);
// console.log(child.money);

//抽象类 抽象描述一种抽象的概念，无法被实例化，只能被继承 无法创建抽象类的实例 抽象方法不能在抽象类中实现，只能在抽象类的具体子类中实现，而且必须实现
abstract class Animal3 {
    name:string;
    abstract speak();
}
class Cat extends Animal3{
    speak(){
        console.log('喵喵喵');
    }
}
let cat = new Cat();
cat.speak();

abstract class Animal5{
    name:string;
    constructor(name:string){
      this.name = name;
    }
    abstract speak();
  }
  interface Flying{
      fly()
  }
  class Duck extends Animal5 implements Flying{
      speak(){
          console.log('汪汪汪');
      }
      fly(){
          console.log('我会飞');
      }
  }
  let duck = new Duck('plus');
  duck.speak();
  duck.fly();

//继承 or 多态
//继承（Inheritance）子类继承父类，子类除了拥有父类的所有特性外，还有一些更具体的特性
//多态（Polymorphism）由继承而产生了相关的不同的类，对同一个方法可以有不同的响应
class Animal7{
    speak(word:string):string{
        return 'Animal: '+word;
    }
}
class Cat7 extends Animal7{
    speak(word:string):string{
        return 'Cat:'+word;
    }
}
class Dog7 extends Animal7{
    speak(word:string):string{
        return 'Dog:'+word;
    }
}
let cat7 = new Cat7();
console.log(cat7.speak('hello'));
let dog7 = new Dog7();
console.log(dog7.speak('hello'));

//重写 or 重载
//重写是指子类重写继承自父类中的方法
//重载是指为同一个函数提供多个类型定义
class Cat6 extends Animal6{
    speak(word:string):string{
        return 'Cat:'+word;
    }
}
let cat6 = new Cat6();
console.log(cat6.speak('hello'));

function double(val:number):number
function double(val:string):string
function double(val:any):any{
  if(typeof val == 'number'){
    return val *2;
  }
  return val + val;
}

let r = double(1);
console.log(r);
```
